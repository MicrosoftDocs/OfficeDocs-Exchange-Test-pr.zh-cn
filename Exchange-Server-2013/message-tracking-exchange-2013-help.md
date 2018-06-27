---
title: '邮件跟踪: Exchange 2013 Help'
TOCTitle: 邮件跟踪
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51408270
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件跟踪

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

在 Microsoft Exchange Server 2013 中，邮件跟踪日志详细记录了邮件从邮箱服务器上的传输服务、邮箱服务器上的邮箱和边缘传输服务器来回传输产生的所有邮件活动。可以使用邮件跟踪日志进行邮件取证、邮件流分析、报告和故障排除。

在 Exchange 2013 中，可以使用 **Set-TransportService** cmdlet 或 **Set-MailboxServer** cmdlet 执行所有的邮件跟踪配置任务，因为 Exchange 2013 邮箱服务器会保留传输服务和邮箱。可以使用这两个 cmdlet 中的任何一个进行下列邮件跟踪配置更改：

  - 启用或禁用邮件跟踪。默认为启用。

  - 指定邮件跟踪日志文件的位置。

  - 指定个人邮件跟踪日志文件的最大大小。默认为 10 MB。

  - 指定包含邮件跟踪日志文件的目录的最大大小：默认为 1000 MB。

  - 指定邮件跟踪日志文件的最长期限：默认为 30 天。

  - 启用或禁用邮件跟踪日志中的邮件主题日志记录。默认为启用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您也可以使用 Exchange 管理中心 (EAC) 来启用或禁用邮件跟踪，并指定邮件跟踪日志文件的位置。</td>
</tr>
</tbody>
</table>


默认情况下，Exchange 使用循环日志记录根据文件大小和文件期限对邮件跟踪日志进行限制，以帮助控制邮件跟踪日志文件所使用的硬盘空间。

**目录**

搜索邮件跟踪日志

邮件跟踪日志文件的结构

邮件跟踪日志文件中的字段

邮件跟踪日志中的事件类型

邮件跟踪日志中的源值

邮件跟踪日志中的示例条目

邮件跟踪日志的安全注意事项

## 搜索邮件跟踪日志

邮件跟踪日志包含邮件在 Exchange 2013 邮箱服务器中移动时产生的大量数据。对于搜索邮件跟踪日志，有几个不同的选择。

  - **Get-MessageTrackingLog**   管理员可以使用此 cmdlet 来搜索邮件跟踪日志，以获取有关使用大量筛选条件的邮件的信息。有关详细信息，请参阅[搜索邮件跟踪日志](search-message-tracking-logs-exchange-2013-help.md)。

  - **管理员的送达报告**   管理员可以使用 Exchange 管理中心 (EAC) 内的“**送达报告**”选项卡或基本的 **Search-MessageTrackingReport** 和 **Get-MesageTrackingReport** cmdlet 来搜索邮件跟踪日志，以获取有关由组织中特定邮箱发送或接收的邮件的信息。有关详细信息，请参阅[管理员的送达报告](delivery-reports-for-administrators-exchange-2013-help.md)。

  - **用户的送达报告**   用户可以使用 Outlook Web App 中的“**送达报告**”选项卡来搜索邮件跟踪日志，以获取有关由其自己邮箱发送或接收的邮件的信息。有关详细信息，请参阅[用户的送达报告](https://go.microsoft.com/fwlink/?linkid=279920)。

返回顶部

## 邮件跟踪日志文件的结构

默认情况下，邮件跟踪日志文件位于 %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking。

邮件跟踪日志目录中日志文件的命名约定是 `MSGTRK`*yyyymmdd-nnnn*`.log`、`MSGTRKMA`*yyyymmdd-nnnn*`.log`、`MSGTRKMD`*yyyymmdd-nnnn*`.log` 和 `MSGTRKMS`*yyyymmdd-nnnn*`.log`。下列服务使用不同的日志：

  - **MSGTRK**   这些日志与传输服务相关。

  - **MSGTRKMA**   这些日志与仲裁传输所使用的批准和拒绝功能相关。有关详细信息，请参阅[管理邮件审批](manage-message-approval-exchange-2013-help.md)。

  - **MSGTRKMD**   这些日志与邮箱传递送达服务传递至邮箱的邮件相关。

  - **MSGTRKMS**   这些日志与邮箱传输提交服务从邮箱发出的邮件相关。

日志文件名称中的占位符代表以下信息：

  - 占位符 *yyyymmdd* 为创建日志文件的协调世界时 (UTC) 日期。*yyyy* = 年，*mm* = 月，*dd* = 日。

  - 占位符 *nnnn* 是每个邮件跟踪日志文件名称前缀的每天的实例编号，其值从 1 开始。

信息写入到每个日志文件中，直到文件大小达到其指定的最大值。然后打开具有递增实例编号的新日志文件。此过程在全天重复进行。当满足以下任一条件时，日志文件轮换功能将删除最旧的日志文件：

  - 日志文件达到其指定的最长期限。

  - 邮件跟踪日志目录达到其指定最大大小。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>邮件跟踪日志目录的最大大小按以下方法计算：将具有相同名称前缀的所有日志文件的大小相加，求其总和。在计算总目录大小时，不会将其他未遵循名称前缀约定的文件计算在内。重命名旧日志文件或将其他文件复制到邮件跟踪日志目录可能会导致目录超出指定的最大大小。<br />
    在 Exchange 2013 邮箱服务器上，邮箱跟踪日志目录的最大大小是指定值的三倍。虽然由这四个不同服务生成的邮件跟踪日志文件有四个不同的名称前缀，但是与另外三个日志文件前缀相比，写入 <strong>MSGTRKMA</strong> 日志文件的数据量和数据频率几乎可以忽略不计。</td>
    </tr>
    </tbody>
    </table>


邮件跟踪日志文件是文本文件，其中包含逗号分隔值 (CSV) 格式的数据。每个邮件跟踪日志文件的文件头都包含下列信息：

  - **\#Software:**   创建邮件跟踪日志文件的软件名称。通常情况下，此值是 Microsoft Exchange Server。

  - **\#Version:**   创建邮件跟踪日志文件的软件版本号。当前值为 15.0.0.0。

  - **\#Log-Type:**   日志类型值，即邮件跟踪日志。

  - **\#Date:**   创建日志文件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年，*mm* = 月，*dd* = 天，T 表示时间部分的开头，*hh* = 小时，*mm* = 分钟，*ss* = 秒，*fff* = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。

  - **\#Fields:**   邮件跟踪日志文件中使用的以逗号分隔的字段名。

返回顶部

## 邮件跟踪日志文件中的字段

邮件跟踪日志将每个邮件事件存储在日志中的一行上。邮件事件信息由字段组织，这些字段由逗号分隔。通常，字段名是描述性的，足以确定其包含的信息的类型。但是，某些字段可能为空，或是存储在字段中的信息类型可能会随邮件事件类型和记录事件的邮件跟踪日志文件类型的变化而发生变化。下表对用于分类各邮件跟踪事件的字段进行了一般性说明。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>date-time</strong></p></td>
<td><p>邮件跟踪事件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年，<em>mm</em> = 月，<em>dd</em> = 天，T 表示时间部分的开头，<em>hh</em> = 小时，<em>mm</em> = 分钟，<em>ss</em> = 秒，<em>fff</em> = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>提交邮件的消息服务器或消息客户端的 IPv4 或 IPv6 地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>客户端主机名</strong></p></td>
<td><p>提交邮件的消息服务器或消息客户端的主机名或 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>源或目标 Exchange 服务器的 IPv4 或 IPv6 地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>目标服务器的主机名或 FQDN。</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>与 <strong>source</strong> 字段相关联的额外信息。例如，传输代理信息。</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>源发送连接器或接收连接器或者目标发送连接器或接收连接器的名称。例如，<em>ServerName</em>\<em>ConnectorName</em> 或 <em>ConnectorName</em>。</p></td>
</tr>
<tr class="even">
<td><p><strong>来源</strong></p></td>
<td><p>负责邮件跟踪事件的 Exchange 传输组件。本主题后面的邮件跟踪日志中的源值部分会对该字段中的值进行介绍。</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>邮件事件类型。本主题后面的邮件跟踪日志中的事件类型部分会对事件类型进行介绍。</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>由当前正在处理邮件的 Exchange 服务器所分配的邮件标识符。</p>
<p>在涉及邮件传输的每个 Exchange 服务器的邮件跟踪日志中，特定邮件的 <strong>internal-message-id</strong> 值是各不相同的。示例值为 <code>73014444033</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>邮件头中 <strong>Message-Id:</strong> 头字段的值。如果 <strong>Message-Id:</strong> 头字段不存在或为空，则为其分配一个任意值。该值在邮件生存期内是常量。对于在 Exchange 中创建的邮件，该值的格式为 <code>&lt;GUID@ServerFQDN&gt;</code>，包括尖括号 (<code>&lt; &gt;</code>)。例如，<code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>。其他邮件系统可能使用不同的语法或值。</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>唯一的邮件 ID 值，因拆分或通讯组扩展而创建，且在各邮件副本中均保持有效。示例值为 <code>1341ac7b13fb42ab4d4408cf7f55890f</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>邮件收件人的电子邮件地址。多个电子邮件地址通过分号字符 (;) 分隔。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>该字段包含由分号字符 (;) 分隔的各收件人状态。收件人状态值的显示顺序与 <strong>recipient-address</strong> 字段中的值相同。示例状态值包括 <code>250 2.1.5 Recipient OK</code> 或 <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>包括附件的邮件的大小，以字节为单位。</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>邮件中的收件人数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>该字段与 <strong>EXPAND</strong>、<strong>REDIRECT</strong> 和 <strong>RESOLVE</strong> 事件一起使用来显示与邮件相关联的其他收件人电子邮件地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>该字段包含特定类型事件的其他信息。例如：</p>
<p><strong>DSN</strong>   包含报告链接，如果 DSN 是在事件发生之后生成的，则该报告链接为相关传递状态通知的 <strong>Message-Id</strong> 值。如果这是 DSN 邮件，<strong>Reference</strong> 字段则包含生成该 DSN 的原始邮件的 <strong>Message-Id</strong> 值。</p>
<p><strong>EXPAND</strong>   该参考字段包含相关邮件的 <strong>related-recipient-address</strong> 值。</p>
<p><strong>RECEIVE</strong>   如果相关邮件由其他过程生成（例如日记或收件箱规则），则该参考字段可能会包含该邮件的 <strong>Message-Id</strong> 值。</p>
<p><strong>SEND</strong> 该参考字段包含任何 DSN 邮件的 <strong>Internal-Message-Id</strong> 值。</p>
<p><strong>THROTTLE</strong>   该参考字段包含邮件限制的原因。</p>
<p><strong>TRANSFER</strong> 该参考字段包含正在被分支的邮件的 Internet 邮件 ID。</p>
<p>对于由收件箱规则生成的邮件，<strong>Reference</strong> 字段包含使收件箱规则生成出站邮件的入站邮件的 <strong>Internal-Message-Id</strong> 值。</p>
<p>对于其他类型的事件，<strong>Reference</strong> 字段可能包含分支邮件的 <strong>Internal-Message-Id</strong> 值。</p>
<p>对于其他类型的事件，<strong>Reference</strong> 字段通常为空。</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>在 <code>Subject:</code> 头字段中找到的邮件主题。邮件主题的跟踪由 <strong>Set-TransportService</strong> 或 <strong>Set-MailboxServer</strong> cmdlet 中的 <em>MessageTrackingLogSubjectLoggingEnabled</em> 参数进行控制。默认情况下，启用邮件主题跟踪。</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p><code>Sender:</code> 头字段中指定的电子邮件地址，如果 <code>Sender:</code> 不存在，则为 <code>From:</code> 头字段中指定的电子邮件地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>由邮件信封中 <code>MAIL FROM:</code> 指定的返回电子邮件地址。尽管此字段从不为空，但它可以有表示为 <code>&lt;&gt;</code> 的空发件人地址值。</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>有关该邮件的其他信息。例如：</p>
<ul>
<li><p><strong>DELIVER</strong> 和 <strong>SEND</strong> 事件的邮件起始 UTC 日期-时间。起始日期-时间是邮件第一次传入 Exchange 组织的时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年，<em>mm</em> = 月，<em>dd</em> = 天，T 表示时间部分的开头，<em>hh</em> = 小时，<em>mm</em> = 分钟，<em>ss</em> = 秒，<em>fff</em> = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。</p></li>
<li><p>身份验证错误。例如，可以看到身份验证出错时所使用的值 <code>11a</code> 和身份验证类型。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>方向性</strong></p></td>
<td><p>邮件的方向。示例值包括 <code>Incoming</code>、<code>Undefined</code> 和 <code>Originating</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>该字段不可用于内部部署 Exchange 2013 组织。</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>原始客户端的 IPv4 或 IPv6 地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>原始服务器的 IPv4 或 IPv6 地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>该字段包含与特定事件类型相关的数据。例如，传输规则代理使用该字段对在邮件上执行的传输规则或 DLP 策略的 GUID 进行记录。有关这些传输规则代理值的更多信息，请参阅 <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">查看 DLP 策略检测报告</a>主题中的“数据日志记录”部分。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件跟踪日志中的事件类型

**event-id** 字段中的各种事件类型可用来对邮件跟踪日志中的邮件事件进行分类。一些邮件事件只出现在一种类型的邮件跟踪日志文件中，还有一些邮件事件存在于所有类型的邮件跟踪日志文件中。下表介绍了用于对各邮件事件进行分类的事件类型。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>传输代理使用该事件记录自定义数据。</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>分拣目录或重播目录提交的邮件无法传递或返回。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>邮件传递延迟。</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>邮件已传递至本地邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>在不提供传递状态通知（亦称为 DSN、退回邮件、未送达报告或 NDR）的情况下删除了一条消息。例如：</p>
<ul>
<li><p>已完成裁决审批请求邮件。</p></li>
<li><p>在不提供 NDR 的情况下悄悄丢弃的垃圾邮件。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>已生成发送状态通知 (DSN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>向收件人传递重复邮件。如果收件人是多个嵌套通讯组的成员，则可能会发生复制邮件情况。信息存储将检测并删除重复邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>在通讯组扩展期间，检测到一个重复收件人。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>邮件的备用收件人已成为收件人。</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>已扩展通讯组。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>邮件传递失败。源包括 <strong>SMTP</strong>、<strong>DNS</strong>、<strong>QUEUE</strong> 和 <strong>ROUTING</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>在主副本传递至下一跃点之后丢弃影子邮件。有关详细信息，请参阅<a href="shadow-redundancy-exchange-2013-help.md">卷影冗余</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>影子邮件由本地数据库可用性组 (DAG) 或 Active Directory 站点中的服务器接收。</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>创建了影子邮件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>影子邮件创建失败。详细信息存储于 <strong>source-context</strong> 字段中。</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>邮件已发送至仲裁收件人，因此该邮件已发送至仲裁邮箱进行审批。有关详细信息，请参阅<a href="manage-message-approval-exchange-2013-help.md">管理邮件审批</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>启动时已成功加载邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>仲裁收件人的仲裁人从不批准或拒绝邮件，进而导致该邮件到期。有关仲裁收件人的更多信息，请参阅<a href="manage-message-approval-exchange-2013-help.md">管理邮件审批</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>仲裁收件人的仲裁人批准了邮件，从而使该邮件传递至仲裁收件人。</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>仲裁收件人的仲裁人拒绝了邮件，从而使该邮件未传递至仲裁收件人。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>发送至仲裁收件人的所有仲裁人的所有批准请求都不可传递，从而导致产生未送达报告 (NDR)。</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>在本地服务器上的邮箱发件箱内检测到一封邮件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>在本地服务器上的邮箱发件箱内检测到一封邮件，并且需要创建该邮件的影子副本。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>邮件被放入带毒邮件队列中或从带毒邮件队列中删除。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>已成功处理邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>会议邮件已由邮箱传输传递服务处理。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>邮件由传输服务的 SMTP 接收组件接收或由分拣或重播目录发送（源：<code>SMTP</code>），或邮件已从邮箱提交至邮箱传输提交服务（源：<code>STOREDRIVER</code>）。</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>在 Active Directory 查找后，邮件被重定向至一个备用收件人。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>在 Active Directory 查找后，邮件收件人被解析为一个不同的电子邮件地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>已从安全网络自动重新提交邮件。有关详细信息，请参阅<a href="safety-net-exchange-2013-help.md">Safety Net</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>已延迟从安全网络重新提交的邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>从安全网络重新提交的邮件失败。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>邮件由传输服务间的 SMTP 发送。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>邮箱传输提交服务已成功将邮件传输至传输服务。对于 <strong>SUBMIT</strong> 事件，<strong>source-context</strong> 属性包含下列详细信息：</p>
<ul>
<li><p><strong>MDB</strong>   邮箱数据库 GUID。</p></li>
<li><p><strong>Mailbox</strong>   邮箱 GUID。</p></li>
<li><p><strong>Event</strong>   事件序列号。</p></li>
<li><p><strong>MessageClass</strong>   邮件类型。例如，<code>IPM.Note</code>。</p></li>
<li><p><strong>CreationTime</strong>   邮件提交的日期-时间。</p></li>
<li><p><strong>ClientType</strong>   例如，<code>User</code>、<code>OWA</code> 或 <code>ActiveSync</code>。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>已延迟将邮件从邮箱传输提交服务传输至传输服务。</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>将邮件从邮箱传输提交服务传输至传输服务的操作失败。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>邮件传输被抑制。</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>邮件被限制。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>由于内容转换、邮件收件人限制或代理原因，收件人被移动到分支的邮件。源包括 <strong>ROUTING</strong> 或 <strong>QUEUE</strong>。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件跟踪日志中的源值

邮件跟踪日志中 **source** 字段的值指示负责邮件跟踪事件的传输组件。下表描述 **source** 字段的值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>源值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>事件源是人工干预。例如，管理员使用队列查看器删除邮件或使用重播目录提交邮件文件。</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>事件源是传输代理。</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>事件源是仲裁收件人使用的审批框架。有关详细信息，请参阅<a href="manage-message-approval-exchange-2013-help.md">管理邮件审批</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>事件源是在启动时存在于服务器上的未处理的消息。这与 <strong>LOAD</strong> 事件类型有关。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>事件源是 DNS。</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>事件源是传递状态通知 (DSN)。例如，未送达报告 (NDR)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>事件源是外部连接器。有关详细信息，请参阅<a href="foreign-connectors-exchange-2013-help.md">外部连接器</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>事件源是收件箱规则。有关更多信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=285479">收件箱规则</a>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>事件源是会议邮件处理器，它会随会议更新而更新日历。</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>事件源是发信请求备用收件人 (ORAR)。您可以通过使用 <strong>New-ReceiveConnector</strong> 或 <strong>Set-ReceiveConnector</strong> cmdlet 中的 <em>OrarEnabled</em> 参数启用或禁用对接收连接器上 ORAR 的支持。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>事件源是分拣目录。有关详细信息，请参阅<a href="pickup-directory-and-replay-directory-exchange-2013-help.md">拾取目录和重播目录</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>事件源是病毒邮件标识符。有关病毒邮件和病毒邮件队列的更多信息，请参阅<a href="queues-exchange-2013-help.md">队列</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>事件源是启用邮件的公用文件夹。</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>事件源是队列。</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>事件源是卷影冗余。有关详细信息，请参阅<a href="shadow-redundancy-exchange-2013-help.md">卷影冗余</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>事件源是传输服务中分类程序的路由解析组件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>事件源是安全网络。有关详细信息，请参阅<a href="safety-net-exchange-2013-help.md">Safety Net</a>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>邮件已由传输服务的 SMTP 发送或 SMTP 接收组件提交。</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>事件源是来自本地服务器上邮箱的 MAPI 提交。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件跟踪日志中的示例条目

在两个用户间发送的无事件邮件可在邮件跟踪日志中生成若干条目。您可以使用 **Get-MessageTrackingLog** cmdlet 查看结果。有关详细信息，请参阅[搜索邮件跟踪日志](search-message-tracking-logs-exchange-2013-help.md)。

在此简化示例中，当用户 chris@contoso.com 将测试邮件成功发送至用户 michelle@contoso.com 时，创建了邮件跟踪日志条目。两个用户的邮箱位于同一服务器上。

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

返回顶部

## 邮件跟踪日志的安全注意事项

邮件跟踪日志中不存储任何邮件内容。默认情况下，电子邮件的主题行存储在邮件跟踪日志中。但可能需要禁用邮件主题日志记录，以满足更高的安全或隐私要求。在启用或禁用邮件主题日志记录之前，请确保已验证有关显示主题行信息的组织策略。有关详细信息，请参阅[配置邮件跟踪](configure-message-tracking-exchange-2013-help.md)。

返回顶部

