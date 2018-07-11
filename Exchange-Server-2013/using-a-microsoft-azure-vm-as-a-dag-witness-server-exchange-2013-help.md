---
title: '使用 Microsoft Azure VM 作为 DAG 见证服务器: Exchange 2013 Help'
TOCTitle: 使用 Microsoft Azure VM 作为 DAG 见证服务器
ms:assetid: 03d1e215-518b-4b48-bfcd-8d187ff8f5ef
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn903504(v=EXCHG.150)
ms:contentKeyID: 63892330
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 Microsoft Azure VM 作为 DAG 见证服务器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

通过 Exchange Server 2013，您可以针对自动数据中心故障转移在数据库可用性组 (DAG) 中配置您的邮箱数据库。该配置需要三个独立的物理位置：用于邮箱服务器的两个数据中心以及存放 DAG 的见证服务器的第三个位置。通过将 Microsoft Azure 文件服务器虚拟机用作 DAG 的见证服务器，仅具有两个物理位置的组织现在也可以利用自动数据中心故障转移。

本文重点介绍 Microsoft Azure 上的 DAG 见证的放置，并假设您已熟知站点恢复概念且已具有跨越两个数据中心的功能完整的 DAG 基础结构。如果您尚未配置您的 DAG 基础结构，我们建议您首先阅读以下文章：

[高可用性和站点恢复](high-availability-and-site-resilience-exchange-2013-help.md)

[数据库可用性组 (DAG)](database-availability-groups-dags-exchange-2013-help.md)

[对高可用性和站点恢复的规划](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

## Microsoft Azure 的更改

该配置需要一个多站点 VPN。通过站点到站点 VPN 连接，可以始终将您组织的网络连接到 Microsoft Azure。但是，Azure 过去只支持单个站点到站点 VPN。由于跨三个数据中心配置 DAG 及其见证需要多个站点到站点 VPN，因此最初无法在 Azure VM 上放置 DAG 见证。

2014 年 6 月，Microsoft Azure 引入了多站点 VPN 支持，让组织可以将多个数据中心连接到同一个 Azure 虚拟网络。这一更改也使得具有两个数据中心的组织能够将 Microsoft Azure 用作放置 DAG 见证服务器的第三个位置。要了解有关 Azure 中的多站点 VPN 功能的更多信息，请参阅[配置多站点 VPN](http://go.microsoft.com/fwlink/?linkid=522621)。

> [!NOTE]  
> 该配置使用 Azure 虚拟机和多站点 VPN 来部署见证服务器，而无需使用 Azure 云见证。


## Microsoft Azure 文件服务器见证

下图简要介绍了将 Microsoft Azure 文件服务器 VM 用作 DAG 见证的过程。您需要一个 Azure 虚拟网络、一个将您的数据中心连接到 Azure 虚拟网络的多站点 VPN、一个域控制器以及一个部署在 Azure 虚拟机上的文件服务器。

> [!NOTE]  
> 从技术上讲，使用单个 Azure VM 即可实现这一目的并将文件见证共享放置在域控制器上。但是，这将导致不必要的特权提升。因此，不建议使用此配置。


**Microsoft Azure 上的 DAG 见证服务器**

![Azure 上的 Exchange DAG 见证概述](images/Dn903504.7cbda882-bbae-4be7-b0ea-60947b8aa4ef(EXCHG.150).png "Azure 上的 Exchange DAG 见证概述")

要为您的 DAG 见证使用 Microsoft Azure VM，需要做的第一件事就是进行订阅。请参阅[如何购买 Azure](http://go.microsoft.com/fwlink/?linkid=398989)，了解订阅 Azure 的最佳方法。

订阅 Azure 后，您需要按顺序执行以下操作：

1.  准备 Microsoft Azure 虚拟网络

2.  配置多站点 VPN

3.  配置虚拟机

4.  配置 DAG 见证

> [!NOTE]  
> 本文中指南的大部分内容都涉及 Microsoft Azure 配置。因此，必要时将使用 Azure 文档的链接。


## 先决条件

  - 两个能够支持 Exchange 高可用性和站点恢复部署的数据中心。有关详细信息，请参阅[对高可用性和站点恢复的规划](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)

  - 适用于每个站点中的 VPN 网关的公用 IP 地址（不在 NAT 的后面）

  - 每个站点中与 Microsoft Azure 兼容的 VPN 设备。有关兼容设备的详细信息，请参阅[关于用于虚拟网络的 VPN 设备](http://go.microsoft.com/fwlink/?linkid=522619)

  - 熟悉 DAG 概念和管理

  - 熟悉 Windows PowerShell

## 阶段 1：准备 Microsoft Azure 虚拟网络

配置 Microsoft Azure 网络是部署过程最关键的部分。在此阶段结束时，您将拥有功能完备的 Azure 虚拟网络，且该虚拟网络已通过多站点 VPN 连接到您的两个数据中心。

## 注册 DNS 服务器

由于该配置需要在内部部署服务器和 Azure VM 之间进行名称解析，因此您需要将 Azure 配置为使用您自己的 DNS 服务器。[名称解析 (DNS)](http://msdn.microsoft.com/zh-cn/library/azure/jj156088.aspx) 主题概述了 Azure 中的名称解析。

要注册您的 DNS 服务器，请执行以下操作：

1.  在 Azure 门户中，转到“网络”，然后单击“新建”。

2.  单击“网络服务”\>“虚拟网络”\>“注册 DNS 服务器”。

3.  键入 DNS 服务器的名称和 IP 地址。此处指定的名称是指在管理门户中使用的逻辑名称，无需匹配 DNS 服务器的实际名称。

4.  对于您要添加的其他所有 DNS 服务器，重复步骤 1 到步骤 3。
    
    > [!NOTE]  
    > 不会按照轮循机制方式使用您注册的 DNS 服务器。Azure VM 将使用列出的第一个 DNS 服务器，并且只有在第一个服务器不可用的情况下才使用其他服务器。


5.  重复步骤 1 到步骤 3，添加您将要为部署到 Microsoft Azure 上的域控制器使用的 IP 地址。

## 在 Azure 中创建本地（内部部署）网络对象

接下来，要创建表示 Microsoft Azure 中的数据中心的逻辑网络对象，请执行以下操作：

1.  在 Azure 门户中，转到“网络”，然后单击“新建”。

2.  单击“网络服务”\>“虚拟网络”\>“添加本地网络”。

3.  键入第一个数据中心站点的名称和位于该站点上的 VPN 设备的 IP 地址。该 IP 地址必须是静态公用 IP 地址，而非 NAT 后面的。

4.  在接下来的屏幕上，为您的第一个站点指定 IP 子网。

5.  对第二个站点重复步骤 1 到步骤 4。

## 创建 Azure 虚拟网络

现在，要创建由 VM 使用的 Azure 虚拟网络，请执行以下操作：

1.  在 Azure 门户中，转到“网络”，然后单击“新建”。

2.  单击“网络服务”\>“虚拟网络”\>“自定义创建”。

3.  在“虚拟网络详细信息”页面上，指定虚拟网络的名称并为该网络选择一个地理位置。

4.  在“DNS 服务器和 VPN 连接”页面上，验证您之前注册的 DNS 服务器是否作为 DNS 服务器列出。

5.  选中“站点到站点连接”下的“配置站点到站点 VPN”复选框。
    
    > [!IMPORTANT]  
    > 切勿选中“使用 ExpressRoute”，因为这将阻止设置多站点 VPN 所需的必要配置更改。


6.  在“本地网络”下，选择您配置的两个内部部署网络中的一个。

7.  在“虚拟网络地址空间”页面中，指定您将为 Azure 虚拟网络使用的 IP 地址范围。

## 检查点：检查网络配置

此时，转到“网络”后，您将看到您配置的虚拟网络位于“虚拟网络”下，您的本地站点位于“本地网络”下，您的注册 DNS 服务器位于“DNS 服务器”下。

## 阶段 2：配置多站点 VPN

下一步是建立到您的内部部署站点的 VPN 网关。为此，您需要：

1.  使用 Azure 门户创建您的一个站点的 VPN 网关。

2.  导出虚拟网络配置设置。

3.  修改多站点 VPN 的配置文件。

4.  导入更新的 Azure 网络配置。

5.  记录 Azure 网关 IP 地址和预共享密钥。

6.  配置内部部署 VPN 设备。

有关配置多站点 VPN 的详细信息，请参阅[配置多站点 VPN](http://go.microsoft.com/fwlink/?linkid=522621)。

## 建立您的第一个站点的 VPN 网关

在创建虚拟网关时，注意您已指定该网关将连接到您的第一个内部部署站点。在转到虚拟网络仪表板时，您将看到该网关尚未创建。

要在 Azure 端建立 VPN 网关，请按照[在管理门户中配置虚拟网络网关](http://msdn.microsoft.com/zh-cn/library/azure/jj156210.aspx)的[启动虚拟网络网关](http://msdn.microsoft.com/zh-cn/library/azure/jj156210.aspx#bkmk_startgateway)部分中的说明操作。

> [!IMPORTANT]  
> 仅执行该文章的“启动虚拟网络网关”部分中的步骤，请勿继续执行后续操作。


## 导出虚拟网络配置设置

Azure 管理门户当前不允许您配置多站点 VPN。对于此配置，您需要将虚拟网络配置设置导出到 XML 文件，然后修改该文件。要导出您的设置，请按照[将虚拟网络设置导出到网络配置文件](http://msdn.microsoft.com/zh-cn/library/azure/dn133804.aspx)中的说明操作。

## 修改多站点 VPN 的网络配置设置

在任意 XML 编辑器中打开您导出的文件。到您的内部部署站点的网关连接列在“ConnectionsToLocalNetwork”部分中。在 XML 文件中查找该词语，以找到相应部分。配置文件中的此部分看上去如下所示（假设您为本地站点创建的站点名称是“站点 A”）。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

要配置您的第二个站点，在“ConnectionsToLocalNetwork”部分下添加另一个“LocalNetworkSiteRef”部分。更新的配置文件中的此部分看上去如下所示（假设您的第二个本地站点的站点名称是“站点 B”）。

    <ConnectionsToLocalNetwork>
    
        <LocalNetworkSiteRef name="Site A">
    
            <Connection type="IPsec" />
    
        <LocalNetworkSiteRef name="Site B">
    
            <Connection type="IPsec" />
    
    </LocalNetworkSiteRef>

保存更新的配置设置文件。

## 导入虚拟网络配置设置

您添加到配置文件的第二个站点引用将触发 Microsoft Azure 创建新的隧道。根据[导入网络配置文件](http://msdn.microsoft.com/zh-cn/library/azure/jj156213.aspx)中的说明，导入更新的文件。导入完成后，虚拟网络仪表板将显示您的两个本地站点的网关连接。

## 记录 Azure 网关 IP 地址和预共享密钥

导入新的网络配置设置后，虚拟网络仪表板将显示 Azure 网关的 IP 地址。该 IP 地址是您的两个站点上的 VPN 设备将要连接到的 IP 地址。记录此 IP 地址，以供参考。

您还需要获取创建的每个隧道的预共享 IPsec/IKE 密钥。您将使用这些密钥和 Azure 网关 IP 地址来配置您的内部部署 VPN 设备。

您需要使用 PowerShell 获取预共享密钥。如果您不熟悉如何使用 PowerShell 管理 Azure，请参阅 [Azure PowerShell](http://msdn.microsoft.com/zh-cn/library/azure/jj156055.aspx)。

使用 [Get-AzureVNetGatewayKey](http://msdn.microsoft.com/zh-cn/library/azure/dn495198.aspx) cmdlet 提取预共享密钥。为每个隧道运行一次此 cmdlet。以下示例展示了提取虚拟网络“Azure 站点”和站点“站点 A”和“站点 B”之间的隧道的密钥所需运行的命令。在本例中，输出结果将被保存到单独的文件中。另外，您可以将这些密钥传输到其他 PowerShell cmdlet 或在脚本中使用它们。

    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site A" > C:\Keys\KeysForTunnelToSiteA.txt 
    
    Get-AzureVNETGatewayKey -VNetName "Azure Site" -LocalNetworkSiteName "Site B" > C:\Keys\KeysForTunnelToSiteB.txt

## 配置内部部署 VPN 设备

Microsoft Azure 为支持的 VPN 设备提供 VPN 设备配置脚本。单击虚拟网络仪表板上的“下载 VPN 设备脚本”链接，下载适用于您的 VPN 设备的相应脚本。

当您建立虚拟网络时，您下载的脚本含有您配置的第一个站点的配置设置，且可用来配置该站点的 VPN 设备。例如，在创建虚拟网络时，如果您将站点 A 指定为“本地网络”，则可以为站点 A 使用 VPN 设备脚本。但是，您需要对其进行修改，才能配置站点 B 的 VPN 设备。具体来说，您需要更新预共享密钥，以匹配第二个站点的密钥。

例如，如果您为站点使用的是路由和远程访问服务 (RRAS) VPN 设备，您将需要执行以下操作：

1.  在任意文本编辑器中打开配置脚本。

2.  查找 `#Add S2S VPN interface` 部分。

3.  在此部分中查找 **Add-VpnS2SInterface** 命令。验证 *SharedSecret* 参数的值是否匹配您用于配置 VPN 设备的站点的预共享密钥。

其他设备可能需要额外的验证。例如，适用于 Cisco 设备的配置脚本使用本地 IP 地址范围设置 ACL 规则。您需要检查并验证对配置脚本中的本地站点的所有引用，然后再进行使用。有关详细信息，请参阅以下主题：

[路由和远程访问服务 (RRAS) 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133801.aspx)

[Cisco ASR 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133802.aspx)

[Cisco ISR 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133800.aspx)

[Juniper SRX 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133794.aspx)

[Juniper J 系列模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133799.aspx)

[Juniper ISG 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133797.aspx)

[Juniper SSG 模板](http://msdn.microsoft.com/zh-cn/library/azure/dn133796.aspx)

## 检查点：检查 VPN 状态

此时，您的两个站点都已通过 VPN 网关连接到 Azure 虚拟网络。通过在 PowerShell 中运行以下命令，您可以验证多站点 VPN 的状态。

    Get-AzureVnetConnection -VNetName "Azure Site" | Format-Table LocalNetworkSiteName, ConnectivityState

如果两个隧道都在正常运行，则此命令的输出结果看上去将如下所示：

    LocalNetworkSiteName    ConnectivityState
    
    --------------------    -----------------
    
    Site A                  Connected
    
    Site B                  Connected

通过在 Azure 管理门户中查看虚拟网络仪表板，您还可以对连接进行验证。两个站点的“状态”列将显示为“已连接”。

> [!NOTE]  
> 成功建立连接后，状态更改可能需要几分钟才能在 Azure 管理门户中显示。


## 阶段 3：配置虚拟机

对于此部署，您需要在 Microsoft Azure 中创建至少两个虚拟机：一个域控制器和一个充当 DAG 见证的文件服务器。

1.  根据[创建运行 Windows 的虚拟机](http://azure.microsoft.com/zh-cn/documentation/articles/virtual-machines-windows-tutorial/)中的说明，为您的域控制器和文件服务器创建虚拟机。在指定虚拟机的设置时，确保选择您为“地区/地缘组/虚拟网络”创建的虚拟网络。

2.  使用 Azure PowerShell 为域控制器和文件服务器指定首选 IP 地址。当您为 VM 指定首选 IP 地址时，该地址需要更新，这将需要重启 VM。以下示例将 Azure-DC 和 Azure-FSW 的 IP 地址分别设置为 10.0.0.10 和 10.0.0.11。
    
        Get-AzureVM Azure-DC | Set-AzureStaticVNetIP -IPAddress 10.0.0.10 | Update-AzureVM
        
        Get-AzureVM Azure-FSW | Set-AzureStaticVNetIP -IPAddress 10.0.0.11 | Update-AzureVM
    
    > [!NOTE]  
    > 带有首选 IP 地址的 VM 将尝试使用该地址。但是，如果该地址已被分配给不同的 VM，则带有首选 IP 地址配置的 VM 将不会启动。为了避免这种情况，确保您使用的 IP 地址没有分配给其他 VM。有关详细信息，请参阅<a href="http://msdn.microsoft.com/zh-cn/library/azure/dn630228.aspx">为 VM 配置静态内部 IP 地址</a>。


3.  使用您组织采用的标准设置 Azure 上的域控制器 VM。

4.  按照 Exchange DAG 见证的先决条件准备文件服务器：
    
    1.  通过“添加角色和功能向导”或 [Add-WindowsFeature](http://technet.microsoft.com/zh-cn/library/ee662309.aspx) cmdlet，添加文件服务器角色。
    
    2.  将 Exchange 信任的子系统通用安全组添加到本地管理员组。

## 检查点：检查虚拟机状态

此时，您的虚拟机应该可以正常运行，并且能够与您的两个内部部署数据中心中的服务器进行通信：

  - 验证 Azure 中的域控制器是否正在复制您的内部部署域控制器。

  - 验证您是否可以按照名称找到 Azure 上的文件服务器并在 Exchange 服务器中建立 SMB 连接。

  - 验证您是否可以按照 Azure 上的文件服务器中的名称找到 Exchange 服务器。

## 阶段 4：配置 DAG 见证

最后，您需要将 DAG 配置为使用新的见证服务器。默认情况下，Exchange 使用 C:\\DAGFileShareWitnesses 作为您的见证服务器上的文件共享见证路径。如果您使用的是自定义文件路径，您还应该为特定的共享更新见证目录。

1.  连接到 Exchange 命令行管理程序。

2.  运行以下命令以配置您的 DAG 的见证服务器。
    
        Set-DatabaseAvailabilityGroup -Identity DAG1 -WitnessServer Azure-FSW

有关详细信息，请参阅以下主题：

[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)

[Set-DatabaseAvailabilityGroup](http://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\).aspx)

## 检查点：验证 DAG 文件共享见证

此时，您已配置 DAG，可以将 Azure 上的文件服务器用作您的 DAG 见证。执行以下操作以验证您的配置：

1.  运行以下命令对 DAG 配置进行验证。
    
        Get-DatabaseAvailabilityGroup -Identity DAG1 -Status | Format-List Name, WitnessServer, WitnessDirectory, WitnessShareInUse
    
    验证 *WitnessServer* 参数是否设置为 Azure 上的文件服务器，*WitnessDirectory* 参数是否设置为正确的路径以及 *WitnessShareInUse* 参数是否显示 **Primary**。

2.  如果 DAG 包含偶数个节点，则将配置文件共享见证。运行以下命令，对群集属性中的文件共享见证设置进行验证。*SharePath* 参数的值应该指向文件服务器并显示正确的路径。
    
        Get-ClusterResource -Cluster MBX1 | Get-ClusterParameter | Format-List

3.  接下来，运行以下命令对“文件共享见证”群集资源的状态进行验证。群集资源的 *State* 应显示 **Online**。
    
        Get-ClusterResource -Cluster MBX1

4.  最后，通过检查“文件资源管理器”中的文件夹和服务器管理器中的共享，验证是否已成功地在文件服务器上创建共享。

## 另请参阅


[对高可用性和站点恢复的规划](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
[切换和故障转移](switchovers-and-failovers-exchange-2013-help.md)  
[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)

