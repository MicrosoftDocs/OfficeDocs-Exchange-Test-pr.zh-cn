---
title: '启用或禁用&quot;向用户发送语音邮件&quot;: Exchange Online Help'
TOCTitle: 启用或禁用“向用户发送语音邮件”
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52061457
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用\&quot;向用户发送语音邮件\&quot;

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-13_

您可以允许呼叫者从统一消息 (UM) 自动助理向用户发送语音邮件，或阻止其执行该操作。默认情况下该选项是启用的，允许呼叫者向与 UM 自动助理关联的 UM 拨号计划中的用户发送语音邮件。如果禁用此选项，则自动助理将不会在系统提示期间邀请呼叫者发送语音邮件。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 以使呼叫者可以发送语音邮件，或阻止其执行该操作

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要管理的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;\>\&quot;通讯簿和话务员权限\&quot;的\&quot;用于联系用户的选项\&quot;下，选中\&quot;允许呼叫者为用户留下语音邮件\&quot;旁边的复选框，以允许呼叫者留下语音邮件。若要阻止呼叫者留下语音邮件，清除该复选框。

4.  单击\&quot;保存\&quot;。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要禁用此选项并禁用&amp;quot;允许呼叫者拨打用户电话&amp;quot;选项，则将同时禁用&amp;quot;用于搜索通讯簿的选项&amp;quot;。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序允许呼叫者发送语音邮件或阻止其执行该操作

本示例将阻止呼叫名为 `MyUMAutoAttendant` 的 UM 自动助理的呼叫者发送语音邮件。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

本示例将允许呼叫名为 `MyUMAutoAttendant` 的 UM 自动助理的呼叫者发送语音邮件。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

