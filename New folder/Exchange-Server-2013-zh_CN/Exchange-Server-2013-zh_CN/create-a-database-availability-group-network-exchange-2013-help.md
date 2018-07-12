---
title: '创建数据库可用性组网络: Exchange 2013 Help'
TOCTitle: 创建数据库可用性组网络
ms:assetid: 6caec7be-788a-4058-87a7-f31c575b870c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298051(v=EXCHG.150)
ms:contentKeyID: 50490882
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建数据库可用性组网络

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-02_

如果需要，可以创建其他网络以供在数据库可用性组 (DAG) 中使用。可以使用 EAC 或命令行管理程序创建 DAG 网络。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - 只有在为 DAG 禁用了自动网络配置后，才能创建 DAG 网络。有关为 DAG 禁用自动网络配置的详细步骤，请参阅[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)。

  - 创建 DAG 网络时，必须分配其他 DAG 网络未在使用的唯一子网。如果使用已分配到现有 DAG 网络的子网，那么这些子网会从现有 DAG 网络中删除，然后添加到新建的 DAG 网络中。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建数据库可用性组网络

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  选择要配置的 DAG，然后单击 ![添加 DAG 网络](images/Dd298051.befcdc4e-7f7a-451d-a0a8-608c79f5d186(EXCHG.150).gif "添加 DAG 网络")。

3.  在\&quot;新建数据库可用性组网络\&quot;页上，提供以下信息：
    
      - **数据库可用性组网络名称**   使用此字段可为网络键入在 DAG 中唯一的名称。
    
      - **描述**   使用此字段可提供 DAG 网络的文本描述。
    
      - **子网**   使用此字段可将一个或多个子网与 DAG 网络相关联。单击 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可添加子网，单击 ![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 可编辑子网，单击负号 (-) 可删除子网。

4.  单击\&quot;保存\&quot;可以创建 DAG 网络。

## 使用命令行管理程序创建数据库可用性组网络

此示例在 DAG DAG1 中创建子网为 10.0.0.0 以及位掩码为 8 的网络 ReplicationDagNetwork02。此网络已启用复制，还添加了可选的网络描述。

    New-DatabaseAvailabilityGroupNetwork -DatabaseAvailabilityGroup DAG1 -Name ReplicationDagNetwork02 -Description "Replication network 2" -Subnets 10.0.0.0/8 -ReplicationEnabled:$True

## 您如何知道这有效？

若要验证是否成功创建了 DAG 网络，可执行以下操作之一：

  - 在 EAC 中，依次转到\&quot;**服务器**\&quot;\>\&quot;**数据库可用性组**\&quot;。选择适当的 DAG。此时，细节窗格中会显示新建的 DAG 网络。

  - 在命令行管理程序中，运行以下命令以验证 DAG 网络是否已创建并显示 DAG 网络配置信息。
    
        Get-DatabaseAvailabilityGroupNetwork <DAGNetworkName> | Format-List

## 详细信息

[Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298008\(v=exchg.150\))

[Get-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd297938\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd335225\(v=exchg.150\))

[Remove-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298131\(v=exchg.150\))

