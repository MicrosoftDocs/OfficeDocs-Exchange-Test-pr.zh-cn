---
title: '配置语音邮件预览合作伙伴服务的用户: Exchange Online Help'
TOCTitle: 配置语音邮件预览合作伙伴服务的用户
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51408242
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置语音邮件预览合作伙伴服务的用户

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

您可以统一邮件 (UM) 邮箱策略上配置语音邮件预览合作伙伴。UM 邮箱策略上配置语音邮件预览合作伙伴设置，如语音邮件预览合作伙伴 ID 和语音邮件预览合作伙伴地址后，您配置的设置将应用于所有已启用 UM 的用户与该邮箱策略链接。

> [!NOTE]  
> 必须使用命令行管理程序配置语音邮件预览合作伙伴。


有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您该如何做？

## 第 1 步︰ 注册合作伙伴服务

经认证的合作伙伴以及有关如何注册的详细的说明，请参阅[语音邮件预览顾问](voice-mail-preview-advisor-exchange-2013-help.md)或者请参阅[Microsoft 查明其](https://go.microsoft.com/fwlink/p/?linkid=281966)网站。注册完后，语音邮件预览合作伙伴将提供您一个合作伙伴 ID 和 SMTP 地址用于转发语音邮件。

在步骤 2 中，将在步骤 1 中获得的合作伙伴 ID 和 SMTP 地址应用到所需的 UM 邮箱策略。

## 步骤 2︰ 设置语音邮件预览合作伙伴地址和 ID

在此示例中，在名为 *MyUMMailboxPolicy* 的 UM 邮箱策略中，将语音邮件预览合作伙伴地址设置为 exumvmp@fabrikam.com，将语音邮件预览合作伙伴 ID 设置为 CON123-2010。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## 步骤 3︰ 配置高级合作伙伴设置语音邮件预览

如果合作伙伴需要自定义设置，则您可能需要再为语音邮件预览合作伙伴设置以下两个参数：

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

在此示例中，在名为 *MyUMMailboxPolicy* 的 UM 邮箱策略中，将最大邮件时长设置为 300 秒（5分钟），将最长发送延迟设置为 600 秒（10 分钟）。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## 第 4 步︰ 为 UM 邮箱策略启用 UM 的用户分配为语音邮件预览伙伴

如果您想要配置的语音邮件预览合作伙伴服务的部分，而不是全部，启用 UM 的用户，在 UM 拨号计划，您必须创建新的 UM 邮箱策略并配置伙伴设置。当您已完成后，可新策略应用到选定的已启用 UM 的用户。有关如何启用 UM 的用户分配一个 UM 邮箱策略的详细信息，请参阅下列主题︰

  - [将 UM 邮箱策略分配](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/zh-cn/library/bb124893\(v=exchg.150\))

有关语音邮件预览合作伙伴计划的详细信息，请参阅 [语音邮件预览顾问](voice-mail-preview-advisor-exchange-2013-help.md)。

