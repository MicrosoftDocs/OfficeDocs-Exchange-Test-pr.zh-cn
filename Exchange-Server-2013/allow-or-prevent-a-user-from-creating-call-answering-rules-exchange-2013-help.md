---
title: '允许或禁止用户创建呼叫应答规则: Exchange Online Help'
TOCTitle: 允许或禁止用户创建呼叫应答规则
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50556609
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许或禁止用户创建呼叫应答规则

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

可以指定单个用户能够创建和管理他们自己呼叫应答通过配置其邮箱属性的规则。默认情况下，他们可以创建呼叫应答规则。

通过配置 UM 拨号计划或 UM 邮箱策略上的电话应用规则，可以为启用了统一消息 (UM) 的多个用户启用或禁用电话应答规则。

> [!NOTE]  
> EAC 不能用于配置此功能。必须使用外壳程序来启用或禁用语音邮件用户呼叫应答规则。


有关与允许用户转移呼叫相关的更多管理任务，请参阅[转发调用过程](forwarding-calls-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认用户的邮箱已启用 UM。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序为启用 UM 的用户启用或禁用呼叫应答规则

此示例为用户 tony@contoso.com 启用电话应答规则。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

此示例将为用户 tony@contoso.com 禁用呼叫应答规则。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

