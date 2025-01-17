---
title: デプロイメント
intro: Deployments API を使うと、デプロイとデプロイ環境を作成および削除できます。
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - API
miniTocMaxHeadingLevel: 3
ms.openlocfilehash: a75c94b609bd166971e23516e8b2af318236a026
ms.sourcegitcommit: 95e6f3d3aba8c637a3f72b571a6beacaa38d367f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2022
ms.locfileid: '147067963'
---
## <a name="about-the-deployments-api"></a>デプロイ API について

デプロイメントとは、特定の ref (ブランチ、SHA、タグ) を配備するためるリクエストです。 GitHub では、[`deployment` イベント](/developers/webhooks-and-events/webhook-events-and-payloads#deployment)がディスパッチされますが、このイベントでは、新しいデプロイが作成されるタイミングを外部サービスがリッスンし、それに応じて動作できます。 デプロイメントにより、開発者や Organization はデプロイメントを中心として、さまざまな種類のアプリケーション (ウェブ、ネイティブなど) を提供するための実装に関する詳細を気にすることなく、疎結合ツールを構築できます。

デプロイ状態という機能では、外部サービスはデプロイに、[`deployment_status` イベント](/developers/webhooks-and-events/webhook-events-and-payloads#deployment_status)をリッスンするシステムが利用できる `error`、`failure`、`pending`、`in_progress`、`queued`、`success` という状態を付けることができます。

デプロイ状態には、任意で `description` と `log_url` も追加できます。デプロイ状態がさらに便利になるため、これらの状態は高く推奨されます。 `log_url` はデプロイ出力の完全 URL です。`description` は、デプロイで起こったことの概要がまとめられたものです。

GitHub では、新しいデプロイとデプロイ状態が作成されたとき、`deployment` イベントと `deployment_status` イベントがディスパッチされます。 これらのイベントにより、サードパーティのインテグレーションがデプロイメントのリクエストに対する応答を受けとり、進展があるたびにステータスを更新できます。

以下は、これらの相互作用がどのように機能するかを示す簡単なシーケンス図です。

```
+---------+             +--------+            +-----------+        +-------------+
| Tooling |             | GitHub |            | 3rd Party |        | Your Server |
+---------+             +--------+            +-----------+        +-------------+
     |                      |                       |                     |
     |  Create Deployment   |                       |                     |
     |--------------------->|                       |                     |
     |                      |                       |                     |
     |  Deployment Created  |                       |                     |
     |<---------------------|                       |                     |
     |                      |                       |                     |
     |                      |   Deployment Event    |                     |
     |                      |---------------------->|                     |
     |                      |                       |     SSH+Deploys     |
     |                      |                       |-------------------->|
     |                      |                       |                     |
     |                      |   Deployment Status   |                     |
     |                      |<----------------------|                     |
     |                      |                       |                     |
     |                      |                       |   Deploy Completed  |
     |                      |                       |<--------------------|
     |                      |                       |                     |
     |                      |   Deployment Status   |                     |
     |                      |<----------------------|                     |
     |                      |                       |                     |
```

GitHub は、あなたのサーバーに実際にアクセスすることはないということは覚えておきましょう。 デプロイメントイベントとやり取りするかどうかは、サードパーティインテグレーション次第です。 複数のシステムがデプロイメントイベントをリッスンできます。コードをサーバーにプッシュする、ネイティブコードを構築するなどを行うかどうかは、それぞれのシステムが決めることができます。

`repo_deployment` [OAuth スコープ](/developers/apps/scopes-for-oauth-apps)は、リポジトリ コードにアクセスを許可 **せずに**、デプロイとデプロイの状態へのターゲット アクセスを許可しますが、{% ifversion not ghae %}`public_repo` スコープと {% endif %}`repo` スコープもコードにアクセス許可を付与することに注意してください。

### <a name="inactive-deployments"></a>非アクティブのデプロイメント

デプロイ状態を `success` に設定すると、同じ環境名で同じリポジトリにある以前の一時的ではない非運用環境デプロイが `inactive` になります。 これを回避するため、デプロイ状態を作成するとき、`auto_inactive` を `false` に設定できます。

その `state` を `inactive` に設定することで、一時的な環境がなくなったことを通知できます。  `state` を `inactive` に設定すると、{% data variables.product.prodname_dotcom %} でデプロイが `destroyed` として表示され、それへのアクセスが削除されます。
