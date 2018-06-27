---
title: '反垃圾邮件代理日志记录: Exchange 2013 Help'
TOCTitle: 反垃圾邮件代理日志记录
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50491704
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 反垃圾邮件代理日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

代理日志通过 Microsoft Exchange Server 2013 中特定的反垃圾邮件代理记录在邮件上执行的操作。只有下列代理可以将信息写入代理日志：

  - 连接筛选代理

  - 内容筛选器代理

  - 边缘规则代理

  - 收件人筛选器代理

  - 发件人筛选器代理

  - 发件人 ID 代理

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>“连接筛选”代理和“边缘规则”代理在邮箱服务器上不可用。</td>
</tr>
</tbody>
</table>


写入代理日志中的信息取决于代理、SMTP 事件和对邮件执行的操作。

使用 Exchange 命令行管理程序中的 **Set-TransportService** cmdlet 可执行所有代理日志配置任务。以下选项可用于代理日志：

  - 启用或禁用代理日志记录。默认为启用。

  - 指定代理日志文件的位置。默认值为 %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog。

  - 指定个别代理日志文件的最大大小。默认大小为 10 MB。

  - 指定包含代理日志文件的目录的最大大小。默认大小为 250 MB。

  - 指定代理日志文件的最长期限。默认期限为 7 天。

Exchange 使用循环日志记录，并基于文件大小和文件期限对代理日志进行限制，以帮助控制日志文件所使用的硬盘空间。

**目录**

传输代理概述

代理日志文件的结构

写入代理日志的信息

搜索代理日志

## 传输代理概述

代理仅可以在 SMTP 命令顺序中的特定点对邮件进行操作，该 SMTP 命令顺序用于通过邮箱服务器或边缘传输服务器上的传输服务传输邮件。SMTP 命令顺序中的这些访问点称为“SMTP 事件”。每个代理都具有可为其分配的优先级值。但是，SMTP 事件必须始终以特定顺序出现。因此，代理的优先级取决于 SMTP 事件。如果在同一个 SMTP 事件期间两个代理都可对邮件进行操作，则具有较高优先级的代理可首先对该邮件进行操作。

下表列出了 SMTP 事件（以出现顺序）和向代理日志写入信息的代理（以代理对每个 SMTP 事件的由高至低优先级顺序）。

### SMTP 事件（以出现顺序）和向代理日志写入信息的代理（以代理对每个 SMTP 事件的优先级顺序）

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>SMTP 事件</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>连接筛选代理</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>连接筛选代理</p>
<p>发件人筛选器代理</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>连接筛选代理</p>
<p>收件人筛选器代理</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>连接筛选代理</p>
<p>发件人 ID 代理</p>
<p>发件人筛选器代理</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>边缘规则代理</p>
<p>内容筛选代理</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>“连接筛选”代理和“边缘规则”代理在邮箱服务器上不可用。</td>
</tr>
</tbody>
</table>


有关代理、SMTP 事件和代理优先级的详细信息，请参阅[传输代理](transport-agents-exchange-2013-help.md)。

返回顶部

## 代理日志文件的结构

代理日志存在于 %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog。

代理日志文件的命名约定为 AGENTLOG*yyyymmdd-nnnn*.log。占位符代表下列信息：

  - 占位符 *yyyymmdd* 是创建日志文件的协调世界时 (UTC) 日期。占位符 *yyyy* = 年，*mm* = 月，*dd* = 天。

  - 占位符 *nnnn* 为每天的实例编号，从值 1 开始。

信息将写入日志文件，直到文件大小达到其指定的最大值，然后打开具有递增实例编号的新日志文件。此过程在全天重复进行。代理日志目录达到其指定的最大大小时，或日志文件达到其指定的最长期限时，循环日志记录将删除最早的日志文件。

代理日志文件是文本文件，其中包含逗号分隔值文件 (CSV) 格式的数据。每个代理日志文件的文件头都包含下列信息：

  - **\#Software：**创建代理日志文件的软件的名称。通常情况下，此值是 Microsoft Exchange Server。

  - **\#Version：**创建代理日志文件的软件的版本号。当前值为 15.0.0.0。

  - **\#Log-Type**   日志类型的值，即代理日志。

  - **\#Date：**创建日志文件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年，*mm* = 月，*dd* = 天，T 表示时间部分的开头，*hh* = 小时，*mm* = 分钟，*ss* = 秒，*fff* = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。

  - **\#Fields：**代理日志文件中使用的字段名（以逗号分隔）。

返回顶部

## 写入代理日志的信息

代理日志将每个代理事务存储在日志中的一行上。存储在每行上的信息按这些字段组织。这些字段用逗号隔开。通常，字段名是描述性的，足以确定其包含的信息类型。但是，某些字段可能为空。或者存储在字段中的信息类型可能根据代理或代理对邮件执行的操作而更改。下表说明了用于对各个代理事务分类的字段。

### 用于对每个代理事务进行分类的字段

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
<td><p><strong>Timestamp</strong></p></td>
<td><p>代理事件的 UTC 日期/时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年，<em>mm</em> = 月，<em>dd</em> = 天，T 表示时间部分的开头，<em>hh</em> = 小时，<em>mm</em> = 分钟，<em>ss</em> = 秒，<em>fff</em> = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>唯一 SMTP 会话标识符。此标识符由 16 位数的十六进制数字表示。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>接受邮件的本地 IP 地址和端口号。SMTP 会话通常使用端口 25。</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>连接到此服务器传递邮件的以前 SMTP 服务器的 IP 地址和端口号。如果 Internet 邮件通过外围网络中的边缘传输服务器流动，邮箱服务器上代理日志中 <strong>RemoteEndpoint</strong> 的值将为边缘传输服务器的 IP 地址。即使通过 SMTP 传输邮件，发送服务器使用的端口号也是大于 1,024 的一个随机数字。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>首先连接到 Exchange 组织以传递邮件的远程 SMTP 服务器的 IP 地址。在边缘传输服务器上，<strong>RemoteEndpoint</strong> 和 <strong>EnteredOrgFromIP</strong> 的值相同。反垃圾邮件代理使用 <strong>EnteredOrgFromIP</strong> 中的 IP 地址检查邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p><code>MessageID</code> 头字段的值。如果此值为空，则 Exchange 传输服务器将分配一个可以接受邮件的任意值。分配值后，<code>MessageID</code> 的值在邮件生存期内是常量。</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>由邮件信封的 <code>MAIL FROM</code> 中指定的发件人电子邮件地址。此值用于在 SMTP 邮件服务器之间传输邮件。此值作为 <strong>P2FromAddresses</strong> 的值的比较，以确定邮件头中的发件人地址是否是伪造的。</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>在邮件头中的 <code>From</code> 头字段或 <code>Sender</code> 头字段中指定的发件人电子邮件地址。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>收件人的电子邮件地址。虽然原始邮件可能包含多个收件人，但是在代理日志中每行仅显示一个收件人。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>原始邮件中的收件人总数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>执行操作的代理的名称。可能的值如下：</p>
<ul>
<li><p>内容筛选器代理</p></li>
<li><p>收件人筛选器代理</p></li>
<li><p>发件人筛选器代理</p></li>
<li><p>发件人 ID 代理</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>代理执行操作的 SMTP 事件。<strong>Event</strong> 的值取决于代理。本主题前面的第一个表中已介绍了可用于各个代理的 SMTP 事件。<strong>Event</strong> 的可能值如下所述：</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>代理对邮件所执行的操作。<strong>Action</strong> 的可能值如下所述：</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>在 RFC 2034 中定义的增强的 SMTP 响应。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>代理所提供的操作原因。</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>代理所提供的有关操作的描述性详细信息。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 搜索代理日志

可以使用 **Get-AgentLog** cmdlet 和 **Get-AntiSpamFilteringReport.ps1** 脚本搜索代理日志。

**Get-AntiSpamFilteringReport.ps1** 脚本位于 `%ExchangeInstallPath%Scripts` 中。需要从脚本文件夹运行命令行管理程序的脚本。若要将命令行管理程序中的位置更改到脚本文件夹，请运行以下命令：

    Cd $env:ExchangeInstallPath\Scripts

若要运行脚本文件夹中的脚本，请使用以下语法：

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

有关使用脚本的详细信息，请运行以下命令：

    Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1

返回顶部

