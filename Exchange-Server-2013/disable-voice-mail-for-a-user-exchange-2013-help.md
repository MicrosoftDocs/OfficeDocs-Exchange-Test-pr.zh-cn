---
title: '禁用用户的语音邮件: Exchange Online Help'
TOCTitle: 禁用用户的语音邮件
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50491576
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用用户的语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

您可以启用 UM 的用户禁用统一邮件 (UM)。当您执行此操作时，用户可以不再使用统一消息中的语音邮件功能。如果您愿意，您禁用 UM 的用户时，您可以保留用户的 UM 设置。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认当前已现有用户启用统一消息。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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

## 使用 EAC 禁用用户的统一消息和语音邮件

1.  在 EAC 中，单击\&quot;收件人\&quot;。

2.  在列表视图中，选择要禁用其邮箱的统一消息的用户。

3.  在详细信息窗格的\&quot;电话和语音功能\&quot;\&quot;统一消息\&quot;下，单击\&quot;禁用\&quot;。

4.  在\&quot;警告\&quot;框中，单击\&quot;是\&quot;确认将禁用该用户的统一消息。

## 使用命令行管理程序禁用用户的统一消息和语音邮件

此示例对用户 tonysmith@contoso.com 禁用统一消息和语音邮件，但保留 UM 邮箱设置。

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

