---
title: '队列: Exchange 2013 Help'
TOCTitle: 队列
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51408287
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 队列

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

“队列”是等待进入下一个处理阶段或传递到目标的邮件的临时存放位置。每个队列代表 Exchange 服务器按照特定顺序处理的逻辑邮件集。在 Microsoft Exchange Server 2013 中，队列存放传递前、传递中和传递后的邮件。队列存在于邮箱服务器和边缘服务器上。在本主题中，邮箱服务器和边缘服务器统称为“传输服务器”。

与先前的 Exchange 版本一样，Exchange 2013 使用单个可扩展存储引擎 (ESE) 数据库存储队列。

您可以使用 Exchange 工具箱里的 Exchange 命令行管理程序和队列查看器管理队列和队列中的邮件。可以使用这些界面来查看队列的状态和内容以及详细的邮件属性。还可以使用这些界面来执行修改队列或队列中的邮件的操作。

**目录**

  - 队列类型

  - 队列数据库文件

  - 队列属性
    
      - NextHopSolutionKey
    
      - 传入率、传出率和速度
    
      - 队列状态
    
      - 其他队列属性

  - 邮件属性
    
      - 邮件状态
    
      - 其他邮件属性

  - 管理队列和队列中的邮件

## 队列类型

Exchange 2013 中使用下列队列类型：

  - **永久性队列**   “永久性队列”是存在于每个 Exchange 组织中每个传输服务器上的队列。与先前的 Exchange 版本一样，在 Exchange 2013 中有三个永久性队列：
    
      - **提交队列**   分类程序在收集必须通过传输服务器上的传输代理解析、路由和处理的所有邮件时所使用的提交队列。传输服务器接收的所有邮件进入提交队列进行处理。在邮箱服务器上，通过接收连接器、拾取或重播目录或邮箱传输提交服务提交邮件。在边缘传输服务器上，通常通过接收连接器提交邮件，但也可以使用拾取目录和重播目录提交。
        
        分类程序从此队列中检索邮件，并确定收件人的位置以及到达该位置的路由。邮件在进行分类之后，会移动到传递队列或无法到达队列。每台传输服务器只有一个提交队列。提交队列中的邮件不能同时处于其他队列中。有关分类程序和传输管道的详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。
    
      - **无法到达队列**   无法到达队列包含无法路由到目标地址的邮件。通常，修改了用于传递的路由路径的配置更改会导致无法到达目标地址。无论目标地址是什么，无法到达收件人的所有邮件均驻留在此队列中。每台传输服务器只有一个无法到达队列。
        
        在检测到路由更改后，无法到达队列中的邮件就会自动重新提交。因此，修复导致邮件进入无法到达队列的错误条件或错误配置之后，无需额外执行将邮件移出无法到达队列以进行传递的操作。
        
        无法到达队列通常为空。如果无法到达队列不包含任何邮件，则邮件也不会在队列查看器或 **Get-Queue** 结果中出现。
    
      - **病毒邮件队列**   病毒邮件队列是一种特殊队列，用于隔离在传输服务器或服务出现故障之后确定对 Exchange 2013 系统有害的邮件。可能这些邮件的内容和格式确实存在问题，也可能是因为代理编写不当，导致 Exchange 服务器在处理这些疑似病毒邮件时发生故障，从而将这些邮件视为了病毒邮件。
        
        病毒邮件队列通常为空。如果病毒邮件队列不包含任何邮件，则邮件也不会在队列查看器或 **Get-Queue** 结果中出现。病毒邮件队列中的邮件绝不会自动恢复或过期。邮件将保留在病毒邮件队列中，直到管理员手动恢复或删除它们为止。

  - **传递队列**   传递队列保留通过使用 SMTP 传递到任何本地或远程目标的邮件。所有邮件通过使用 SMTP 在 Exchange 服务器间传输。如果由传递代理连接器为目标服务，那么非 SMTP 目标也使用传递队列。. 每个传递队列包含正在被路由到相同目标的邮件。实际上，多个传递队列存在于一个传输服务器上是不可避免的。当传递队列为空且过期时间已过，要求删除和自动删除传递队列时，则会动态创建传递队列。队列过期时间由 **Set-TransportService** cmdlet 上的 *QueueMaxIdleTime* 参数控制。默认值为 3 分钟。

  - **卷影队列**   卷影队列在邮件传输时会保留邮件的冗余副本。有关详细信息，请参阅[卷影冗余](shadow-redundancy-exchange-2013-help.md)。

  - **Safety Net**   Safety Net 保留传输服务器成功传递的邮件备份。尽管队列管理工具无法访问 Safety Net，但是 Safety Net 只是队列数据库里的另一个队列。有关详细信息，请参阅[Safety Net](safety-net-exchange-2013-help.md)。

返回顶部

## 队列数据库文件

所有不同的队列都存储在一个 ESE 数据库中。默认情况下，这个队列数据库位于 `%ExchangeInstallPath%TransportRoles\data\Queue` 中的传输服务器上。

与任何 ESE 数据库一样，队列数据库使用日志文件接受、跟踪和维护数据。为了提高性能，先将所有的邮件事务写入日志文件和内存中，然后再写入数据库文件中。检查点文件会跟踪已提交给数据库的事务日志条目。在 Microsoft Exchange 传输服务的日常关闭期间，在事务日志中找到的对未提交数据库所做的更改始终提交给数据库。

队列数据库使用循环日志记录。这表示将不会维护在事务日志中发现的已提交事务的历史记录。系统将立即自动删除任何早于当前检查点的事务日志。因此，在执行队列数据库恢复时，不能从备份重播事务日志。

Exchange 2013 使用“生成表格”存储和清理队列数据库中的邮件。队列数据库不是从一个大表中处理和删除单个邮件记录，而是在基于时间的表格中存储邮件，而且仅在成功处理表中的所有邮件之后，删除整个表。例如，从下午 1:00 到下午 2:00 排列的所有邮件不论队列或目标，都存储在 `1p-2p_msgs` 表中。下午 2:00 的新邮件会存储在 `2p-3p_msgs` 表中。下午 4:00，会创建一个名为 `4p-5p_msgs` 的新表，并删除整个 `1p-2p_msgs` 表，但是前提是已成功处理了表中的所有邮件。删除整个邮件表格而不是删除单个邮件的方法有助于提高保留队列数据库的驱动器的 I/O 性能。

下表列出了构成队列数据库的文件。

### 构成队列数据库的文件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>此队列数据库文件存储所有排队的邮件。</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>此临时数据库文件用于验证启动时的队列数据库架构。</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>该事务日志用于记录队列数据库的所有更改。数据库的更改首先写入事务日志，然后提交到数据库。Trn.log 是当前的活动事务日志文件。Trntmp.log 是提前创建接下来提供的事务日志文件。如果现有 Trn.log 事务日志文件达到其最大大小，则 Trn.log 将重命名为 Trn<em>nnnn</em>.log，其中 <em>nnnn</em> 是序列号。然后，Trntmp.log 重命名为 Trn.log，并用作当前的活动事务日志文件。</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>此检查点文件会跟踪已提交给数据库的事务日志条目。该文件始终在与 mail.que 文件相同的位置中。</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>这些保留事务日志文件将用作占位文件。仅当包含事务日志的硬盘空间已满，使队列数据库完全停止时，才能使用它们。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 用于配置队列数据库的选项

通过添加或更改 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 应用程序配置文件中的项来配置队列数据库。此文件与 Microsoft Exchange 传输服务相关联。在重启 Microsoft Exchange 传输服务后，对 EdgeTransport.exe.config 文件做出的改动才会生效。

您可以在 EdgeTransport.exe.config 文件的 `<appSettings>` 部分中添加新项或修改现有项。如果不存在指定的项，您可以手动添加再更改其值。

下表描述了 EdgeTransport.exe.config 文件中可用的队列数据库的项。

### EdgeTransport.exe.config 文件中可用的邮件队列数据库项

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>项</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>此项指定在执行之前可以组合到一起的数据库 I/O 操作的数量。默认情况下，EdgeTransport.exe.config 文件中不存在此项。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>此项指定在数据库执行多个数据库 I/O 操作之前将等待它们进行组合的最长时间（毫秒）。如果以下条件为真，则执行数据库 I/O 操作，而不再进行任何等待：</p>
<ul>
<li><p>还没有达到 <em>QueueDatabaseBatchSize</em> 项所指定的数据库 I/O 操作的数量。</p></li>
<li><p>已超过 <em>QueueDatabaseBatchTimeout</em> 项所指定的时间。</p></li>
</ul>
<p>默认情况下，EdgeTransport.exe.config 文件中不存在此项。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>此项指定可以打开的 ESE 数据库连接数。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>此项指定在将事务记录写入到事务日志文件之前用于缓存它们的内存。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>此项指定事务日志文件的最大大小。当达到最大日志文件大小时，将打开新日志文件。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>此项指定队列数据库日志文件的默认目录。有关如何更改队列数据库位置的说明，请参阅<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">更改队列数据库的位置</a>。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>此项指定可以随时排入数据库引擎线程池中的后台清理工作项目的最大数量。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>此项启用或禁用邮件队列数据库的已安排联机碎片整理。默认情况下，EdgeTransport.exe.config 文件中不存在此项。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> 或凌晨 1:00。</p></td>
<td><p>此项指定一天中开始邮件队列数据库的联机碎片整理的时间（以 24 小时格式表示）。若要指定值，请输入一个值作为时间：<em>hh:mm:ss</em>，其中 <em>h</em> = 小时，<em>m</em> = 分钟，<em>s</em> = 秒。</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> 或 3 小时</p></td>
<td><p>此项指定允许联机整理碎片任务运行的时间。即使整理碎片任务未在指定的时间内完成，队列数据库仍将处于一致的状态。若要指定值，请输入一个时间跨度：<em>hh:mm:ss</em>，其中 <em>h</em> = 小时，<em>m</em> = 分钟，<em>s</em> = 秒。</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>此项指定队列数据库文件的默认目录。有关如何更改队列数据库位置的说明，请参阅<a href="change-the-location-of-the-queue-database-exchange-2013-help.md">更改队列数据库的位置</a>。</p></td>
</tr>
</tbody>
</table>


> [!NOTE]  
> 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。


返回顶部

## 队列属性

队列有许多描述队列目的和状态的属性。一些队列属性可应用到创建的队列中，且不能对其更改。其他属性包括经常更新的状态大小、时间或其他指示器。

返回顶部

## NextHopSolutionKey

Microsoft Exchange 传输服务中分类程序的路由组件选择邮件的目标，并且此目标用于创建传递队列。每个收件人都标有目标，作为 **NextHopSolutionKey** 属性。**NextHopSolutionKey** 属性的每个唯一值对应于单独的传递队列。

**NextHopSolutionKey** 属性包含以下字段：

  - **DeliveryType**   此字段的值表示邮件分类的结果，和传输服务如何将邮件传输到下一个跃点，该跃点可能是邮件的最终目标，也可能是传输过程中的中间跃点。传输服务使用预定义值列表来决定基于目标路由目标或传递组的 **DeliveryType**。

  - **NextHopDomain**   此字段使用基于 **DeliveryType** 字段的指定值。对于传递队列，字段的值实际上就是队列的名称。而 **NextHopDomain** 的值不总是域名。例如，此值可能是目标 Active Directory 站点的名称，也可能是数据库可用性组 (DAG) 的名称。将此字段视作下一个跃点名称，其值为路由目标的名称或目标传递组的名称。

  - **NextHopConnector**   此字段使用基于 **DeliveryType** 字段值的指定值。此值通常表述为 GUID。如果未使用此字段，那么其值是均为零的 GUID。**NextHopConnector** 的值不总是连接器的 GUID。例如，此值可能是目标 Active Directory 站点或 DAG 的 GUID。将此字段视作下一个跃点 GUID，其值为路由目标的 GUID 或目标传递组的 GUID。

Exchange 2013 也将 **NextHopCategory** 属性添加到基于 **DeliveryType** 值的队列中。**NextHopCategory** 的值为 `External` 或 `Internal`。`External` 值表示队列的下一个跃点在 Exchange 组织之外。`Internal` 值表示队列的下一个跃点在 Exchange 组织之内。请注意，外部收件人的邮件在外部传递之前可能需要一个或多个内部跃点。

**DeliveryType**、**NextHopCategory**、**NextHopDomain** 和 **NextHopConnector** 的值都在下表中说明。


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>队列查看器中的传递类型</th>
<th>命令行管理程序中的 DeliveryType</th>
<th>描述</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>传递代理</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>队列会保留传递到非 SMTP 地址空间中收件人的邮件。通过使用本地服务器上配置的传递代理连接器来传递邮件。</p></td>
<td><p>External</p></td>
<td><p>此值为在传递代理连接器上配置的目标地址空间。</p></td>
<td><p>此值为传递代理连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>队列会保留传递到 SMTP 地址空间中收件人的邮件。通过使用本地服务器上配置的发送连接器来传递邮件。配置发送连接器以使用 DNS 路由。</p></td>
<td><p>External</p></td>
<td><p>此值为在发送连接器上配置的目标地址空间。例如，<code>contoso.com</code>。</p></td>
<td><p>此值为发送连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>队列会保留传递到非 SMTP 地址空间中收件人的邮件。通过使用本地服务器上配置的外部连接器来传递邮件。</p></td>
<td><p>External</p></td>
<td><p>此值为在外部连接器上配置的目标地址空间。</p></td>
<td><p>此值为外部连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>队列会保留传递到 SMTP 地址空间中收件人的邮件。通过使用本地服务器上配置的发送连接器来传递邮件。配置发送连接器以使用智能主机路由。</p></td>
<td><p>External</p></td>
<td><p>此值为在发送连接器上配置的智能主机列表。智能主机可配置为 FQDN 和/或 IP 地址。值可以是下列之一：</p>
<ul>
<li><p><strong>FQDN</strong>   语法是 <code>&lt;FQDN1,FQDN2,...&gt;</code>。例如，<code>smarthost01.contoso.com</code> 或 <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>。</p></li>
<li><p><strong>IP 地址</strong>   语法是 <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>。例如，<code>[10.10.10.100]</code> 或 <code>[10.10.10.100],[10.10.10.101]</code>。</p></li>
<li><p><strong>FQDN 和 IP 地址</strong>   语法是 <code>&lt;[IPAddress1],FQDN1,...&gt;</code>，并取决于智能主机如何在发送连接器上显示。例如，<code>[172.17.17.7],relay.tailspintoys.com</code> 或 <code>mail.contoso.com,[192.168.1.50]</code>。</p></li>
</ul></td>
<td><p>此值为发送连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP 传递到邮箱</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>队列会保留传递到 Exchange 2013 邮箱收件人的邮件。目标邮箱数据库位于下列位置之一：</p>
<ul>
<li><p>本地 Exchange 2013 邮箱服务器。</p></li>
<li><p>同一个 DAG 中的 Exchange 2013 邮箱服务器。</p></li>
<li><p>非 DAG 环境中同一个 Active Directory 站点中的 Exchange 2013 邮箱服务器。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>此值为目标邮箱数据库的名称。例如，<code>Mailbox Database 0471695037</code>。</p></td>
<td><p>此值为目标邮箱数据库的 GUID。例如，<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP 中继到发送连接器源服务器</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>队列会保留传递到 SMTP 或非 SMTP 收件人的邮件。通过使用在远程传输服务器上配置的发送连接器、传递代理连接器或外部连接器传递邮件。远程传输服务器可能是 Exchange 2013 邮箱服务器，也可能是 Exchange 先前版本的 Exchange 2007 或 Exchange 2010 集线器传输服务器。远程服务器可能位于本地 Active Directory 站点，也可能位于远程 Active Directory 站点。</p></td>
<td><p>Internal</p></td>
<td><p>此值为目标发送连接器、传递代理连接器或外部连接器的名称。例如，<code>Contoso.com Send Connector</code>。</p></td>
<td><p>此值为目标发送连接器、传递代理连接器或外部连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP 中继到数据库可用性组</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>队列会保留传递到 Exchange 2013 邮箱收件人的邮件，其中目标邮箱数据库位于远程 DAG 中。远程 DAG 可能位于本地 Active Directory 站点，也可能位于远程 Active Directory 站点。</p></td>
<td><p>Internal</p></td>
<td><p>此值为目标 DAG 的名称。例如，<code>DAG1</code>。</p></td>
<td><p>此值为目标 DAG 的 GUID。例如，<code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP 中继到邮箱传递组</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>此队列会保留传递到旧版邮箱收件人的邮件，其中目标邮箱位于 Exchange 2007 或 Exchange 2010 邮箱服务器上。邮件与正在运行同一版本的 Exchange 的集线器传输服务器（作为目标邮箱）有关。目标集线器传输服务器可能位于本地 Active Directory 站点，也可能位于远程 Active Directory 站点。</p></td>
<td><p>Internal</p></td>
<td><p>队列名称使用以下语法：<code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>，其中 <em>&lt;ADSiteName&gt;</em> 为目标 Active Directory 站点的名称，<em>&lt;ExchangeVersion&gt;</em> 为邮箱服务器上的 Exchange 版本。</p></td>
<td><p>此值为空。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SMTP 中继到远程 Active Directory 站点</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>队列会保留传递到远程目标的邮件，并且路由拓扑需要通过指定的 Active Directory 站点路由邮件。此站点是通往最终目标的中间跃点。在以下环境情况下会出现此情况：</p>
<ul>
<li><p>需要通过集线器站点来路由邮件。</p></li>
<li><p>需要通过远程 Active Directory 站点订阅的边缘传输服务器上配置的发送连接器来传递邮件。</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>此值为目标 Active Directory 站点的名称。例如，<code>NorthAmericanSite</code>。</p></td>
<td><p>此值为目标 Active Directory 站点的 GUID。例如，<code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP 中继到指定的 Exchange 服务器</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>队列会保留传递到为指定展开服务器配置的通讯组的邮件。扩展可能是一个 Exchange 2013 邮箱服务器，也可能是 Exchange 2007 或 Exchange 2010 集线器传输服务器。服务器可能位于本地 Active Directory 站点，也可能位于远程 Active Directory 站点。</p></td>
<td><p>Internal</p></td>
<td><p>此值为目标展开服务器的 FQDN。例如，<code>mailbox01.contoso.com</code>。</p></td>
<td><p>此值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Active Directory 站点中的 SMTP 中继到边缘传输服务器</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>队列会保留传递到 SMTP 地址空间的邮件。通过使用本地 Active Directory 站点订阅的边缘传输服务器上配置的发送连接器来传递邮件。</p></td>
<td><p>Internal</p></td>
<td><p>此值为将出站 Internet 邮件从组织发送到 Internet 的发送连接器的名称。边缘订阅会自动创建发送连接器，并命名为 <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>。<em>&lt;ADSiteName&gt;</em> 是本地 Active Directory 站点订阅的边缘传输服务器的名称。</p></td>
<td><p>此值为发送连接器的 GUID。例如，<code>4520e633-d83d-411a-bbe4-6a84648674ee</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>此值保留供 Microsoft 内部使用。有关检测信号的详细信息，请参阅<a href="shadow-redundancy-exchange-2013-help.md">卷影冗余</a>。</p></td>
<td><p>无</p></td>
<td><p>不适用</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p><strong>卷影冗余</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>队列会保留卷影队列中的邮件。卷影队列保留传输中邮件的冗余副本以防主邮件没有成功传递。有关详细信息，请参阅<a href="shadow-redundancy-exchange-2013-help.md">卷影冗余</a>。</p></td>
<td><p>Internal</p></td>
<td><p>此值为让卷影队列保留主邮件冗余副本的主服务器的 FQDN。例如，<code>mailbox01.contoso.com</code>。</p></td>
<td><p>此值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>此值只用于提交队列和病毒邮件队列。</p></td>
<td><p>Internal</p></td>
<td><p>对于提交队列，此值为 <code>Submisssion</code>。对于病毒邮件队列，此值为 <code>Poison Message</code>。</p></td>
<td><p>此值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
<tr class="odd">
<td><p><strong>无法到达</strong></p></td>
<td><p><strong>Unreachable</strong></p></td>
<td><p>此值只用于无法到达队列。</p></td>
<td><p>Internal</p></td>
<td><p>此值是 <code>Unreachable Domain</code>。</p></td>
<td><p>此值是 <code>00000000-0000-0000-0000-000000000000</code>。</p></td>
</tr>
</tbody>
</table>


请注意，Exchange 2013 支持 **DeliveryType** 的旧值以向后兼容 Exchange 的先前版本。这些值可在队列查看器和命令行管理程序中使用，但是不能用于 Exchange 2013。这些旧的 **DeliveryType** 值为：

  - **MapiDelivery**   队列保留由 Exchange 2007 或 Exchange 2010 集线器传输服务器传递到本地 Active Directory 站点的 Exchange 2007 或 Exchange 2010 邮箱服务器上邮箱的邮件。

  - **SmtpRelayWithinAdSite**   队列保留由 Exchange 2007 或 Exchange 2010 集线器传输服务器传递到同一个 Active Directory 站点中另一个集线器传输服务器的邮件。目标集线器传输服务器可以是连接器或通讯组展开服务器的源服务器。

  - **SmtpRelaytoTiRg**   队列保留由 Exchange 2007 或 Exchange 2010 集线器传输服务器传递到 Exchange Server 2003 路由组的邮件。目标服务器可以是连接器、通讯组展开服务器或 Exchange 2003 桥头服务器的源服务器。

返回顶部

## 传入率、传出率和速度

Exchange 2013 测量邮件进入和离开队列的速率并将这些值存储在队列属性中。您可以使用这些速率作为队列和传输服务器运行状况的指示器。队列属性为：

  - **传入率**   此属性为邮件进入队列的速率。
    
    此值通过最后 60 秒内平均每 5 秒进入队列的邮件数量计算得出。这个公式可以表述为 `(i1+i2+i3+i4+i5+i6)/6`，其中 i*n* = 5 秒内传入邮件的数量。

  - **传出率**   此属性为邮件离开队列的速率。
    
    此值通过最后 60 秒内平均每 5 秒离开队列的邮件数量计算得出。这个公式可以表述为 `(o1+o2+o3+o4+o5+o6)/6`，其中 o*n* = 5 秒内传出邮件的数量。

  - **速率**   此属性为队列的消耗率，通过 **OutgoingRate** 的值减去 **IncomingRate** 的值计算得出。
    
    如果 **Velocity** 的值大于 0，那么邮件离开队列的速度大于邮件进入队列的速度。
    
    如果 **Velocity** 的值等于 0，那么邮件离开队列的速度等于邮件进入队列的速度。当队列不活动时，也会看到值。
    
    如果 **Velocity** 的值小于 0，那么邮件进入队列的速度大于邮件离开队列的速度。

在基本级别，**Velocity** 的正值表示有效消耗的是一个正常的队列，**Velocity** 的负值表示队列没有有效消耗。但是您也需考虑 **IncomingRate**、**OutgoingRate** 和 **MessageCount** 属性的值，还有队列的 **Velocity** 值的度量值。例如，一个队列的 **Velocity** 值为大负值、**MessageCount** 值大、**OutgoingRate** 值小、**IncominRate** 值大，则精确显示了此队列没有正常消耗。但是，如果一个队列的 **Velocity** 值为接近零的负值，而且 **IncomingRate** 值、**OutgoingRate** 值和 **MessageCount** 值都非常小，则不表示此队列有问题。

返回顶部

## 队列状态

队列的当前状态存储在队列的 **Status** 属性中。队列可以使用下列状态值之一：

  - **活动**   此队列正在主动传输邮件。

  - **连接**   此队列处于连接到下一个跃点的过程中。

  - **就绪**   此队列最近传输的邮件，但是队列现在是空的。

  - **重试**   最后一次自动或手动连接尝试失败，队列正等待重试连接。

  - **挂起**   此队列已经被管理员手动挂起以禁止邮件传递。新邮件可以进入队列，正在传输到下一个跃点的邮件将会结束传递并离开队列。否则，要等到管理员手动恢复了队列后，邮件才能离开队列。请注意，挂起队列并不改变队列中单个邮件的状态。
    
    可以挂起状态为“活动”或“重试”的队列。也可以挂起“无法到达”队列和“提交”队列。
    
    如果挂起“无法到达”队列，当检测到配置更新后，邮件不会自动地重新提交到分类程序中。若要自动重新提交这些邮件，需要手动恢复无法到达队列。如果挂起“提交”队列，则在恢复队列之前，分类程序不会选取邮件。

返回顶部

## 其他队列属性

还有一些其他一目了然的队列属性。最常使用的作为筛选器选项的队列属性。通过指定筛选条件，可以快速找到队列并对队列执行操作。有关可筛选队列属性的完整说明，请参阅[队列筛选器](queue-filters-exchange-2013-help.md)。

在此还值得一提的队列的重要属性就是 **MessageCount** 属性，它显示了一个队列中的邮件数量。这是队列运行状况的一个重要指示器。例如，一个包含持续增加从不减少的大量邮件的传递队列可能表示需要关注路由或传输管道问题。

返回顶部

## 邮件属性

队列中的邮件有许多属性。许多属性都反映了用于创建邮件的信息。一些邮件状态和信息属性受到队列相应属性的严重影响。但是，单封邮件可能与队列的相应属性的值不同。其他属性包括经常更新的状态、时间或其他指示器。

返回顶部

## 邮件状态

邮件的当前状态存储在邮件的 **Status** 属性中。邮件可以具有下列状态值之一：

  - **活动**   如果邮件在传递队列中，则此邮件正准备传递到目标。如果邮件在提交队列中，则此邮件正在由分类程序进行处理。

  - **锁定**   此值保留为 Microsoft 内部所用，并且在内部部署 Exchange 组织中不可用。

  - **暂停删除**   邮件虽被管理员删除，但已在传输到下一跃点的行动中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被删除。否则，邮件传递将继续进行。

  - **暂停挂起**   邮件虽被管理员挂起，但已在传输到下一跃点的行动中。如果邮件传递出现错误，从而导致此邮件重新进入队列，则该邮件将被挂起。否则，邮件传递将继续进行。

  - **就绪**   邮件正在队列中等待进行处理。

  - **重试**   最后一次尝试自动或手动连接邮件所在队列失败。邮件正在等待下一次队列自动连接重试。

  - **挂起**   邮件由管理员手动挂起。病毒邮件队列中的所有邮件都处于永久挂起状态。

返回顶部

## 其他邮件属性

还有一些其他一目了然的邮件属性。最常使用的作为筛选器选项的邮件属性。通过指定筛选条件，可以迅速找到邮件并对其执行操作。有关可筛选邮件属性的完整说明，请参阅[邮件筛选器](message-filters-exchange-2013-help.md)。

返回顶部

## 管理队列和队列中的邮件

队列查看器和实际上所有队列和邮件管理 cmdlet 都受制于单个 Exchange 服务器。您可以查看或操作单个或多个队列或邮件，但是只能在一个指定的服务器上进行。

Exchange 2013 介绍了 **Get-QueueDigest** cmdlet，它在指定范围内提供了一个高级别、聚合的视图以查看所有服务器上的队列状态，例如，DAG、Active Directory 站点、服务器列表或整个 Active Directory 林。请注意，外围网络中已订阅的边缘传输服务器上的队列不包括在结果中。此外，**Get-QueueDigest** 在边缘传输服务器中可用，但结果仅限于边缘传输服务器上的队列。

> [!NOTE]  
> 默认情况下，<strong>Get-QueueDigest</strong> cmdlet 显示包含 10 封或更多邮件的传递队列，而且结果每一到两分钟更新一次。有关如何更改这些默认值的说明，请参阅 <a href="configure-get-queuedigest-exchange-2013-help.md">配置 Get-QueueDigest</a>。


下表说明了可以对队列或队列中的邮件执行的管理任务。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>任务</th>
<th>描述</th>
<th>使用工具</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在服务器上查看和筛选队列</p></td>
<td><p>此操作会在传输服务器上显示出一个或多个队列。您可以使用结果来对队列进行操作。</p></td>
<td><p>队列查看器或 <strong>Get-Queue</strong> cmdlet。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="even">
<td><p>查看并筛选特定 DAG 中的特定服务器、特定 Active Directory 站点上或整个 Active Directory 林中的队列。</p></td>
<td><p>此操作显示了定义范围内（服务器、DAG、Active Directory 站点或整个 Active Directory 林）队列的摘要视图。</p></td>
<td><p>仅 <strong>Get-QueueDigest</strong> cmdlet</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="odd">
<td><p>挂起队列</p></td>
<td><p>此操作暂时禁止传递当前队列中的邮件。队列继续接受新邮件，但是任何邮件都不会离开队列。</p></td>
<td><p>队列查看器或 <strong>Suspend-Queue</strong> cmdlet。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="even">
<td><p>恢复队列</p></td>
<td><p>此操作的作用与挂起队列操作相反，恢复排队邮件的传递。</p></td>
<td><p>队列查看器或 <strong>Resume-Queue</strong> cmdlet。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="odd">
<td><p>重试队列</p></td>
<td><p>此操作立即尝试连接下一跃点。在没有手动干涉的情况下，当无法连接到下一跃点时，在每次尝试的特定时间间隔后，会以特定次数尝试连接。</p>
<p>不论连接尝试是手动还是自动，任何连接尝试都会重置下一次重试时间。有关详细信息，请参阅<a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">邮件重试间隔、重新提交间隔和过期间隔</a>。</p></td>
<td><p>队列查看器或 <strong>Retry-Queue</strong> cmdlet。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="even">
<td><p>重新提交队列中的邮件</p></td>
<td><p>此操作导致队列中的邮件被重新提交到提交队列并通过分类过程返回。</p></td>
<td><p>使用 <em>Resubmit</em> 参数的 <strong>Retry-Queue</strong></p>
<p>请注意，您可以使用队列查看器重新提交邮件，但只能从病毒邮件队列中提交。若要重新提交病毒邮件中的邮件，可以恢复队列查看器中的邮件，或通过使用 <strong>Resume-Message</strong> cmdlet 提交邮件。</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">管理队列</a></p></td>
</tr>
<tr class="odd">
<td><p>挂起队列中的邮件</p></td>
<td><p>此操作暂时禁止传递邮件。可以使用挂起邮件操作来禁止将邮件传递给特定队列中的所有收件人或所有队列中的所有收件人。</p></td>
<td><p>队列查看器或 <strong>Suspend-Message</strong> cmdlet。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理队列中的邮件</a></p></td>
</tr>
<tr class="even">
<td><p>恢复队列中的邮件</p></td>
<td><p>此操作的作用与挂起邮件操作相反，恢复排队邮件的传递。可以使用恢复邮件操作来继续将邮件传递给特定队列中的所有收件人或所有队列中的所有收件人。</p></td>
<td><p>队列查看器或 <strong>Resume-Message</strong> cmdlet。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理队列中的邮件</a></p></td>
</tr>
<tr class="odd">
<td><p>删除队列中的邮件</p></td>
<td><p>此操作永久禁止传递邮件。可以使用删除邮件操作来禁止将邮件传递给指定队列中的任何收件人或所有队列中的所有收件人。还可以将删除邮件操作配置为在删除邮件时，向发件人发送未送达报告 (NDR)。</p></td>
<td><p>队列查看器或 <strong>Remove-Message</strong> cmdlet。</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">管理队列中的邮件</a></p></td>
</tr>
<tr class="even">
<td><p>从队列导出邮件</p></td>
<td><p>此操作将邮件复制到指定的文件路径。不会从队列中删除邮件，但是会将文件副本保存到某个文件位置。这样，组织中的管理员或官员可以以后再检查邮件。在导出邮件之前，需要在队列中挂起该邮件，以便在导出过程中不会继续通常的传递操作。</p></td>
<td><p>仅 <strong>Export-Message</strong> cmdlet。</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">从队列导出邮件</a></p></td>
</tr>
</tbody>
</table>


返回顶部

