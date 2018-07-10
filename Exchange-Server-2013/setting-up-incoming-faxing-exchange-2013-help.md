---
title: '设置传入传真: Exchange Online Help'
TOCTitle: 设置传入传真
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52061357
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置传入传真

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

Microsoft 统一消息 (UM) 依赖于通过认证的传真合作伙伴解决方案，实现诸如发送传真或传真路由等增强的传真功能。默认情况下，Exchange 服务器不会配置为允许将传入传真传递给启用 UM 的用户。相反地，Exchange 服务器会将传入传真呼叫重定向至认证的传真合作伙伴解决方案中。传真伙伴的服务器收到传真数据后，以 .tif 附件的形式将传真包含在一封电子邮件中，并将其发送到收件人邮箱。

有关传真合作伙伴的详细信息，请参阅Microsoft 查明其传真合作伙伴[](https://go.microsoft.com/fwlink/?linkid=190238)

## 部署和配置传真

UM 将传入传真呼叫转发到专用传真合作伙伴解决方案，此解决方案然后与传真发件人建立传真呼叫，并代表启用了 UM 的用户接收传真。然而，要允许启用 UM 的用户在他们的邮箱中接收传真邮件，首先必须使传真能够传入并对关联到启用 UM 的用户的 UM 邮箱策略设置传真合作伙伴的 URI。您可以允许或禁止 UM 拨号计划、UM 邮箱策略和启用 UM 的用户的邮箱上的传入传真。有关详细信息，请参阅下列主题：

  - [允许用户接收传真的同一拨号计划中](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [禁止用户在同一拨号计划中接收传真](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [启用发送传真的用户组](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [禁用发送传真的用户组](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [允许用户接收传真](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [防止用户接收传真](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## 步骤 1：部署统一消息

可以为内部部署组织或混合组织设置传真之前，您需要成功地部署客户端访问服务器和邮箱服务器，并配置支持的 Voice over IP (VoIP) 网关，从而允许传真。有关如何部署 UM 的详细信息，请参阅[部署 Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)。关于如何部署 VoIP 网关和 IP 专用交换机 (PBX) 的详细信息，请参阅[将 UM 连接到电话系统](connect-um-to-your-telephone-system-exchange-2013-help.md)。

> [!important]
> 在统一消息和 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server 相集成的环境中，不支持使用 T.38 或 G.711 发送和接收传真。


## 步骤 2：配置传真合作伙伴服务器

接下来，您需要启用传入传真，您需要在您的组织中每个 UM 邮箱策略上配置传真伙伴的 URI。若要成功部署传入传真，必须使用 Exchange 统一消息集成认证的传真合作伙伴解决方案。有关详细信息，请参阅[对于 Exchange UM 传真顾问](fax-advisor-for-exchange-um-exchange-2013-help.md)。有关传真经认证的合作伙伴的列表，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)

> [!NOTE]
> 由于传真合作伙伴服务器在组织之外，防火墙端口必须配置为允许 T.38 协议端口以便能够通过基于 IP 的网络传真。默认情况下，T.38 协议使用 TCP 端口 6004。它也可以使用用户数据报协议 (UDP) 端口 6044，但是这将由硬件制造商定义。防火墙端口必须配置为允许传真数据，该传真数据使用 TCP 或 UDP 端口或制造商定义的端口范围。


## 步骤 3：在统一消息上启用传真

若要使用户可以使用统一消息接收传真，必须正确地配置三个组件。

  - UM 拨号计划

  - UM 邮箱策略

  - UM 邮箱

可以对 UM 拨号计划、UM 邮箱策略或各个启用 UM 的用户的邮箱启用或禁用传真。可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序对传真启用或禁用 UM 邮箱策略。拨号计划以及各个启用 UM 的用户的启用和禁用需要使用 Exchange 命令行管理程序来完成。下表显示了可用的选项以及用于启用和禁用传真的 cmdlet 和参数。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 组件</th>
<th>使用 EAC 启用/禁用？</th>
<th>启用传真的命令行管理程序示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>拨号计划</p></td>
<td><p>否</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM 邮箱策略</p></td>
<td><p>是</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>启用 UM 的用户</p></td>
<td><p>否</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


默认情况下，虽然用户的邮箱允许传入传真，但您必须首先对启用 UM 的用户所分配的 UM 邮箱策略启用入站传真，然后输入传真合作伙伴的 URI。

若要使已启用 UM 的用户可以接收传真，必须执行下列操作：

  - 验证每个 UM 拨号计划是否允许与该拨号计划关联的用户接收传真。默认情况下，所有与拨号计划关联的用户都能接收传真。要使启用 UM 的用户在他们的邮箱接收传真邮件，每个 VoIP 网关或 IP PBX 必须配置为接受传入传真呼叫。还必须使与拨号计划关联的用户能够接收传真邮件。有关如何使与拨号计划相关联的用户接收传真或阻止其接收传真的详细信息，请参阅[允许用户接收传真](enable-a-user-to-receive-faxes-exchange-2013-help.md).
    
    > [!NOTE]
    > 如果禁止在拨号计划上接收传真邮件，则与拨号计划关联的所有用户都不能接收传真邮件，即使您将单个用户的属性配置为允许接收传真邮件也是如此。在 UM 拨号计划上启用或禁用传真功能优先于单个启用 UM 的用户的设置。


  - 配置与启用 UM 的用户关联的 UM 邮箱策略。UM 邮箱策略必须配置为允许传入传真，包括传真合作伙伴的 URI 以及传真合作伙伴服务器的名称。*FaxServerURI* 参数必须使用以下形式：sip:\<*传真服务器 URI*\>:\<*端口*\>;\<*传输*\>，其中\&quot;传真服务器 URI\&quot;是传真合作伙伴服务器的完全限定域名 (FQDN) 或 IP 地址。\&quot;端口\&quot;是传真服务器侦听传入传真呼叫的端口，而\&quot;传输\&quot;是用于传入传真的传输协议（UDP、TCP 或传输层安全性 (TLS)）。例如，您可以按如下方式配置一个 UM 邮箱策略来接收传真。
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - 有关详细信息，请参阅[设置传真服务器 URI 以允许发送传真的伙伴](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md)。
    
    > [!warning]
    > 尽管您可以通过分号分隔在格式中包含多个 <em>FaxServerURI</em> 条目，只有一个条目可以使用。这个参数仅允许使用一个条目，并且添加多个条目将使您无法平衡传真请求负载。


  - 验证启用 UM 的邮箱是否可以接收传真邮件。默认情况下，所有与拨号计划关联的用户都能接收传真。但是，由于禁用了其邮箱接收传真的功能，可能会有用户无法接收传真的情况。有关如何使已启用 UM 的用户可以接收传真的详细信息，请参阅[允许用户接收传真](enable-a-user-to-receive-faxes-exchange-2013-help.md)。
    
    您可以阻止与拨号计划关联的单个用户接收传真邮件。要执行此操作，可使用命令行管理程序中的 **Set-UMMailbox** cmdlet 配置用户的属性。也可以使用 **Set-UMMailbox** cmdlet 阻止多个用户接收传真邮件。有关如何阻止一个或多个用户接收传真邮件的详细信息，请参阅[防止用户接收传真](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)。

## 步骤 4：配置身份验证

除了配置您的 UM 拨号计划、UM 邮箱策略和启用 UM 的用户，您还需要在您的 Exchange 服务器和传真合作伙伴服务器上配置身份验证。Exchange 服务器必须能够验证声称来自传真合作伙伴服务器的邮件的来源。任何未经验证的声称来自传真合作伙伴服务器的邮件将不会被 Exchange 服务器处理。

要验证传真合作伙伴服务器与 Exchange 服务器的联系，您可以使用：

  - 相互 TLS

  - 发件人 ID 验证

  - 专用的接收连接器

一个接收连接器应该足以验证部署在您组织中的传真合作伙伴服务器。接收连接器将会确保 Exchange 服务器将所有来自传真合作伙伴服务器的通信视为已通过身份验证。

接收连接器应在传真合作伙伴服务器用来提交 SMTP 传真邮件而使用的 Exchange 服务器上进行配置，而且必须为其配置以下值：

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

有关详细信息，请参阅[连接器](connectors-exchange-2013-help.md)。

如果传真合作伙伴服务器通过公共网络向 Exchange 服务器发送网络通信（例如，云中托管的基于服务的传真合作伙伴服务器），较好的方法是使用发件人 ID 检查对传真合作伙伴服务器进行身份验证。这种身份验证类型确保了发出传真邮件的 IP 地址得到授权，可以邮件声称来源的传真合作伙伴域的名义发送电子邮件。DNS 用来储存发件人 ID 记录（或发件人策略框架 (SPF) 记录），而且传真合作伙伴必须在 DNS 正向查找区域中发布他们的 SPF 记录。Exchange 将会通过查询 DNS 验证 IP 地址。而，发件者 ID 代理必须在邮箱服务器上运行，才能够执行 DNS 查询。

您也可以使用 TLS 对网络通信进行加密，或使用相互 TLS 为传真合作伙伴服务器和 Exchange 服务器之间的通信进行加密和身份验证。

