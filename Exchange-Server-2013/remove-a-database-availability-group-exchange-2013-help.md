---
title: '删除数据库可用性组: Exchange 2013 Help'
TOCTitle: 删除数据库可用性组
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50489872
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除数据库可用性组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-16_

删除数据库可用性组 (DAG) 是一个快速且方便的任务。可以使用 EAC 或命令行管理程序删除 DAG。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - DAG 必须为空才能删除它。如果要删除的 DAG 包含任何邮箱服务器，必须首先从该 DAG 中删除这些服务器。有关如何从 DAG 中删除邮箱服务器的详细步骤，请参阅[管理数据库可用性组成员身份](manage-database-availability-group-membership-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 您想执行什么操作？

## 使用 EAC 删除数据库可用性组

1.  导航到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  选择要删除的 DAG 并单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  单击\&quot;是\&quot;确认警告并删除 DAG。

## 使用命令行管理程序删除数据库可用性组

此示例将删除名为 DAG1 的 DAG。

    Remove-DatabaseAvailabilityGroup -Identity DAG1

## 您如何知道这有效？

若要验证是否成功删除了 DAG，请执行以下操作之一：

  - 在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;，查看是否仍显示 DAG。

  - 在命令行管理程序中，运行以下命令以查看 DAG 是否仍存在：
    
        Get-DatabaseAvailabilityGroup <DAGName>
    
    如果成功删除了 DAG，则上面的命令会生成错误消息，以指示找不到对象。

