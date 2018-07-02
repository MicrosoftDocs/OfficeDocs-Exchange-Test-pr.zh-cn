---
title: '执行服务器切换: Exchange 2013 Help'
TOCTitle: 执行服务器切换
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523846
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 执行服务器切换

 

_**适用于：** Exchange Server 2013 SP1_

_**上一次修改主题：** 2014-06-23_

服务器切换是一项将所有活动邮箱数据库副本，从其当前邮箱服务器移到数据库可用性组 (DAG) 中的一个或多个其他邮箱服务器的任务。此任务将在当前邮箱服务器计划中断的准备过程中执行。

## 在开始之前，您需要知道什么？

  - 预计完成时间：每个数据库 30 秒

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 EAC 执行服务器切换

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  选择要用来切换的邮箱服务器。

3.  在详细信息窗格中，选择\&quot;服务器切换\&quot;。

4.  在\&quot;服务器切换\&quot;页面上，执行以下一种操作：
    
    1.  接受默认设置\&quot;自动选择目标服务器\&quot;（在这种情况下，系统将为要切换的每个数据库自动选择最佳邮箱服务器），然后单击\&quot;保存\&quot;。
    
    2.  单击\&quot;使用指定的服务器作为切换目标\&quot;，再单击\&quot;浏览\&quot;选择邮箱服务器，然后单击\&quot;保存\&quot;。

5.  成功完成切换后，单击\&quot;关闭\&quot;退出\&quot;服务器切换\&quot;页面。

## 使用命令行管理程序执行服务器切换

本示例将对服务器 MBX1 执行服务器切换。系统将自动为 MBX1 上的每个活动数据库选择最佳邮箱服务器。

    Move-ActiveMailboxDatabase -Server MBX1

本示例将对邮箱服务器 MBX4 执行服务器切换。当命令完成时，MBX5 将托管先前在 MBX4 上处于活动状态的数据库的活动副本。

    Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5

有关详细的语法和参数信息，请参阅[Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-cn/library/dd298068\(v=exchg.150\))。

