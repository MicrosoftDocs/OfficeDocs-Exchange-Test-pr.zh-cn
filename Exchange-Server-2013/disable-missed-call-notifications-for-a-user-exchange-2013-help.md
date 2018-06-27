---
title: '禁用用户的未接的来电通知: Exchange Online Help'
TOCTitle: 禁用用户的未接的来电通知
ms:assetid: e54937d5-3074-454f-b561-e601fecfc6ad
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673570(v=EXCHG.150)
ms:contentKeyID: 52061429
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用用户的未接的来电通知

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-12-09_

您可以通过启用或禁用统一邮件 (UM) 邮箱策略未接的电话通知使用 Shell 或 EAC。未接的来电通知是用户没应答传入的呼叫时向用户发送电子邮件，并调用方未留下语音信息。这是比包含留给用户的语音邮件的一个不同的电子邮件消息。

禁用 UM 邮箱策略上的未接的电话通知时，您将阻止与接收电子邮件的 UM 邮箱策略相关联的所有用户时它们不作出应答的传入呼叫时，呼叫者并不留下语音信息。默认情况下，创建的每个 UM 邮箱策略启用未接的电话通知。此外在默认情况下，每次创建 UM 拨号计划创建 UM 邮箱策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当您集成统一消息和 Microsoft Lync Server 时，对于邮箱位于 Exchange 2007 或 Exchange 2010 邮箱服务器上的用户而言，如果他/她在呼叫发送至运行 Microsoft Exchange 统一消息服务的邮箱服务器之前断开，则将无法使用未接来电通知。</td>
</tr>
</tbody>
</table>


有关与 UM 邮箱策略相关的其他管理任务，请参阅[管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

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


## 要执行什么操作？

## 使用 EAC 为 UM 邮箱策略禁用未接电话通知

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面 \>\&quot;常规\&quot;，清除\&quot;启用未接电话通知\&quot;旁边的复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序为 UM 邮箱策略禁用未接电话通知

本示例为名为 `MyUMMailboxPolicy` 的 UM 邮箱策略禁用未接电话通知。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $false

