---
title: '删除就地电子数据展示搜索: Exchange Online Help'
TOCTitle: 删除就地电子数据展示搜索
ms:assetid: 78461a78-1255-4a26-9d36-c6b8eb82a4f9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298078(v=EXCHG.150)
ms:contentKeyID: 50490868
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除就地电子数据展示搜索

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-07-14_

在 Microsoft Exchange Server 2013 中，可以使用就地电子数据展示来搜索邮箱内容。可以随时删除就地电子数据展示搜索。删除就地电子数据展示搜索时，搜索结果将从发现邮箱中删除。

> [!CAUTION]  
> 删除就地电子数据展示搜索将删除复制到发现邮箱的所有搜索结果。


## 在开始之前，您需要知道什么？

  - 估计完成时间：2-5 分钟。

  - 要删除启用了就地保留的就地电子数据展示搜索，必须首先从搜索中删除就地保留。有关详细信息，请参阅[创建或删除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;就地电子数据展示\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 删除就地电子数据展示搜索

1.  导航到\&quot;合规性管理\&quot;\>\&quot;就地电子数据展示与保留\&quot;。

2.  在列表视图中，选择要删除的就地电子数据展示搜索，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用命令行管理程序删除就地电子数据展示搜索

有关如何删除就地电子数据展示搜索的示例，请参阅 [Remove-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298130\(v=exchg.150\)) 中的\&quot;示例\&quot;部分。

## 您如何知道这有效？

要验证您是否已成功删除了就地电子数据展示搜索，请执行以下操作之一：

  - 使用 EAC 确认该搜索不再显示在\&quot;就地电子数据展示和保留\&quot;选项卡的列表视图中。

  - 使用 **Get-MailboxSearch** cmdlet 检索就地电子数据展示搜索。有关如何检索就地电子数据展示搜索的示例，请参阅 [Get-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351021\(v=exchg.150\)) 中的\&quot;示例\&quot;部分。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

