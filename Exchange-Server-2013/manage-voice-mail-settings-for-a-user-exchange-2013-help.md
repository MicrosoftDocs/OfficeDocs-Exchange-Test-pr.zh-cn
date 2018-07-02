---
title: '管理用户的语音邮件设置: Exchange Online Help'
TOCTitle: 管理用户的语音邮件设置
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50490840
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理用户的语音邮件设置

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以查看或设置的统一邮件 (UM) 和语音邮件功能和已启用 UM 和语音邮件的用户的配置设置。例如，可以执行以下操作 ︰

  - 重置 Outlook Voice Access PIN。

  - 添加个人话务员分机号。

  - 添加其他分机号。

  - 启用或禁用自动语音识别 (ASR)。

  - 启用或禁用呼叫应答规则。

  - 启用或禁用对电子邮件或日历的访问。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>某些设置和功能只能通过使用命令行管理程序来配置。</td>
</tr>
</tbody>
</table>


有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 查看或配置启用了 UM 的用户的属性

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要更改 UM 邮箱策略的邮箱。

3.  在详细信息窗格的\&quot;电话和语音功能\&quot; \>\&quot;统一消息\&quot;下，单击\&quot;视图详细信息\&quot;。

4.  在\&quot;UM 邮箱\&quot;页上，单击\&quot;UM 邮箱设置\&quot;查看或更改启用了 UM 的现有用户的以下 UM 属性：
    
      - **PIN 状态**  仅显示该域显示该用户的邮箱的状态。默认情况下，当用户启用 UM 的针状态被列为**未锁定状态**。但是，如果用户有多次输入错误Outlook语音访问 PIN，状态被列为**锁定**。
    
      - **UM 邮箱策略**   此框显示与启用 UM 的用户相关联的 UM 邮箱策略的名称。您可以单击\&quot;浏览\&quot;来定位并指定要与此 UM 邮箱关联的 UM 邮箱策略。
    
      - **个人话务员分机** 使用此框可为用户指定话务员分机号码。默认情况下不会配置分机号码。分机号码的长度可以是 1 到 20 个字符。这会使向启用了 UM 的用户发出的传入呼叫可转移到在此框中指定的分机号码。
        
        您可以配置其他类型的运算符分机号码拨号计划和自动助理。但是，这些扩展通常用于整个公司的接待员或运算符。当行政助理或个人助理回答打入的电话，他们要为特定用户接听之前，可以使用个人运算符扩展设置。

5.  在\&quot;UM 邮箱\&quot;页上的\&quot;其他分机号\&quot;下，您可以添加、更改和查看用户的分机号码。
    
      - 要添加分机号码，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在\&quot;添加其他分机号\&quot;页上，使用\&quot;浏览\&quot;选择 UM 拨号计划，然后在\&quot;分机号码\&quot;框中输入分机号码。
    
      - 要删除分机号码，请选择要删除的分机号码，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

6.  如果您进行了任何更改，请单击\&quot;保存\&quot;。

## 使用命令行管理程序为启用了 UM 的用户配置功能

此示例禁用\&quot;在电话上播放\&quot;和未接来电通知，但启用文本邮件 (SMS) 通知。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于内部部署和混合部署，正在集成统一消息和 Lync Server 时未接电话通知不会有了 Exchange 2007 或 Exchange 2010 邮箱服务器上的邮箱的用户可以使用。在用户断开呼叫发送到邮箱服务器之前，会生成未接的来电通知。</td>
</tr>
</tbody>
</table>


    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

此示例在用户使用 Outlook Voice Access 时阻止用户访问日历，但允许访问电子邮件。

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

此示例在用户使用 Outlook Voice Access 时阻止用户访问日历和电子邮件。

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

此示例阻止用户创建呼叫应答规则、接收传入的传真和使用 Outlook Voice Access，但启用自动语音识别 (ASR)。

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## 使用命令行管理程序查看启用了 UM 的用户的属性

本示例在格式化列表中显示林中所有已启用 UM 的邮箱的列表。

    Get-UMMailbox | Format-List

本示例显示 tonysmith@contoso.com 的 UM 邮箱属性。

    Get-UMMailbox -Identity tonysmith@contoso.com

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当您运行的 Exchange 2007 和 Exchange 2013 和用户的邮箱位于 Exchange 2007 邮箱服务器上，运行<strong>Get-UMMailbox</strong> cmdlet 将不会正常工作。若要解决此问题，请从 Exchange 2007 服务器或运行 Exchange 2007 管理工具的计算机运行<strong>Get-UMMailbox</strong> cmdlet。</td>
</tr>
</tbody>
</table>

