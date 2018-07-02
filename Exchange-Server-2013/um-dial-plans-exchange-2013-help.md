﻿---
title: 'UM 拨号计划: Exchange Online Help'
TOCTitle: UM 拨号计划
ms:assetid: ed7afc03-94af-4b23-8745-6a61f203c149
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125151(v=EXCHG.150)
ms:contentKeyID: 50491897
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 拨号计划

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-21_

统一消息 (UM) 拨号计划是统一消息的主要组件并且是在网络上成功部署统一消息语音邮件必不可少的。以下各部分讨论了 UM 拨号计划以及如何在 UM 部署中使用它们。

## UM 拨号计划概述

UM 拨号计划代表共享公用用户分机号码的专用交换机 (PBX) 或 IP PBX 组。在拨号计划中的 PBX 或 IP PBX 上托管的所有用户的分机号都包含相同的位数。用户在拨打其他用户的电话分机时，可以不必为分机加拨特殊号码，也不必拨打完整的电话号码。

UM 拨号计划镜像了电话服务拨号计划。电话拨号计划是在 PBX 或 IP PBX 上配置的。

在统一消息中可以存在下列 UM 拨号计划拓扑：

  - 代表拥有一台 PBX 或 IP PBX 的组织的部分分机或所有分机的一个拨号计划。

  - 代表拥有多台联网 PBX 或 IP PBX 的组织的部分分机或所有分机的一个拨号计划。

  - 代表拥有一台 PBX 或 IP PBX 的组织的部分分机或所有分机的多个拨号计划。

  - 代表拥有多台 PBX 或 IP PBX 的组织的部分分机或所有分机的多个拨号计划。

属于同一拨号计划的用户具有下列特征：

  - 在拨号计划中唯一标识用户邮箱的分机号码。

  - 可以只使用分机号码呼叫拨号计划中的其他成员或向拨号计划中的其他成员发送语音邮件。

有关如何启用用户的统一消息的详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

在统一消息中使用 UM 拨号计划可以确保用户电话分机是唯一的。在某些电话网络中，可以存在多台 PBX 或 IP PBX。在此类电话网络中，可能会存在两个拥有相同电话分机号的用户。UM 拨号计划可以解决这种情况。将这两个用户放入两个不同的 UM 拨号计划中可以使他们的分机成为唯一分机。

## 拨号计划的工作方式

将电话网络与统一消息集成在一起时，必须有一个或多个称为网络电话 (VoIP) 网关或 IP PBX 的硬件设备，将电话网络与基于 IP 的数据包交换网络连接在一起。VoIP 网关将电话网络中的来自 PBX 的电路交换协议转换为数据交换协议（例如 IP）。IP Pbx 还将电路交换协议转换为数据交换的协议。会话边界控制器 (SBC) 可让您在公共或私有 WAN 上将两个基于 IP 的网络连接到一起并在 UM 混合或联机部署中发现它们。组织中每个 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 都用 UM IP 网关表示。有关 UM IP 网关的详细信息，请参阅[UM IP 网关](um-ip-gateways-exchange-2013-help.md)。

统一信息要求创建至少一个 UM 拨号计划。无论创建一个还是多个拨号计划，组织中的所有 Exchange 服务器将会应答传入呼叫。还必须有单个或多个与拨号计划关联的 UM IP 网关。在内部部署和混合部署中，在安装 Exchange 服务器和关联 UM IP 网关后，所有 Exchange 服务器将会应答所有拨号计划的传入呼叫。然而，对于内部部署和混合部署，当集成 Exchange 和 Lync Server 时，必须创建 SIP URI 拨号计划。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每次创建 UM 拨号计划时，也会创建一个默认 UM 邮箱策略。UM 邮箱策略将命名为 &lt;<em>Dial Plan Name</em>&gt; 默认策略。可以删除或以不同的方式配置此 UM 邮箱策略。</td>
</tr>
</tbody>
</table>


如果在创建第一个 UM IP 网关时指定了 UM 拨号计划，则还会创建默认 UM 智能寻线。创建这些组件可让 Exchange 服务器接收来自 VoIP 网关、IP PBX 或 SBC 的呼叫，然后为与 UM 拨号计划关联的用户处理那些传入呼叫。在内部部署或混合部署中，在有呼叫进入 VoIP 网关、IP PBX 或 SBC 时，它会将此呼叫转发到客户端访问服务器。然后客户端服务器会将呼叫转发至邮箱服务器，并且邮箱服务器将尝试将用户的分机号码与关联的 UM 拨号计划匹配。

## 拨号计划的类型

统一资源标识符 (URI) 是一个字符串（数字或字母），用来标识或命名资源。在统一消息中，URI 的主要用途是允许 VoIP 设备通过特定的协议与其他设备通信。URI 定义了用于呼叫方及被叫方信息的命名和编号格式或方案，该信息包含在传入或传出呼叫的会话初始协议 (SIP) 标头中。

统一消息中创建的 UM 拨号计划类型取决于组织中受 VoIP 网关或 IP PBX 支持的 URI 类型。URI 类型为从 PBX 或 IP PBX 发送的字符串类型。在创建拨号计划时，应了解 PBX 或 IP PBX 所支持的特定 URI 类型。可以在 UM 拨号计划上配置以下三种格式或 URI 类型：

  - 电话分机 (TelExtn)

  - SIP URI

  - E.164

默认情况下，每次在统一消息中创建拨号计划时，创建的拨号计划将使用电话分机 URI 类型。在创建拨号计划后，将无法更改该 URI 类型。您必须删除现有拨号计划并使用正确的 URI 类型另行创建一个。

## 电话分机 URI 类型

电话分机 URI 类型是 UM 拨号计划中最常见的类型，与 IP PBX 和 PBX 配合使用。在配置电话分机 (TelExtn) 拨号计划时，使用的 VoIP 网关、PBX 和 IP PBX 必须支持 TelExtn URI 类型。如今，大多数 PBX 和 IP PBX 都支持此 URI 类型。

当 PBX 接到呼叫而启用 UM 的用户无法应答呼叫时，PBX 将把该呼叫转发给 VoIP 网关。如果使用了 VoIP 网关或 IP PBX 中的一个，会将呼叫从基于电路的协议转换为基于 IP 的协议。在 SIP 包（该包从 VoIP 网关或 IP PBX 接收）的标头中，呼叫方和被叫方信息将采用以下某种格式列出：

  - 电话：512345

  - 512345@\<*IP 地址*\>

所用的电话分机 (TelExtn) 格式基于 VoIP 网关或 IP PBX 的配置。

## SIP URI 类型

会话初始协议 (SIP) 是一种用于初始化交互用户会话（其中包括一些多媒体元素，如视频、音频、聊天和游戏）的标准协议。SIP 是一种基于请求到响应的协议，它回答来自客户端的请求和来自服务器的响应。客户端由 SIP URI 标识。可以通过任何传输协议（如 UDP 或 TCP）发送请求。SIP 通过选择通信介质和介质参数来确定用于会话的终结点。

在创建新的拨号计划时，如果您的环境部署有 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server，则可选择创建 SIP URI 拨号计划。如果您的组织有 IP PBX 或启用 SIP 的 PBX，也可创建 SIP URI 拨号计划。在后一种情况中，您的组织还必须支持 SIP URI 和 SIP 路由。

SIP URI 是用户的 SIP 电话号码。SIP URI 类似于电子邮件地址，并用以下格式书写：sip*:\<user name\>@\<domain or IP address\>*：*Port*。当通过启用了 SIP 的 IP PBX 或 PBX 向 Exchange 服务器发送呼叫时，该设备将发送位于 SIP 标头中呼叫方或被叫方的 SIP URI，而不包括分机号码。

## E.164 URI 类型

E.164 是一种标准的编号格式，它定义了在公用电话交换网 (PSTN) 和一些数据网络中所使用的国际公用电信编号计划。E.164 定义了电话号码的格式。E.164 号码最多可有 15 位数，并且一般在电话号码的数字前有一个加号 (+)。若要通过电话拨打 E.164 格式的电话号码，所拨的号码中必须包括正确的国际呼叫前缀。在公用电话系统的 E.164 编号计划中，每个指定的号码都包含一个国家/地区代码 (CC)、一个国内目的地代码 (NDC) 和一个订阅者号码 (SN)。

在创建新拨号计划时，可以选择创建 E.164 拨号计划。不过，如果创建和配置 E.164 拨号计划，PBX 和 IP PBX 必须支持 E.164 路由。从与 E.164 拨号计划关联的 VoIP 网关接收的 SIP 标头将包括呼叫方和被叫方的 E.164 格式的电话号码和信息，并且将采用以下格式列出：电话号码：+14255550123。对于与 Exchange 统一信息和 Lync Server 的 Exchange Online 部署，必须使用 Outlook Voice Access 格式正确的 E.164 号码和自动助理号码。

## VoIP 安全性

Exchange 服务器可以在不安全、SIP 安全或安全模式下与 VoIP 网关、IP PBX 及其他 Exchange 计算机进行通信，这具体取决于配置 UM 拨号计划的方式。在内部部署和混合部署中，客户端访问服务器和邮箱服务器可在拨号计划上配置的任何模式下工作，因为如果将 TCP 端口 5060 和 5061 配置为以双协议栈模式启动，服务器会针对不安全请求监听 TCP 端口 5060，同时针对安全请求监听 TCP 端口 5061。客户端访问和邮箱服务器会应答所有 UM 拨号计划的所有传入呼叫，但是这些拨号计划可具有不同的 VoIP 安全设置。

在内部部署和混合部署中，默认情况下，创建 UM 拨号计划时，它将使用不安全模式进行通信，并且客户端访问和邮箱服务器将使用非加密方式收发来自 VoIP 网关、IP PBX 及 SBC 的数据。在非安全模式下，实时传输协议 (RTP) 媒体通道与 SIP 信号信息都不会进行加密。可以使用命令行管理程序中的 **Get-UMDialPlan** cmdlet 来确定特定 UM 拨号计划的安全设置。

在内部部署和混合部署中，可以将客户端访问和邮箱服务器配置为使用相互传输层安全性（相互 TLS）对从其他设备和服务器发送和接收的 SIP 和 RTP 通信进行加密。在配置拨号计划以使用 SIP 安全模式时，只对 SIP 信号通信进行加密，RTP 媒体通道将仍然使用不进行加密的 TCP。但是，如果您配置拨号计划以使用安全模式，会将 SIP 信号通信和 RTP 媒体通道加密。使用安全实时传输协议 (SRTP) 的加密信号媒体通道还将使用相互 TLS 来加密 VoIP 数据。

在创建新拨号计划时或在创建拨号计划之后，可以通过在命令行管理程序中使用 EAC 或 **Set-UMDialPlan** cmdlet 来配置 VoIP 安全模式。将 UM 拨号计划配置为使用 SIP 安全或安全模式时，客户端访问和邮箱服务器将加密 SIP 信号通信或 RTP 媒体通道，或者同时加密两者。但是，为了能够通过 Exchange 服务器收发加密数据，必须正确配置 UM 拨号计划，并且 VoIP 设备（例如 VoIP 网关、IP PBX 和 SBC）必须支持相互 TLS。

## Outlook Voice Access

下列两种类型的呼叫者将使用 UM 拨号计划中配置的 Outlook Voice Access 号码来访问语音邮件系统：未经身份验证的呼叫者和经过身份验证的呼叫者。当呼叫者拨打拨号计划中配置的 Outlook Voice Access 号码时，则在输入包括语音邮件分机和 PIN 在内的信息之前，这些呼叫者将被视为匿名呼叫者或未经身份验证的呼叫者。为匿名或未经身份验证的呼叫者提供的唯一选项是目录搜索功能。呼叫者输入其语音邮件分机号和 PIN 后，系统将对其进行身份验证，并给予他们访问其邮箱的权限。呼叫者获取对语音邮件系统的访问权限后，可以使用 Outlook Voice Access 功能。

Outlook Voice Access 是一系列语音提示，这些提示给予呼叫者访问电子邮件、语音邮件、日历和其他信息的权限。Outlook Voice Access 可使经过身份验证的呼叫者使用双音多频 (DTMF)（也称为按键）或语音输入在其邮箱中导航个人信息、发出呼叫或查找用户。

## Outlook Voice Access 号码

创建 UM 拨号计划之后，您需要至少添加一个 Outlook Voice Access 号码。Outlook 语音访问号码也称为拨号计划引导号码。此号码供 Outlook Voice Access 用户用来访问其邮箱，并使他们可以搜索目录。

默认情况下，创建 UM 拨号计划时，不会配置 Outlook Voice Access 号码。要让用户使用 Outlook Voice Access 功能，必须至少配置一个电话或分机号码。Outlook Voice Access 号码中的字母数字字符数不能超过 20 个。在拨号计划上配置此号码后，此号码将显示在 Microsoft Outlook 中的语音邮件选项中和 Outlook Web App 中。

您可使用 UM 拨号计划上的\&quot;Outlook Voice Access 号码\&quot; 框来添加电话号码或分机号，用户将呼叫这些号码借助 Outlook Voice Access 来访问语音邮件系统。大多数情况下，应当输入分机号码或外部电话号码。但是，由于此字段接受字母数字字符，因此，如果正在使用 IP PBX、启用 SIP 的 PBX、Office Communications Server 2007 R2 或 Microsoft Lync Server，则可以使用 SIP URI。

根据您组织的需求，可能需要配置一个或多个 Outlook Voice Access 号码。您可以在一个 UM 拨号计划中配置一个 Outlook Voice Access 号码，也可以在一个 UM 拨号计划中拥有多个 Outlook Voice Access 号码，但是您不能配有一个跨多个 UM 拨号计划的单个 Outlook Voice Access 号码。

