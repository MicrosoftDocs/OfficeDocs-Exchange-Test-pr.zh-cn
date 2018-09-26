---
title: '部署高可用性和站点恢复: Exchange 2013 Help'
TOCTitle: 部署高可用性和站点恢复
ms:assetid: 4c4e00a4-1f57-4fdb-b9b2-2779abf381a9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638129(v=EXCHG.150)
ms:contentKeyID: 50490515
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署高可用性和站点恢复

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2013 使用称为“增量部署”的概念来实现高可用性和站点恢复。只需将两台或更多 Exchange 2013 邮箱服务器都安装为独立服务器，然后根据需要增量配置这些服务器和邮箱数据库来实现高可用性和站点恢复。

## 部署过程概述

尽管每个组织使用的实际步骤可能稍有不同，但是在高可用性配置或站点恢复配置中部署 Exchange 2013 的总体过程通常是相同的。在为构建和部署数据库可用性组 (DAG) 执行必要的计划和设计任务并创建邮箱数据库副本之后，您将：

1.  创建一个 DAG。有关详细步骤，请参阅[创建数据库可用性组](create-a-database-availability-group-exchange-2013-help.md)。

2.  如有必要，请预留群集名称对象 (CNO)。部署具有运行 Windows Server 2012 的邮箱服务器的 DAG 时，需要预先暂存 CNO。如果您部署的 DAG 不带有管理访问点，但使用运行 Windows Server 2012 R2 的邮箱服务器，则无需预先暂存 CNO。如果在环境中创建计算机帐户受到限制或在默认计算机容器以外的容器中创建计算机帐户，则同样需要预先暂存。有关详细步骤，请参阅[为数据库可用性组预留群集名称对象](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

3.  向 DAG 添加两个或多个邮箱服务器。有关详细步骤，请参阅[管理数据库可用性组成员身份](manage-database-availability-group-membership-exchange-2013-help.md)。

4.  根据需要配置 DAG 属性：
    
    1.  有选择地配置 DAG 加密和压缩、复制端口、DAG IP 地址和其他 DAG 属性。有关详细步骤，请参阅[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)。
    
    2.  对 DAG 启用数据中心激活协调 (DAC) 模式。这可防止 DAG 在执行数据中心切换后、再切换回主数据中心期间出现数据库级的网络分区状态，并可实现内置 DAG 恢复 cmdlet 的使用。有关详细信息，请参阅[数据中心激活协调模式](datacenter-activation-coordination-mode-exchange-2013-help.md)。

5.  在 DAG 中跨邮箱服务器添加邮箱数据库副本。有关详细步骤，请参阅[添加邮箱数据库副本](add-a-mailbox-database-copy-exchange-2013-help.md)。

## 部署示例：在两个数据中心中部署四个成员 DAG

此示例详细描述了名为 Contoso, Ltd. 的组织如何配置和部署跨两个物理位置扩展的四成员 DAG：华盛顿州雷德蒙德市和俄勒冈州波特兰市。

## 基本基础结构

每个位置包含操作基于 Exchange 2013 的邮件基础结构所必需的基础结构元素，即：

  - 目录服务（Active Directory 或 Active Directory 域服务 (AD DS))

  - 域名系统 (DNS) 名称解析

  - 多个 Exchange 2013 客户端访问服务器

  - 多个 Exchange 2013 邮箱服务器

下图说明了 Contoso 的配置。

**跨两个站点扩展的数据库可用性组**

![扩展到两个站点的数据库可用性组](images/Dd638129.1c326fd4-3c7b-4416-a63d-fbfdd0cc6b18(EXCHG.150).gif "扩展到两个站点的数据库可用性组")

## 网络配置

如上图所示，该解决方案涉及多个子网和多个网络的使用。DAG 中的每个邮箱服务器在单独的子网上都有两个网络适配器。在每个邮箱服务器中，一个网络适配器用于 MAPI 网络 (192.168.*x*.*x*)，一个网络适配器用于复制网络 (10.0.*x*.*x*)。仅 MAPI 网络提供指向 Active Directory、DNS 服务、其他 Exchange 服务器和客户端的连接。每个成员中用于复制网络的适配器仅提供指向 DAG 其他成员中的复制网络适配器的连接。

下表中详细介绍了每个节点中的每个网络适配器的设置。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>IPv4 地址</th>
<th>子网掩码</th>
<th>默认网关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MBX1 (MAPI)</p></td>
<td><p>192.168.1.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>MBX2 (MAPI)</p></td>
<td><p>192.168.1.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX3 (MAPI)</p></td>
<td><p>192.168.2.4</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="even">
<td><p>MBX4 (MAPI)</p></td>
<td><p>192.168.2.5</p></td>
<td><p>255.255.255.0</p></td>
<td><p>192.168.2.1</p></td>
</tr>
<tr class="odd">
<td><p>MBX1（复制）</p></td>
<td><p>10.0.1.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>MBX2（复制）</p></td>
<td><p>10.0.1.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>MBX3（复制）</p></td>
<td><p>10.0.2.4</p></td>
<td><p>255.255.0.0</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>MBX4（复制）</p></td>
<td><p>10.0.2.5</p></td>
<td><p>255.255.0.0</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>


如上表所示，用于复制网络的适配器不使用默认网关。为了在每个复制网络适配器之间提供网络连接，Contoso 使用永久静态路由（这些路由使用 Netsh.exe 工具进行配置）。

为了在 MBX1 和 MBX2 上为复制网络适配器配置路由，在每个服务器上运行以下命令。

```powershell
netsh interface ipv4 add route 10.0.2.0/24 <NetworkName> 10.0.1.254
```

为了在 MBX3 和 MBX4 上为复制网络适配器配置路由，在每个服务器上运行以下命令。

```powershell
netsh interface ipv4 add route 10.0.1.0/24 <NetworkName> 10.0.2.254
```

还配置了下列其他网络设置：

  - 为每个 DAG 成员的 MAPI 网络适配器选中“在 DNS 中注册此连接的地址”复选框，并为每个复制网络适配器清除该复选框。

  - 为每个 DAG 成员的 MAPI 网络适配器配置至少一个 DNS 服务器地址，不要为复制网络适配器配置任何 DNS 服务器地址。为实现冗余，Contoso 将多个 DNS 服务器地址用于其 MAPI 网络适配器。

  - Contoso 不使用 Windows 防火墙，并已在其服务器上关闭该防火墙。

在配置了网络适配器之后，Contoso 准备创建 DAG，并将邮箱服务器添加到 DAG。

## 数据库可用性组的创建和配置

管理员已决定创建执行多个任务的 Windows PowerShell 命令行接口脚本：

  - 使用 [New-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd351107\(v=exchg.150\)) cmdlet 创建 DAG。因为 REDMOND 被视为主数据中心，所以 Contoso 选择在相同数据中心中使用见证服务器，即 CAS1。

  - 使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) cmdlet 预配置备用见证服务器和备用见证目录，以备数据中心切换之需。

  - 使用 [Add-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd298049\(v=exchg.150\)) cmdlet 将四个邮箱服务器中的每个邮箱服务器添加到 DAG。

  - 使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) cmdlet 为 DAC 模式配置 DAG。有关 DAC 模式的详细信息，请参阅[数据中心激活协调模式](datacenter-activation-coordination-mode-exchange-2013-help.md)。

下面是在脚本中使用的命令：

```PowerShell
New-DatabaseAvailabilityGroup -Name DAG1 -WitnessServer CAS1 -WitnessDirectory C:\DAGWitness\DAG1.contoso.com -DatabaseAvailabilityGroupIPAddresses 192.168.1.8,192.168.2.8
```

上述命令将创建 DAG DAG1，将 CAS1 配置为见证服务器，配置一个特定的见证目录 (C:\\DAGWitness\\DAG1.contoso.com)，并为 DAG 配置两个 IP 地址（为 MAPI 网络上的每个子网配置一个）。

```PowerShell
Set-DatabaseAvailabilityGroup -Identity DAG1 -AlternateWitnessDirectory C:\DAGWitness\DAG1.contoso.com -AlternateWitnessServer CAS4
```

上述命令将 DAG1 配置为使用 CAS4 的备用见证服务器，以及 CAS4（使用在 CAS1 上配置的相同路径）上的备用见证目录。

> [!NOTE]  
> 使用相同路径不是必需的；Contoso 选择这样做是为了标准化其配置。


```PowerShell
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX1
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX3
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX2
Add-DatabaseAvailabilityGroupServer -Identity DAG1 -MailboxServer MBX4
```

上述命令将每个邮箱服务器添加到 DAG（一次添加一个）。这些命令还在每个邮箱服务器上安装 Windows 故障转移群集组件（如果尚未安装）、创建故障转移群集，并将每个邮箱服务器加入到最近创建的群集。

```powershell
Set-DatabaseAvailabilityGroup -Identity DAG1 -DatacenterActivationMode DagOnly
```

上述命令为 DAG 启用 DAC 模式。

## 邮箱数据库和邮箱数据库副本

在创建 DAG 并将邮箱服务器添加到 DAG 之后，Contoso 准备创建邮箱数据库和邮箱数据库副本。为符合抗故障标准，Contoso 计划为每个邮箱数据库配置三个非延迟数据库副本和一个延迟数据库副本。延迟副本配置了为期三天的日志重播延迟。

此配置为每个数据库总共提供四个副本（一个活动副本、两个非延迟被动副本和一个延迟被动副本）。Contoso 计划为每个服务器提供四个活动数据库。由于每个服务器具有四个活动数据库，每个数据库具有三个被动副本，Contoso 解决方案共包含 16 个数据库副本。

如下图所示，Contoso 在将平衡方法引入其数据库布局。

**Contoso, Ltd 的数据库副本布局**

![Contoso, Ltd 的数据库副本布局](images/Dd638129.41d0c78e-ccaf-4b67-8bab-6fb344668ead(EXCHG.150).gif "Contoso, Ltd 的数据库副本布局")

每个邮箱服务器承载一个活动邮箱数据库副本、两个非延迟被动数据库副本和一个延迟被动数据库副本。其他站点中的邮箱服务器上承载每个活动邮箱数据库的延迟副本。

为创建此配置，管理员需运行几个命令。

在 MBX1 上运行以下命令。

```PowerShell    
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -SuspendComment "Seed from MBX4" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB1\MBX3 -SourceServer MBX4
    Suspend-MailboxDatabaseCopy -Identity DB1\MBX3 -ActivationOnly
```    

在 MBX2 上运行以下命令。

```PowerShell
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -SuspendComment "Seed from MBX3" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB2\MBX4 -SourceServer MBX3
    Suspend-MailboxDatabaseCopy -Identity DB2\MBX4 -ActivationOnly
```    

在 MBX3 上运行以下命令。

```PowerShell
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX4
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX2
    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX1 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -SuspendComment "Seed from MBX2" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB3\MBX1 -SourceServer MBX2
    Suspend-MailboxDatabaseCopy -Identity DB3\MBX1 -ActivationOnly
```    

在 MBX4 上运行以下命令。

```PowerShell    
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX3
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX1
    Add-MailboxDatabaseCopy -Identity DB4 -MailboxServer MBX2 -ReplayLagTime 3.00:00:00 -SeedingPostponed
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -SuspendComment "Seed from MBX1" -Confirm:$False
    Update-MailboxDatabaseCopy -Identity DB4\MBX2 -SourceServer MBX1
    Suspend-MailboxDatabaseCopy -Identity DB4\MBX2 -ActivationOnly
```    

在上述 **Add-MailboxDatabaseCopy** cmdlet 示例中，未指定 *ActivationPreference* 参数。任务将自动递增添加的每个副本的激活首选项编号。原始数据库的首选项编号始终为 1。使用 **Add-MailboxDatabaseCopy** cmdlet 添加的第一个副本自动获得首选项编号 2。假定未删除任何副本，则添加的下一个副本自动获得首选项编号 3 等等。因此，在上述示例中，与活动副本位于同一数据中心中的被动副本的激活首选项编号为 2；远程数据中心中的非延迟被动副本的激活首选项编号为 3，远程数据中心中的延迟被动副本的激活首选项编号为 4。

尽管在另一位置中跨 WAN 的每个活动数据库有两个副本，但是通过 WAN 只执行一次种子设定。这是因为 Contoso 在利用 Exchange 2013 功能，将数据库的被动副本用作设定种子的源。结合使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 和 *SeedingPostponed* 参数可以阻止该任务为正在创建的新数据库副本自动设定种子。然后，管理员可以挂起取消设定种子的副本，通过结合使用 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 和 *SourceServer* 参数，管理员可以指定数据库的本地副本作为设定种子操作的源。结果，对添加到每个位置的第二个数据库副本设定种子可本地发生，不需要通过 WAN。

> [!NOTE]  
> 在上述示例中，非延迟数据库副本通过 WAN 设定种子，然后使用该副本为与非延迟副本位于同一数据中心中的数据库的延迟副本设定种子。


Contoso 将每个邮箱数据库的被动副本之一配置为延迟数据库副本，以防范非常少见的灾难性数据库逻辑损坏。因此，通过结合使用 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) cmdlet 和 *ActivationOnly* 参数，管理员要将延迟副本配置为阻止激活。这可确保在发生数据库或服务器故障转移时，延迟数据库副本不会被激活。

## 验证解决方案

在部署和配置解决方案之后，将生产邮箱移入 DAG 的数据库之前，管理员应执行几个任务来验证解决方案的准备情况。应当使用多个方法测试和检查解决方案，其中包括故障模拟方法。若要验证解决方案，管理员应执行几个任务。

若要验证 DAG 的总体运行状况，管理员应运行 [Test-ReplicationHealth](https://technet.microsoft.com/zh-cn/library/bb691314\(v=exchg.150\)) cmdlet。此 cmdlet 将检查复制和重播状态的多个方面，以提供有关 DAG 中的每个邮箱服务器和数据库副本的信息。

若要验证复制和重播活动，管理员应运行 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\)) cmdlet。此 cmdlet 可提供有关特定服务器上特定邮箱数据库副本或所有邮箱数据库副本的实时状态信息。有关监视 DAG 中复制的数据库的运行状况和状态的详细信息，请参阅[监视数据库可用性组](monitoring-database-availability-groups-exchange-2013-help.md)。

若要验证切换是否按预期工作，管理员应使用 [Move-ActiveMailboxDatabase](https://technet.microsoft.com/zh-cn/library/dd298068\(v=exchg.150\)) cmdlet 执行一系列数据库切换和服务器切换。这些任务成功完成时，管理员应使用同一 cmdlet 将活动数据库副本移回其原始位置。

若要在各种故障场景中验证预期行为，管理员应执行模拟故障或实际导致故障发生的几个任务。例如，管理员可以：

  - 拔下 MBX1 上的电源线，从而触发服务器故障转移。管理员然后验证 DB1 是否在另一个服务器（基于激活首选项值，最好是 MBX2）上成为活动数据库。

  - 拔下 MBX2 上 MAPI 网络适配器的网络线缆，从而触发服务器故障转移。管理员然后验证 DB2 是否在另一个服务器（基于激活首选项值，最好是 MBX1）上成为活动数据库。

  - 使 DB3 的活动副本使用的磁盘脱机，从而触发数据库故障转移。管理员然后验证 DB3 是否在另一个服务器（基于激活首选项值，最好是 MBX4）上成为活动数据库。

基于业务需要，组织还可以测试其他故障情况。在模拟单个故障（如拔下电源插头）并验证解决方案的恢复行为之后，管理员可以将解决方案恢复为其原始配置状态。在某些情况下，可以针对多个并发故障测试解决方案。最后，在完成每个故障模拟之后，解决方案测试计划要确定解决方案是否恢复其原始配置。

此外，管理员可以决定在两个数据中心之间断开网络连接，从而模拟站点故障。执行数据中心切换需要涉及和协调的过程很多；但是，如果要部署的解决方案的目的是为邮件服务和数据提供站点恢复，则建议执行该过程。

## 过渡到运营状态

在部署解决方案之后，可以使用增量部署进一步对其进行扩展。此时，解决方案的管理也将转换为运营过程，在该过程中应执行以下任务：

  - 监视 DAG 和邮箱数据库副本的运行状况和状态。有关详细信息，请参阅[监视数据库可用性组](monitoring-database-availability-groups-exchange-2013-help.md)。

  - 根据需要执行数据库切换。有关如何执行数据库切换的详细步骤，请参阅[激活邮箱数据库副本](activate-a-mailbox-database-copy-exchange-2013-help.md)。

有关管理解决方案的详细信息，请参阅[管理高可用性和站点恢复](managing-high-availability-and-site-resilience-exchange-2013-help.md)。

