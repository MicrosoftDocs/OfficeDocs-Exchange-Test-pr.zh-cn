---
title: 'POP3 和 IMAP4 的协议日志记录: Exchange 2013 Help'
TOCTitle: POP3 和 IMAP4 的协议日志记录
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50556542
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# POP3 和 IMAP4 的协议日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

可以使用协议日志记录，在 Exchange 环境中查看 POP3 和 IMAP4 连接。如果要解决与 POP3 或 IMAP4 性能相关的问题，这可能很有用。

## 启用 POP3 和 IMAP4 协议日志记录

可以使用 Exchange 命令行管理程序来启用、禁用或更改协议日志记录。如果使用命令行管理程序启用协议日志记录，则将使用默认的协议日志记录设置。在大多数情况下，默认设置就足够了。

或者，也可通过编辑位于 MicrosoftExchange Server 2013 客户端访问服务器上的 Microsoft.Exchange.Pop3.exe.config 和 Microsoft.Exchange.Imap4.exe.config 配置文件，启用、禁用和修改协议日志记录选项。有关如何管理 POP3 和 IMAP4 协议设置的详细信息，请参阅[配置 POP3 和 IMAP4 的协议日志记录](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)。

## 查看协议日志

协议日志文件是文本文件，其中包含逗号分隔值 (CSV) 文件格式的数据。协议日志将每个协议事件存储在单独的一行中。存储在每行上的信息按这些字段组织。这些字段用逗号隔开。下表介绍了对每个协议事件进行分类所用的字段。

### 对每个协议事件分类所用的字段

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>date-time</p></td>
<td><p>协议事件的日期和时间。该值的格式为 <em>yyyy-mm-ddhh:mm:ss.fffZ</em>，其中 <em>yyyy</em> = 年，<em>mm</em> = 月，<em>dd</em> = 日，<em>hh</em> = 小时，<em>mm</em> = 分，<em>ss</em> = 秒，<em>fff</em> = 秒的小数，<em>Z</em> 表示 Zulu。Zulu 是表示协调世界时 (UTC) 的另一种方式。</p></td>
</tr>
<tr class="even">
<td><p>connector-id</p></td>
<td><p>该字段不能用于 POP3 和 IMAP4 协议日志记录。</p></td>
</tr>
<tr class="odd">
<td><p>session-id</p></td>
<td><p>可唯一标识与协议事件关联的 SMTP 的 GUID。</p></td>
</tr>
<tr class="even">
<td><p>sequence-number</p></td>
<td><p>从 0 开始计数并针对同一个会话内的每个事件递增的计数器。</p></td>
</tr>
<tr class="odd">
<td><p>local-endpoint</p></td>
<td><p>POP3 或 IMAP4 会话的本地终结点。这包括 IP 地址和 TCP 端口号，格式如下所示：<em>&lt;IP 地址&gt;</em>:<em>&lt;端口&gt;</em>。</p></td>
</tr>
<tr class="even">
<td><p>remote-endpoint</p></td>
<td><p>POP3 或 IMAP4 会话的远程终结点。这包括 IP 地址和 TCP 端口号，格式如下所示：<em>&lt;IP 地址&gt;</em>:<em>&lt;端口&gt;</em>。</p></td>
</tr>
<tr class="odd">
<td><p>event</p></td>
<td><p>代表协议事件的单个字符。事件的可能值如下：</p>
<ul>
<li><p>+：连接</p></li>
<li><p>-：断开连接</p></li>
<li><p>&gt;：发送</p></li>
<li><p>&lt;：接收</p></li>
<li><p>*：信息</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>数据</p></td>
<td><p>与 POP3 或 IMAP4 事件关联的文本信息。</p></td>
</tr>
<tr class="odd">
<td><p>context</p></td>
<td><p>该字段不能用于 POP3 和 IMAP4 协议日志记录。</p></td>
</tr>
</tbody>
</table>

