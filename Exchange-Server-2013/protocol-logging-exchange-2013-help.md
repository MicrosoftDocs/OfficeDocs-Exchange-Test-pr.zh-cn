---
title: '协议日志记录: Exchange 2013 Help'
TOCTitle: 协议日志记录
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50490429
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 协议日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

协议日志记录可记录邮件服务器之间作为邮件传递的一部分进行的 SMTP 会话。这些 SMTP 会话在发送连接器和接收连接器上进行，而这些连接器分别位于客户端访问服务器上的前端传输服务、邮箱服务器上的传输服务以及邮箱服务器上的邮箱传输服务中。可以使用协议日志记录诊断邮件流问题。

默认情况下，在所有发送连接器和接收连接器上禁用协议日志记录。按每个连接器启用或禁用协议日志记录。其他协议日志记录选项针对的是服务器上各个传输服务中的所有接收连接器或发送连接器。传输服务中的所有接收连接器使用相同的协议日志文件和协议日志选项。这些协议日志文件和协议日志选项独立于同一服务器上传输服务中的发送连接器协议日志文件和协议日志选项。

Exchange 服务器上每个传输服务中的所有发送连接器或接收连接器的协议日志可以使用下列选项：

  - 指定发送连接器或接收连接器的协议日志文件的位置。

  - 指定发送连接器或接收连接器的协议日志文件的最大大小。默认大小为 10 MB。

  - 指定包含发送连接器或接收连接器的协议日志文件的目录的最大大小。默认大小为 250 MB。

  - 指定发送连接器或接收连接器的协议日志文件的最长期限。默认期限为 30 天。

默认情况下，Exchange 使用循环日志记录方式基于文件大小和文件期限来限制协议日志，这样有助于控制日志文件占用的硬盘空间。

在每台邮箱服务器上的传输服务中，以及每台客户端访问服务器上的前端传输服务中，都存在一个名为组织内发送连接器的特殊发送连接器。此连接器是隐式创建的，不可见，也不要求管理。组织内发送连接器供下列传输服务使用：

  - **邮箱服务器上的传输服务**
    
      - 将邮件中继到组织内其他 Exchange 2013 邮箱服务器上的传输服务和邮箱传输服务。
    
      - 将邮件中继到组织内其他 Exchange 2007 或 Exchange 2010 集线器传输服务器。
    
      - 将邮件中继到外围网络中的边缘传输服务器。

  - **客户端访问服务器上的前端传输服务**   将邮件中继到组织内的 Exchange 2013 邮箱服务器上的传输服务。

每台邮箱服务器上的邮箱传输服务中，都有一个名为邮箱传递发送连接器的等效发送连接器。此连接器同样是隐式创建的，不可见，且无需进行管理。邮箱传递发送连接器用于将邮件中继到组织内其他邮箱服务器上的传输服务和邮箱传输服务。

默认情况下，邮箱传递发送连接器的协议日志记录功能也是禁用的。您可以使用 **Set-MailboxTransportService** cmdlet 上的 *MailboxDeliveryConnectorProtocolLoggingLevel* 参数为邮箱传递发送连接器启用或禁用协议日志记录。如果为邮箱传递发送连接器启用了协议日志记录，则会在邮箱服务器的邮箱传输服务的发送连接器协议日志中开始进行日志记录。

**目录**

协议日志文件的结构

写入协议日志的信息

## 协议日志文件的结构

默认情况下，协议日志文件处于下列位置：

  - **邮箱服务器上的传输服务的接收连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **邮箱服务器上的邮箱传输服务的接收连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **客户端服务器上的前端传输服务的接收连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **邮箱服务器上的传输服务的发送连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **邮箱服务器上的邮箱传输服务的发送连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **客户端访问服务器上的前端传输服务的发送连接器协议日志文件**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

每个协议日志目录中日志文件的命名约定为 *prefixyyyymmdd-nnnn*.log。占位符代表下列信息：

  - 占位符 *prefix* 为 SEND（对于发送连接器）或 RECV（对于接收连接器）。

  - 占位符 *yyyymmdd* 为创建日志文件的协调世界时 (UTC) 日期。占位符 *yyyy* = 年，*mm* = 月，*dd* = 日。

  - 占位符 *nnnn* 为每天的实例编号，从值 1 开始。

信息将写入日志文件，直到文件大小达到其指定的最大值，然后打开具有递增实例编号的新日志文件。此过程在全天重复进行。协议日志目录达到其指定的最大大小时，或日志文件达到其指定的最长期限时，循环日志记录将删除最旧的日志文件。

协议日志文件是文本文件，其中包含逗号分隔值文件 (CSV) 格式的数据。每个协议日志文件的文件头都包含下列信息：

  - **\#Software**   创建协议日志文件的软件名称。通常情况下，此值是 Microsoft Exchange Server。

  - **\#Version**   创建协议日志文件的软件版本号。当前值为 15.0.0.0。

  - **\#Log-Type**   此字段的日志类型值是 SMTP 接收协议日志或 SMTP 发送协议日志。

  - **\#Date**   创建日志文件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：*yyyy-mm-dd*T*hh:mm:ss.fff*Z，其中 *yyyy* = 年，*mm* = 月，*dd* = 天，T 表示时间部分的开头，*hh* = 小时，*mm* = 分钟，*ss* = 秒，*fff* = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。

  - **\#Fields**   协议日志文件中使用的字段名（以逗号分隔）。

返回顶部

## 写入协议日志的信息

协议日志将每个 SMTP 协议事件存储在协议日志中的一行上。存储在每行上的信息按这些字段组织。这些字段用逗号隔开。下表介绍了对每个协议分类所用的字段。

### 对每个协议事件分类所用的字段

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
<td><p>协议事件的 UTC 日期-时间。UTC 日期-时间以 ISO 8601 日期-时间格式表示：<em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z，其中 <em>yyyy</em> = 年，<em>mm</em> = 月，<em>dd</em> = 天，T 表示时间部分的开头，<em>hh</em> = 小时，<em>mm</em> = 分钟，<em>ss</em> = 秒，<em>fff</em> = 几分之几秒，而 Z 表示祖鲁语（另一种 UTC 表示方法）。</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>与 SMTP 事件关联的连接器的可分辨名称 (DN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>GUID 对于每个 SMTP 会话是唯一的，但是对于与该 SMTP 会话关联的每个事件是相同的。</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>从 0 开始并为同一个 SMTP 会话内的每个事件递增的计数器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>SMTP 会话的本地终结点。此字段由 IP 地址和 TCP 端口号组成，格式为 <em>&lt;IP 地址&gt;</em>:<em>&lt;端口&gt;</em>。</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>SMTP 会话的远程终结点。此字段由 IP 地址和 TCP 端口号组成，格式为 <em>&lt;IP 地址&gt;</em>:<em>&lt;端口&gt;</em>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>代表协议事件的单个字符。事件的可能值如下：</p>
<ul>
<li><p><strong>+</strong> 连接</p></li>
<li><p><strong>-</strong> 断开连接</p></li>
<li><p><strong>&gt;：</strong>发送</p></li>
<li><p><strong>&lt;：</strong>接收</p></li>
<li><p><strong>*</strong>   信息</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>与 SMTP 事件关联的文本信息。</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>可能与 SMTP 事件关联的其他上下文信息。</p></td>
</tr>
</tbody>
</table>


代表收发单封电子邮件的单个 SMTP 会话会生成多个 SMTP 事件。这些 SMTP 事件造成在协议日志中写入多行。代表收发多封电子邮件的多个 SMTP 会话可能会同时进行。这样，将通过不同的 SMTP 转换创建零散的协议日志条目。可使用 session-id 和 sequence-number 字段按 SMTP 转换对协议日志条目进行排序。

返回顶部

