---
title: '将 UM 连接到电话系统: Exchange 2013 Help'
TOCTitle: 将 UM 连接到电话系统
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50556636
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将 UM 连接到电话系统

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-30_

统一消息 (UM) 结合语音邮件和电子邮件消息到一个可以从许多不同的设备中访问的邮箱。用户可以收听语音邮件通过 Outlook Voice Access 从任何电话或电子邮件收件箱。

当您在 Microsoft Exchange 组织中部署 UM 时，必须安装、 部署和配置 IP (VoIP) 网关连接到电话网络中专用分组交换机 (Pbx) 或安装、 部署和配置会话初始化协议 SIP 启用 Pbx 或 IP Pbx 上的单个或多个声音。如果您要升级您当前的语音邮件系统，将需要部署到您的电话网络连接的设备的安装您 Exchange 客户端访问服务器和邮箱服务器，然后创建所需的 UM 组件，使电话网络连接到您的数据网络。这使传入呼叫的电话网络连接到您的 VoIP 网关，IP Pbx 或 SIP 启用 Pbx 和这些设备连接到您的 Exchange 组织。

如果您正在安装、 部署和配置 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync 服务器，将不会使用 VoIP 网关，IP Pbx 或 SIP 启用 Pbx 来直接连接到 Exchange 统一消息。相反，Lync 中介服务器和 VoIP 网关或高级的 VoIP 网关具有中介服务器的功能和 VoIP 网关将允许您连接到 UM 交换。企业语音为启用 UM 用户可以检索、 欣赏，和回复语音邮件和进行出站呼叫。他们还可以访问其他 Lync 相关的功能，包括使用 Office Communicator 或 Lync 客户端出席信息和即时消息 (IM)。

以下信息将帮助您设置和部署 UM 并启用语音邮件功能为您的组织中的用户 ︰

  - [将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)  了解如何连接 UM VoIP 网关或 IP Pbx。

  - [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)  了解有关支持 VoIP 网关，IP Pbx 和 Pbx。

  - [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) 了解如何设置您的 VoIP 网关，IP Pbx 和 Pbx。

