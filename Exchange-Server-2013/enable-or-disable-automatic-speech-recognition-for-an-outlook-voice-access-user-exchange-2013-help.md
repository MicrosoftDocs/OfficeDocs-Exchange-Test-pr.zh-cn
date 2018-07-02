---
title: '启用或禁用 Outlook Voice Access 用户的自动语音识别: Exchange Online Help'
TOCTitle: 启用或禁用 Outlook Voice Access 用户的自动语音识别
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50556576
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用 Outlook Voice Access 用户的自动语音识别

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置自动语音识别 (ASR) 的用户启用统一邮件 (UM) 和语音邮件功能。在Outlook的语音访问用户的邮箱上启用 ASR 时，用户可以移动邮箱菜单使用声音命令。默认情况下启用 ASR。如果 ASR 处于禁用状态，用户必须使用双音多频 (DTMF)，也称为按键，输入菜单中移动。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EAC 不能用于配置此功能。您必须使用外壳程序启用或禁用 ASR 语音邮件用户。</td>
</tr>
</tbody>
</table>


与 UM 或语音邮件用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，请先确认用户的邮箱已启用 UM。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 使用命令行管理程序为启用了 UM 的用户启用或禁用 ASR

本示例将为名为 `tonysmith`、启用了 UM 的用户启用 ASR。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

本示例为名为 `tonysmith`、启用了 UM 的用户禁用 ASR。

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

