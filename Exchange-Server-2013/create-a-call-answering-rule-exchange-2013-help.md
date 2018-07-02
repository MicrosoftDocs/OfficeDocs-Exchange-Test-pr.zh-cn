---
title: '创建呼叫应答规则: Exchange Online Help'
TOCTitle: 创建呼叫应答规则
ms:assetid: 0976f8f2-3449-44f1-b0d1-20c91622e827
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ898495(v=EXCHG.150)
ms:contentKeyID: 51408192
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建呼叫应答规则

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2015-04-08_

可使用命令行管理程序为某一个用户创建一个或多个呼叫应答规则。也可使用 Exchange 命令行管理程序脚本中的 **New-UMCallAnsweringRule** cmdlet 为多个用户创建呼叫应答规则。

呼叫应答规则应用于传入呼叫的方式与收件箱规则应用于传入电子邮件的方式类似。默认情况下，用户启用统一消息 (UM) 时，未配置呼叫应答规则。即使如此，传入呼叫由邮件系统应答，并提示呼叫者留下语音邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已启用 UM 的用户可登录 Outlook Web App 来创建、管理和删除呼叫应答规则。</td>
</tr>
</tbody>
</table>


有关与呼叫应答规则相关的其他管理任务，请参阅[转发调用过程](forwarding-calls-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 呼叫应答规则\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认用户的邮箱已启用 UM。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。 若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

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


## 使用命令行管理程序创建呼叫应答规则。

该示例在 Tony Smith 邮箱中创建呼叫应答规则 `MyCallAnsweringRule`，优先级为 2。

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith

该示例在 Tony Smith 邮箱中创建呼叫应答规则 `MyCallAnsweringRule`，并执行以下操作：

  - 将该呼叫应答规则设置为两个呼叫者 ID。

  - 将呼叫应答规则的优先级设置为 2。

  - 设置该呼叫应答规则为允许呼叫者中断问候语。

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

该示例在 Tony Smith 邮箱中创建呼叫应答规则 `MyCallAnsweringRule`，并执行以下操作：

  -  
    将呼叫应答规则的优先级设置为 2。

  -  
    创建呼叫应答规则的键映射。

  -  
    如果呼叫者访问了用户的语音邮件，且用户的状态设置为\&quot;忙\&quot;，那么呼叫者可以：
    
      - 按 1 键，呼叫者会被转到分机号为 45678 的接待员。
    
      - 按 2 键，会为紧急问题使用\&quot;联系我\&quot;功能，并首先呼叫分机 23456，然后呼叫分机 45671。

<!-- end list -->

    New-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith -ScheduleStatus 0x4 - -KeyMappings "1,1,Receptionist,,,,,45678,","5,2,Urgent Issues,23456,23,45671,50,,"

