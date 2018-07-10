---
title: '语音体系结构更改: Exchange 2013 Help'
TOCTitle: 语音体系结构更改
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50490599
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 语音体系结构更改

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2013 体系结构与 Exchange Server 2007 和 Exchange Server 2010 中的体系结构不同。在 Exchange 2007 和 Exchange 2010 中，服务器类型分为多个服务器角色：客户端访问、邮箱、集线器传输和统一消息。在 Exchange 2013 中，服务器角色合并为两种服务器类型，来自这些服务器角色的所有组件或服务都在相同物理服务器上或在两个称为“客户端访问”和“邮箱”的单独服务器上运行。在新模型中，运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器会将从传入呼叫生成的会话初始化协议 (SIP) 流量重定向到邮箱服务器。随后会建立从 VoIP 网关或 IP 专用交换机 (PBX) 到托管用户邮箱的邮箱服务器的媒体（实时传输协议 (RTP) 或安全 RTP (SRTP)）通道。在 Exchange 2013 中，邮箱服务器的进程与 Exchange 2007 和 Exchange 2010 中的统一消息服务器角色相同。邮箱服务器同时运行 Microsoft Exchange 统一消息服务和 UM 工作进程。客户端访问服务器运行 Microsoft Exchange 统一消息呼叫路由器服务，该服务接收传入呼叫并将其转发到邮箱服务器。

**目录**

新 Exchange 体系结构支持

UM 端口

UM 拨号计划

UM 呼叫路由器性能计数器

## 新 Exchange 体系结构支持

在 Exchange 2013 中，客户端访问服务器负责自动发现、安全套接字层 (SSL)、身份验证、重定向和代理。客户端访问服务器是针对统一消息 (UM) 的任何入站呼叫或 SIP 请求的入口点。路由逻辑和 SIP REDIRECT 作为自动包含在客户端访问服务器中的服务来实现。此服务称为 Microsoft Exchange 统一消息呼叫路由器服务。此服务会在组织中的每台客户端访问服务器上安装并运行。当客户端访问服务器收到传入呼叫的 SIP INVITE 时，Microsoft Exchange 统一消息呼叫路由器服务会将该传入呼叫重定向到邮箱服务器。随后会在 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 与邮箱服务器之间创建媒体通道（RTP 或 SRTP）。虽然客户端访问服务器充当 SIP 重定向程序，但是它仅处理来自 VoIP 网关、IP PBX 或 SBC 的 SIP 请求。它不会接收任何媒体流体。使用 RTP 或 SRTP 的媒体流量仅在邮箱服务器与 SIP 对等机（如 VoIP 网关、IP PBX 或 SBC）之间传递，而不会传递到客户端访问服务器。部署 Exchange 2013 和 UM 时，必须将 VoIP 网关、IP PBX 或 SBC 配置为指向已安装的客户端访问服务器，以便为 UM 正确路由传入呼叫。

在某些情况下，要求部署多个客户端访问服务器，需要在与邮箱服务器不同的物理硬件上单独部署客户端访问服务器。可以使用 L4 或 L5 硬件或软件负载平衡器在阵列中对客户端访问服务器进行分组。但是，不存在基于 Active Directory Exchange 对象的客户端访问服务器阵列。在较大 Exchange 部署中可接受在客户端访问服务器之前使用硬件或软件负载平衡器。

安装客户端访问服务器时，会运行 Microsoft Exchange 统一消息呼叫路由器服务。该服务执行下列操作：

  - 进行初始化时，会读取名为 msexchangeumcallrouter.config 的本地配置文件。

  - 通过对组织使用仲裁邮箱来执行语音语法生成。

  - 支持传输控制协议 (TCP) 和/或传输层安全性 (TLS) 连接。此设置是可配置的。

  - 仅当存在配置错误或无法注册所需端口时才会停止。

在 Exchange 2013 中，邮箱服务器不负责应答来自传入呼叫的 SIP 请求。它仅负责从客户端访问服务器接收 SIP 流量，然后建立到 VoIP 网关、IP PBX 或 SBC 的 RTP 或 SRTP 连接。

在客户端访问服务器将传入呼叫重定向到邮箱服务器之后，会在 VoIP 网关、IP PBX 或 SBC 与邮箱服务器之间建立媒体通道。在建立了媒体通道之后，邮箱服务器上的 Microsoft Exchange 统一消息服务会播放用户的语音邮件问候语、处理用户的呼叫应答规则并邀请呼叫者留下语音消息。邮箱服务器随后会录制语音消息，创建消息的转录并将它存放在用户邮箱中。但是，如果将 Exchange 与 Office Communications Server 2007 R2 或 Lync Server 集成，则传入呼叫的 SIP 和 RTP 或 SRTP 媒体通道都由 Lync Server 和邮箱服务器处理。在集成了 Lync 的环境中，没有 VoIP 网关、IP PBX 或 SBC。对于 Lync，运行 Microsoft Exchange 统一消息服务的邮箱服务器看上去如同 Exchange 2010 UM 服务器一样。邮箱服务器和运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器被视为受信任对等机，因为这两个服务器都必须添加到 SIP 拨号计划中。Lync 使用入站路由组件来路由传入呼叫，该组件会使用 SIP 与客户端访问服务器通信，随后将呼叫路由到邮箱服务器。

Exchange 2010 UM 管理员可以在每个 UM 服务器上为统一消息配置一组属性。在 Exchange 2013 中，客户端访问和邮箱服务器上都具有 UM 组件和 UM 配置设置。应用于运行 Exchange 2010 中统一消息服务器角色的单台计算机的所有配置设置仍然可用。但是，其中某些属性和配置设置会在运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器上设置，而其他属性和配置设置可在运行 Microsoft Exchange 统一消息服务的邮箱服务器上使用。在某些情况下，相同设置在两个服务器上都可用。以下列表显示了客户端访问服务器和邮箱服务器中可用的 cmdlet 和参数，并列出了对 cmdlet 所做的更改，以便使用旧期版本的统一消息支持部署方案。

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**   既可在 Exchange 2013 邮箱服务器中运行，亦可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**   可在 Exchange 2013 客户端访问服务器中运行，但不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMService -MaxCallsAllowed \<Int32\>**   既可在 Exchange 2013 邮箱服务器中运行，亦可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   既不可在 Exchange 2013 客户端访问服务器中运行，也不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMService -SipTcpListeningPort \<Int32\>**   在 Exchange 2013 邮箱服务器中不可配置，但在 Exchange 2007 和 Exchange 2010 统一消息服务器中可运行。

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   在 Exchange 2013 邮箱服务器中不可配置，但在 Exchange 2007 和 Exchange 2010 统一消息服务器中可运行。

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**   可在 Exchange 2013 客户端访问服务器中运行，但不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   可在 Exchange 2013 客户端访问服务器中运行，但不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   不可在 Exchange 2013 邮箱服务器中运行，但可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**   不可在 Exchange 2013 客户端访问服务器中运行，亦不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   可在 Exchange 2013 邮箱服务器中运行，亦可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**   可在 Exchange 2013 客户端访问服务器中运行，但不可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Enable-UMService**   不可在 Exchange 2013 邮箱服务器中运行，但可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

  - **Disable-UMService**   不可在 Exchange 2013 邮箱服务器中运行，但可在 Exchange 2007 和 Exchange 2010 统一消息服务器中运行。

对于邮箱服务器，您可以使用 **Set/Get/Enable/Disable-UMService** cmdlets，为 Exchange 2013 邮箱服务器或 Exchange 2007 或 Exchange 2010 统一消息服务器中的 Microsoft Exchange 统一消息服务查看或配置 UM 属性。另一组 cmdlet **Set/Get-UMCallRouterSettings** 用于查看或配置客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务属性。这可确保 Exchange 2007 和 Exchange 2010 中的现有 **Get-UMServer**、**Set-UMServer**、**Enable-UMServer** 和 **Disable-UMServer** cmdlet 在具有 Exchange 2013 邮箱服务器的共存部署中正常工作。这还可确保当在相同或不同服务器上安装邮箱和客户端访问服务器时，这些 cmdlet 会正常工作。

新 Exchange 体系结构支持

## UM 端口

客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务使用 SIP 通过传输控制协议 (TCP) 或相互传输层安全性（相互 TLS）与运行 Microsoft Exchange 统一消息服务的邮箱服务器通信。为了避免 TCP/用户数据报协议 (UDP) 端口冲突，Microsoft Exchange 统一消息呼叫路由器服务和 Microsoft Exchange 统一消息服务默认为不同 TCP 端口并在这些端口上进行侦听。它们可以接受不安全和安全的连接，具体取决于是否将相互 TLS 用于 SIP 和 RTP 流量。默认情况下，在使用相互 TLS 时，客户端访问服务器会同时在 TCP 端口 5060（在非安全模式下）和 TCP 端口 5061（在 SIP 安全模式下）侦听 SIP 请求。这些端口可使用 **Set-UMCallRouterSettings** cmdlet 进行配置。客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务不处理媒体（RTP 或 SRTP）流量，因此仅使用 TCP 端口，而不使用 UDP 端口。默认情况下，在使用相互 TLS 时，邮箱服务器会同时在 TCP 端口 5062（在非安全模式下）和 TCP 端口 5063（在 SIP 安全模式下）侦听 SIP 请求。不能使用 Exchange 命令行管理程序 cmdlet 配置这些端口。在运行 Microsoft Exchange 统一消息服务的邮箱服务器上，无法通过使用命令行管理程序或通过在注册表中配置设置在 Exchange 服务器上配置 TCP 端口。邮箱服务器上的 Microsoft Exchange 统一消息服务会在 SIP 端口 5062 和 5063 上接受来自客户端访问服务器的连接。在客户端访问服务器将 SIP 请求重定向到邮箱服务器之后，会使用 VoIP 网关、IP PBX 或 SBC 和邮箱服务器上的 Microsoft Exchange 统一消息工作进程创建 RTP 或 SRTP 媒体通道。

下表汇总了 Exchange 2013 端口和协议以及这些端口是否可以更改。

### UM 侦听端口

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>协议</th>
<th>TCP 端口</th>
<th>UDP 端口</th>
<th>这些端口是否可以更改？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP（客户端访问服务器 – Microsoft Exchange 统一消息呼叫路由器服务）</p></td>
<td><p>5060（不安全）、5061（安全）。该服务同时侦听这两个端口。</p></td>
<td><p>不适用</p></td>
<td><p>可以，使用 <strong>Set-UMCallRouterSettings</strong> cmdlet。</p></td>
</tr>
<tr class="even">
<td><p>SIP（邮箱服务器 – Microsoft Exchange 统一消息服务）</p></td>
<td><p>5062（不安全）、5063（安全）。该服务同时侦听这两个端口。</p></td>
<td><p>不适用</p></td>
<td><p>不能更改端口。</p></td>
</tr>
<tr class="odd">
<td><p>SIP（邮箱服务器 - UM 工作进程）</p></td>
<td><p>5065 和 5067 用于 TCP（不安全）。5066 和 5068 用于相互 MTLS（安全）。当 <em>UMStartupMode</em> 设置为 <em>Dual</em> 时便是这种情况。如果 <em>UMStartUpMode</em> 设置为 <em>TCP</em> 或 <em>TLS</em>，会使用端口 5065 和 5066。默认 <em>UMStartupMode</em> 为 <em>TCP</em>。</p></td>
<td><p>不适用</p></td>
<td><p>不能更改端口。</p></td>
</tr>
<tr class="even">
<td><p>RTP（邮箱服务器 - UM 工作进程）</p></td>
<td><p>不适用</p></td>
<td><p>1024 到 65535 之间的端口。</p></td>
<td><p>可以通过注册表（但这不是支持的配置）更改端口范围：</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


新 Exchange 体系结构支持

## UM 拨号计划

在 Exchange 2013 中，不需要采用 Exchange 2007 和 Exchange 2010 中的方式将 UM 拨号计划映射或关联到 UM 服务器。运行 UM 服务的客户端访问或邮箱服务器无需链接到拨号计划，因为所有客户端访问和邮箱服务器都应从 VoIP 网关、IP PBX 或 SBC 接收所有传入呼叫。例外情况是用于 Lync 2013、Lync Server 2010 和 Office Communications Server 2007 R2 的 SIP 拨号计划必须与部署的客户端访问和邮箱服务器关联。两种类型的 Exchange 服务器都必须添加到每个 SIP 拨号计划，以作为 Communications Server 2007 R2 或 Lync Server 的受信任对等机包含在其中。否则，Communications Server 2007 R2 或 Lync Server 会拒绝来自用户的出站呼叫。

下表汇总了客户端访问和邮箱服务器与 UM 拨号计划之间的关系。

### 链接 UM 拨号计划

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>拓扑</th>
<th>拨号计划</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>相同服务器上的客户端访问和邮箱（不使用 Communications Server 2007 R2 或 Lync Server 2010 非 SIP 拨号计划）</p></td>
<td><p>拨号计划不再需要与客户端访问或邮箱服务器关联。不允许将客户端访问或邮箱服务器添加到拨号计划。如果运行 <strong>Set-UMService</strong> cmdlet，则它会在您尝试将邮箱服务器与非 SIP 拨号计划关联时生成错误。</p></td>
</tr>
<tr class="even">
<td><p>不同服务器上的客户端访问和邮箱（不使用 Communications Server 2007 R2 或 Lync Server 2010 非 SIP 拨号计划）</p></td>
<td><p>拨号计划不再需要与客户端访问或邮箱服务器关联。不允许将客户端访问或邮箱服务器添加到拨号计划。如果运行 <strong>Set-UMService</strong> cmdlet，则它会在您尝试将邮箱服务器与非 SIP 拨号计划关联时生成错误。</p></td>
</tr>
<tr class="odd">
<td><p>相同物理服务器上的客户端访问和邮箱服务器（使用 Communications Server 2007 R2 和 Lync Server 2010 – SIP 拨号计划）</p></td>
<td><p>对于单个 SIP 拨号计划，请将所有客户端访问和邮箱服务器添加到 SIP 拨号计划。对于多个 SIP 拨号计划，请将所有客户端访问和邮箱服务器添加到每个 SIP 拨号计划。这会使两种服务器都成为 Office Communications Server 2007 R2 或 Lync Server 的受信任对等项。在 Office Communications Server 2007 R2 或 Lync Server 部署中使用的证书必须与在每台客户端访问和邮箱服务器上使用的证书相同。</p></td>
</tr>
<tr class="even">
<td><p>不同物理服务器上的客户端访问和邮箱服务器（使用 Communications Server 2007 R2 和 Lync Server 2010 – SIP 拨号计划）</p></td>
<td><p>对于单个 SIP 拨号计划，请将所有客户端访问和邮箱服务器添加到 SIP 拨号计划。对于多个 SIP 拨号计划，请将所有客户端访问和邮箱服务器添加到每个 SIP 拨号计划。这会使两种服务器都成为 Office Communications Server 2007 R2 或 Lync Server 的受信任对等项。如果在客户端访问和邮箱服务器上使用的证书不同，则在 Office Communications Server 2007 R2 或 Lync Server 部署中使用的证书必须与组织中每台客户端访问和邮箱服务器上使用的证书相同。</p></td>
</tr>
</tbody>
</table>


新 Exchange 体系结构支持

## UM 呼叫路由器性能计数器

过去的 Exchange 版本包括运行 Microsoft Exchange 统一消息服务的统一消息服务器角色。因为 Exchange 2013 中的体系结构进行了更改，所以客户端访问服务器运行 Microsoft Exchange 统一消息呼叫路由器服务，而邮箱服务器运行 Microsoft Exchange 统一消息服务。管理员可使用与较早 Exchange UM 版本中相同的 Microsoft Exchange 统一消息服务性能计数器。但是，还可以在客户端访问服务器上使用其他性能计数器来验证 Microsoft Exchange 统一消息呼叫路由器服务并排除故障。

为了支持 Exchange 2013 中的新客户端访问统一消息呼叫路由器服务，现在提供以下性能计数器。

### 性能计数器

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>性能计数器类别</th>
<th>计数器名称</th>
<th>描述</th>
<th>阈值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>上一小时内 Microsoft Exchange 统一消息呼叫路由器服务拒绝的入站呼叫百分比</p></td>
<td><p>显示 Microsoft Exchange 统一消息呼叫路由器服务在上一小时内拒绝的入站呼叫百分比。</p></td>
<td><p>应始终小于 5%，但是应始终为 0。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange 统一消息呼叫路由器服务在出现不可恢复的内部错误时断开连接的呼叫数</p></td>
<td><p>显示发生内部系统错误之后断开连接的呼叫数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange 统一消息呼叫路由器服务拒绝的入站呼叫的总数</p></td>
<td><p>显示自 Microsoft Exchange 统一消息呼叫路由器服务启动之后，由该服务拒绝的入站呼叫的总数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Microsoft Exchange 统一消息呼叫路由器服务接收的呼叫的总数</p></td>
<td><p>显示自 Microsoft Exchange 统一消息呼叫路由器服务启动之后，由该服务接收的入站呼叫的总数。</p></td>
<td><p>应为 0 或更大。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>上一小时内 Microsoft Exchange 统一消息呼叫路由器服务拒绝的入站呼叫百分比</p></td>
<td><p>显示 Microsoft Exchange 统一消息呼叫路由器服务在上一小时内拒绝的入站呼叫百分比。</p></td>
<td><p>应小于 5%。</p></td>
</tr>
</tbody>
</table>


新 Exchange 体系结构支持

