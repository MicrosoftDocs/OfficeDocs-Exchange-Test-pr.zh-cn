---
title: '重置语音邮件 PIN: Exchange Online Help'
TOCTitle: 重置语音邮件 PIN
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50556667
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# 重置语音邮件 PIN

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

启用统一邮件 UM 的语音邮件用户无法访问其邮箱如何使用 Outlook Voice Access，因为他们尝试登录中使用多次的 PIN 不正确，或者他们忘记了他们的 PIN，可以使用以下过程之一来重置用户的 PIN。重置用户的Outlook语音访问针时，您可以配置 UM 自动生成 PIN 或者您可以手动指定的 PIN。新 PIN 被发送到用户在电子邮件中。您可以指定其他针选项如要求用户在首次登录时重置其 PIN。用户还可以将使用Outlook或Outlook Web App的 UM PIN 重置。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要访问已启用 UM 的邮箱，Outlook Voice Access 用户需要使用按键，也称为双音多频 (DTMF) 输入。语音识别不可用针输入。</td>
</tr>
</tbody>
</table>


有关与 Outlook Voice Access PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

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

## 使用 EAC 重置统一消息 PIN

1.  在 EAC 中，导航到\&quot;收件人\&quot;。在列表视图中，选择要查看的用户邮箱。

2.  在详细信息窗格中\&quot;电话和语音功能\&quot;下的\&quot;统一消息\&quot;下，单击\&quot;查看详细信息\&quot;。

3.  在\&quot;UM 邮箱\&quot;页面上的\&quot;UM 邮箱设置\&quot;下，单击\&quot;重置 PIN\&quot;。

4.  使用\&quot;重置 UM 邮箱 PIN\&quot;页面上，使用以下选项重置启用 UM 用户的 PIN：
    
      - **自动生成 PIN**  使用此选项可以自动生成用户用于访问使用Outlook语音访问其邮箱的 PIN。默认情况下，启用此设置。
        
        自动生成的 PIN 将用户的邮箱的电子邮件中发送。他们将获得针和登录到他们的邮箱后，将会提示他们变为更熟悉这些针针。
        
        Outlook Web App和 Microsoft Outlook 还允许用户重置其 PIN。PIN 自动生成与用户的邮箱具有关联的 UM 邮箱策略配置的 PIN 策略基础。我们建议您自动的Outlook语音访问用户生成的针脚。
    
      - **PIN 类型**  使用此选项，可以手动指定Outlook语音访问用户的 PIN。默认情况下，此设置被禁用。
        
        如果您指定用户的 PIN，PIN 将发送电子邮件给该用户的邮箱中。他们将获得针和登录到他们的邮箱后，他们可以通过配置Outlook语音访问个人选项更改 pin 码。但是，在Outlook Web App和 Microsoft Outlook，没有选项来手动指定的 PIN。
    
      - **要求用户重置其 PIN 登录他们第一次**  使用此选项可以要求用户在首次登录到 Outlook Voice Access 时重置其 PIN。默认情况下，此选项被启用。
        
        如果您选择的选项来自动生成用户的 PIN，您可以启用此选项将要求用户在首次登录到Outlook语音访问时更改他们的 PIN。这有助于防止用户的 PIN。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序重置统一消息 PIN

此示例将 Tony Smith 的语音邮件 PIN 重置为 1985848。但是，当用户首次登录 Outlook Voice Access 时必须更改该 PIN。

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

