---
title: '来自已通过身份验证的调用方配置受保护的语音邮件: Exchange Online Help'
TOCTitle: 来自已通过身份验证的调用方配置受保护的语音邮件
ms:assetid: f69e94a7-9768-4445-9ded-e78d732bd623
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423560(v=EXCHG.150)
ms:contentKeyID: 52061449
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 来自已通过身份验证的调用方配置受保护的语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置统一消息应答传入的呼叫，然后确定是否它将应用保护到语音邮件使用的加密方法。当受保护语音消息 ︰

  - 在 Microsoft Outlook 和 Outlook Web App 中，邮件会被标记为\&quot;私人\&quot;。

  - 只有语音邮件的预期收件人才能打开该语音邮件。

  - 收件人可以答复语音邮件，但无法将其转发给未包括在原始语音邮件中的人员。

此设置适用于语音消息发送给已启用 UM 的用户他们不接听电话。当调用方登录到使用Outlook语音访问其邮箱创建和发送语音邮件时，该设置也适用。

有关与受保护语音邮件步骤相关的其他管理任务，请参阅[受保护的语音邮件过程](protected-voice-mail-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置来自已通过身份验证的呼叫者的受保护语音邮件

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面 \>\&quot;受保护的语音邮件\&quot;上，在\&quot;保护来自已通过身份验证的呼叫者的语音邮件\&quot;下，选择以下选项之一：
    
      - **无：** 如果不希望对发送给启用 UM 的用户的任何语音邮件应用保护，则使用该设置。
    
      - **私人：** 若要统一消息仅对由呼叫者标记为私人的语音邮件应用保护，请使用此设置。
    
      - **全部：** 若要统一消息对所有语音邮件（包括未标记为私人的邮件）应用保护，请使用此设置。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置来自已通过身份验证的呼叫者的受保护语音邮件

本示例将保护来自 UM 邮箱策略 `MyUMMailboxPolicy` 上的所有已通过身份验证的呼叫者的语音邮件。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy ProtectAuthenticatedVoiceMail -All

