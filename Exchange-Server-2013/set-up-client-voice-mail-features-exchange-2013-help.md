---
title: '设置客户端语音邮件功能: Exchange 2013 Help'
TOCTitle: 设置客户端语音邮件功能
ms:assetid: 5e661cfd-d34e-4caa-91a5-967bbecb75eb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673529(v=EXCHG.150)
ms:contentKeyID: 50556586
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置客户端语音邮件功能

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-20_

本主题介绍使启用 Exchange 统一消息 (UM) 访问电子邮件和语音邮件消息在其邮箱的用户的客户端功能。这些功能使您可以提供您的用户简化的访问语音邮件和电子邮件和改进了整体的用户体验。

**目录**

Voice mail client support

Outlook Voice Access

Forwarding calls

Voice Mail Preview

Receiving faxes

## 语音邮件客户端支持

**Exchange ActiveSync 客户端**  使用 Microsoft Exchange ActiveSync协议连接移动客户端，如在互联网的移动设备，到 Exchange 邮箱上找到。用户可以使用移动设备来访问其邮箱和查看电子邮件、 查看和更改日历和联系人信息和收听语音邮件。它们还可以同步电子邮件、 语音邮件、 日历项，并与其他设备的联系信息。

**与 Outlook 集成**  Microsoft Outlook 使用户能够访问其 Exchange 邮箱和查看电子邮件在收件箱，查看和更改日历信息和收听语音邮件使用 Microsoft Windows Media Player，其中嵌入的电子邮件。使用支持的电子邮件客户端，用户获得其他功能，如电话播放功能。

**与 Outlook Web App 的集成**  Microsoft Outlook Web App为用户提供一套 UM 接口和工具媲美如 Outlook 功能完整的电子邮件客户端。与Outlook Web App，用户可以通过使用符合标准的 web 浏览器访问其 Exchange 邮箱。如 Outlook， Outlook Web App提供了 Windows Media Player 嵌入到电子邮件中，以便用户可以收听语音邮件，并使用户可以访问其他功能，如在电话上播放。

## Outlook Voice Access

在 Exchange 嗯，启用 UM 的用户可以连接到 UM 拨号计划要访问其邮箱和使用Outlook语音访问菜单系统上配置的内部或外部的电话号码。使用此菜单，启用 UM 的用户可以读取电子邮件、 收听语音邮件、 与他们的Outlook日历进行交互、 访问其个人联系人和执行任务，如配置其Outlook语音访问 PIN 或录制他们的语音邮件问候语。有关详细信息，请参阅[设置 Outlook Voice Access](https://technet.microsoft.com/zh-cn/library/dd298010(v=exchg.150))。

## 转移呼叫

已启用 UM 的用户可以创建和配置呼叫应答规则使用Outlook或Outlook Web App。呼叫应答规则允许用户控制应如何处理他们的来电。规则应用于传入的调用类似于收件箱规则应用于传入的电子邮件和其他语音设置在用户的邮箱存储的方式。最多九个呼叫应答规则可以设置为每个已启用 UM 的邮箱。这些规则的收件箱规则无关，并不会占据用户的收件箱规则存储配额的一部分。有关详细信息，请参阅[允许语音邮件用户转接来电](https://technet.microsoft.com/zh-cn/library/dd335138(v=exchg.150))。

## 语音邮件预览

语音邮件预览是从 UM 语音邮件系统接收语音邮件的用户都可以使用的功能。语音邮件预览增强语音邮件体验了通过提供录音的文本版本。有关详细信息，请参阅[允许用户查看语音邮件成绩单](https://technet.microsoft.com/zh-cn/library/ff629381(v=exchg.150))。

## 接收传真

UM 将转发到专用的传真合作伙伴解决方案，建立向传真发件人的传真呼叫，并代表用户传真接收传入传真呼叫启用 UM 的用户。已启用 UM 的用户可以在其邮箱中接收传真之前，必须执行以下操作 ︰

  - 通过将 *FaxEnabled* 参数设置为 `$true`，在链接至用户的 UM 拨号计划中启用入站传真。

  - 通过将 *Allowfax* 参数设置为 `$true`，在链接至用户的 UM 拨号计划中启用入站传真。

  - 通过将 *FaxEnabled* 参数设置为 `$true`，为用户启用入站传真。

  - 对合作伙伴的传真服务器 URI 进行设置，使其允许入站传真。

  - 配置邮箱服务器与传真合作伙伴服务器之间的身份验证。

