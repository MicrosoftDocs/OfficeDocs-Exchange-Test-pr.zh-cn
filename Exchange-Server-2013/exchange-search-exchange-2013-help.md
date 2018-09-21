---
title: 'Exchange 搜索: Exchange 2013 Help'
TOCTitle: Exchange 搜索
ms:assetid: 967e2a13-4e54-486a-ac22-08768674abbb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232132(v=EXCHG.150)
ms:contentKeyID: 52061535
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 搜索

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-09-17_

随着邮箱大小和以邮件和附件形式存储于邮箱中的数据量的不断增长，对用户来说，快速搜索和找到所需邮件非常重要。[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)通过将旧的和不常用的访问项目移动到存档，帮助您减少或消除对 .pst 文件的使用。这会导致用户存储更多邮箱数据，并会使在用户的主要和存档邮箱中搜索成为重要的工作效率工具。[就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)允许经过授权的用户跨本地和基于云的 Exchange 组织搜索邮箱内容，以符合电子发现（电子数据展示）请求、法规审核或内部调查。就地电子数据展示还使用由 Exchange 搜索创建的内容索引。

Exchange 搜索与可在 Exchange Server 2003 中进行的全文索引不同。性能、内容索引和搜索已得到改进。将在传输管道中或几乎在新项目创建或发送到邮箱中的同时对这些项目建立索引，这样，用户便可快速、稳定且更加可靠地搜索邮箱数据。默认情况下启用内容索引，不需要初始设置或配置。

要查找与 Exchange 搜索相关的管理任务吗？请参阅[Exchange 搜索过程](exchange-search-procedures-exchange-2013-help.md)。

## 新增功能

Exchange 2013 引入对 Exchange 搜索的下列更改：

  - 基础内容索引引擎已替换为 Microsoft Search Foundation，Microsoft Search Foundation 增强了性能和功能，并充当 Exchange 和 SharePoint 中的常用基础内容索引引擎。不过，管理界面仍保持相同。

  - 默认情况下，Search Foundation 处理电子邮件附件中最常用的文件格式。您不再需要安装用于 Exchange 搜索的 Microsoft Office Filter Pack。有关 Exchange 搜索处理的文件格式的列表，请参阅[由 Exchange 搜索编制索引的文件格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)。
    
    可以像在 Exchange 2010 中一样，通过安装 IFilter 添加对任何其他文件格式的支持。

  - 内容索引的效率更高，因为它现在处理传输管道中的邮件。因此，发送到多个收件人或通讯组的邮件只需处理一次。批注流附加到邮件，在使用更少资源的同时，显著提高了内容索引速度。

