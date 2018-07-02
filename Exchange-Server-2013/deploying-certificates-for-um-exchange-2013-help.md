---
title: '为 UM 部署证书: Exchange 2013 Help'
TOCTitle: 为 UM 部署证书
ms:assetid: 95658f6f-eac2-4674-90e7-f2d3f25c5242
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee681661(v=EXCHG.150)
ms:contentKeyID: 52061538
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为 UM 部署证书

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-29_

您可以使用相互传输层安全性 (相互 TLS) 来启用统一邮件 (UM) Microsoft Exchange 2013 服务器和 VoIP 网关，IP Pbx，会话边框控制器 (SBCs) 之间发送的数据进行加密和 Microsoft Lync Server。证书将用于加密和数字签名的信息到一个电子密钥 （公钥和私钥） 对证书所有者的身份绑定。

如果您使用的 SIP 安全或 Exchange 2010 组织中的安全拨号计划，您将需要使用证书导入到运行 Microsoft Exchange UM 呼叫路由器服务的 Exchange 2013 客户端访问服务器和邮箱服务器运行 UM Microsoft Exchange 服务。您可以使用下列证书之一的 UM 和 UM 呼叫路由器的服务 ︰

  - 自签名 (Exchange) 证书

  - 内部公钥基础结构 (PKI) 证书

  - 第三方商业证书

默认情况下，安装统一消息时自行签署式证书创建和使用。与 VoIP 网关，IP Pbx 和 SBCs，而不是在您正在使用 Lync Server 集成 UM 可以使用自签名的证书。如果正在部署证书使用 Lync Server，您需要使用交换证书向导或**New-ExchangeCertificate** cmdlet 将获得由内部颁发的证书或 PKI 证书颁发机构 (CA) 或商业或第三方购买证书，由统一消息和 Lync 服务器相互信任。

## 为 VoIP 网关、IP PBX 和 SBC 部署证书

要启用 UM 以便对 VoIP 网关、IP PBX 和 SBC 之间发送的数据进行加密，需要执行下列操作：

  - 使用自签名 UM 证书，创建新的 Exchange 证书请求，获取内部 PKI 证书，或者购买可用于 UM 与 VoIP 网关、IP PBX 和 SBC 之间的相互 TLS 的第三方商业证书。

  - 导入将在组织中所有客户端访问服务器和邮箱服务器上使用的证书。

  - 允许证书供 UM 服务使用。

  - 将证书导入到 VoIP 网关、IP PBX 和 SBC。

  - 将 UM 拨号计划配置为\&quot;SIP 安全\&quot;或\&quot;安全\&quot;。

  - 在组织中的客户端访问服务器和邮箱服务器上配置 UM 启动模式。

  - 使用完全限定域名 (FQDN) 创建所需的 UM IP 网关。

  - 配置 UM IP 网关上的侦听端口以使用 TLS 端口 5061。

  - 在所有客户端访问服务器上重新启动统一消息呼叫路由器，并在所有邮箱服务器上重新启动 Microsoft Exchange 统一消息服务。

## 为 Lync Server 部署证书

要对 UM 与 Lync Server 之间发送的数据进行加密，需要执行下列操作：

  - 创建新的交换证书申请并获得内部 PKI 证书，或购买第三方专业证书。证书必须由 UM 和 Lync 服务器相互信任。

  - 导入将在组织中所有客户端访问服务器和邮箱服务器上使用的证书。

  - 允许证书供 UM 服务使用。

  - 将证书导入到运行 Lync Server 的计算机。

  - 将 SIP URI UM 拨号计划配置为\&quot;SIP 安全\&quot;或\&quot;安全\&quot;。

  - 在组织中的客户端访问服务器和邮箱服务器上配置 UM 启动模式。

  - 从 Lync Server 计算机运行 OcsUmUtil.exe。

  - 重新启动所有客户端访问服务器上的统一消息呼叫路由器服务并重新启动组织中的所有邮箱服务器上的 Microsoft Exchange 统一消息服务。有关详细信息，请参阅[UM 服务过程](um-services-procedures-exchange-2013-help.md)。

  - 重新启动所有 Lync 服务器前端企业版池的一部分或重新启动标准版前端服务器上的 Lync 服务器前端服务。您可以使用**Stop-CsWindowsService** cmdlet Lync Server 服务和**Start-CsWindowsService**用于启动 Lync Server 服务停止。
    
    **Start-CsWindowsService**和**Stop-CsWindowsService** cmdlet 都类似于一般 Windows PowerShell cmdlet **Start-Service**和**Stop-Service**。如果需要，您可以使用**Start-Service**或**Stop-Service** cmdlet 启动和停止 Lync Server 服务。但是， **Start-CsWindowsServiceStop-CsWindowsService** cmdlet 包括容易地停止和启动 Lync 服务器服务的远程计算机上的*ComputerName*参数。若要执行此操作，您可以包括跟远程计算机的完全限定的域名 (FQDN) 的*ComputerName*参数。**Start-Service**和**Stop-Service** cmdlet 没有可比较的参数。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>要使 UM 与 Lync Server 完全集成，还必须在组织中的任何客户端访问服务器或邮箱服务器上运行 ExchUcUtil.ps1 脚本。</td>
    </tr>
    </tbody>
    </table>

