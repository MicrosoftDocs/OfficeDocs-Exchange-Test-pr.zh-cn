---
title: 'Exchange 2013 中客户端和邮件流的网络端口: Exchange 2013 Help'
TOCTitle: Exchange 2013 中客户端和邮件流的网络端口
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64118126
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中客户端和邮件流的网络端口

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题提供有关 MicrosoftExchange Server 2013 用于与电子邮件客户端、Internet 邮件服务器以及本地 Exchange 组织的其他外部服务进行通信的网络端口的信息。在深入介绍之前，请了解以下基本规则：

  - 我们不支持限制或更改内部 Exchange 服务器之间或内部 Exchange 服务器与内部 Lync 或 Skype for Business 服务器之间或所有类型的拓扑中的内部 Exchange 服务器与内部 Active Directory 域控制器之间的网络通信。如果您有防火墙或可能会限制或改变上述网络通信的网络设备，您需要配置规则，允许这些服务器之间的可用/不受限制的通信（允许任意端口（包括随机 RPC 端口）上的传入和传出网络流量的规则，以及永远不会改变网络上位数的任何协议）。

  - 边缘传输服务器几乎始终位于外围网络中，因此您应该可以限制边缘传输服务器和 Internet 之间，以及边缘传输服务器和内部 Exchange 组织之间的网络流量。本主题介绍了这些网络端口。

  - 您可以限制外部客户端和服务与内部 Exchange 组织之间的网络流量。您也可以决定限制内部客户端和内部 Exchange 服务器之间的网络流量。本主题介绍了这些网络端口。

**目录**

客户端和服务所需的网络端口

邮件流所需的网络端口（没有边缘传输服务器）

邮件流所需的网络端口（具有边缘传输服务器）

混合部署所需的网络端口

统一消息所需的网络端口

## 客户端和服务所需的网络端口

下列图表中介绍了电子邮件客户端访问邮箱和 Exchange 组织中其他服务所需的网络端口。

**说明：** 

  - 这些客户端和服务的目标是客户端访问服务器。这可能是独立的客户端访问服务器，也可能是安装在同一台计算机上的客户端访问服务器和邮箱服务器。

  - 虽然图中显示来自 Internet 的客户端和服务，但内部客户端的概念都是相同的（例如，帐户林中的客户端访问资源林中的 Exchange 服务器）。同样，表中没有源列，因为源可能是 Exchange 组织外部的任何位置（例如，Internet 或帐户林）。

  - 边缘传输服务器不涉及与这些客户端和服务相关的网络流量。

![客户端和服务所需的网络端口](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "客户端和服务所需的网络端口")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>端口</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>下列客户端和服务使用加密的 Web 连接：</p>
<ul>
<li><p>自动发现服务</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>Exchange Web 服务 (EWS)</p></li>
<li><p>脱机通讯簿分发</p></li>
<li><p>Outlook Anywhere（HTTP 上的 RPC）</p></li>
<li><p>Outlook（HTTP 上的 MAPI）</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP (HTTPS)</p></td>
<td><p>有关这些客户端和服务的详细信息，请参阅下列主题：</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">自动发现服务</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">EWS reference for Exchange</a>（Exchange 的 EWS 参考）</p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">脱机通讯簿</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook 无处不在</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中 Outlook Web App 的新增内容</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>下列客户端和服务使用未加密的 Web 连接：</p>
<ul>
<li><p>Internet 日历发布</p></li>
<li><p>Outlook Web App重定向到 443/TCP）</p></li>
<li><p>自动发现（443/TCP 不可用时回退）</p></li>
</ul></td>
<td><p>80/TCP (HTTP)</p></td>
<td><p>如果可能，建议对 443/TCP 使用加密的 Web 连接以帮助保护数据和凭据。但是，您可能会发现必须将某些服务配置为对客户端访问服务器上的 80/TCP 使用未加密的 Web 连接。</p>
<p>有关这些客户端和服务的详细信息，请参阅下列主题：</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">启用 Internet 日历发布</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中 Outlook Web App 的新增内容</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">自动发现服务</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IMAP4 客户端</p></td>
<td><p>143/TCP (IMAP)、993/TCP（安全 IMAP）</p></td>
<td><p>默认情况下 IMAP4 处于禁用状态。有关详细信息，请参阅 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013 中的 POP3 和 IMAP4</a>。</p>
<p>客户端访问服务器上的 IMAP4 服务负责将连接代理到邮箱服务器上的 IMAP4 后端服务。</p></td>
</tr>
<tr class="even">
<td><p>POP3 客户端</p></td>
<td><p>110/TCP (POP3)、995/TCP（安全 POP3）</p></td>
<td><p>默认情况下 POP3 处于禁用状态。有关详细信息，请参阅 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013 中的 POP3 和 IMAP4</a>。</p>
<p>客户端访问服务器上的 POP3 服务负责将连接代理到邮箱服务器上的 POP3 后端服务。</p></td>
</tr>
<tr class="odd">
<td><p>SMTP 客户端（已经过身份验证）</p></td>
<td><p>587/TCP（通过身份验证的 SMTP）</p></td>
<td><p>名为“客户端前端 <em>&lt;服务器名称&gt;</em>”的默认接收连接器会侦听客户端访问服务器上端口 587 上的已通过身份验证的 SMTP 客户端提交。</p>
<p><strong>注意：</strong></p>
<p>如果您有的邮件客户端只能在端口 25 上提交经过身份验证的 SMTP 邮件，可以修改此接收连接器的网络适配器绑定值，以便还侦听端口 25 上经过身份验证的 SMTP 邮件提交。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件流所需的网络端口

邮件传入和传出您的 Exchange 组织的方式取决于您的 Exchange 拓扑。最重要的因素是您是否已在外围网络中部署订阅的边缘传输服务器。

## 邮件流所需的网络端口（没有边缘传输服务器）

对于仅具有客户端访问服务器和邮箱服务器的 Exchange 组织，邮件流所需的网络端口如下列图表中所示。尽管图中显示了单独的邮箱服务器和客户端访问服务器，无论客户端访问服务器和邮箱服务器安装在同一台计算机上还是在不同计算机上，概念是相同的。

![邮件流所需的网络端口（没有边缘传输服务器）](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "邮件流所需的网络端口（没有边缘传输服务器）")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>端口</th>
<th>源</th>
<th>目标</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>入站邮件</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet（任何）</p></td>
<td><p>客户端访问服务器</p></td>
<td><p>客户端访问服务器上名为“默认前端 <em>&lt;Client Access server name&gt;</em>”的默认接收连接器会在端口 25 上侦听匿名的入站 SMTP 邮件。</p>
<p>邮件使用隐式和不可见的组织内部发送连接器从客户端访问服务器中继到邮箱服务器，此连接器可在同一组织中的 Exchange 服务器之间自动路由邮件。</p></td>
</tr>
<tr class="even">
<td><p>出站邮件</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>邮箱服务器</p></td>
<td><p>Internet（任何）</p></td>
<td><p>默认情况下，Exchange 不会创建任何发送连接器允许您将邮件发送到 Internet。您必须手动创建发送连接器。有关详细信息，请参阅<a href="send-connectors-exchange-2013-help.md">发送连接器</a>。</p></td>
</tr>
<tr class="odd">
<td><p>出站邮件（如果通过客户端访问服务器路由）</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>客户端访问服务器</p></td>
<td><p>Internet（任何）</p></td>
<td><p>仅当使用 Exchange 管理中心的“通过客户端访问服务器的代理”或通过 Exchange 命令行管理程序中的 <code>-FrontEndProxyEnabled $true</code> 配置发送连接器时，出站邮件才会通过客户端访问服务器进行路由。</p>
<p>在这种情况下，客户端访问服务器上名为“出站代理前端 <em>&lt;客户端访问服务器名称&gt;</em>”的默认接收连接器会侦听来自邮箱服务器的出站邮件。有关详细信息，请参阅<a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">为发送到 Internet 的电子邮件创建发送连接器</a>。</p></td>
</tr>
<tr class="even">
<td><p>用于下一个邮件跃点的名称解析的 DNS（未显示在图中）</p></td>
<td><p>53/UDP、53/TCP (DNS)</p></td>
<td><p>面向 Internet 的 Exchange 服务器（客户端访问服务器或邮箱服务器）</p></td>
<td><p>DNS 服务器</p></td>
<td><p>请参阅名称解析部分。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件流所需的网络端口（具有边缘传输服务器）

安装在外围网络中的订阅边缘传输服务器基本上消除了通过客户端访问服务器的 SMTP 邮件流。具体来说：

  - 来自 Exchange 组织的出站邮件永远不会流经客户端访问服务器。邮件始终从订阅的 Active Directory 网站中的邮箱服务器流到边缘传输服务器（不论边缘传输服务器上的 Exchange 版本如何）。

  - 入站邮件永远不会流经独立的客户端访问服务器。邮件从边缘传输服务器流向订阅的 Active Directory 网站中的邮箱服务器。如果邮箱服务器和客户端访问服务器安装在同一台计算机上，则来自 Exchange 2013 边缘传输服务器的邮件将先到达计算机上的前端传输服务（客户端访问服务器角色），然后再流向传输服务（邮箱服务器角色）。Exchange 2007 或 Exchange 2010 边缘传输服务器始终将邮件直接传递到传输服务，即使邮箱服务器和客户端访问服务器安装在同一台计算机上也是如此。

有关详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。

对于具有边缘传输服务器的 Exchange 组织，邮件流所需的网络端口如下列图表中所示。除非另有说明，无论客户端访问服务器和邮箱服务器安装在同一台计算机上还是在不同计算机上，概念是相同的。

![邮件流所需的网络端口（具有边缘传输服务器）](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "邮件流所需的网络端口（具有边缘传输服务器）")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>用途</th>
<th>端口</th>
<th>源</th>
<th>目标</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>入站邮件 - 从 Internet 到边缘传输服务器</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>Internet（任何）</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>边缘传输服务器上名为“默认内部接收连接器 <em>&lt;边缘传输服务器名称&gt;</em>”的默认接收连接器会侦听端口 25 上的匿名 SMTP 邮件。</p></td>
</tr>
<tr class="even">
<td><p>入站邮件 - 从边缘传输服务器到内部 Exchange 组织</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>订阅的 Active Directory 站点中的邮箱服务器</p></td>
<td><p>默认的“EdgeSync - 入站到 <em>&lt;Active Directory 站点名称&gt;</em>”发送连接器会将端口 25 上的入站邮件中继到订阅的 Active Directory 站点中的任意邮箱服务器。有关详细信息，请参阅<a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>主题中的“在边缘订阅过程中创建的发送连接器”部分。</p>
<p>实际接收邮件的服务取决于邮箱服务器和客户端访问服务器安装在同一台计算机上还是不同计算机上。</p>
<ul>
<li><p><strong>独立邮箱服务器</strong>   名为“默认 <em>&lt;邮箱服务器名称&gt;</em>”的默认接收连接器会侦听端口 25 上的入站邮件（包括来自边缘传输服务器的邮件）。</p></li>
<li><p><strong>邮箱服务器和客户端访问服务器安装在同一台计算机上：</strong>前端传输服务（客户端访问服务器角色）中的“默认前端 <em>&lt;服务器名称&gt;</em>”默认接收连接器会侦听端口 25 上的入站邮件（包括来自 Exchange 2013 边缘传输服务器的邮件）。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>出站邮件 - 从内部 Exchange 组织到边缘传输服务器</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>订阅的 Active Directory 站点中的邮箱服务器</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>出站邮件将始终绕过客户端访问服务器。</p>
<p>邮件使用隐式和不可见的组织内部发送连接器从订阅的 Active Directory 站点中的任意邮箱服务器中继到边缘传输服务器，此连接器可在同一组织中的 Exchange 服务器之间自动路由邮件。</p>
<p>边缘传输服务器上的“默认内部接收连接器 <em>&lt;边缘传输服务器名称&gt;</em>”默认接收连接器会侦听端口 25 上发送自订阅的 Active Directory 站点中任意邮箱服务器的 SMTP 邮件。</p></td>
</tr>
<tr class="even">
<td><p>出站邮件 - 从边缘传输服务器到 Internet</p></td>
<td><p>25/TCP (SMTP)</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>Internet（任何）</p></td>
<td><p>名为“EdgeSync - <em>&lt;Active Directory 站点名称&gt;</em> 到 Internet”的默认发送连接器会将端口 25 上的出站邮件从边缘传输服务器中继到 Internet。</p></td>
</tr>
<tr class="odd">
<td><p>EdgeSync 同步</p></td>
<td><p>50636/TCP（安全 LDAP）</p></td>
<td><p>订阅的 Active Directory 站点中参与 EdgeSync 同步的邮箱服务器</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>当边缘传输服务器订阅 Active Directory 站点时，站点中的所有现有邮箱服务器都会参与 EdgeSync 同步。但是，您以后添加的任何邮箱服务器不会自动参与 EdgeSync 同步。</p></td>
</tr>
<tr class="even">
<td><p>用于下一个邮件跃点的名称解析的 DNS（未显示在图中）</p></td>
<td><p>53/UDP、53/TCP (DNS)</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>DNS 服务器</p></td>
<td><p>请参阅名称解析部分。</p></td>
</tr>
<tr class="odd">
<td><p>发件人信誉的代理服务器定义（无图示）</p></td>
<td><p>用户定义</p></td>
<td><p>边缘传输服务器</p></td>
<td><p>Internet</p></td>
<td><p>发件人信誉（协议分析代理）会分析入站的邮件路径以减少垃圾邮件。如果您的组织使用代理服务器控制对 Internet 的访问，您需要定义关于代理服务器的详细信息，以便发件人信誉正常运行（尤其是在开放式代理检测和发件人阻止中）。您可以在 <strong>Set-senderreputationconfig</strong> cmdlet 上使用 <em>ProxyServerName</em>、<em>ProxyServerPort</em> 和 <em>ProxyServerType</em> 参数，定义您组织的代理服务器，以便发件人信誉可以成功连接到 Internet。有关详细信息，请参阅<a href="manage-sender-reputation-exchange-2013-help.md">管理发件人信誉</a>。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 名称解析

在任何 Exchange 组织中，下一个邮件跃点的 DNS 解析都是邮件流的基本组成部分。负责接收入站邮件或传递出站邮件的 Exchange 服务器必须能够解析内部和外部主机名，以确保正确的邮件路由。所有内部 Exchange 服务器都必须能够解析内部主机名，以确保正确的邮件路由。有很多不同设计 DNS 基础结构的方法，但重要的结果是确保下一个跃点的名称解析对您的所有 Exchange 服务器均运行正常。

## 混合部署所需的网络端口

对于同时使用 Exchange 2013 和 MicrosoftOffice 365 的组织，所需的网络端口如[混合部署先决条件](https://technet.microsoft.com/zh-cn/library/hh534377\(v=exchg.150\))中的“混合部署协议、端口和终结点”部分所述。

## 统一消息所需的网络端口

以下主题中包含统一消息所需的网络端口：

  - [UM 协议、端口和服务](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Exchange Server 2013 SP1 体系结构海报](https://go.microsoft.com/fwlink/p/?linkid=518646)

返回顶部

