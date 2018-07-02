---
title: '信息权限管理日志记录: Exchange 2013 Help'
TOCTitle: 信息权限管理日志记录
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 50491807
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信息权限管理日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

在 Microsoft Exchange Server 2013，IRM 日志中记录信息权限管理 (IRM) 操作。IRM 日志可帮助您监视并排除权限管理服务 (RMS) 客户端在Exchange 2013服务器上的与您的组织中Active Directory权限管理服务 (AD RMS) 群集之间的交互。

要了解 IRM，请参阅[信息权限管理](information-rights-management-exchange-2013-help.md)。

**目录**

Structure of IRM logs

Logging process

Information written to IRM logs

Managing IRM logs

要了解与 IRM 相关的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## IRM 日志的结构

默认情况下，IRM 日志位于 C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs 中。

IRM 日志文件的命名约定为 \<*进程*\>\_\<*进程标识符* 或 *IIS 应用程序池标识符*\>\_IRMLOG*yyyymmdd*-*nnnn*.log，其中：

  - \<*Process*\>= 日志文件创建的进程。例如，在传输服务，这将是 EdgeTransport。

  - \<*进程标识符*或 *IIS 应用程序池标识符\>* =进程的数字 ID。

  - *yyyymmdd* = 创建日志文件时的协调世界时 (UTC) 日期。

  - *nnnn* = 实例编号，每天从 1 开始。

IRM 日志文件名的一个示例为 EdgeTransport\_1056\_IRMLOG20101201-1.log。

下表显示在不同服务器角色上生成的日志。

### 服务器角色上的日志

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器角色</th>
<th>IRM 日志文件名</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>传输服务</p></td>
<td><p>EdgeTransport_&lt;<em>进程标识符</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此日志用来记录所有的 RMS 事务通过传输管道运输服务 （例如，传输保护规则和日志报告解密） 上进行。Edgetransport.exe 进程的进程标识符 (PID) 用于生成日志文件名。</p></td>
</tr>
<tr class="even">
<td><p>邮箱</p></td>
<td><p>msftefd_&lt;<em>进程标识符</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此日志用于记录在搜索和索引请求过程中发生的所有 RMS 事务。Exchange 2013邮箱服务器使用 msftefd.exe 过程的内容索引。Msftefd.exe 过程的 PID 用于生成日志文件名。</p></td>
</tr>
<tr class="odd">
<td><p>客户端访问</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>此日志用于记录 IRM 在 Microsoft OfficeOutlook Web App 中的所有事务。</p></td>
</tr>
<tr class="even">
<td><p>所有 Exchange 2013 服务器角色</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>发出 <strong>Test-IRMConfiguration</strong> cmdlet 时，此日志用于记录从 Windows PowerShell 发出的所有 IRM RMS 事务。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 日志记录进程

信息写入到日志文件中，直到文件大小达到其最大的指定的值。达到最大大小后，将创建具有增量的实例编号日志文件。在一天重复此过程。IRM 日志目录大小达到其最大指定或日志文件中的 IRM 日志记录配置每台服务器上指定的最长期限时，循环日志记录将删除最旧的日志文件。

返回顶部

## 写入 IRM 日志的信息

IRM 日志文件是文本文件，包含以逗号分隔值 (CSV) 格式的数据。每个 IRM 日志包含标头包含以下信息 ︰

  - **\#Software**  创建 IRM 日志文件的软件名称。通常情况下，值为`Microsoft Exchange Server`。

  - **\#Version** 创建 IRM 日志文件的软件的版本号。

  - **\#Log-type** 日志类型值，为 `Rms Client Manager Log`。

  - **\#Date**  UTC 日期和时间创建日志文件时。UTC 日期和时间表示的 ISO 8601 日期时间格式 ︰ *yyyy*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z，其中 ︰
    
      - yyyy = 年
    
      - *mm* = 月
    
      - *dd* = 日
    
      - T = 用于显示开始时间部分的时间指示符
    
      - *hh* = 小时
    
      - *mm* = 分钟
    
      - *ss* = 秒
    
      - *fff* = 秒的小数部分
    
      - Z = Zulu，是 UTC 的另一种表示方式

  - **\#Fields** IRM 日志文件中使用的逗号分隔字段名。
    
    IRM 日志存储在单独的一行，组织以逗号分隔的字段在 RMS 事务的每个事件。下表列出所有 IRM 功能已启用的服务器角色的 IRM 日志中的字段。
    
    ### IRM 日志中使用的字段
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>字段</th>
    <th>描述</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>列出 UTC 时间戳。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>列出使用 RMS 客户端功能。有效值包括 ︰</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>Signature verification</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>列出的事件类型。有效值包括 ︰</p>
    <ul>
    <li><p><code>Acquire</code> 请求 RMS 许可证或模板。</p></li>
    <li><p><code>Success</code> 成功获取了 RMS 许可证或模板。</p></li>
    <li><p><code>Exception</code> 发生了错误。</p></li>
    <li><p><code>Queued</code> 请求挂起。</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>保留供 Microsoft 内部使用。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>列出操作过程中访问的 RMS 服务器 URL。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>调用进程被用来将多个 RMS 事务联系在一起。有效值包括 ︰</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>标识唯一的交易记录。在一个事务期间发生的所有事件都具有相同的事务 id。</p></td>
    </tr>
    </tbody>
    </table>


返回顶部

## 管理 IRM 日志

在每个服务器角色启用 IRM 功能，默认情况下启用 IRM 记录。对于每个服务器角色，可以通过使用该服务器角色的相应**Set** cmdlet 修改下面的 IRM 日志配置。例如，若要配置 IRM 的邮箱服务器上的记录，您可以使用**Set-MailboxServer** cmdlet。

### IRM 日志的配置参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>启用 IRM 的交易记录的记录。默认情况下启用 IRM 记录。若要禁用 IRM 服务器角色的日志记录，请将参数设置为<code>$false</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>指定 IRM 日志文件的最长期限。删除早于指定存在时间的文件。默认值是<code>30.00:00:00</code> （30 天）。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>连接日志目录中指定所有 IRM 日志最大的大小。当一个目录达到最大文件大小时，服务器将首先删除最旧的日志文件。默认值是<code>250 MB</code>。</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>指定一个日志文件的最大文件大小。当文件达到指定的大小时，将创建日志文件，和实例编号就会增加。默认值是<code>10 MB</code>。</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>指定 IRM 日志的位置。默认路径为 %ExchangeInstallPath%Logging\IRMLogs。</p></td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅下列主题：

  - [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/zh-cn/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/zh-cn/library/jj215682\(v=exchg.150\))

返回顶部

