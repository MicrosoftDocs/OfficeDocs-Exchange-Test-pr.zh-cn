---
title: '反压力: Exchange 2013 Help'
TOCTitle: 反压力
ms:assetid: 03003544-e802-4988-9427-5fc4da64dcb8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201658(v=EXCHG.150)
ms:contentKeyID: 52061476
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 反压力

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

“反压力”是 Microsoft Exchange 2013 邮箱服务器和边缘传输服务器上存在的 Microsoft Exchange 传输服务的系统资源监视功能。

Exchange 可以检测重要资源（例如可用硬盘空间和内存）何时具有压力，并采取操作以尝试阻止服务不可用性。反压力可以防止过多地使用系统资源，Exchange 服务器在接受任何新邮件前会尝试将现有邮件进行处理。当系统资源使用率恢复到正常级别后，Exchange 服务器就可以逐渐恢复正常运行并再次开始接受新邮件。

在 Exchange 2013 中，当邮箱服务器或边缘传输服务器上的传输服务具有资源压力时，会接受传入连接，但是会以更慢的速度接受或拒绝通过这些连接传入的邮件。当 SMTP 主机试图连接具有资源压力的 Exchange 服务器时，该连接可成功进行。但是，当主机发出 **MAIL FROM** 命令来提交邮件时，传输服务会根据具有压力的资源来延迟确认 **MAIL FROM** 命令或拒绝连接。

**目录**

监视的资源

具有资源压力时 Exchange 传输执行的操作

EdgeTransport.exe.config 文件中的反压力配置选项

反压力日志记录信息

## 监视的资源

作为反压功能的一部分，将监视下列系统资源：

  - 存储邮件队列数据库的硬盘中的可用空间。

  - 存储邮件队列数据库事务日志的硬盘中的可用空间。

  - 内存中的未提交邮件队列数据库事务数目。

  - EdgeTransport.exe 进程使用的内存大小。

  - 所有其他进程使用的内存大小。

  - 提交队列中的邮件数。

对于邮箱服务器或边缘传输服务器中的每个受监视系统资源，可应用下列三种资源使用率级别：

  - **正常**   资源的使用未过度。服务器可以接受新的连接和邮件。

  - **中等**   资源的使用稍微过度。此时将以有限的方式对服务器应用反压功能。来自权威域中的发件人的邮件可以流动。但是，根据具有压力的特定资源，服务器会使用缓送技术延迟服务器响应或拒绝来自其他源的传入 **MAIL FROM** 命令。

  - **高**   资源的使用严重过度。此时将充分应用反压功能。所有邮件都停止流动，服务器将拒绝一切新传入的 **MAIL FROM** 命令。

下列部分说明特定资源具有压力时 Exchange 如何处理此情况。

## 邮件队列数据库的可用硬盘空间

默认情况下，邮件队列数据库存储在 %ExchangeInstallPath%TransportRoles\\data\\Queue。Exchange 监视该位置的硬盘空间使用率。可使用以下公式计算高级别的硬盘空间使用率：

100 \* (*hard disk size* - *fixed constant*) / *hard drive size*

*fixed constant*的值为 500 MB。

该公式的结果用所用硬盘空间占全部硬盘空间百分比的形式表示。该公式的结果总是向下舍入为最接近的整数。默认情况下，中等级别硬盘使用率比高级别硬盘使用率低 2%。默认情况下，正常级别硬盘使用率比高级别硬盘使用率低 4%。

返回顶部

## 邮件队列数据库事务日志的可用硬盘空间

默认情况下，邮件队列数据库事务日志存储在 %ExchangeInstallPath%TransportRoles\\data\\Queue。Exchange 监视该位置的硬盘空间使用率。%ExchangeInstallPath%Bin\\EdgeTransport.exe.config 应用程序配置文件包含一个 *DatabaseCheckPointDepthMax* 项，其默认值为 384 MB。此项控制硬盘上允许存在的所有未提交的事务日志的总大小。在计算硬盘使用率的公式中，将使用此项。

> [!NOTE]  
> <em>DatabaseCheckPointDepthMax</em> 项的值将应用于邮箱服务器或边缘传输服务器上所有与传输相关的可扩展存储引擎 (ESE) 数据库。这包括邮件队列数据库和 IP 筛选数据库。


默认情况下，使用以下公式计算高级别的硬盘使用率：

100 \* (*hard drive size* - Min(5 GB, 3\**DatabaseCheckPointDepthMax*)) / *hard drive size*

该公式的结果总是向下舍入为最接近的整数。默认情况下，中等级别硬盘使用率比高级别硬盘使用率低 2%。正常级别硬盘使用率比高级别硬盘使用率低 4%。

返回顶部

## 内存中的未提交邮件队列数据库事务数目

在可将对邮件队列数据库的更改提交到事务日志之前，会将该更改列表保存在内存中。然后，会将该列表提交给邮件队列数据库自身。这些保存在内存中的未完成邮件队列数据库事务被称为“版本存储桶”。版本存储桶数目可能会因出乎意料的大量传入邮件、垃圾邮件攻击、邮件队列数据库完整性问题或硬盘性能而增大到不可接受的数目。

Exchange 开始接收邮件时，这些邮件会按批处理进行分组，然后准备用作版本存储桶。如果传入邮件包含较大的附件，可以将其分为多个批处理。正在处理的这些批处理称为“批处理点”。未完成的批处理点数目可以超过设置的阈值，尤其是存在出乎意料的大量带有较大附件的传入邮件时。

版本存储桶或批处理点具有压力时，Exchange 服务器将通过延迟确认传入邮件来开始限制传入连接。Exchange 将通过引入延迟 **MAIL FROM** 命令的缓送技术来降低入站邮件流的速率。如果资源压力情况继续存在，Exchange 将逐渐增加缓送延迟。在资源使用率恢复正常后，Exchange 将逐渐开始减少确认延迟并渐渐进入正常操作。默认情况下，Exchange 将在具有资源压力时开始将邮件确认延迟 10 秒钟。如果资源继续具有压力，延迟会以 5 秒的增量增加，最高为 55 秒。

Exchange 保留版本存储桶和批处理点资源使用率的历史记录。如果资源使用率在特定数量的轮询间隔内没有下降到正常级别，称为历史记录深度，Exchange 将停止缓送延迟并开始拒绝传入邮件，直到资源使用率恢复正常。默认情况下，版本存储桶和批处理点的历史记录深度分别为 10 个和 300 个轮询间隔。

返回顶部

## EdgeTransport.exe 进程使用的内存大小

默认情况下，使用以下公式计算 EdgeTransport.exe 进程使用的高级别内存使用率：

总物理内存的 75% 或 1 TB，选择二者中较小的值

上述计算并未包括硬盘上页面文件中可用的虚拟内存，也未包括其他进程使用的内存。该公式的结果用 EdgeTransport.exe 进程所用内存占全部内存百分比的形式表示。该公式的结果总是向下舍入为最接近的整数。

默认情况下，EdgeTransport.exe 文件的中等级别内存使用率为总物理内存的 73%，或为比高级别内存使用率低 2% 的值，选择二者中较小的值。默认情况下，EdgeTransport.exe 文件的正常级别内存使用率为总物理内存的 71%，或为比高级别内存使用率低 4% 的值，选择二者中较小的值。

如果 EdgeTransport.exe 进程的内存使用率高于指定的正常级别，则会强制执行“垃圾收集”。垃圾收集是一个检查内存中未使用的对象并收回这些对象所用内存的进程。

Exchange 保留 EdgeTransport.exe 进程的内存使用率的历史记录。如果使用率在特定数量的轮询间隔内没有下降到正常级别，称为历史记录深度，Exchange 将开始拒绝传入邮件，直到资源使用率恢复正常。默认情况下，EdgeTransport.exe 内存使用率的历史记录深度为 30 个轮询间隔。

返回顶部

## 所有进程使用的内存

默认情况下，全部进程的高级别内存使用率为总物理内存的 94%。此值并不包括硬盘上页面文件中可用的虚拟内存。

达到指定的内存使用率级别时，会出现“邮件冻结”情况。邮件冻结是一个删除内存中缓存的排队邮件的不必要元素的操作。为了提高性能，完成的邮件都缓存在内存中。因为邮件是从邮件队列数据库中直接读取的，所以删除内存中排队邮件的 MIME 内容可减少内存使用量，但会出现较高延迟。默认情况下，会启用邮件冻结。

返回顶部

## 提交队列中的邮件数

提交队列与 Exchange 2013 邮箱服务器和边缘传输服务器上的传输服务相关联。分类程序处理提交队列中的各个邮件。该分类会将邮件放置在传递队列中。有关详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)和[队列](queues-exchange-2013-help.md)。提交队列中的大量邮件表明分类程序处理邮件会有困难。

提交队列具有压力时，Exchange 服务器将通过延迟确认传入邮件来开始限制传入连接。Exchange 将通过引入延迟 **MAIL FROM** 命令的缓送技术来降低入站邮件流的速率。如果提交队列压力情况继续存在，Exchange 将逐渐增加缓送延迟。在提交队列使用率恢复正常后，Exchange 将逐渐开始减少确认延迟并渐渐进入正常操作。默认情况下，Exchange 将在具有提交队列压力时开始将邮件确认延迟 10 秒钟。如果提交队列继续具有压力，延迟会以 5 秒的增量增加，最高为 55 秒。

Exchange 保留提交队列使用率的历史记录。如果提交队列使用率在特定数量的轮询间隔内没有下降到正常级别，称为历史记录深度，Exchange 将停止缓送延迟并开始拒绝传入邮件，直到提交队列使用率恢复正常。默认情况下，提交队列的历史记录深度为 300 个轮询间隔。

## 具有资源压力时 Exchange 传输执行的操作

下表汇总了特定资源具有压力时 Exchange 传输执行的操作。

### 邮箱服务器和边缘传输服务器响应资源压力时执行的反压力操作

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>具有压力的资源</th>
<th>使用率级别</th>
<th>执行的操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮件队列数据库的硬盘空间</p></td>
<td><p>中等</p></td>
<td><ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>邮件队列数据库的硬盘空间</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>邮件队列数据库事务日志的硬盘空间</p></td>
<td><p>中等</p></td>
<td><ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>邮件队列数据库事务日志的硬盘空间</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>版本存储桶</p></td>
<td><p>中等</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个版本存储桶历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>版本存储桶</p></td>
<td><p>高</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个版本存储桶历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>批处理点</p></td>
<td><p>中等</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个批处理点历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>批处理点</p></td>
<td><p>高</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个批处理点历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>EdgeTransport.exe 进程使用的内存</p></td>
<td><p>中等</p></td>
<td><ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
<li><p>强制垃圾收集</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe 进程使用的内存</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>所有进程使用的内存</p></td>
<td><p>中等</p></td>
<td><ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
<li><p>强制垃圾收集</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>所有进程使用的内存</p></td>
<td><p>高</p></td>
<td><ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
<li><p>从内存刷新增强的 DNS 缓存</p></li>
<li><p>启动邮件冻结</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>提交队列中的邮件数</p></td>
<td><p>中等</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个提交队列历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
<li><p>强制垃圾收集</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>提交队列中的邮件数</p></td>
<td><p>高</p></td>
<td><p>引入或增加对传入邮件的缓送延迟。如果未达到整个提交队列历史记录深度的正常级别，请执行下列操作：</p>
<ul>
<li><p>拒绝来自其他 Exchange 服务器的传入邮件</p></li>
<li><p>通过使用邮箱服务器上的邮箱传输提交服务来拒绝来自邮箱数据库的邮件提交</p></li>
<li><p>拒绝来自非 Exchange 服务器的传入邮件</p></li>
<li><p>拒绝拾取目录和重播目录中的邮件提交</p></li>
<li><p>从内存刷新增强的 DNS 缓存</p></li>
<li><p>启动邮件冻结</p></li>
</ul></td>
</tr>
</tbody>
</table>


返回顶部

## EdgeTransport.exe.config 文件中的反压力配置选项

反压力功能的所有配置选项都位于 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 应用程序配置文件中。

> [!CAUTION]  
> 列出的这些设置仅供参考。我们非常不鼓励对 EdgeTransport.exe.config 文件中的反压力功能设置进行修改。对反压功能设置进行修改可能导致性能不佳或数据丢失。我们建议您调查并纠正可能遇到的任何反压力事件的根本原因。


### 反压力配置选项

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>项名称</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>EnableResourceMonitoring</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>ResourceMonitoringInterval</em></p></td>
<td><p><code>00:00:02</code>（2 秒）</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 该值指示将使用默认公式。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentageDatabaseDiskSpaceUsedHighThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentageDatabaseDiskSpaceUsedMediumThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em></p></td>
<td><p>0. 该值指示将使用默认公式。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentageDatabaseLoggingDiskSpaceUsedHighThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentageDatabaseLoggingDiskSpaceUsedNormalThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentageDatabaseLoggingDiskSpaceUsedMediumThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedHighThreshold</em></p></td>
<td><p>0. 该值指示将使用默认计算。</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePrivateBytesUsedMediumThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentagePrivateBytesUsedHighThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="odd">
<td><p><em>PercentagePrivateBytesUsedNormalThreshold</em></p></td>
<td><p>0. 此值意味着实际值比 <em>PercentagePrivateBytesUsedMediumThreshold</em> 值低 2%。</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsHighThreshold</em></p></td>
<td><p>200</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsMediumThreshold</em></p></td>
<td><p>120</p></td>
</tr>
<tr class="even">
<td><p><em>VersionBucketsNormalThreshold</em></p></td>
<td><p>80</p></td>
</tr>
<tr class="odd">
<td><p><em>VersionBucketsHistoryDepth</em></p></td>
<td><p>10</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointHighThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointMediumThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointNormalThreshold</em></p></td>
<td><p>1000</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointUseCostForPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointBatchSize</em></p></td>
<td><p>40</p></td>
</tr>
<tr class="even">
<td><p><em>BatchPointBatchTimeout</em></p></td>
<td><p><code>00:00:00.100</code>（0.1 秒）</p></td>
</tr>
<tr class="odd">
<td><p><em>BatchPointItemExpiryInterval</em></p></td>
<td><p><code>00:05:00</code>（5 分钟）</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPBaseThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:00</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPMaxThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:55</code>（55 秒）</p></td>
</tr>
<tr class="even">
<td><p><em>SMTPStepThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:05</code>（5 秒）</p></td>
</tr>
<tr class="odd">
<td><p><em>SMTPStartThrottlingDelayInterval</em></p></td>
<td><p><code>00:00:10</code>（10 秒）</p></td>
</tr>
<tr class="even">
<td><p><em>PercentagePhysicalMemoryUsedLimit</em></p></td>
<td><p>94</p></td>
</tr>
<tr class="odd">
<td><p><em>DehydrateMessagesUnderMemoryPressure</em></p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p><em>PrivateBytesHistoryDepth</em></p></td>
<td><p>30</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueHighThreshold</em></p></td>
<td><p>10000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueMediumThreshold</em></p></td>
<td><p>4000</p></td>
</tr>
<tr class="odd">
<td><p><em>SubmissionQueueNormalThreshold</em></p></td>
<td><p>2000</p></td>
</tr>
<tr class="even">
<td><p><em>SubmissionQueueHistoryDepth</em></p></td>
<td><p>300</p></td>
</tr>
</tbody>
</table>


返回顶部

## 反压力日志记录信息

以下列表介绍了 Exchange 中特定反压力事件生成的事件日志条目：

  - **因任何资源使用率级别的增加而生成的事件日志条目**
    
    事件类型：错误
    
    事件源：MSExchangeTransport
    
    事件类别：资源管理器
    
    事件 ID：15004
    
    说明：资源压力已从*Previous Utilization Level*增加到*Current Utilization Level*。

  - **因任何资源使用率级别降低而生成的事件日志条目**
    
    事件类型：信息
    
    事件源：MSExchangeTransport
    
    事件类别：资源管理器
    
    事件 ID：15005
    
    说明：资源压力已从*Previous Utilization Level*降低到*Current Utilization Level*。

  - **非常低的可用磁盘空间的事件日志条目**
    
    事件类型：错误
    
    事件源：MSExchangeTransport
    
    事件类别：资源管理器
    
    事件 ID：15006
    
    说明：Microsoft Exchange 传输服务拒绝邮件，因为可用磁盘空间低于所配置的阀值。可能需要执行管理操作以释放磁盘空间，以便服务可以继续进行操作。

  - **非常低的可用内存事件日志条目**
    
    事件类型：错误
    
    事件源：MSExchangeTransport
    
    事件类别：资源管理器
    
    事件 ID：15007
    
    说明：Microsoft Exchange 传输服务拒绝邮件提交，因为该服务会继续占用多于配置阈值的内存。可能需要重新启动该服务，才能继续正常操作。

返回顶部

