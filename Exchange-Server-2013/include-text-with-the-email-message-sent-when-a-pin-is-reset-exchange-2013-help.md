---
title: '与 Pin 重置时发送该电子邮件包含文本: Exchange Online Help'
TOCTitle: 与 Pin 重置时发送该电子邮件包含文本
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51408295
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 与 Pin 重置时发送该电子邮件包含文本

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-22_

可以在他们的统一邮件 (UM) 或语音邮件 PIN 重置时将发送给用户的电子邮件中包含附加文本。通过在**重置用户的 Outlook Voice Access 针时**框中输入自定义文本，UM 邮箱策略上执行此操作。例如，自定义的文本可以包含已启用 UM 的用户的安全相关信息。

默认情况下，如果登录尝试失败次数超过 5 次，统一消息或语音邮件系统会重置用于 Outlook Voice Access 的 PIN。用户也可以使用 Outlook Web App 或 Outlook 2010 或更高版本随附的 UM 功能，或者使用 Outlook 电话的 Voice Access，重置其 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此框中输入的文本限制为 512 个字符，可以包含简单的 HTML 文本。</td>
</tr>
</tbody>
</table>


有关 Outlook Voice Access PIN 安全性相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

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


## 您想执行什么操作？

## 在重置用户的 PIN 后使用 EAC 在发送给这些用户的电子邮件中添加文本

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面 \>\&quot;邮件文本\&quot;的\&quot;在重置用户的 Outlook Voice Access PIN 时\&quot;文本框中，输入要包含在重置用户 PIN 后发送的电子邮件中的文本。

4.  单击\&quot;保存\&quot;。

## 在重置用户的 PIN 后使用命令行管理程序在发送给这些用户的电子邮件中添加文本

此示例包含附加的文本，"不要与其他用户共享您的 PIN。这样做所以可能导致纪律处分"，在电子邮件中发送给用户重置其 PIN 时与`MyUMMailboxPolicy` UM 邮箱策略相关联的。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

