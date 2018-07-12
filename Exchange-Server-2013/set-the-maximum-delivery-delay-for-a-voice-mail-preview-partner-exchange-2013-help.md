---
title: '语音邮件预览合作伙伴设置最大传递延迟: Exchange Online Help'
TOCTitle: 语音邮件预览合作伙伴设置最大传递延迟
ms:assetid: c9a07f6d-6f7f-4036-9a4a-d668d21e2c76
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff630928(v=EXCHG.150)
ms:contentKeyID: 51408276
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 语音邮件预览合作伙伴设置最大传递延迟

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-13_

统一消息 (UM) 邮箱策略上，您可以设置语音邮件预览合作伙伴最大传递延迟。已经设置的最大的交付延迟之后，设置将应用于与该 UM 邮箱策略链接的所有已启用 UM 的用户。

> [!NOTE]  
> 您必须使用命令行管理程序来设置语音邮件预览合作伙伴的最长送达延迟时间。


有关语音邮件预览伙伴计划的详细信息，请参阅[语音邮件预览顾问](voice-mail-preview-advisor-exchange-2013-help.md)。

有关与语音邮件预览相关的其他管理任务，请参阅[语音邮件预览过程](voice-mail-preview-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序设置语音邮件预览合作伙伴的最长送达延迟时间

该示例在名为 *MyUMMailboxPolicy* 的 UM 邮箱策略上将最长送达延迟时间设置为 600 秒（10 分钟）。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy - VoiceMailPreviewPartnerMaxDeliveryDelay 600

