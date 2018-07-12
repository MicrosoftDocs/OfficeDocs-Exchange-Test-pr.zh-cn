---
title: '配置侦听端口: Exchange Online Help'
TOCTitle: 配置侦听端口
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50556540
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置侦听端口

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置用于侦听会话启动协议 (SIP) 统一邮件 (UM) IP 网关的请求的 TCP 端口。默认情况下，当您创建 UM IP 网关的 SIP TCP 侦听的端口号设置为 5060。无法配置或通过 EAC 更改 SIP TCP 侦听端口。通过使用**Set-UMIPGateway** cmdlet，您必须配置 SIP TCP 侦听的端口号。

如果您要进行以下操作，必须将 TCP 侦听端口号配置为 5061：

  - 将 UM 拨号计划中的 VoIP 安全设置设为\&quot;SIP 安全\&quot;。

  - 将 UM 拨号计划中的 VoIP 安全设置设为\&quot;安全\&quot;。

  - 与 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server 集成。

  - 使用相互传输层安全性（相互 TLS）对 Exchange 服务器和 VoIP 网关、针对 SIP 启用的专用交换机 (PBX)、IP PBX 或会话边界控制器 (SBC) 之间的网络数据进行加密。

如果您要在 UM IP 网关和在\&quot;SIP 安全\&quot;模式或\&quot;安全\&quot;模式下运行的拨号计划之间使用相互 TLS，则在您创建 UM IP 网关时，必须使用完全限定域名 (FQDN) 对其进行配置，然后使用命令行管理程序配置 UM IP 网关，以侦听 TCP 端口 5061。您必须验证任何 VoIP 网关、针对 SIP 启用的 PBX、IP PBX 和 SBC 是否也配置为可侦听端口 5061 上的相互 TLS 请求。

> [!IMPORTANT]  
> 创建 UM IP 网关使用 FQDN 时，必须在您的 DNS 正向查找区域中创建相应的主机 (A) 记录。如果您创建 UM IP 网关使用 FQDN，并更改 DNS 配置 UM IP 网关，您必须禁用然后再启用 UM IP 网关，以确保正确更新后的 UM IP 网关的配置信息。


有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 执行此过程之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序配置 TCP 侦听端口

此示例配置了名为 `MyUMIPGateway` 的 UM IP 网关，该网关具有名为 mTLS.MyUMIPGateway.contoso.com 的 FQDN，并侦听 TCP 端口 5061 上的 SIP 请求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

此示例配置了名为 `MyUMIPGateway` 的 UM IP 网关，该网关具有名为 SIPSecured.MyUMIPGateway.contoso.com 的 FQDN，并侦听 TCP 端口 5061 上的 SIP 请求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

此示例配置了名为 `MyUMIPGateway` 的 UM IP 网关，该网关具有名为 MyOCSUMIPGateway.contoso.com 的 FQDN，并侦听 TCP 端口 5061 上的 SIP 请求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

