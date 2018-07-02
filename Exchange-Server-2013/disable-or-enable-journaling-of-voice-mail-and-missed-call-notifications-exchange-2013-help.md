---
title: '禁用或启用语音邮件和未接来电通知的日记功能: Exchange 2013 Help'
TOCTitle: 禁用或启用语音邮件和未接来电通知的日记功能
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 50490546
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用或启用语音邮件和未接来电通知的日记功能

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

在 Microsoft Exchange Server 2013 中，创建对 Exchange 组织中的收件人或发件人接收或发送的电子邮件进行日志记录的日记规则时，由统一消息 (UM) 服务生成的语音邮件和未接来电通知将包括在内。使用本主题中的过程可为整个组织关闭或打开此功能。

若要了解与日记功能相关的其他管理任务，请查看[管理日记](manage-journaling-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;日记功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序禁用或启用语音邮件和未接来电通知的日记功能

此示例通过将 *VoicemailJournalingEnabled* 参数设置为 `$false`，禁用语音邮件和未接来电通知的日记功能。

    Set-TransportConfig -VoicemailJournalingEnabled $false

此示例通过将相同参数设置为 `$true`，启用语音邮件和未接来电通知的日记功能。

    Set-TransportConfig -VoicemailJournalingEnabled $true

有关语法和参数的详细信息，请参阅 [Set-TransportConfig](https://technet.microsoft.com/zh-cn/library/bb124151\(v=exchg.150\))。

## 详细信息

[日记](journaling-exchange-2013-help.md)

[管理日记](manage-journaling-exchange-2013-help.md)

