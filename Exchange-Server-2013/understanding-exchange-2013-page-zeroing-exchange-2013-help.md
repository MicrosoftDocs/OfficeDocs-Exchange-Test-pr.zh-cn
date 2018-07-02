﻿---
title: '了解 Exchange 2013 页清零: Exchange 2013 Help'
TOCTitle: 了解 Exchange 2013 页清零
ms:assetid: 0ca7b188-efbc-4c0d-bcfe-5138cffc803c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg549096(v=EXCHG.150)
ms:contentKeyID: 61642435
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解 Exchange 2013 页清零

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

## Exchange 2013 中的页清零

*清零*是一种安全机制，可对已删除数据写入零或二进制模式，使其更加难以恢复。在 Exchange Server 2013 中，ESE 数据库使用*页*作为其存储单位，从而实现了*页清零*。页清零默认启用，且无法禁用。页清零操作会记录在事务日志文件中，从而以相似方式对数据库的所有副本进行页清零。对活动数据库上的页清零会使该页在数据库的被动副本上被清零。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>没有机制可供可扩展存储引擎 (ESE) 用于使重复利用清零的页优先于分配新空间。分配顺序空间分配的表会有意跳过碎片化或清零的页，以便使用新的或空闲的顺序页。这种方法可以减少数据库 IOP。</td>
</tr>
</tbody>
</table>


在 Exchange 2013 中，页清零可以在服务器执行清零功能时，减轻对服务器的性能影响。这包括：

  - **优化了存储和网络容量**   ESE 会将页清零记录写入事务日志文件而不是记录整个页映像。这种方法可以减少日志写入 I/O，以及对传输日志文件的带宽要求。

  - **优化了数据库磁盘 I/O**   在 Exchange 2010 RTM 及早期版本中，页清零只在备份或计划维护过程中进行，并且会导致大量的数据库磁盘 I/O。在 Exchange 2010 SP1 及更高版本（包括 Exchange 2013）中，默认情况下会进行页清零，并且在事务时间进行。在大多数情况下，清零在硬删除之后立即进行。此设计使数据库可以利用引擎的检查点深度功能，这可确保脏页在数据库缓存中保持一段特定时间，因此在临近关闭时间进行的其他页更新不会导致更多数据库写入 I/O。得益于此设计，页清零对数据库 I/O 没有重大影响，这也是为何默认情况下会启用该功能的原因所在。

## ESE 数据库中的页清零实现

页清零会对硬删除的记录写入二进制模式。页清零模式特定于 ESE 引擎操作，对于运行时操作和维护操作有所不同。下表列出对应于特定运行时操作的填充模式。

### ESE 运行时的页清零填充模式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE 运行时操作</th>
<th>填充模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>替换</p></td>
<td><p>R</p></td>
</tr>
<tr class="even">
<td><p>记录/长数值删除</p></td>
<td><p>D</p></td>
</tr>
<tr class="odd">
<td><p>释放的页空间</p></td>
<td><p>H</p></td>
</tr>
</tbody>
</table>


下表列出对应于在 ESE 后台数据库维护期间进行的特定操作的填充模式。

### ESE 后台数据库维护期间的页清零填充模式

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ESE 后台数据库维护操作</th>
<th>填充模式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>记录删除</p></td>
<td><p>D</p></td>
</tr>
<tr class="even">
<td><p>长数值删除</p></td>
<td><p>L</p></td>
</tr>
<tr class="odd">
<td><p>部分使用的页的释放页空间</p></td>
<td><p>Z</p></td>
</tr>
<tr class="even">
<td><p>未使用的页的释放页空间</p></td>
<td><p>U</p></td>
</tr>
</tbody>
</table>


## 后台数据库维护

后台数据库维护是对每个数据库持续进行校验和检查与扫描的过程。其主要功能是对数据库页进行校验和检查，但它还会清理空间，清零由于存储崩溃而未能清零的记录与页。对于每个数据库，后台数据库维护每秒大约处理 1 MB。如果需要优先及时进行页清零，则可以减少数据库大小，以确保在较短时间段（例如 24 小时）内针对崩溃恢复情况进行页清零。

后台数据库维护是一个持续的过程，因此没有事件与其开始和完成关联。您可以通过读取性能计数器的值来跟踪后台数据库维护的进度：

  - MSExchange 数据库 -\> 实例 -\> 数据库维护持续时间

此计数器指示自针对给定数据库上次完成维护以来经过的秒数。

## ESE 数据库页清零的过程

下表讨论数据库删除方案以及页清零功能的执行时间。

### ESE 后台数据库维护

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>数据库删除方案</th>
<th>对数据库数据清零的 ESE 过程和时间范围</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>方案 1：禁用单个项目恢复，用户在“可恢复的项目”文件夹中清除项目。</p></li>
<li><p>方案 2：禁用单个项目恢复，“可恢复的项目”保留期设置为零。</p></li>
<li><p>方案 3：启用单个项目恢复，项目基于删除的项目保留期而过期。</p></li>
</ul></td>
<td><p>一个异步线程对删除的数据写入二进制模式。此操作在数毫秒的记录删除过程中发生。如果存储过程崩溃，而异步清零工作仍未完成（或由于版本存储增长而取消了版本存储清理），则当后台数据库维护处理该部分数据库时会完成清零。</p></td>
</tr>
<tr class="even">
<td><p>视图方案：Outlook/Outlook Web App 文件夹视图（例如会话视图）中的项目过期</p></td>
<td><p>当后台数据库维护处理该部分数据库时会进行数据清零。</p></td>
</tr>
<tr class="odd">
<td><p>移动邮箱/删除邮箱方案：源邮箱已删除（转储程序中的已删除邮箱过期）</p></td>
<td><p>当后台数据库维护处理该部分数据库时会进行数据清零。</p></td>
</tr>
</tbody>
</table>


## 监视页清零行为

您可以通过查看两个 ESE 计数器来测量和监视页清零：

  - MSExchange 数据库 -\> 数据库维护清零的页：指示自调用性能计数器以来，由数据库引擎清零的页数。

  - MSExchange 数据库 -\> 数据库维护清零的页/秒：指示页清零的速率。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要了解如何启用这些计数器，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=101194">如何启用扩展的 ESE 性能计数器</a>。</td>
</tr>
</tbody>
</table>


页清零是一种数据库维护功能，因此，与运行时事务的页清零和由于后台数据库维护导致的页清零相关的性能信息，都会包括在这些计数器中。

## 不进行页清零的邮箱数据类型

以下邮箱数据类型没有针对页清零的设置：

  - 邮箱数据库事务日志 (.log)
    
    当删除事务日志（由于通过备份或循环日志记录而截断）时，没有过程可用于对在存储已删除日志文件的 NTFS 文件系统中的块进行清零。NTFS 可能会很快对新创建的日志重复利用该可用空间，但是无法保证会发生此情况。

  - 内容索引编录文件
    
    Exchange 2013 将 Search Foundation 用于搜索索引功能。搜索索引编录由存储在与邮箱数据库文件相同的卷上的几十个文件组成。当从邮箱数据库中硬删除邮件时，不会立即删除搜索编录中的关联内容。当 Search Foundation 将许多小编录文件卷影（或主合并）到单个较大文件中时，会进行内容删除。主合并完成后，会删除较小的编录文件。没有过程可用于对存储已删除编录文件的块进行清零。

