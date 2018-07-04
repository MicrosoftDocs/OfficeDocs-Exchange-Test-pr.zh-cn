---
title: '配置数据库可用性组属性: Exchange 2013 Help'
TOCTitle: 配置数据库可用性组属性
ms:assetid: 50daeac5-a16f-4362-a325-19e0fe25d59d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd297985(v=EXCHG.150)
ms:contentKeyID: 50490543
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置数据库可用性组属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-24_

可以使用 EAC 或命令行管理程序配置数据库可用性组 (DAG) 的属性，包括 DAG IP 地址配置以及由 DAG 使用的见证服务器和见证目录。命令行管理程序使您能够配置在 EAC 中不可用的 DAG 属性，如备用见证服务器和备用见证目录信息、用于复制的 TCP 端口以及数据中心激活协调 (DAC) 模式。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - DAG 属性值存储在 Active Directory 和群集数据库中。但是，某些属性仅存储在群集数据库中。因此，DAG 的基础群集必须正在运行，并且必须具有仲裁才能设置以下项的属性：
    
      - ReplicationPort
    
      - NetworkCompression
    
      - NetworkEncryption
    
      - DiscoverNetworks

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置数据库可用性组属性

1.  在 EAC 中，转到\&quot;服务器\&quot;\>\&quot;数据库可用性组\&quot;。

2.  选择要配置的 DAG 并单击 ![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  
    
    使用\&quot;常规\&quot;页面可以查看 DAG 成员资格和操作状态，并配置 DAG 的见证服务器、见证目录和自动网络配置：
    
      - **见证服务器**   DAG 的见证服务器的主机名或完全限定域名 (FQDN)。虽然这是所有 DAG 的必需属性，但是存在偶数数量的 DAG 成员时会使用见证服务器，群集使用的仲裁模型为\&quot;节点和文件共享多数\&quot;。
    
      - **见证目录**   用于在见证服务器上存储 witness.log 文件的目录的完整路径。虽然这是所有 DAG 的必需属性，但是使用仅当 DAG 见证服务器时才会使用见证目录。
    
      - **操作服务器**   显示 DAG 成员及其当前操作状态列表的只读字段。
    
      - **手动配置数据库组网络**   如果要手动配置所有 DAG 网络，请选中此框。如果将此复选框保留为清除状态，则系统将根据网络接口配置来自动配置 DAG 网络。如果复选框已清除，则应针对 DAG 的管理使用禁用 **Set-DatabaseAvailabilityGroupNetwork** 和 **New-DatabaseAvailabilityGroupNetwork** Cmdlet。

4.  
    
    使用\&quot;IP 地址\&quot;页面可查看并修改分配给 DAG 的 IP 地址：
    
      - 选择现有 IP 地址并单击 ![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 可修改它。
    
      - 选择现有 IP 地址并单击减号图标（删除）可删除它。
    
      - 输入 IP 地址并单击 ![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可将其添加到 DAG。

5.  
    
    单击\&quot;保存\&quot;可保存所做的任何更改。

## 使用命令行管理程序配置数据库可用性组属性

本示例将名为 DAG1 的 DAG 的见证目录设置为 C:\\DAG1DIR。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessDirectory C:\DAG1DIR

本示例预配置 CAS3 的备用见证服务器，以及为 DAG DAG1 的 C:\\DAGFileShareWitnesses\\DAG1.contoso.com 预配置备用见证目录。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGFileShareWitnesses\DAG1.contoso.com -AlternateWitnessServer CAS3

本示例配置名为 DAG1 的 DAG 以使用动态主机配置协议 (DHCP) 获得 IP 地址。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 0.0.0.0

本示例配置名为 DAG1 的 DAG 以使用静态 IP 地址 10.0.0.8。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8

本示例使用多个静态 IP 地址配置名为 DAG1 的多子网 DAG。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatabaseAvailabilityGroupIPAddresses 10.0.0.8,10.0.1.8

此示例为 DAC 模式配置名为 DAG1 的 DAG。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly

本示例将名为 DAG1 的 DAG 的复制端口配置为 63132。

    Set-DatabaseAvailabilityGroup -Identity DAG1 -ReplicationPort 63132

> [!NOTE]
> 更改 DAG 默认的复制端口后，必须手动修改 DAG 每个成员上的 Windows 防火墙例外，以允许通过指定的端口进行通信。


## 您如何知道这有效？

若要验证是否成功配置了 DAG，请执行以下操作：

  - 在命令行管理程序中，运行以下命令来显示 DAG 配置设置并验证是否成功配置了 DAG。
    
        Get-DatabaseAvailabilityGroup <DAGName> | Format-List

## 详细信息

[创建数据库可用性组](create-a-database-availability-group-exchange-2013-help.md)

[删除数据库可用性组](remove-a-database-availability-group-exchange-2013-help.md)

[创建数据库可用性组网络](create-a-database-availability-group-network-exchange-2013-help.md)

[管理数据库可用性组成员身份](manage-database-availability-group-membership-exchange-2013-help.md)

[Get-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd351226\(v=exchg.150\))

[Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\))

