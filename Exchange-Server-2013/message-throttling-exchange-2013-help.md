---
title: '邮件限制: Exchange 2013 Help'
TOCTitle: 邮件限制
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50492037
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

*邮件限制*指一组可以由 Microsoft Exchange Server 2013 计算机处理的邮件和连接数量上设置的一组限制。这些限制可以避免无意或有意地造成 Exchange 服务器上的系统资源耗尽。

**目录**

邮件限制作用域

邮件短信和邮件流限制

服务器上的邮件限制

发送连接器上的邮件限制

接收连接器上的邮件限制

邮件限制策略

## 邮件限制作用域

邮件限制包括对邮件处理速率、SMTP 连接速率和 SMTP 会话超时值的各种限制。这些限制共同保护 Exchange 服务器，防止由于接受和交付邮件而导致过度使用。尽管可能会有大量积压的邮件和连接等待处理，但是邮件限制使 Exchange 服务器可以有序地处理这些邮件和连接。

除了邮件限制之外，还可以对邮件的各个组成部分的大小（例如收件人数、邮件标题大小或各个附件的大小）进行限制。有关邮件大小限制的详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

帮助避免 Exchange 传输服务器系统资源过度使用的另一项功能是*回压*。回压是邮箱服务器和边缘传输服务器上的传输服务的系统资源监视功能。当被监视的系统资源（例如硬盘驱动器或内存）的利用率超过指定的阈值时，服务器将降低其接收新连接和新邮件的速率，并集中于传递现有邮件。被监视的系统资源的利用率恢复正常水平后，服务器会慢慢提高接受新连接的速度，然后建立正常的水平。

返回顶部

## 邮件短信和邮件流限制

为了提供更加一致邮件吞吐量以及可预测的邮件传递延迟，Exchange 2013 建立了邮件累积开销。此服务质量 (QoS) 功能被添加到 Microsoft Exchange Server 2010 SP1。这种开销基于以下条件：

  - 邮件大小

  - 收件人数量

  - 传输频率

Exchange 2013 传输服务将跟踪单个用户发送的邮件的平均传递成本。通过使用邮件开销，Exchange 2013 提供了一组设置，可以控制用户或连接对 Exchange 组织的影响。这组设置称为*限制策略*。当用户重复发送高开销邮件（如有大附件的邮件或有许多收件人的邮件）时，基于 Exchange 2013 的传输服务器将使用限制策略向来自用户的高开销邮件分配较低的优先级，同时继续传递开销较低的邮件。这种新的行为为 Exchange 2013 中的邮件限制功能增加了“服务质量”方面。

> [!NOTE]  
> 从用户的角度来看，邮件限制不会影响邮件优先级。邮件仍保留用户设置的原始优先级。例如，邮件保留“重要”或“紧急”等设置。


为了支持这一功能，Exchange 2013 使用了以下机制：

  - **内部优先级代理**   此代理会在发生 **OnResolvedMessage** 事件时触发，并向来自高累积开销发件人的邮件分配一个较低优先级。此开销每分钟测量一次，将影响具有超过 500 个收件人的影响或者大于 1 MB 的邮件。

  - **MapiDelivery 队列类型基于配额的优先级排队**    此机制将使 Exchange 以更高频率传递正常优先级队列中的邮件，而以较低频率传递低优先级队列中的邮件。默认情况下，正常对低邮件比例为 20:1。但是，较低优先级队列中的新邮件在任何情况下都不会早于较高优先级队列中的邮件传递。以下面的情形为例：
    
    1.  已经传递了二十封正常优先级邮件。默认情况下，下一封传递的邮件是一封较低优先级邮件。
    
    2.  传输服务器收到了两封新邮件：一封来自较高优先级队列，另一封来自较低优先级队列。
    
    在这种情形下，将先传递来自较高优先级队列的邮件，然后再传递来自较低优先级队列的邮件。

  - **根据邮件数据库运行状况限制并发连接数**   此机制将监视 Exchange 邮件数据库 (MDB) 的运行状况，并根据指定的运行状况度量值限制到 Exchange 传输服务器的并发连接数。由邮箱服务器上的传输服务中的资源运行状况监控 API 监控 MDB，并分配从 -1 到 100 的运行状况值。该值基于 RPC 性能统计数据，该数据包括在邮箱传输服务中的 Store.exe 进程的每个 RPC 响应。资源运行状况框架使用“请求数/秒”比率性能计数器和“平均 RPC 延迟”性能计数器计算数据库的运行状况值。为了帮助保持一致的交互式用户体验，Exchange 会随运行状况值的降低减少并发连接的数量。以下是可用的运行状况值范围：
    
      - **-1：** 此值指示 MDB 运行状况未知。此值是在数据库启动时指定的。在这种情况下，认为数据库运行正常。
    
      - **0：** 如果数据库处于不正常运行状态，则将指定此值。在此状态下，不应连接数据库。
    
      - **1 至 99：** 这些值表示一种还算正常的状态。值越低表示运行状况越差。
    
      - **100：** 此值表示数据库运行状况正常。

Microsoft Exchange 限制服务为邮件流限制提供框架。Microsoft Exchange 限制服务将记录某个特定用户的邮件流限制设置，并将限制信息缓存在内存中。邮件流限制设置也称为*预算*。重新启动 Microsoft Exchange 限制服务时，也会重置邮件流限制预算。

可以使用 Exchange 2013 中提供的限制策略 cmdlet 为某个限制策略配置单个预算设置。预算是某个特定设置中用户或应用程序可以拥有的访问数量。预算表示用户可以拥有的连接数，或者用户每分钟允许的活动数。例如，可以配置一个预算，设置用户在 Exchange 中可用于特定功能（例如，ActiveSync、Outlook Web App 或 Exchange Web 服务）的时间数。此阈值存储在限制策略中并定义预算。

预算的时间设置是以一分钟的百分比的方式设置的。因此，100% 阈值表示 60 秒。例如，假定需要指定 Outlook Web App 策略设置，将用户可以在客户端访问服务器上运行 Outlook Web App 代码的时间以及用户可以与客户端访问服务器通信的时间设置为每分钟 600 毫秒。为此，需要将以下两个参数的值设置为一分钟（600 毫秒）的 1%：

  - **OWAPercentTimeInCAS**1

  - **OWAPercentTimeInMailboxRPC**1

应用了此策略的用户的 OWAPercentTimeInCAS 预算为 600 毫秒，OWAPercentageTimeInMailboxRPC 预算为 600 毫秒。在这种情况下，当用户登录到 Outlook Web App 中时，可以运行客户端访问代码的时间最多为 600 毫秒。过了 600 毫秒后，将认为连接超过了预算，Exchange 服务器将不允许任何进一步的 Outlook Web App 操作，直到达到预算限制后一分钟。在一分钟之后，用户可以再运行 Outlook Web App 客户端访问代码 600 毫秒。

返回顶部

## 服务器上的邮件限制

可以在下列位置设置邮件限制选项：

  - 传输服务中

  - 发送连接器

  - 接收连接器

您可以使用 Exchange 命令行管理程序设置所有在邮箱服务器上的传输服务、邮箱服务器上的邮箱传输服务或客户端访问服务器上的前端传输服务中可用的邮件限制选项。还可以通过在 Exchange 管理中心 (EAC) 中配置传输服务器属性来设置其中部分选项。

下表显示在传输服务器上可用的邮件限制选项。

### 传输服务器上的邮件限制选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数</th>
<th>默认值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>此参数指定将邮件传递给邮箱时，传输服务可以打开的最大传递线程数。此参数的有效输入范围是 1 到 256。建议您不要修改默认值，除非 Microsoft Customer 服务和支持人员建议您这样做。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>此参数指定从邮箱发送邮件时，传输服务可以打开的最大提交线程数。此参数的有效输入范围是 1 到 256。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>此参数指定允许对传输服务打开连接的最大速率。如果同时有许多连接尝试访问传输服务，<em>MaxConnectionRatePerMinute</em> 参数将限制打开连接的速率，以免服务器的资源负荷过重。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> 或</p>
<p>传输服务器属性</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>此参数指定可以同时打开的最大出站连接数。如果输入值 <code>unlimited</code>，则不限制出站连接数。此参数的值必须大于或等于 <em>MaxPerDomainOutboundConnections</em> 参数的值。</p>
<p>还可使用“服务器” &gt; “服务器” &gt; “属性” &gt; “传输限制” &gt; “出站连接限制”中的 EAC 配置该值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> 或</p>
<p>传输服务器属性</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>此参数指定任何一个域的最大并发连接数。如果输入值 <code>unlimited</code>，则不限制每个域的出站连接数。此参数的值必须大于或等于 <em>MaxOutboundConnections</em> 参数的值。</p>
<p>还可使用“服务器” &gt; “服务器” &gt; “属性” &gt; “传输限制” &gt; “出站连接限制”中的 EAC 配置该值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>此参数指定分拣目录和重播目录每分钟处理的最大邮件数。每个目录都能够以此参数指定的速率独立处理邮件文件。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 发送连接器上的邮件限制

下表显示发送连接器上可用的邮件限制选项。需要使用 Exchange 命令行管理程序配置此选项。

### 发送连接器上的可用邮件限制选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 分钟</p></td>
<td><p>此参数指定在关闭连接之前，已打开的、与目标邮件传递服务器的 SMTP 连接可以保持空闲的最长时间。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 接收连接器上的邮件限制

下表显示在邮箱服务器或边缘传输服务器上的传输服务中配置的接收连接器上可用的邮件限制选项。需要使用 Exchange 命令行管理程序配置这些选项。

### 接收连接器上的可用邮件限制选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>在邮箱服务器上的传输服务 5 分钟</p>
<p>在客户端访问服务器上的前端传输服务 5 分钟。</p>
<p>在边缘传输服务器上 1 分钟。</p></td>
<td><p>此参数指定在关闭连接之前，已打开的、与源邮件传递服务器的 SMTP 连接可以保持空闲的最长时间。该参数的值必须小于 <em>ConnectionTimeout</em> 参数指定的值。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>在邮箱服务器上的传输服务 10 分钟</p>
<p>在客户端访问服务器上的前端传输服务 10 分钟。</p>
<p>在边缘传输服务器上 5 分钟。</p></td>
<td><p>此参数指定与源邮件传递服务器的 SMTP 连接可以保持打开状态的最长时间（即使源邮件传递服务器正在传输数据）。该参数的值必须大于 <em>ConnectionInactivityTimeout</em> 参数指定的值。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>此参数指定此接收连接器允许同时建立的最大入站 SMTP 连接数。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100 % 在邮箱服务器上的传输服务中的默认接收连接器</p>
<p>2 % 在邮箱服务器上的传输服务器、客户端访问服务器上的前端传输服务中的其他接收连接器。</p></td>
<td><p>此参数指定接收连接器允许同时从单个源邮件传递服务器建立的最大 SMTP 连接数。该值以接收连接器上的可用剩余连接百分比表示。接收连接器允许的最大连接数通过 <em>MaxInboundConnection</em> 参数定义。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited 在邮箱服务器上的传输服务中的默认接收连接器</p>
<p>20 在邮箱服务器上的传输服务器、客户端访问服务器上的前端传输服务中的其他接收连接器。</p></td>
<td><p>此参数指定接收连接器允许同时从单个源邮件传递服务器建立的最大 SMTP 连接数。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>此参数指定在接收连接器断开与源邮件传递服务器的连接之前，接收连接器允许出现的最大 SMTP 协议错误数。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 秒</p></td>
<td><p>此参数指定<em>缓送技术</em>中使用的延迟。缓送技术是针对表明存在帐户搜集攻击或其他不受欢迎的邮件的特定 SMTP 通信模式，人为延迟 SMTP 响应的一种方法。<em>帐户搜集攻击</em>尝试从特定组织收集有效的电子邮件地址，作为商业垃圾邮件的目标。</p>
<p><em>TarpitInterval</em> 参数指定的延迟只适用于匿名连接。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件限制策略

在 Exchange 2013 中，每个邮箱都具有 *ThrottlingPolicy* 设置。此设置的默认值为空 (`$null`)。您可以在 **Set-Mailbox** cmdlet 上使用 *ThrottlingPolicy* 参数为邮箱配置限制策略。

对于连接到 Exchange 的用户，可以使用默认限制策略来提供默认的预算配置设置。若要为一个或多个用户配置自定义预算设置，需要创建一个新的限制策略。然后，将该策略应用于相应的用户或组。

> [!IMPORTANT]  
> 建议不要修改默认限制策略。


可以在 Exchange 命令行管理程序中设置邮箱服务器上的所有可用邮件限制选项。以下 cmdlet 可用于管理限制策略：

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

可以使用 **New-ThrottlingPolicy** 和 **Set-ThrottlingPolicy** cmdlet 配置用户可通过特定连接或在特定时间内对 Exchange 执行的活动数量。这些设置形成了用户的预算。可以建立限制策略来控制对以下 Exchange 功能的访问：

  - Exchange ActiveSync

  - Exchange Web 服务 (Exchange Web Services)

  - Outlook Web App

  - 统一消息

  - IMAP4

  - POP3

  - Outlook 客户端连接（MAPI 或 RPC 连接）

  - 邮件流设置

  - PowerShell 命令

  - CPU 使用情况

返回顶部

