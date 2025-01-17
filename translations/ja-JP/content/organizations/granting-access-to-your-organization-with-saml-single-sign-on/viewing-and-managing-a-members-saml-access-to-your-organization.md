---
title: 組織に対するメンバーの SAML アクセスの表示と管理
intro: Organization のメンバーのリンクされたアイデンティティ、アクティブなセッション、認可されたクレデンシャルの表示と取り消しが可能です。
permissions: Organization owners can view and manage a member's SAML access to an organization.
redirect_from:
  - /articles/viewing-and-revoking-organization-members-authorized-access-tokens
  - /github/setting-up-and-managing-organizations-and-teams/viewing-and-revoking-organization-members-authorized-access-tokens
  - /github/setting-up-and-managing-organizations-and-teams/viewing-and-managing-a-members-saml-access-to-your-organization
versions:
  ghec: '*'
topics:
  - Organizations
  - Teams
shortTitle: Manage SAML access
ms.openlocfilehash: 5b8dbe15037eabe416a6b0c63df7f893db8445bb
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2022
ms.locfileid: '145130843'
---
## Organization への SAML アクセスについて

Organizationに対する SAMLシングルサインオンを有効にすると、各 Organizationメンバーは IDプロバイダ (IdP) での外部アイデンティティを、 {% data variables.product.product_location %}上の既存のアカウントにリンクできます。 {% data variables.product.product_name %}上の Organizationのリソースにアクセスするには、メンバーはアクティブなSAMLセッションをブラウザーに持っていなければなりません。 OrganizationのリソースにAPIまたはGitを使ってアクセスするには、メンバーは、メンバーがOrganizationでの利用のために認可した個人アクセストークンもしくはSSHキーを使わなければなりません。

各メンバーのリンクされたアイデンティティ、アクティブなセッション、同じページで認可されたクレデンシャルの表示と取り消しが可能です。

## リンクされているアイデンティティの表示と取り消し

{% data reusables.saml.about-linked-identities %} 

利用できる場合には、このエントリにはSCIMデータが含まれます。 詳しくは、「[Organization の SCIM について](/organizations/managing-saml-single-sign-on-for-your-organization/about-scim-for-organizations)」をご覧ください。

{% warning %}

**警告:** SCIM を使用している Organization の場合:
- {% data variables.product.product_name %}上のリンクされたユーザIDを削除すると、SAML及びSCIMのメタデータも削除されます。 その結果、アイデンティティプロバイダはリンクされたユーザのアイデンティティとの同期やプロビジョニング解除ができなくなります。
- 管理者は、リンクされたアイデンティティの削除をアイデンティティプロバイダを通じて行わなければなりません。
- リンクされたアイデンティティを削除し、アイデンティティプロバイダを通じて異なるアカウントをリンクするために、管理者は{% data variables.product.product_name %}アプリケーションからユーザを削除し、再アサインできます。 詳しい情報については、アイデンティティプロバイダのドキュメンテーションを参照してください。

{% endwarning %}


{% data reusables.identity-and-permissions.revoking-identity-team-sync %}

{% data reusables.profile.access_org %} {% data reusables.user-settings.access_org %} {% data reusables.organizations.people %} {% data reusables.saml.click-person-revoke-identity %} {% data reusables.saml.saml-identity-linked %} {% data reusables.saml.view-sso-identity %} {% data reusables.saml.revoke-sso-identity %} {% data reusables.saml.confirm-revoke-identity %}

## アクティブな SAML セッションの表示と取り消し

{% data reusables.profile.access_org %} {% data reusables.user-settings.access_org %} {% data reusables.organizations.people %} {% data reusables.saml.click-person-revoke-session %} {% data reusables.saml.saml-identity-linked %} {% data reusables.saml.view-saml-sessions %} {% data reusables.saml.revoke-saml-session %}

## 認可されたクレデンシャルの表示と取り消し

{% data reusables.saml.about-authorized-credentials %}

{% data reusables.profile.access_org %} {% data reusables.user-settings.access_org %} {% data reusables.organizations.people %} {% data reusables.saml.click-person-revoke-credentials %} {% data reusables.saml.saml-identity-linked %} {% data reusables.saml.view-authorized-credentials %} {% data reusables.saml.revoke-authorized-credentials %} {% data reusables.saml.confirm-revoke-credentials %}

## 参考資料

- 「[SAML シングル サインオンを使用した ID およびアクセス管理について](/articles/about-identity-and-access-management-with-saml-single-sign-on)」{% ifversion ghec %}
- 「[Enterprise アカウントへのユーザーの SAML アクセスの表示および管理](/admin/user-management/managing-users-in-your-enterprise/viewing-and-managing-a-users-saml-access-to-your-enterprise)」{% endif %}
