---
title: Sobre o uso de armazenamento e largura de banda
intro: '{% data reusables.large_files.free-storage-bandwidth-amount %}'
redirect_from:
  - /articles/billing-plans-for-large-file-storage
  - /articles/billing-plans-for-git-large-file-storage
  - /articles/about-storage-and-bandwidth-usage
  - /github/managing-large-files/about-storage-and-bandwidth-usage
  - /github/managing-large-files/versioning-large-files/about-storage-and-bandwidth-usage
versions:
  fpt: '*'
  ghec: '*'
shortTitle: Storage & bandwidth
ms.openlocfilehash: 8a6dd01c62b5b1c69afe29536e3d4ba206e988e7
ms.sourcegitcommit: 872c4751a3fc255671295a5dea6a2081c66b7b71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2022
ms.locfileid: '145126962'
---
O {% data variables.large_files.product_name_short %} está disponível para cada repositório do {% data variables.product.product_name %}, sua conta ou organização tendo ou não uma assinatura paga.

## Rastrear o uso de armazenamento e largura de banda

Quando você faz commit e push de uma alteração em um arquivo rastreado com o {% data variables.large_files.product_name_short %}, é feito push de uma nova versão de todo o arquivo e o tamanho total do arquivo é contado no limite de armazenamento do proprietário do repositório. Quando você baixa um arquivo rastreado com o {% data variables.large_files.product_name_short %}, o tamanho total do arquivo é contado no limite da largura de banda do proprietário do repositório. Os uploads do {% data variables.large_files.product_name_short %} não contam no limite de largura de banda.

Por exemplo:
- Se você fizer push de um arquivo de 500 MB no {% data variables.large_files.product_name_short %}, serão usados 500 MB do armazenamento alocado e nada da largura de banda. Se você fizer uma alteração de 1 byte e fizer push do arquivo novamente, serão usados outros 500 MB do armazenamento e nada a largura de banda, totalizando 1 GB de uso total do armazenamento e zero de largura de banda para esses dois pushes.
- Se você baixar um arquivo de 500 MB que é rastreado com o LFS, serão usados 500 MB da largura de banda alocada do proprietário do repositório. Se um colaborador fizer push de uma alteração no arquivo e você fizer pull da nova versão no repositório local, serão usados outros 500 MB de largura de banda, totalizando 1 GB de uso total da largura de banda para esses dois downloads.
- Se {% data variables.product.prodname_actions %} fizer o download de um arquivo de 500 MB rastreado com LFS, ele usará 500 MB da largura de banda atribuída pelo proprietário do repositório.

{% ifversion fpt or ghec %} Se {% data variables.large_files.product_name_long %} ({% data variables.large_files.product_name_short %}) os objetos forem incluídos nos arquivos de código-fonte para o seu repositório, os downloads desses arquivos contarão para o uso de largura de banda para o repositório. Para obter mais informações, confira "[Como gerenciar objetos do {% data variables.large_files.product_name_short %} nos arquivos do repositório](/github/administering-a-repository/managing-git-lfs-objects-in-archives-of-your-repository)".
{% endif %}

{% tip %}

**Dicas**:
- {% data reusables.large_files.owner_quota_only %}
- {% data reusables.large_files.does_not_carry %}

{% endtip %}

## Cota de armazenamento

Se você usar mais de {% data variables.large_files.initial_storage_quota %} de armazenamento sem comprar um pacote de dados, ainda será possível clonar repositórios com ativos grandes, mas será possível recuperar apenas os arquivos de ponteiro, não sendo possível fazer push do backup de novos arquivos. Para obter mais informações sobre arquivos de ponteiro, confira "[Sobre o {% data variables.large_files.product_name_long %}](/github/managing-large-files/about-git-large-file-storage#pointer-file-format)".

## Cota de largura de banda

Se você usar mais de {% data variables.large_files.initial_bandwidth_quota %} de largura de banda por mês sem comprar um pacote de dados, o suporte do {% data variables.large_files.product_name_short %} será desabilitado na sua conta até o próximo mês.

## Leitura adicional

- "[Como ver seu uso do {% data variables.large_files.product_name_long %}](/articles/viewing-your-git-large-file-storage-usage)"
- "[Como gerenciar a cobrança do {% data variables.large_files.product_name_long %}](/articles/managing-billing-for-git-large-file-storage)"
