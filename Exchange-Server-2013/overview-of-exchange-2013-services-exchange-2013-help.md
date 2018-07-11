---
title: '交换 2013年服务概述: Exchange 2013 Help'
TOCTitle: 交换 2013年服务概述
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479257
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 交换 2013年服务概述

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-10-20_

在Exchange Server 2013的安装时，安装程序运行一的组在 Microsoft Windows中安装新的服务的任务。服务是一个后台进程，可以在服务器的启动Windows服务控制管理器启动。服务是可执行文件配合独立和无需管理员干预。服务可以使用图形用户界面 (GUI) 模式或控制台模式运行。

所有以前版本的Exchange包括作为服务实现的组件。每个Exchange服务器角色包括属于 （或可能需要的） 服务的服务器角色，以执行其功能。请注意，某些服务仅处于活动状态时使用特定的功能。

本主题中的各节描述了由Exchange 2013邮箱服务器、 客户端访问服务器和边缘传输服务器上安装的各种服务。标记为可选的服务，您可以禁用服务，如果您确定您的组织不需要该服务提供的功能。

## Exchange Exchange 2013邮箱服务器上的服务

下表描述在邮箱服务器安装的Exchange服务。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服务名</th>
<th>服务简短名称</th>
<th>描述及依赖关系</th>
<th>默认启动类型</th>
<th>安全上下文</th>
<th>相关性</th>
<th>必需或可选</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>提供了Active Directory与Exchange服务的拓扑信息。如果停止此服务，则大多数Exchange服务将无法启动。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Net.TCP 端口共享服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 反垃圾邮件更新</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>提供Exchange SmartScreen 垃圾邮件定义更新。</p>

> [!NOTE]  
> 2016 年 11 月 1 日起，Microsoft 停止为 Exchange 和 Outlook 中的 SmartScreen 筛选器生成垃圾邮件定义更新。现有的 SmartScreen 垃圾邮件定义将予以保留，但其效力可能会随时间的推移而逐渐降低。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">停止为 Outlook 和 Exchange 中的 SmartScreen 提供支持</a>。

</td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeDAG 管理</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>提供了存储和数据库中数据库可用性组 (Dag) 的邮箱服务器的布局管理。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p>
<p>Net.TCP 端口共享服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange诊断程序</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供了Exchange服务器运行状况监视代理。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>无</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>通过安全 LDAP 通道UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 在已订阅的边缘传输服务器和邮箱服务器之间复制配置和收件人数据。</p>
<p>如果您没有任何订阅的边缘传输服务器，您可以禁用此服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange健康管理器</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>在Exchange服务器上的关键组件的运行状况监视的托管可用性的一部分。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Windows事件日志</p>
<p>Windows管理规范</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangeIMAP4 后端</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>接收从代理客户机连接从客户端访问服务器上的 IMAP4 服务。默认情况下，此服务未在运行，以便启动此服务之前，IMAP4 客户端无法连接到Exchange服务器。</p>
<p>如果您没有任何 IMAP4 客户端，您可以禁用此服务。</p></td>
<td><p>手动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 信息存储</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>管理服务器上的邮箱数据库。如果此服务被停止，服务器上的邮箱数据库不可用。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p>
<p>远程过程调用 (RPC)</p>
<p>服务器</p>
<p>Windows事件日志</p>
<p>工作站</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 邮箱助理</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>执行后台处理的邮箱服务器上的邮箱数据库。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange邮箱复制</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>流程邮箱移动，移动的请求。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p>
<p>Net.TCP 端口共享服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange邮箱运输交货</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>接收来自Microsoft Exchange （本地或远程邮箱服务器上） 的传输服务 SMTP 消息并将它们传送到本地邮箱数据库使用 RPC。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange邮箱传输提交</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>接收来自本地邮箱数据库的 RPC 消息，通过 SMTP 提交到Microsoft Exchange （本地或远程邮箱服务器上） 的传输服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft ExchangePOP3 后端</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>从客户端访问服务器上的 POP3 服务，接收代理的客户端连接。默认情况下，此服务未在运行，以便启动此服务之前，POP3 客户端不能连接到Exchange服务器。</p></td>
<td><p>手动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 复制服务</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>提供数据库中的邮箱数据库可用性组 (Dag) 的复制功能。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange RPC 客户端访问</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>管理Exchange的客户端 RPC 的连接。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange搜索</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>提供索引的邮箱内容，提高了内容搜索的性能。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange搜索主机控制器</p></td>
<td><p>HostControllerService</p></td>
<td><p>本地Exchange服务器上提供应用程序的部署和管理服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>HTTP 服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>用于 Windows 服务器备份的 Microsoft Exchange Server 扩展</p></td>
<td><p>WSBExchange</p></td>
<td><p>使Windows Server备份来备份和还原Exchange服务器数据。</p></td>
<td><p>手动</p></td>
<td><p>本地系统</p></td>
<td><p>无</p></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 服务主机</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>没有他们自己服务的Exchange组件提供服务主机。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 限制</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>提供用户工作负载管理，用于限制用户操作 （以前称为用户限制） 的速度。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 传输</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>提供 SMTP 服务器，并传输堆栈。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p>
<p>Microsoft筛选管理服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 传输日志搜索</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>传输日志文件 （例如，邮件跟踪） 提供远程搜索功能。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 统一消息</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>提供统一消息 (UM) 功能： 允许语音和传真邮件存储在Exchange和赋予用户电话访问电子邮件、 语音邮件、 日历、 联系人或自动助理。如果此服务被停止，统一邮件不可用。</p>
<p>如果您不使用 UM，您可以禁用此服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>CNG 关键隔离</p>
<p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
</tbody>
</table>


## Exchange Exchange 2013客户端访问服务器上的服务

下表描述了客户端访问服务器安装的Exchange服务。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服务名</th>
<th>服务简短名称</th>
<th>描述及依赖关系</th>
<th>默认启动类型</th>
<th>安全上下文</th>
<th>相关性</th>
<th>必需或可选</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>提供了Active Directory与Exchange服务的拓扑信息。如果停止此服务，则大多数Exchange服务将无法启动。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Net.TCP 端口共享服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange诊断程序</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供了Exchange服务器运行状况监视代理。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>无</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange前端传输</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>从Microsoft Exchange邮箱服务器上的传输服务到的外部主机代理 SMTP 连接。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange健康管理器</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>在Exchange服务器上的关键组件的运行状况监视的托管可用性的一部分。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Windows事件日志</p>
<p>Windows管理规范</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>代理 IMAP4 客户端连接到邮箱服务器上的 IMAP4 服务。默认情况下，此服务未在运行，以便启动此服务之前，IMAP4 客户端无法连接到Exchange服务器。</p>
<p>如果您没有任何 IMAP4 客户端，您可以禁用此服务。</p></td>
<td><p>手动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>代理服务器 POP3 客户端连接到邮箱服务器上的 IMAP4 服务。默认情况下，此服务未在运行，以便启动此服务之前，POP3 客户端不能连接到Exchange服务器。</p></td>
<td><p>手动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange搜索主机控制器</p></td>
<td><p>HostControllerService</p></td>
<td><p>本地Exchange服务器上提供应用程序的部署和管理服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>HTTP 服务</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 服务主机</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>没有他们自己服务的Exchange组件提供服务主机。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange统一消息呼叫路由器</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>将 UM 客户端连接重定向到统一消息服务对邮箱服务器上。</p>
<p>如果您不使用 UM，您可以禁用此服务。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>CNG 关键隔离</p>
<p>Microsoft Exchange Active Directory 拓扑</p></td>
<td><p>可选</p></td>
</tr>
</tbody>
</table>


## Exchange Exchange 2013边缘传输服务器上的服务

下表描述在边缘传输服务器安装的Exchange服务。


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>服务名</th>
<th>服务简短名称</th>
<th>说明</th>
<th>默认启动类型</th>
<th>安全上下文</th>
<th>相关性</th>
<th>必需或可选</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>在边缘传输服务器上存储配置数据和收件人。此服务表示UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS)，由Exchange安装程序自动创建的命名的实例。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>COM + 事件系统</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 反垃圾邮件更新</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>提供Exchange SmartScreen 垃圾邮件定义更新。</p>
> [!NOTE]  
> 2016 年 11 月 1 日起，Microsoft 停止为 Exchange 和 Outlook 中的 SmartScreen 筛选器生成垃圾邮件定义更新。现有的 SmartScreen 垃圾邮件定义将予以保留，但其效力可能会随时间的推移而逐渐降低。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">停止为 Outlook 和 Exchange 中的 SmartScreen 提供支持</a>。

</td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>可选</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 凭据服务</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>监视凭据更改UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 和安装在边缘传输服务器上所做的更改。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange诊断程序</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>提供了Exchange服务器运行状况监视代理。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>无</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange健康管理器</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>在Exchange服务器上的关键组件的运行状况监视的托管可用性的一部分。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Windows 事件日志</p>
<p>Windows Management Instrumentation</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 服务主机</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>没有他们自己服务的Exchange组件提供服务主机。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必需</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 传输</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>提供 SMTP 服务器，并传输堆栈。</p></td>
<td><p>自动</p></td>
<td><p>网络服务</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>必需</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 传输日志搜索</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>传输日志文件 （例如，邮件跟踪） 提供远程搜索功能。</p></td>
<td><p>自动</p></td>
<td><p>本地系统</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>可选</p></td>
</tr>
</tbody>
</table>

