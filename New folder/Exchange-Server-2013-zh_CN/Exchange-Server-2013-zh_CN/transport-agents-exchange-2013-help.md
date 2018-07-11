---
title: '传输代理: Exchange 2013 Help'
TOCTitle: 传输代理
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50491837
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 传输代理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

通过传输代理，您可以在 Exchange 服务器上安装由 Microsoft、第三方供应商或您的组织创建的自定义软件。随后该软件便可以处理通过传输管道的电子邮件。在 Microsoft Exchange Server 2013 中，传输管道由以下进程组成：

  - 客户端访问服务器上的前端传输服务

  - 邮箱服务器上的传输服务

  - 邮箱服务器上的邮箱传输服务

  - 边缘传输服务器上的传输服务

有关传输管道的详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。

如同以前版本的 Exchange，Exchange 2013 传输通过 Microsoft Exchange Server 2013 传输代理 SDK 提供扩展性。SDK 的 Exchange 2013 版本基于 Microsoft.NET Framework 版本 4.0，并允许第三方实施以下预定义类：

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

在遵照 SDK 库时，结果程序集通过 Exchange 2013 注册，这样会在 SMTP 会话或邮件处理的某个特定阶段加载代理，并调用代理的时间处理器。这些阶段或事件，是代理定义的一部分。代理注册信息存储在 XML 配置文件中。

以下列表说明了在 Exchange 2013 中使用传输代理的要求。

  - 邮箱服务器和边缘传输服务器上的传输服务完全支持 SDK 中的所有预定义分类，所以任何在 Microsoft Exchange Server 2010 上为集线器传输或边缘传输服务器角色写入的第三方传输代理均应该在 Exchange 2013 的传输服务中工作。

  - 前端传输服务仅仅支持 SDK 中的 **SmtpReceiveAgent**类，而第三方代理可以运行在 **OnEndOfData** SMTP 事件上。

  - 邮件传输服务完全不支持 SDK，所以在邮箱传输服务中不可使用任何第三方代理。

对于基于 .NET Framework 4.0 之前版本的旧版传输代理的支持并非默认启用，但是可自行启用。有关说明，请参阅[启用对旧版传输代理的支持](enable-support-for-legacy-transport-agents-exchange-2013-help.md)。

**目录**

对传输代理管理的更新

传输代理和 SMTP 事件

传输代理的优先级

内置传输代理

解决传输代理问题

## 对传输代理管理的更新

由于对 Exchange 2013 传输管道的更新，传输代理 cmdlet 需要在传输服务与前端传输服务之间进行分辨，尤其是客户端访问服务器与邮箱服务器安装在同一计算机上时。有关详细信息，请参阅[管理传输代理](manage-transport-agents-exchange-2013-help.md)。

传输代理管理 cmdlet 操作位于 `%ExchangeInstallPath%TransportRoles\Shared` 的配置文件。对于邮箱服务器和边缘传输服务器上的传输服务，此文件为 `agents.config`。对于客户端访问服务器上的前端传输服务，此文件为 `fetagents.config`。这两个文件使用与 Exchange 2010 中相同的格式。有关管理传输代理的详细信息，请参阅[管理传输代理](manage-transport-agents-exchange-2013-help.md)。

返回顶部

## 传输代理和 SMTP 事件

传输代理使用 SMTP 事件。邮件在传输管道中移动时会触发这些事件。SMTP 事件使传输代理可以在 SMTP 会话期间以及通过组织路由邮件期间，在特定的时间点访问邮件。

请注意，Exchange 2013 中有新的 SMTP 接收事件。客户端访问服务器上的前端传输服务、邮箱服务器和边缘传输服务器上的传输服务以及邮箱服务器上的邮箱传输传递服务中存在 SMTP 接收。分类程序只存在于邮箱服务器和边缘传输服务器上的传输服务。有关运输服务和分类程序的详细信息，请参阅[邮件路由](mail-routing-exchange-2013-help.md)。

下表列出了可提供对传输管道中邮件的访问权限的 SMTP 事件。

### SMTP 接收事件

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>序列</th>
<th>SMTP 事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>通过远程 SMTP 主机的初始连接触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>HELO</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>EHLO</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>STARTTLS</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>AUTH</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>处理远程 SMTP 主机的身份验证时，将触发此事件。</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>远程 SMTP 主机完成身份验证时将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>XSESSIONPARAMS</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>MAIL FROM</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>RCPT TO</code> 命令时将触发此事件。</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>DATA</code>（文本）或 <code>BDAT</code>（二进制数据）命令时将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>远程 SMTP 主机完成提交电子邮件头时，将触发此事件。此由分隔邮件头和邮件正文的空白行 (<code>&lt;CRLF&gt;</code>) 指明。</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>客户端访问服务器上的前端传输服务将传入 SMTP 会话中继或<em>代理</em>到邮箱服务器上的传输服务时，将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>远程 SMTP 主机发出数据结尾命令时，将触发此事件。对于 <code>DATA</code> 命令启动的文本会话，数据结尾指示符为 <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>。对于 <code>BDAT</code> 命令启动的二进制会话，数据结尾指示符为 <code>BDAT LAST</code>。</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>HELP</code> 命令时将触发此事件</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>远程 SMTP 主机发出 <code>NOOP</code> 命令时将触发此事件</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>如果接收 SMTP 主机向发送 SMTP 主机发出临时或永久传递状态通知 (DSN) 代码，则触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>发送 SMTP 主机发出 <code>RSET</code> 命令时将触发此事件</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>接收或发送 SMTP 主机断开 SMTP 会话前，将触发此事件。通常，远程 SMTP 主机发出 <code>QUIT</code> 命令时将触发此事件</p></td>
</tr>
</tbody>
</table>


\*\* 在 **OnConnectEvent** 之后和 **OnDisconnectEvent** 之前，随时可以发生这些事件。

### 分类程序事件

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>序列</th>
<th>分类程序事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>邮件到达接收邮箱服务器或边缘传输服务器上传输服务中的提交队列时，将触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>在解析所有收件人之后到为每个收件人确定跃点之前的这段时间，将触发此事件。使用 <strong>OnResolvedMessage</strong> 路由事件，能够通过每个收件人的 <strong>SetRoutingOverride</strong> 方法使用后续事件覆盖默认的路由行为。</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>对邮件进行分类、扩展通讯组列表并且解析了收件人后，将会触发此事件。</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>分类程序完成邮件处理时，将触发此事件。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 传输代理的优先级

有两个因素可确定传输管道中邮件传输代理操作的顺序：

1.  注册传输代理位置的 SMTP 事件，以及该 SMTP 事件遇到邮件的时间。

2.  多个代理注册到同一个 SMTP 事件时，分配给传输代理的优先级值。最高优先级为 1。较高的整数值表示较低的代理优先级。

例如，假设您已配置以下传输代理：

  - 优先级为 1 的传输代理 A 与优先级为 2 的传输代理 C 被注册到 **OnEndOfHeaders** SMTP 事件。

  - 优先级为 4 的传输代理 B 被注册到 **OnMailCommand** SMTP 事件。

因为 **OnMailCommand** 事件在 **OnEndOfHeaders** 事件之前遇到邮件，因此传输代理 B 最先应用于邮件。当邮件到达 **OnEndOfHeaders** 事件时，因为传输代理 A 优先级高于（整数值低于）传输代理 C，所以在传输代理 C 之前先应用传输代理 A。

## 内置传输代理

Exchange 2013 包含许多内置的传输代理，这些代理具有反垃圾邮件、传输规则和日志记录等功能。通过传输代理 cmdlet，Exchange 2013 邮箱服务器和客户端访问服务器上的大多数内置传输代理均不可见且不受管理。实际上，邮箱服务器和边缘传输服务器上传输服务中的所有内置传输代理均可见且易管理。

邮箱服务器上更令人关注的内置传输代理详见下表。请注意，此表不包括许多不可见且不受管理的传输代理。

### 邮箱服务器上令人关注的内置传输代理

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理名</th>
<th>易于管理？</th>
<th>Priority</th>
<th>SMTP 或分类程序事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>传输规则代理</p></td>
<td><p>是</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>恶意软件代理</p></td>
<td><p>是</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>文本消息路由代理</p></td>
<td><p>是</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>文本消息传递代理</p></td>
<td><p>是</p></td>
<td><p>4</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>日记代理</p></td>
<td><p>否</p></td>
<td><p>无法配置</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>日记报告解密代理</p></td>
<td><p>否</p></td>
<td><p>无法配置</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 解密代理</p></td>
<td><p>否</p></td>
<td><p>无法配置</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>RMS 加密代理</p></td>
<td><p>否</p></td>
<td><p>无法配置</p></td>
<td><p><strong>OnSubmittedMessage</strong> 和 <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 协议解密代理</p></td>
<td><p>否</p></td>
<td><p>无法配置</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


通过传输代理管理 cmdlet 或其他特定功能 cmdlet，边缘传输服务器上的大多数内置传输代理均可见且易管理。

边缘传输服务器上更令人关注的内置传输代理详见下表。请注意，此表不包括不可见或不受管理的传输代理。

### 边缘传输服务器上令人关注的内置传输代理

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>代理名</th>
<th>易于管理？</th>
<th>优先级</th>
<th>SMTP 或分类程序事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>连接筛选代理</p></td>
<td><p>是</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>、<strong>OnMailCommand</strong>、<strong>OnRcptComand</strong> 和 <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>地址重写入站代理</p></td>
<td><p>是</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong> 和 <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>边缘规则代理</p></td>
<td><p>是</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>内容筛选器代理*</p></td>
<td><p>是</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>发件人 ID 代理*</p></td>
<td><p>是</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>发件人筛选器代理*</p></td>
<td><p>是</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong> 和 <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>收件人筛选器代理</p></td>
<td><p>是</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>协议分析代理*</p></td>
<td><p>是</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>、<strong>OnEndOfHeaders</strong>、<strong>OnEndOfData</strong>、<strong>OnReject</strong>、<strong>OnRsetCommand</strong> 和 <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>附件筛选代理</p></td>
<td><p>是</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>地址重写出站代理</p></td>
<td><p>是</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong> 和 <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* 您还可以在邮箱服务器上安装和配置这些反垃圾邮件代理。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

返回顶部

## 解决传输代理问题

为了帮助您解决传输代理问题，可以使用以下功能：

  - **Get-TransportPipeline**   此 cmdlet 显示 SMTP 事件以及在 Exchange 服务器上遇到邮件的相应传输代理。有关详细信息，请参阅[查看传输管道中的传输代理](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md)。

  - **管道跟踪**   管道跟踪能够在邮件遇到每个传输代理前后创建邮件的准确快照。这使您可以找到导致意外结果的传输代理。有关详细信息，请参阅[管道跟踪](pipeline-tracing-exchange-2013-help.md)。

返回顶部

