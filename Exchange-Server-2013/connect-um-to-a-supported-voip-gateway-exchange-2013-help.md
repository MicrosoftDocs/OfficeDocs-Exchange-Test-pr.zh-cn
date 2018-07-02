---
title: '将 UM 连接到支持 VoIP 网关: Exchange 2013 Help'
TOCTitle: 将 UM 连接到支持 VoIP 网关
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50556665
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将 UM 连接到支持 VoIP 网关

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-04-19_

在设置了统一邮件 (UM) 时，您必须配置与运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和邮箱服务器Exchange组织中运行 Microsoft Exchange 统一消息服务通信网络上通过 IP (VoIP) 网关，IP Pbx、 SIP 启用 Pbx 或会话边框控制器 (SBCs) 声音。您还必须配置与 VoIP 网关，IP Pbx、 SIP 启用 Pbx 或 SBCs 进行通信的客户端访问和邮箱服务器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在将客户端访问服务器和邮箱服务器连接到数据网络上的 VoIP 网关、IP PBX、启用了 SIP 的 PBX 或 SBC 之后，您必须创建所需的 UM 组件，同时为用户启用统一消息，使其能使用语音邮件系统。</td>
</tr>
</tbody>
</table>


## 步骤

以下是将 VoIP 网关、IP PBX、启用了 SIP 的 PBX 或 SBC 连接到客户端访问服务器和邮箱服务器的基本步骤：

步骤 1 ︰ 您的组织中安装在客户端访问、 邮箱服务器。

步骤 2 ︰ 创建和配置电话分机、 SIP URI 或 E.164 UM 拨号计划。

步骤 3 ︰ 创建和配置 UM IP 网关。您必须创建和配置每个 VoIP 网关，IP PBX、 SIP 启用 PBX 或将接受传入的呼叫和发送的传出呼叫的 SBC 的 UM IP 网关。

如果需要则第 4 步 ︰ 创建新的 UM 查寻组。如果您创建 UM IP 网关，并没有指定 UM 拨号计划，将自动创建 UM 查寻组。

有关每一步的信息，请参见以下部分。

## 步骤 1 ︰ 将安装客户端访问和邮箱服务器

当您正在您的组织中部署 Exchange 服务器时，可以在同一台计算机上安装客户端访问和邮箱服务器或邮箱服务器中的单独计算机上安装客户端访问服务器。若要安装客户端访问服务器，请从安装介质运行 Setup.exe。在从邮箱服务器的单独计算机上安装客户端访问服务器或将其安装在同一台计算机上时，您可以使用相同的命令。有关详细信息，请参阅[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)。如果您想要将功能添加到您现有的 Exchange 服务器，您可以使用**程序和功能**或 Setup.exe。

## 步骤 2 ︰ 创建和配置 UM 拨号计划

安装所需的服务器之后，您必须首先创建 UM 拨号计划。UM 拨号计划中包含的配置设置，使您能够通过将链接到一个或多个 UM IP 网关连接到电话网络。UM IP 网关和 UM 查寻组直接链接到 UM 拨号计划，还需要。有关详细信息，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

UM 拨号计划建立从用户的电话分机号码链接到启用 UM 的邮箱。创建 UM 拨号计划时，可以配置分机号码、 统一资源标识符 (URI) 类型和 VoIP 安全设置为拨号计划中的数字位数。

有三种类型的拨号计划 ︰ 电话分机、 会话启动协议 (SIP) URI 以及 E.164。当您创建并配置 UM 拨号计划时，必须确定 PBX，或 PBX 和调用发送到电话分机或 E.164 格式的客户端访问或邮箱服务器是否从您的 IP PBX、 SIP 启用已发送的信息的类型。如果您正在部署 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server，您必须创建和配置 SIP URI 的拨号计划。

## 步骤 3 ︰ 创建并配置 UM IP 网关

在创建后 UM 拨号计划，您必须创建 UM IP 网关来表示每个 VoIP 网关，IP PBX 或 SBC 在您的网络上。创建 UM IP 网关时，您可以配置它以使用一个 IP 地址或完全合格的域名称 (FQDN)。如果您使用 FQDN，必须确保已经正确地配置了 DNS 主机记录的 IP 网关使主机名称将被正确解析为 IP 地址。

VoIP 网关，IP PBX 或 SBC 安装后，您必须创建一个 UM IP 网关来表示物理硬件设备。创建 UM IP 网关之后，使用 UM IP 网关的客户端访问服务器会发送 SIP 选项请求 VoIP 网关，IP PBX 或 SBC 以确保快速响应。如果 VoIP 网关，IP PBX、 SIP 启用 PBX、 或 SBC 未响应，客户端访问服务器将记录事件 ID 1088 声明，请求失败。要解决此问题，请确保 VoIP 网关，IP PBX 或 SBC 是可用而且在线，统一消息配置正确。

客户端访问和邮箱服务器将只使用 VoIP 网关，IP PBX 或被列为受信任的 SIP 对等端的 SBC 进行通信。在某些情况下，如果两个 VoIP 网关，IP Pbx 或 SBCs 被配置为使用相同的 IP 地址，将记录事件 ID 1175。如果您已经在网络上 DNS 区域配置了 VoIP 网关为完全限定的域名 (Fqdn)，则可能发生此事件。统一消息可防止未授权的请求通过检索位于邮箱服务器的统一消息的 Web 服务虚拟目录的内部 URL，然后使用 URL 为受信任的 SIP 构建的 Fqdn 的列表同级。两个 Fqdn 解析为相同的 IP 地址之后，将记录此事件。

如果 UM IP 网关配置为使用 FQDN 和 UM IP 网关的 DNS 记录更改启动该服务后，必须重新启动MicrosoftExchange统一消息服务。如果不重新启动该服务，邮箱服务器无法查找 UM IP 网关。因为邮箱服务器维护的缓存在内存中的所有 UM IP 网关和 DNS 解析只有在服务重新启动时执行或 VoIP 网关，IP PBX 或 SBC 的配置发生更改时，将发生这种情况。

Exchange 统一消息支持各种 VoIP 网关供应商和其他供应商提供的 IP Pbx、 SIP 启用 Pbx 和 SBCs。每个受支持 VoIP 网关用于连接到各种第三方 PBX 系统。

有关 VoIP 网关的详细信息，请参阅下列主题：

  - [创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)

  - [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

有关详细信息，请参阅[连接到电话网络的语音邮件系统](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)。

## 步骤 4 ︰ 创建新的 UM 查寻组 （如果需要）

\&quot;智能寻线\&quot;一词用于描述由用户共享的一组专用交换机 (PBX) 或者 IP PBX 分机号码。使用智能寻线可以有效地将呼叫转接进或转接出特定的业务单位。创建并定义智能寻线，可以使接到传入呼叫时，呼叫者听到忙音的几率最小。

UM 查寻组镜像 Pbx 和 IP Pbx 使用查寻组。您的 Pbx 或 IP Pbx 配置时，您必须创建并配置一个或多个 UM 查寻组。UM 查寻组充当 UM IP 网关与 UM 拨号计划之间的链接。

这取决于如何创建 UM IP 网关，您可能需要创建一个或多个新的 UM 查寻组。如果没有链接的 UM IP 网关与某个拨号计划创建 UM IP 网关时，默认情况下创建单个 UM 查寻组。如果链接 UM IP 网关与 UM 拨号计划，当您创建 UM IP 网关、 所有传入呼叫将被发送通过 UM IP 网关和服务器客户端访问和邮箱服务器将接受这些调用。如果创建 UM IP 网关时，不链接到 UM 拨号计划的 UM IP 网关，您需要使用拨入的呼叫转发从 UM IP 网关与拨号计划正确引导标识符创建 UM 查寻组。

如果您有多个 Outlook Voice Access 并自动助理号码并已链接到拨号计划的 UM IP 网关，您将需要删除 UM 查寻组，默认情况下创建并创建多个 UM 查寻组。有关如何创建 UM 查寻组，请参阅[创建 UM 智能寻线](create-a-um-hunt-group-exchange-2013-help.md)。

