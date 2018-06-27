---
title: '混合迁移的性能因素和最佳做法: Exchange 2013 Help'
TOCTitle: 混合迁移的性能因素和最佳做法
ms:assetid: 120a7832-d2d3-47d7-b305-918360c2ef66
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt483789(v=EXCHG.150)
ms:contentKeyID: 70118019
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合迁移的性能因素和最佳做法

 


_<strong>适用于：</strong>Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_


在 Office 365 中有许多途径可以将本地电子邮件组织中的数据迁移到 Office 365。在计划迁移到 Office 365 时，一个常见的问题是如何提高数据迁移的性能并优化迁移速度。本文讨论了 Exchange 混合部署的迁移性能，有关其他迁移方法的性能信息，请参阅 [Office 365 迁移性能和最佳做法](http://go.microsoft.com/fwlink/p/?linkid=623651)。

## 混合迁移的性能因素和最佳做法

混合部署迁移支持本地 Exchange 服务器和 Office 365 中的 Exchange Online 之间的顺利迁移。

混合部署迁移是到目前为止将邮箱数据迁移到 Office 365 的最快迁移方法。我们看到在实际客户部署期间吞吐量高达 100 GB/小时。下表列出了适用于本机 Office 365 混合迁移方案的因素。

如果你的本地环境在分散的地理位置中包含多个站点，可以通过创建地理位置邻近感应的迁移终结点来提高迁移性能。这是因为在这样的情况下迁移使用 Microsoft 的网络，而不使用集中式迁移终结点（使用本地网络）。

## 因素 1：数据源 (Exchange Server)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>检查表</th>
<th>说明</th>
<th>最佳做法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>系统性能</p></td>
<td><p>数据提取是一项非常占用资源的任务。源系统必须具有足够的资源（如 CPU 时间和内存）才能提供更佳的迁移性能。在迁移时，源系统通常接近于最大容量，以便为常规最终用户工作负载提供服务 - 其他迁移工作负载有时甚至会因为缺少系统资源而妨碍最终用户访问。</p></td>
<td><p>在试点迁移测试过程中监视系统性能。如果系统繁忙，我们建议不要对特定系统执行很占用资源的迁移计划，因为这可能导致迁移变慢和服务可用性问题。如果可能，应通过增加硬件资源和减少系统中的负载（通过将任务和用户移至迁移未涉及的其他服务器）提高源系统性能。</p>
<p>有关详细信息，请参阅：</p>
<ul>
<li><p><a href="http://go.microsoft.com/fwlink/?linkid=723566">询问性能专家：Sizing Exchange 2016 Deployments</a>（调整 Exchange 2016 部署的大小）</p></li>
<li><p><a href="https://technet.microsoft.com/zh-cn/library/jj150551(v=exchg.150)">服务器运行状况和性能</a></p></li>
<li><p><a href="http://technet.microsoft.com/zh-cn/library/dd351192.aspx">了解 Exchange 2010 性能</a></p></li>
</ul>
<p>当从存在多个邮箱服务器和多个数据库的本地 Exchange 组织迁移时，我们建议创建在多个邮箱服务器和数据库之间均匀分布的迁移用户列表。根据各个服务器的性能，可以对该列表进一步微调以最大限度地增加吞吐量。</p>
<p>例如，如果服务器 A 的资源可用性比服务器 B 高 50%，那么在同一个迁移批次中让服务器 A 中多迁移 50% 的用户较为合理。类似的做法可应用于其他源系统。</p>
<p>在服务器具有最大资源可用性时（如下班后或周末和假日）执行迁移。</p></td>
</tr>
<tr class="even">
<td><p>后端任务</p></td>
<td><p>在迁移期间运行的其他后端任务。最佳做法是在下班之后执行迁移，因此经常会遇到迁移与您的内部部署服务器上运行的其他维护任务（如数据备份）相冲突的情况。</p></td>
<td><p>查看在迁移期间可能会运行的其他系统任务。我们建议在没有运行其他占用资源较多的任务时执行数据迁移。</p>
<p><strong>注意</strong>   对于使用内部部署 Microsoft Exchange 的客户，常见的后端任务是备份解决方案和 <a href="http://technet.microsoft.com/zh-cn/library/aa996226(exchg.65).aspx">Exchange 存储维护</a>。</p></td>
</tr>
</tbody>
</table>


## 因素 2：迁移服务器

混合部署迁移是云发起的数据提取/推送迁移，Exchange 混合服务器充当迁移服务器。而这一点经常被忽略，且客户会使用规模较小的虚拟机充当混合服务器。这会导致迁移性能降低

**最佳做法**

除了应用之前描述的最佳做法之外，我们还测试了以下最佳做法，这些做法提高了实际客户迁移的迁移性能：

  - 为 Exchange 混合服务器使用强大的服务器类物理计算机来替代虚拟机。

  - 使用多台位于客户的网络负载平衡器之后的混合服务器。

例如，在实际客户迁移中，我们已通过以下配置达到了一致的 30 GB/小时的吞吐量：

  - **网络**  500 MB 的 Internet 出站管道；10 GB 的光纤主干网的内部网络传输速率为 1 GB。

  - **硬件**   两个客户端访问/中心（物理）服务器的规格：
    
      - CPU：Intel® Xeon® CPU E5520 @ 2.27 GHz 2.26 GHz（两个处理器）。
    
      - RAM：24 GB。
    
      - 磁盘：每个磁盘 8×146 GB。RAID 5 配置 = 960 GB 总原始空间。

  - **MRSProxy**   其并发数配置为 100 个。

## 因素 3：迁移引擎

混合部署迁移使用本机 Office 365 工具。它受 Office 365 迁移服务限制的约束。

**Exchange 2003 和更高版本的 Exchange**

从 Exchange 2003 进行迁移时，存在最终用户体验的重大差异。与 Exchange 的更高版本不同，Exchange 2003 最终用户无法在迁移数据时访问其邮箱。因此，Exchange 2003 客户通常更关注何时安排迁移以及迁移所需的时间（尤其是在因邮箱较大或网速较慢而导致迁移性能降低时）。

Exchange 2003 迁移对中断也非常敏感。例如，在实际客户迁移中，在 10 GB 邮箱迁移期间，在邮箱迁移完成 50% 时发生了服务事件。处理数据迁移的 Office 365 客户端访问服务器必须重新启动才能解决问题。在这种情况下，必须重新启动邮箱迁移，这意味着客户必须重新迁移所有 10 GB 的数据。不能从停止的点恢复迁移。但 Exchange 2010 和更高版本的 Exchange 却能在中断后恢复迁移。

**最佳做法**

有些客户选择对规模较大且敏感的 Exchange 2003 邮箱执行两跳迁移：

  - **第一个跃点**   将邮箱从 Exchange 2003 迁移到 Exchange 2010 或更高版本的服务器（通常为混合服务器）。第一个跃点是脱机移动，但通常是通过本地网络执行的速度极快的迁移。

  - **第二个跃点**   将邮箱从 Exchange 2010 或更高版本迁移到 Office 365。

第二个跃点是联机移动，会提供更好的用户体验和容错功能。这两个跃点方法需使用临时本地用户邮箱的 Exchange 许可证。

**邮箱复制服务代理 (MRSProxy)**

MRS 代理是与 Office 365 端运行的邮箱复制服务结合使用的本地迁移功能。有关详细信息，请参阅[了解移动请求](http://technet.microsoft.com/zh-cn/library/dd298174.aspx)。

**最佳做法**

可以为本地 Exchange 混合服务器 配置最大数量的 MRSProxy 连接。运行以下 Windows PowerShell 命令。

    Set-WebServicesVirtualDirectory -Identity "EWS (Default Web Site)" -MRSMaxConnections <number between 0 and unlimited; default is 100>

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于大多数客户迁移，无需更改默认 MRSMaxConnections 值。如果需要保护源服务器以免迁移负载过大，客户可以减少连接数。此设置按每个 MRSProxy 服务器进行设置。如果客户有两个 MRSProxy 服务器，每个服务器都设置为 10 个连接，它们的总 MRSProxy 连接数将为 20 (2 x 10)。有关在本地 Exchange 2010 组织中配置 MRSProxy 服务的详细信息，请参阅<a href="http://technet.microsoft.com/zh-cn/library/ee732395.aspx">在远程客户端访问服务器上启动 MRSProxy 服务</a>。</td>
</tr>
</tbody>
</table>


## 因素 4：网络

**验证测试**

对于运行 Exchange 2010 或更高版本的客户，可通过执行多个测试邮箱迁移完成对混合迁移网络性能的测试。或者，也可以使用 -SuspendWhenReadyToComplete 选项迁移实际用户邮箱，以满足迁移性能指标。测试完成时，删除移动请求，以避免影响最终用户。

有关移动请求的详细信息，请参阅 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 因素 5：Office 365 服务

基于 Office 365 资源运行状况的限制将影响使用 Office 365 混合部署迁移的迁移。请参阅上面的基于 Office 365 资源运行状况的限制部分，以了解更多详细信息。

