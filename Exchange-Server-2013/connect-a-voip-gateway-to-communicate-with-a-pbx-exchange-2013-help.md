---
title: '连接 VoIP 网关以便与 PBX 通信: Exchange 2013 Help'
TOCTitle: 连接 VoIP 网关以便与 PBX 通信
ms:assetid: 76bcdc54-3ec2-408a-bdbe-37826580dd62
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998872(v=EXCHG.150)
ms:contentKeyID: 50556601
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 连接 VoIP 网关以便与 PBX 通信

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-15_

在 Exchange Server 2013 中配置统一消息 (UM) 的电话网络和数据网络时，必须配置 VoIP 网关，以便这些网关与运行 Microsoft Exchange 统一消息呼呼叫路由器服务的客户端访问服务器以及运行 Microsoft Exchange 统一消息服务的邮箱服务器通信。同时，还必须地配置 VoIP 网关，以便与组织中的专用交换机 (PBX) 通信。可以使用本主题中的信息和链接配置 VoIP 网关以与 PBX 通信。

## 配置 VoIP 网关

配置 VoIP 网关时，必须考虑 VoIP 网关设备是模拟网关、数字网关还是模拟数字网关设备。如果连接 PBX 的 VoIP 网关接口是模拟接口，则必须正确地配置相应的设置，以便 VoIP 网关可以与 PBX 进行通信。如果连接 PBX 的 VoIP 网关接口是数字接口，则可能不需要进行附加配置，数字接口即可与 PBX 进行通信。

Exchange TechCenter 中的以下建议资源提供的信息可帮助您正确地配置 VoIP 网关和 PBX：

  - **支持的 VoIP 网关、IP PBX 和 PBX 文档**   [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)中包含在配置 VoIP 网关和 PBX 时可以使用的配置文件和设置信息。

  - **配置和技术说明**   [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)中包含在配置 VoIP 网关和 PBX 时可以使用的配置文件和设置信息。

  - **配置基于 AudioCodes 的 VoIP 网关** [Microsoft Exchange Server 资源页](https://www.audiocodes.com/solutions/microsoft/exchange-server)提供最新的支持和配置信息，以帮助您配置为使用基于 AudioCodes 的 VoIP 网关与统一消息。

  - **配置基于 Dialogic VoIP 网关**  [对话式的网站](https://www.dialogic.com/)提供 Dialogic 基于 VoIP 网关的最新支持和配置信息。

我们建议计划部署统一消息的所有客户都获取统一消息专家的协助。Exchange 统一消息专家将帮助确保平滑升级到统一消息从传统或没有第三方语音邮件系统和帮助您规划并部署新的语音邮件系统与 Exchange 统一消息。 部署新的语音邮件系统或升级一个传统语音要求有关 VoIP 网关、 Pbx，和统一消息的重要知识。有关如何联系统一消息专家的详细信息，请参阅[Microsoft Exchange Server 2013年统一消息 (UM) 专家](http://go.microsoft.com/fwlink/p/?linkid=262708)或在[Microsoft 查明其](https://go.microsoft.com/fwlink/p/?linkid=261951)的认证的 UM 合作伙伴。

## 详细信息

[支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

[将 UM 连接到支持 VoIP 网关](connect-um-to-a-supported-voip-gateway-exchange-2013-help.md)

