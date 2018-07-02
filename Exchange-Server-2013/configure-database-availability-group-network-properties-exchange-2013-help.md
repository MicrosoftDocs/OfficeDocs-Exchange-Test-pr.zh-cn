---
title: '配置数据库可用性组网络属性: Exchange 2013 Help'
TOCTitle: 配置数据库可用性组网络属性
ms:assetid: 41197639-988f-476c-9788-51d5191a7dce
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd297927(v=EXCHG.150)
ms:contentKeyID: 50490432
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置数据库可用性组网络属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-31_

每个数据库可用性组 (DAG) 网络包含多个可以配置的属性，包括 DAG 网络名称、DAG 网络的描述字段、DAG 网络使用的子网列表，以及是否为复制启用 DAG 网络。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - 只有在为 DAG 禁用自动网络配置后，才能配置 DAG 网络。有关为 DAG 禁用自动网络配置的详细步骤，请参阅[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)。

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

## 使用 EAC 配置数据库可用性组的网络属性

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  选择要配置的 DAG，然后在详细信息窗格中要配置的 DAG 网络下选择：
    
      - **禁用复制**或**启用复制**   为 DAG 网络配置这些复制设置。
    
      - **删除**   删除 DAG 网络。必须先从 DAG 网络中删除所有关联的子网，然后才能删除 DAG 网络。
    
      - **查看详细信息**   配置 DAG 网络属性，如 DAG 网络名称、描述和关联子网。还可以查看与这些子网相关联的网络接口，并为 DAG 网络启用或禁用复制。

## 使用命令行管理程序配置数据库可用性组网络属性

此示例将子网 10.0.0.0 和子网掩码 255.0.0.0 添加到名为 DAG1 的 DAG 中的 DAG 网络 MapiDagNetwork。

    Set-DatabaseAvailabilityGroupNetwork -Subnets 10.0.0.0/8 -Identity DAG1\MapiDagNetwork

## 您如何知道这有效？

要验证您是否成功配置了 DAG 网络，请执行以下操作：

  - 在命令行管理程序中，运行以下命令以显示 DAG 网络配置设置，并验证是否成功配置了 DAG 网络。
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## 详细信息

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298131\(v=exchg.150\))

