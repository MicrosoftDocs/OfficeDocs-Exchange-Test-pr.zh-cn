---
title: '删除 UM 邮箱策略: Exchange Online Help'
TOCTitle: 删除 UM 邮箱策略
ms:assetid: c8758464-3c52-4dd3-b2a6-142a99bb0628
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124536(v=EXCHG.150)
ms:contentKeyID: 50556658
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 UM 邮箱策略

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

删除统一邮件 (UM) 邮箱策略时，将不再可与收件人启用了 UM 的 UM 邮箱策略。如果它被引用的所有已启用 UM 的邮箱，并且不能删除 UM 拨号计划，如果 UM 邮箱策略与它相关联，则无法删除 UM 邮箱策略。

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 删除 UM 邮箱策略

1.  
    
    在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面上的\&quot;UM 邮箱策略\&quot;下，单击工具栏上的\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用命令行管理程序删除 UM 邮箱策略

本示例将删除名为 `MyUMMailboxPolicy` 的 UM 邮箱策略。

    Remove-UMMailboxPolicy -Identity MyUMMailboxPolicy

