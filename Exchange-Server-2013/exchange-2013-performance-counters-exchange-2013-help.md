---
title: 'Exchange 2013 性能计数器: Exchange 2013 Help'
TOCTitle: Exchange 2013 性能计数器
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63913014
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 性能计数器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-02-06_

## Exchange 2013 性能计数器

下列各节列出了在解决 Exchange 2013 性能问题时您可以使用的有用性能计数器。

## Exchange 域控制器连接计数器

下表显示了可接受的阈值和有关 Exchange 域控制器连接计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>计数器</th>
<th>描述</th>
<th>阈值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchange ADAccess Domain Controllers(*)\LDAP Read Time</p></td>
<td><p>显示将 LDAP 读请求发送至指定域控制器并接收响应的时间（毫秒）。</p></td>
<td><p>平均应该低于 50。峰值（最大值）不应高于 100 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Domain Controllers(*)\LDAP Search Time</p></td>
<td><p>显示发送 LDAP 搜索请求并接收响应的时间（毫秒）。</p></td>
<td><p>平均应该低于 50。峰值（最大值）不应高于 100 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ADAccess Processes(*)\LDAP Read Time</p></td>
<td><p>显示将 LDAP 读请求发送至指定域控制器并接收响应的时间（毫秒）。</p></td>
<td><p>平均应该低于 50。峰值（最大值）不应高于 100 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess Processes(*)\LDAP Search Time</p></td>
<td><p>显示发送 LDAP 搜索请求并接收响应的时间（毫秒）。</p></td>
<td><p>平均应该低于 50。峰值（最大值）不应高于 100 毫秒。</p></td>
</tr>
</tbody>
</table>


## 处理器和进程计数器

下表显示了可接受的阈值以及有关处理器和进程计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>计数器</th>
<th>描述</th>
<th>阈值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processor(_Total)\% Processor Time</p></td>
<td><p>显示处理器执行应用程序或操作系统进程的时间的百分比。这是处理器未处于空闲状态时的情况。</p></td>
<td><p>平均应该少于 75%。</p></td>
</tr>
<tr class="even">
<td><p>Processor(_Total)\% User Time</p></td>
<td><p>显示花在用户模式上的处理器时间的百分比。用户模式是受限制的处理模式，旨在用于应用程序、环境子系统和完整子系统。</p></td>
<td><p>平均应该少于 75%。</p></td>
</tr>
<tr class="odd">
<td><p>Processor(_Total)\% Privileged Time</p></td>
<td><p>显示花在特权模式上的处理器时间的百分比。特权模式是一种处理模式，旨在用于操作系统组件和硬件处理驱动程序。它允许直接访问硬件和所有内存。</p></td>
<td><p>平均应该少于 75%。</p></td>
</tr>
<tr class="even">
<td><p>System\Processor Queue Length（所有实例）</p></td>
<td><p>表示每个处理器所服务的线程数。处理器队列长度可用于确定处理器争用或 CPU 使用率很高是否由处理器处理所分配的工作负荷时容量不足所致。处理器队列长度显示了处理器就绪队列中延迟的线程数以及等待计划执行的线程数。列出的值是进行测量时最后一次观察到的值。</p></td>
<td><p>每个处理器的队列长度不应大于 5。</p></td>
</tr>
<tr class="odd">
<td><p>Process(*)\% Processor Time</p></td>
<td><p>可以用于标识占用 CPU 的特定进程。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## 内存计数器

下表显示了可接受的阈值和有关内存计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>Memory\Available Mbytes</p></td>
<td><p>显示可立即分配给进程或供系统使用的物理内存量 (MB)。它等于分配给备用（已缓存）、可用和零分页列表的内存总和。有关内存管理器的完整解释，请参阅 Microsoft Developer Network (MSDN) 或 Windows Server 2003 资源工具包中的&amp;quot;系统性能和疑难解答指南&amp;quot;。</p></td>
<td><p>应该保持在 RAM 总量的 5% 以上。</p></td>
</tr>
<tr class="odd">
<td><p>Memory\% Committed Bytes In Use</p></td>
<td><p>显示 Memory\Committed Bytes 与 Memory\Commit Limit 的比率。已提交内存是指在需要写入磁盘时已在分页文件中保留空间的使用中的物理内存。提交限制由分页文件的大小确定。如果扩大分页文件，则提交限制会增加，并且该比率会减小。此计数器仅显示当前的百分比值；它不是平均值。</p></td>
<td><p>如果该值大于 80%，则表明系统很可能无法提供更多的内容。</p></td>
</tr>
</tbody>
</table>


## .NET Framework 计数器

下表显示了可接受的阈值和有关 .NET Framework 计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\% Time in GC</p></td>
<td><p>显示进行垃圾收集的时间。当计数器超过阈值时，表示 CPU 正在进行清理，并且不能有效用于加载。向服务器添加内存可以改善这种情况。</p></td>
<td><p>平均起来应该低于 10%。</p></td>
</tr>
<tr class="odd">
<td><p>.NET CLR Exceptions(*)\# of Excepts Thrown / sec</p></td>
<td><p>显示每秒钟抛出的异常数。这包括 .NET Framework 异常和转换为 .NET Framework 异常的非托管异常。例如，非托管代码中的空指针引用异常将在非托管代码中作为 .NET Framework System.NullReferenceException 再次抛出。此指针包含已处理和未处理的异常。</p></td>
<td><p>应小于每秒请求总数 (RPS) (Web Server(_Total)\Connection Attempts/sec * .05) 的 5%。</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR Memory(*)\# Bytes in all Heaps</p></td>
<td><p>显示其他四个计数器的总和：Gen 0 堆大小、Gen 1 堆大小、Gen 2 堆大小以及大型对象堆大小。此计数器表示 GC 堆上当前分配的内存（字节）。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## 网络计数器

下表显示了可接受的阈值和有关通用网络计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>Network Interface(*)\Packets Outbound Errors</p></td>
<td><p>指示由于错误而无法传输的出站数据包数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connection Failures</p></td>
<td><p>显示当前状态为 ESTABLISHED 或 CLOSE-WAIT 的 TCP 连接的数目。可以建立的 TCP 连接数受非页面缓冲池大小的限制。当非页面缓冲池用尽时，将不能建立新的连接。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Connections Reset</p></td>
<td><p>显示 TCP 连接直接从 ESTABLISHED 状态或 CLOSE-WAIT 状态转换为 CLOSED 状态的次数。</p></td>
<td><p>重置的次数增加，或者重置的比率持续增加，都可能表明带宽不足。</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connections Reset</p></td>
<td><p>显示 TCP 连接直接从 ESTABLISHED 状态或 CLOSE-WAIT 状态转换为 CLOSED 状态的次数。</p></td>
<td><p>重置的次数增加，或者重置的比率持续增加，都可能表明带宽不足。</p></td>
</tr>
</tbody>
</table>


## Netlogon 计数器

下表显示了可接受的阈值和有关监控 NTLM 身份验证问题和 MaxConcurrentAPI 问题的通用计数器的信息。有关详细信息，请参阅 Microsoft 知识库文章 2688798 [如何通过使用 MaxConcurrentAPI 设置来进行 NTLM 身份验证的性能调整](https://go.microsoft.com/fwlink/p/?linkid=389728)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore Waiters</p></td>
<td><p>正在等待获取信号的线程数量。</p></td>
<td><p>请参阅 Microsoft 知识库文章 2688798 <a href="https://go.microsoft.com/fwlink/p/?linkid=389728">如何通过使用 MaxConcurrentAPI 设置来进行 NTLM 身份验证的性能调整</a></p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore Holders</p></td>
<td><p>存放信号的线程数量。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore Acquires</p></td>
<td><p>在安全通道连接的整个生命周期或自系统为 _Total 启动以来，获取信号的总次数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore Timeouts</p></td>
<td><p>线程在安全通道连接的整个生命周期或自系统为 _Total 启动以来等待信号期间，线程超时的总次数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Average Semaphore Hold Time</p></td>
<td><p>在上个示例中信号停留的平均时间（秒）。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## 数据库计数器

下表显示了活动日志 I/O 延迟要求计数器及其可接受的阈值。在超出阈值时，客户体验会下降。例如，用户可能会体验到邮件传递延迟或缓慢的系统性能。

> [!NOTE]  
> Exchange 2013 中的普通存储延迟指导与 Exchange 2010 中的指导非常相似。可以在<a href="https://go.microsoft.com/fwlink/p/?linkid=525622">邮箱服务器计数器</a>中找到更多数据库计数器。



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Attached) Average Latency</p></td>
<td><p>显示每个数据库读取操作的平均时间长度（毫秒）。</p></td>
<td><p>平均时间应小于 20 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Attached) Average Latency</p></td>
<td><p>显示每个数据库写入操作的平均时间长度（毫秒）。</p></td>
<td><p>平均时间应小于 50 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Log Writes Average Latency</p></td>
<td><p>显示每个日志写入操作的平均时间长度（毫秒）。</p></td>
<td><p>平均时间应小于 10 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Recovery) Average Latency</p></td>
<td><p>显示每个被动数据库读取操作的平均时间长度（毫秒）。</p></td>
<td><p>平均时间应小于 200 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Recovery) Average Latency</p></td>
<td><p>显示每个被动数据库写入操作的平均时间长度（毫秒）。</p></td>
<td><p>应小于相同实例的读取延迟时间，如 MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Recovery) Average Latency 计数器所测量。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Reads (Attached)/sec</p></td>
<td><p>显示每个附加数据库实例的每秒数据库读取操作数量。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Database Writes (Attached)/sec</p></td>
<td><p>显示每个附加数据库实例的每秒数据库写入操作数量。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Database ==&gt; Instances(*)\I/O Log Writes/sec</p></td>
<td><p>显示每个数据库实例每秒写入的日志数量。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange Active Manager(_total)\Database Mounted</p></td>
<td><p>显示服务器上活动数据库副本的数量。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## ASP.NET

下表显示了可接受的阈值和有关 ASP.NET 计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Application Restarts</p></td>
<td><p>显示在 Web 服务器的生存期期间已重新启动应用程序的次数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Worker Process Restarts</p></td>
<td><p>显示在计算机上已重新启动工作进程的次数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Request Wait Time</p></td>
<td><p>显示队列中最新请求等待的毫秒数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Requests In Application Queue</p></td>
<td><p>显示应用程序请求队列中的请求数。</p></td>
<td><p>应始终为 0。</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET Applications(*)\Requests Executing</p></td>
<td><p>显示当前执行的请求数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET Applications(*)\Requests/Sec</p></td>
<td><p>显示每秒执行的请求数。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## RPC 客户端访问计数器

下表显示可接受的阈值和有关 RPC 客户端访问计数器的信息。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC Averaged Latency</p></td>
<td><p>显示过去 1,024 个数据包的平均延迟（毫秒）。</p></td>
<td><p>应小于 250 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\RPC Requests</p></td>
<td><p>显示 RPC 客户端访问服务当前正处理的客户端请求数。</p></td>
<td><p>不应大于 40。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Active User Count</p></td>
<td><p>显示最近 2 分钟之内进行过某些活动的唯一用户数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Connection Count</p></td>
<td><p>显示所维护的客户端连接总数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC Operations/sec</p></td>
<td><p>显示 RPC 操作发生的速率（每秒）。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\User Count</p></td>
<td><p>显示连接到服务的用户数。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## HTTP 代理计数器

下表显示了有关 HTTP 代理计数器的信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\MailboxServerLocator Average Latency</p></td>
<td><p>显示 MailboxServerLocator Web 服务调用的平均延迟（毫秒）。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Average Authentication Latency</p></td>
<td><p>显示最近 200 个示例中对 CAS 请求进行身份验证所花费的平均时间。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Average ClientAccess Server Processing Latency</p></td>
<td><p>显示最近 200 个请求中 CAS 处理时间（不包括代理所花费时间）的平均延迟（毫秒）。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Mailbox Server Proxy Failure Rate</p></td>
<td><p>显示最近 200 个示例中涉及此客户端访问服务器和 MBX 服务器之间失败的连接百分比。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Outsanding Proxy Requests</p></td>
<td><p>显示并发未处理代理请求的数量。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy(*)\Proxy Requests/Sec</p></td>
<td><p>显示每秒处理的代理请求数。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy(*)\Requests/Sec</p></td>
<td><p>显示每秒处理的请求数。</p></td>
</tr>
</tbody>
</table>


## 信息存储计数器

下表显示了可接受的阈值和有关信息存储计数器的信息。

> [!NOTE]  
> Exchange 2013 中的普通存储延迟指导与 Exchange 2010 中的指导非常相似。可以在<a href="https://go.microsoft.com/fwlink/p/?linkid=525622">邮箱服务器计数器</a>中找到更多信息存储计数器。



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
<td><p>阈值</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 存储库 （*） \RPC 请求</p></td>
<td><p>指示当前在信息存储进程中执行的全部 RPC 请求。</p></td>
<td><p>应始终小于 70。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Client Type(*)\RPC Average Latency</p></td>
<td><p>显示针对某个特定客户端协议，过去 1,024 个数据包的平均服务器 RPC 延迟（毫秒）。</p></td>
<td><p>每个客户端的平均时间应小于 50 毫秒。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Store(*)\RPC Average Latency</p></td>
<td><p>RPC Latency average (msec) 是每个数据库的 RPC 请求的平均延迟（毫秒）。平均延迟通过加载 exrpc32 以来的所有 RPC 计算得出。</p></td>
<td><p>应始终小于 50 毫秒，且峰值小于 100 毫秒。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS Store(*)\RPC Operations/sec</p></td>
<td><p>显示每个数据库实例每秒的 RPC 操作数。</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS Client Type(*)\RPC Operations/sec</p></td>
<td><p>显示每个客户端类型连接每秒的 RPC 操作数。</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


## 客户端访问服务器计数器

下表显示有关客户端连接计数器和 Internet Information Services (IIS) 计数器的信息。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Requests/sec</p></td>
<td><p>显示每秒通过 ASP.NET 从客户端接收到的 HTTP 请求数。确定当前的 Exchange ActiveSync 请求速率。仅用于确定当前用户负载。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Ping Commands Pending</p></td>
<td><p>显示队列中当前挂起的 ping 命令数。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Sync Commands/sec</p></td>
<td><p>显示每秒处理的同步命令数。客户端使用此命令同步文件夹中的项目。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange Availability Service\Availability Requests (sec)</p></td>
<td><p>显示每秒服务的请求数。该请求仅针对于忙/闲信息或包括建议。一个请求可能包含多个邮箱。确定可用性服务请求发生的速率。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Current Unique Users</p></td>
<td><p>显示当前登录到 Outlook Web App 的唯一用户数。此值监视唯一活动用户会话数，以便仅在用户注销或其会话超时后从该计数器将其删除。确定当前用户负载。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Requests/sec</p></td>
<td><p>显示每秒由 Outlook Web App 处理的请求数。确定当前用户负载。</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>显示每秒处理的自动发现服务请求数。确定当前用户负载。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>显示每秒处理的请求数。确定当前用户负载。</p></td>
</tr>
<tr class="even">
<td><p>Web Service(_Total)\Current Connections</p></td>
<td><p>显示当前与 Web 服务建立连接的数量。确定当前用户负载。</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(Default Web Site)\Current Connections</p></td>
<td><p>显示对默认网站建立的当前连接数，此数目对应于命中前端 CAS 服务器角色的连接数。确定当前用户负载。</p></td>
</tr>
<tr class="even">
<td><p>WebService(_Total)\Connection Attempts/sec</p></td>
<td><p>显示尝试连接到 Web 服务的速率。确定当前用户负载。</p></td>
</tr>
<tr class="odd">
<td><p>Web Service(_Total)\Other Request Methods/sec</p></td>
<td><p>显示没有使用 OPTIONS、GET、HEAD、POST、PUT、DELETE、TRACE、MOVE、COPY、MKCOL、PROPFIND、PROPPATCH、SEARCH、LOCK 或 UNLOCK 方法发出 HTTP 请求的速率。确定当前用户负载。</p></td>
</tr>
</tbody>
</table>


## 工作负载管理计数器

下表显示了有关 Exchange 工作负载管理计数器的信息。监视这些计数器非常重要，因为在非高峰期工作负载管理可能在后台运行任务。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>计数器</p></td>
<td><p>描述</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\ActiveTasks</p></td>
<td><p>显示当前工作负载管理在后台运行的活动任务数。</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement Workloads(*)\CompletedTasks</p></td>
<td><p>显示已经完成的工作负载管理任务数。</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement Workloads(*)\QueuedTasks</p></td>
<td><p>显示当前正在排队等待处理的工作负载管理任务数。</p></td>
</tr>
</tbody>
</table>

