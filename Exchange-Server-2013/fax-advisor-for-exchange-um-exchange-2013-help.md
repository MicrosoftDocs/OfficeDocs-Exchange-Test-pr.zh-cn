---
title: '对于 Exchange UM 传真顾问: Exchange Online Help'
TOCTitle: 对于 Exchange UM 传真顾问
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52061381
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 对于 Exchange UM 传真顾问

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft统一消息 (UM) 依赖于认证的传真的传真增强的功能，如传真路由或出站传真的合作伙伴解决方案。默认情况下，用户不能配置以允许传入传真消息传递到已启用 UM 的用户。Exchange 服务器将传真请求发送到传真认证的合作伙伴解决方案。传真伙伴的服务器接收传真数据，然后将其发送到收件人的邮箱中的电子邮件与传真包含.tif 附件的形式。有关详细信息，请参阅[为语音邮件用户启用接收传真功能](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>我们建议计划部署统一消息的所有客户都获取统一消息专家的协助。统一消息专家可帮助您确保有平稳过渡到统一消息从传统语音邮件系统。执行新部署或升级旧的语音邮件系统需要重大的 Pbx 和统一消息有关的知识。有关如何联系统一消息专家的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013年统一消息 (UM) 专家</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft 查明其统一消息</a>。</td>
</tr>
</tbody>
</table>


## Exchange 统一消息传真伙伴计划

若要成为与 UM 交换的互操作性鉴定传真合作伙伴，合作伙伴必须实现传真合作伙伴的互操作性规范中所包含的要求，必须由独立的认证供应商认证的传真解决方案。有关验证传真产品使用 Exchange 统一消息的详细信息，将申请提交到[统一消息传真合作伙伴](mailto:fax-part@microsoft.com)。

## 经过认证可与统一消息互操作的传真伙伴解决方案

如果您没有部署 Exchange 统一消息，并正在寻找可以使您的组织的传入传真的传真合作伙伴，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/p/?linkid=190238)。这些软件供应商已被认证为与 Exchange Server 互操作和统一消息包括认证的软件解决方案。

## VoIP、媒体网关和 IP PBX 支持

正确配置为您的组织的 VoIP 网关是一个困难的部署任务，必须完成成功地部署 Exchange 统一消息的传入传真。若要帮助回答问题并获取最新的 VoIP 网关配置信息，请参阅[Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)。[支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)提供 VoIP 网关配置说明和您必须正确地配置您的组织的 VoIP 网关，IP Pbx 和 SBCs 使用 Exchange 统一消息的文件。

现在与Microsoft统一通信打开的互操作性程序集成的 Exchange 统一消息使用 VoIP 网关的互操作性测试。有关详细信息，请参阅[Microsoft 统一通信开放互操作性程序](http://go.microsoft.com/fwlink/p/?linkid=140722)。

[Microsoft 统一通信开放式互操作性计划](http://go.microsoft.com/fwlink/p/?linkid=140722)资格计划专门用于 VoIP 网关和 IP PBX，可以确保客户将合格的电话网关和 IP PBX 以及 Microsoft 统一通信软件结合使用时，拥有无缝的安装体验和支持体验。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在统一消息和 Communications Server 2007 R2 或 Microsoft Lync Server 相集成的环境中，不支持使用 T.38 或 G.711 发送和接收传真。</td>
</tr>
</tbody>
</table>


## 部署和配置传真

UM 将转发到专用的传真合作伙伴解决方案，然后建立向传真发件人的传真呼叫并接收代表已启用 UM 的用户传真的传入传真呼叫。但是，若要允许已启用 UM 的用户在其邮箱中接收传真，您必须配置传真伙伴服务器，UM 拨号计划、 UM 邮箱策略，然后将配置和启用已启用 UM 的用户接收传真。有关详细信息，请参阅[设置传入传真](setting-up-incoming-faxing-exchange-2013-help.md)。

