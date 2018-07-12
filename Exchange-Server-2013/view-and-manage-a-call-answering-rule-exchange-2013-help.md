---
title: '查看和管理电话应答规则: Exchange Online Help'
TOCTitle: 查看和管理电话应答规则
ms:assetid: de6d9fa1-7878-49a9-bddb-e3317d94f4d8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn140251(v=EXCHG.150)
ms:contentKeyID: 54652258
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看和管理电话应答规则

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-04-08_

您可以使用命令行管理程序为用户查看或配置一个或多个电话应答规则。您还可以使用 Exchange 命令行管理程序脚本中的 **Get-UMCallAnsweringRule** 或 **Set-UMCallAnsweringRule** cmdlet 为多个用户查看或管理电话应答规则。

呼叫应答规则应用于传入呼叫的方式与收件箱规则应用于传入电子邮件的方式类似。默认情况下，用户启用统一消息 (UM) 时，未配置呼叫应答规则。即使如此，传入呼叫由邮件系统应答，并提示呼叫者留下语音邮件。

> [!IMPORTANT]  
> 已启用 UM 的用户可登录 Outlook Web App 来创建、管理和删除呼叫应答规则。


有关与呼叫应答规则相关的其他管理任务，请参阅[转发调用过程](forwarding-calls-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 呼叫应答规则\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认用户的邮箱已启用 UM。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。 若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 要执行什么操作？

## 使用命令行管理程序查看电话应答规则

您可以获取已启用 UM 的用户邮箱中单个电话应答规则或一系列电话应答规则的属性。

本示例返回已启用 UM 的用户邮箱中的电话应答规则列表（已设置格式）。

    Get-UMCallAnsweringRule-Mailbox tonysmith | Format-List

本示例显示电话应答规则 `MyUMCallAnsweringRule` 的属性。

    Get-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

## 使用命令行管理程序配置电话应答规则

您可以配置或更改用户邮箱中存储的电话应答规则。可以指定下列条件：

  - 传入呼叫的呼叫者

  - 当天时间

  - 日历忙/闲状态

  - 电子邮件的自动答复是否处于打开状态

您还可以指定以下操作：

  - 与我联系

  - 将呼叫者转接到其他人

  - 留下语音邮件

本示例将电话应答规则 `MyCallAnsweringRule`（存在于 Tony Smith 的邮箱中）的优先级设置为 2。

    Set-UMCallAnsweringRule -Mailbox tonysmith -Name MyCallAnsweringRule -Priority 2

本示例根据电话应答规则 `MyCallAnsweringRule`（存在于 Tony Smith 的邮箱中）执行下列操作：

  - 将该呼叫应答规则设置为两个呼叫者 ID。

  - 将呼叫应答规则的优先级设置为 2。

  - 设置该呼叫应答规则以允许呼叫者中断问候语。

<!-- end list -->

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -CallerIds "1,4255550100,,","1,4255550123,," -Priority 2 -CallersCanInterruptGreeting $true -Mailbox tonysmith

本示例将电话应答规则 `MyCallAnsweringRule`（存在于 Tony Smith 的邮箱中）的闲/忙状态更改为\&quot;离开\&quot;，并将优先级设置为 2。

    Set-UMCallAnsweringRule -Name MyCallAnsweringRule -Priority 2 -Mailbox tonysmith@contoso.com -ScheduleStatus 0x8

