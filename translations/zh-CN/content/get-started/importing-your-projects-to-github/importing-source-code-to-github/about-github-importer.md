---
title: 关于 GitHub 导入工具
intro: 如果您在 Subversion、Mercurial、Team Foundation Version Control (TFVC) 或其他 Git 仓库中有源代码，可使用 GitHub 导入工具将其移至 GitHub。
redirect_from:
  - /articles/about-github-importer
  - /github/importing-your-projects-to-github/about-github-importer
  - /github/importing-your-projects-to-github/importing-source-code-to-github/about-github-importer
versions:
  fpt: '*'
  ghec: '*'
ms.openlocfilehash: 86fa3129982afcdf99da7879792881c522d4a6fc
ms.sourcegitcommit: 47bd0e48c7dba1dde49baff60bc1eddc91ab10c5
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/05/2022
ms.locfileid: '145128971'
---
GitHub 导入工具是一种可快速将源代码仓库（包括提交和修订记录）导入 GitHub 的工具。

![导入仓库 gif](/assets/images/help/importer/github-importer.gif)

在导入过程中，根据导入来源的版本控制系统，您可以向远程仓库进行身份验证，更新提交作者属性，以及导入包含大文件的仓库（如果不想使用 Git Large File Storage，也可删除大文件）。

| 导入操作 | Subversion | Mercurial | TFVC | Git |
|:--------------|:----------:|:---------:|:----------------------:|:---:|
| 向远程仓库进行身份验证 | **X** | **X** | **X** | **X** |
| [更新提交作者属性](/articles/updating-commit-author-attribution-with-github-importer) | **X** | **X** | **X** | |
| 将大型文件移动到 [Git 大型文件存储](/articles/about-git-large-file-storage) | **X** | **X** | **X** | |
| 从仓库删除大文件 | **X** | **X** | **X** | |

## 延伸阅读

- [使用 GitHub 导入工具导入存储库](/articles/importing-a-repository-with-github-importer)
- [使用 GitHub 导入工具更新提交作者属性](/articles/updating-commit-author-attribution-with-github-importer)
- [使用命令行导入 Git 存储库](/articles/importing-a-git-repository-using-the-command-line)
- [源代码迁移工具](/articles/source-code-migration-tools)
