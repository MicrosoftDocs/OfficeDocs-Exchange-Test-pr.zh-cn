---
title: '创建数据库可用性组: Exchange 2013 Help'
TOCTitle: 创建数据库可用性组
ms:assetid: d6b98299-e203-488b-af73-50753fe152c8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351172(v=EXCHG.150)
ms:contentKeyID: 50491639
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建数据库可用性组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

数据库可用性组 (DAG) 是一组 Microsoft Exchange Server 2013 邮箱服务器（最多 16 个），提供从数据库、服务器或网络故障中自动执行数据库级恢复的功能。将邮箱服务器添加到 DAG 后，此服务器与 DAG 中的其他服务器协同工作，提供从数据库、服务器和网络故障中自动执行数据库级恢复的功能。

要查找与 DAG 相关的其他管理任务吗？请查看[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - 在创建包含运行 Windows Server 2012 的邮箱服务器的 DAG 时，在向 DAG 添加成员之前必须预留群集名称对象 (CNO)。如果您创建的 DAG 不包含管理访问点，但具有运行 Windows Server 2012 R2 的邮箱服务器，则无需为 DAG 预先暂存 CNO。有关详细步骤，请参阅[为数据库可用性组预留群集名称对象](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

  - 创建 DAG 时，请为 DAG 提供最多 15 个字符的唯一名称。除了为 DAG 提供名称，还必须为 DAG 分配一个或多个 IP 地址（都为 IPv4，或同时包含 IPv4 和 IPv6），除非创建的 Windows Server 2012 R2 DAG 不包含管理访问点并且未向 DAG 分配任何 IP 地址。否则，分配的 IP 地址必须处在用于 MAPI 网络的每个子网上，且必须可用。如果您指定一个或多个 IPv4 地址，并且您的系统已配置为使用 IPv6，该任务还会尝试自动为 DAG 分配一个或多个 IPv6 地址。

  - 在创建 DAG 时，可以选择指定见证服务器和见证目录。如果要指定见证服务器，建议使用没有安装邮箱服务器角色的客户端访问服务器。这可让 Exchange 管理员了解见证的可用性，并且它可确保使用见证服务器必需的所有安全权限都已准备好。
    
    可以使用以下选项和行为组合：
    
      - 可以仅指定 DAG 的名称，将\&quot;见证服务器\&quot;和\&quot;见证目录\&quot;字段留空。在此情况下，任务将搜索未安装邮箱服务器角色的客户端访问服务器。系统将自动在该客户端访问服务器上创建默认见证目录并共享该目录，并配置 DAG 以使用该服务器作为其见证服务器。
    
      - 可以指定 DAG 的名称、要使用的见证服务器以及要在见证服务器上创建并共享的目录。
    
      - 可以指定 DAG 的名称、要使用的见证服务器，并将\&quot;见证目录\&quot;字段留空。在这种情况下，任务将在指定的见证服务器上创建默认见证目录。
    
      - 可以指定 DAG 的名称、将\&quot;见证服务器\&quot;字段留空，并指定要在见证服务器上创建并共享的目录。在这种情况下，向导将搜索没有安装邮箱服务器角色的客户端访问服务器，在该服务器上自动创建并共享指定的见证目录，然后配置 DAG 以使用该客户端访问服务器作为其见证服务器。
    
    > [!important]
    > 如果您指定的见证服务器不是 Exchange 2013 或 Exchange 2010 服务器，则必须将 Exchange 受信任子系统通用安全组添加到见证服务器上的本地管理员组中。需要这些安全权限来确保 Exchange 可以根据需要在见证服务器上创建并共享目录。如果未配置正确权限，将会返回以下错误：
    > <code>Error: An error occurred during discovery of the database availability group topology. Error: An error occurred while attempting a cluster operation. Error: Cluster API &quot;AddClusterNode() (MaxPercentage=12) failed with 0x80070005. Error: Access is denied.&quot;</code>


  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建数据库可用性组

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  单击 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 以创建 DAG。

3.  在\&quot;新建数据库可用性组\&quot;页上，提供 DAG 的以下信息：
    
      - **数据库可用性组名称**   使用此字段为 DAG 键入最多 15 个字符的有效唯一名称。该名称等同于计算机名，相应的 CNO 将使用该名称在 Active Directory 中创建。该名称将同时为 DAG 和基础群集的名称。
    
      - **见证服务器**   使用该字段指定 DAG 的见证服务器。如果将该字段留空，系统将尝试自动选择没有安装于计算机上的本地 Active Directory 站点中的客户端访问服务器，并将邮箱服务器用作见证服务器。
        
        > [!NOTE]
        > 如果指定见证服务器，则必须使用主机名 (FQDN) 或完全限定的域名 (FQDN)。不支持使用 IP 地址或通配符名称。此外，见证服务器不能是 DAG 的成员。
    
      - **见证目录**   使用该字段键入指向将用于存储见证数据的见证服务器上的目录的路径。如果该目录不存在，系统将会在见证服务器上为您创建该目录。如果将该字段留空，将在见证服务器上创建默认目录 (%SystemDrive%\\DAGFileShareWitnesses\\\<DAG FQDN\>)。
    
      - **数据库可用性组 IP 地址**   使用该字段将一个或多个静态 IPv4 地址分配至 DAG。输入一个 IPv4 地址，然后单击 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 添加它。如果希望 DAG 使用动态主机配置协议 (DHCP) 获取必要的 IPv4 地址，则将该字段留空。或者，输入 255.255.255.255 以创建不含 IP 地址或群集管理访问点的 DAG，这仅适用于将包含运行 Windows Server 2012 R2 的邮箱服务器的 DAG。

4.  单击\&quot;保存\&quot;以创建 DAG。

## 使用命令行管理程序创建数据库可用性组

本示例将创建一个名为 DAG1 的 DAG，此 DAG 配置为使用见证服务器 FILESRV1 和本地目录 C:\\DAG1。DAG1 还配置为对 DAG 的 IP 地址使用 DHCP。

    New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer FILESRV1 -WitnessDirectory C:\DAG1

此示例创建名为 DAG2 的 DAG。系统会自动选择位于不包含邮箱服务器角色的本地 Active Directory 站点中的客户端访问服务器作为 DAG 的见证服务器。由于本例中的所有 DAG 成员的 MAPI 网络都位于同一子网中，因此为 DAG2 分配了一个静态 IP 地址。

    New-DatabaseAvailabilityGroup -Name DAG2 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

此示例创建名为 DAG3 的 DAG。DAG3 配置为使用见证服务器 MBX2 和本地目录 C:\\DAG3。由于 DAG3 的 DAG 成员所处的 MAPI 网络位于不同子网中，因此为 DAG3 分配了多个静态 IP 地址。

    New-DatabaseAvailabilityGroup -Name DAG3 -WitnessServer MBX2 -WitnessDirectory C:\DAG3 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,192.168.0.8

此示例创建配置为使用 DHCP 的名为 DAG4 的 DAG。此外，系统将自动选择见证服务器，并创建默认的见证目录。

    New-DatabaseAvailabilityGroup -Name DAG4

本示例创建的 DAG DAG5 不包含管理访问点（仅对 Windows Server 2012 R2 DAG 有效）。此外，MBX4 将用作 DAG 的见证服务器，并将创建默认的见证目录。

    New-DatabaseAvailabilityGroup -Name DAG5 -DatabaseAvailabilityGroupIPAddresses ([System.Net.IPAddress]::None) -WitnessServer MBX4

## 您如何知道这有效？

若要验证是否成功创建了 DAG，请执行以下操作之一：

  - 在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。将显示新创建的 DAG。

  - 在 Shell 中，运行以下命令检查是否已创建 DAG 并显示 DAG 属性信息。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 详细信息

[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\))

[New-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd351107\(v=exchg.150\))

[New-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd335225\(v=exchg.150\))

[Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd298049\(v=exchg.150\))

