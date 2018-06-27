---
title: '连接日志记录: Exchange 2013 Help'
TOCTitle: 连接日志记录
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50491628
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 连接日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

连接日志记录可记录传出连接活动，该活动用于通过 Exchange 服务器上的传输服务传输邮件。连接日志的用途不是跟踪各个电子邮件的传输。而是从源到目的地跟踪连接活动，不考虑传输了多少邮件。连接日志记录在客户端访问服务器上的前端传输服务、邮箱服务器上的集线器传输服务和邮箱服务器上的邮箱传输服务可用。以下列表介绍了在连接日志中记录的信息类型：

  - 来源

  - Destination

  - DNS 解析信息

  - 有关连接故障的详细信息

  - 传输的邮件和字节数

使用 Exchange 命令行管理程序中的 **Set-TransportService**、**Set-FrontEndTransportService** 和 **Set-MailboxTransportService** cmdlet 来执行所有连接日志配置任务。以下选项可用于连接日志：

  - 启用或禁用连接日志记录。默认为启用。

  - 指定连接日志文件的位置。

  - 指定个别连接日志文件的最大大小。默认大小为 10 MB。

  - 指定包含连接日志文件的目录的最大大小。默认大小为 1,000 MB。

  - 指定连接日志文件的最长期限。默认期限为 30 天。

默认情况下，Exchange 使用循环日志记录，根据文件大小和文件期限对连接日志进行限制，以帮助控制连接日志文件所使用的硬盘空间。

**目录**

连接日志文件的结构

写入连接日志的信息

## 连接日志文件的结构

默认情况下，连接日志文件处于下列位置：

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

连接日志文件的命名约定为 CONNECTLOG*yyymmdd-nnnn*.log。占位符代表下列信息：

  - 占位符 *yyyymmdd* 是创建日志文件的协调世界时 (UTC) 日期。占位符 *yyyy* = 年，*mm* = 月，*dd* = 天。

  - 占位符 *nnnn* 为每天的实例编号，从值 1 开始。

信息将写入日志文件，直到文件大小达到其指定的最大值，然后打开具有递增实例编号的新日志文件。此过程在全天重复进行。连接日志目录达到其指定的最大大小时，或日志文件达到其指定的最长期限时，循环日志记录将删除最早的日志文件。

连接日志文件是文本文件，其中包含逗号分隔值文件 (CSV) 格式的数据。每个连接日志文件的文件头都包含下列信息：

  - **\#Software**   创建连接日志文件的软件的名称。通常情况下，此值是 Microsoft Exchange Server。

  - **\#Version**   创建连接日志文件的软件的版本号。当前值为 15.0.0.0。

  - **\#Log-Type**   日志类型的值，即传输连接日志。

  - **\#Date**   创建日志文件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年，*mm* = 月，*dd* = 天，T 表示时间部分的开头，*hh* = 小时，*mm* = 分钟，*ss* = 秒，*fff* = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。

  - **\#Fields**   连接日志文件中使用的字段名（以逗号分隔）。

返回顶部

## 写入连接日志的信息

连接日志将每个出站传输服务连接事件存储在连接日志中的一行上。存储在每行上的信息按这些字段组织。这些字段用逗号隔开。下表说明了用于对各个传出连接事件分类的字段。

### 用于对每个连接事件进行分类的字段

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
<td><p>连接事件的 UTC 日期/时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>GUID 对于每个 SMTP 会话是唯一的，但是对于与该 SMTP 会话关联的每个事件是相同的。对于邮箱传输服务中的 MAPI 会话，会话字段为空。</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p>SMTP 连接的 <strong>SMTP</strong>，指向本地邮箱数据库的邮箱传输服务连接的 <strong>MAPI</strong>。</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>目标的名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>代表连接的开始、中间和结束的一个字符。方向字段使用的可能值如下所示：</p>
<ul>
<li><p><strong>+</strong> 连接</p></li>
<li><p><strong>-</strong> 断开连接</p></li>
<li><p><strong>&gt;</strong> 发送</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>与连接事件相关的文本信息。下列值是描述字段使用的值的示例：</p>
<ul>
<li><p>传输的邮件数和大小</p></li>
<li><p>目标域的 DNS MX 资源记录解析信息</p></li>
<li><p>目标邮箱服务器的 DNS 解析信息</p></li>
<li><p>连接建立消息</p></li>
<li><p>连接失败消息</p></li>
</ul></td>
</tr>
</tbody>
</table>


当传输服务建立起指向目标的连接时，传输服务可能准备好了发送一个邮件或数个邮件。连接和邮件传输过程生成多个事件，这些事件写入连接日志中的多个行中。到不同目标的同时连接创建与不同的交错目标相关的连接日志条目。但是，您可以使用日期-时间、会话、源和方向字段为每个单独的连接排列从开始到结束的连接日志条目。

返回顶部

