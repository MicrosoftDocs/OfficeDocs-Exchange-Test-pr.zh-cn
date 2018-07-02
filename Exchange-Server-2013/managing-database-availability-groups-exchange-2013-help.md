---
title: '管理数据库可用性组: Exchange 2013 Help'
TOCTitle: 管理数据库可用性组
ms:assetid: 74be3f97-ec0f-4d2a-b5d8-7770cc489919
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298065(v=EXCHG.150)
ms:contentKeyID: 50490926
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理数据库可用性组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-10-04_

数据库可用性组 (DAG) 是一组 Microsoft Exchange Server 2013 邮箱服务器（最多 16 个），提供从数据库、服务器或网络故障中自动执行数据库级恢复的功能。DAG 使用连续复制和 Windows 故障转移群集技术的子集来提供高可用性和站点恢复。DAG 中的邮箱服务器相互进行故障监视。邮箱服务器添加到 DAG 后，它会与 DAG 中的其他服务器协同工作，提供从数据库故障中自动执行数据库级恢复的功能。

创建 DAG 时，DAG 最初是空的。将第一个服务器添加到 DAG 时，将为 DAG 自动创建故障转移群集。此外，还将启动监视服务器的网络或故障的基础结构。然后，使用故障转移群集检测信号机制和群集数据库来跟踪和管理有关 DAG 可能快速更改的信息，比如数据库装入状态、复制状态和最后装入位置。

**目录**

创建 DAG

DAG 成员身份

配置 DAG 属性

DAG 网络

配置 DAG 成员

对 DAG 成员执行维护

关闭 DAG 成员

在 DAG 成员上安装更新

## 创建 DAG

可以在 Exchange 管理中心 (EAC) 中使用“新建数据库可用性组”向导，或在 Exchange 命令行管理程序中运行 **New-DatabaseAvailabilityGroup** cmdlet 来创建 DAG。创建 DAG 时，需提供 DAG 名称、可选的见证服务器及见证目录设置。此外，还可以为 DAG 分配一个或多个 IP 地址（可以使用静态 IP 地址，也可以使用动态主机配置协议 (DHCP) 为 DAG 自动分配必要的 IP 地址）。可以使用 *DatabaseAvailabilityGroupIpAddresses* 参数手动为 DAG 分配 IP 地址。如果省略此参数，则 DAG 会尝试使用网络中的 DHCP 服务器来获取 IP 地址。

如果您要创建一个将包含运行 Windows Server 2012 R2 的邮箱服务器的 DAG，您也可以选择创建一个不含群集管理访问点的 DAG。在这种情况下，群集在 Active Directory 中将不会有群集名称对象 (CNO)，群集核心资源组也不会包含网络名称资源或 IP 地址资源。

有关如何创建 DAG 的详细步骤，请参阅[创建数据库可用性组](create-a-database-availability-group-exchange-2013-help.md)。

创建 DAG 时，将在 Active Directory 中创建一个空对象，以代表具有指定名称且对象类为 **msExchMDBAvailabilityGroup** 的 DAG。

DAG 使用 Windows 故障转移群集技术的子集，如群集检测信号、群集网络以及群集数据库（用于存储更改的或可以快速更改的数据，例如数据库状态从活动更改为被动或相反的情况，或从装入更改为卸除或相反的情况）。因为 DAG 依赖于 Windows 故障转移群集，所以只能在运行 Windows Server 2008 R2 Enterprise 或 Datacenter 操作系统、Windows Server 2012 Standard 或 Datacenter 操作系统，或者 Windows Server 2012 R2 Standard 或 Datacenter 操作系统的 Exchange 2013 邮箱服务器上创建。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由 DAG 创建和使用的故障转移群集必须专用于 DAG。该群集不能用于任何其他高可用性解决方案或任何其他用途。例如，故障转移群集不能用于对其他应用程序或服务进行群集。不支持将某个 DAG 的基础故障转移群集用于该 DAG 以外的用途。</td>
</tr>
</tbody>
</table>


## DAG 见证服务器和见证目录

创建 DAG 时，需要为其指定一个不超过 15 个字符、在 Active Directory 林中唯一的名称。此外，每个 DAG 会配置一个见证服务器和见证目录。见证服务器及其目录仅当 DAG 中成员数为偶数时使用并且仅用于仲裁目的。不需要提前创建见证目录。Exchange 将在见证服务器上自动创建并保护该目录。目录不应用于 DAG 见证服务器之外的其他任何目的。

见证服务器的要求如下：

  - 见证服务器不能是 DAG 的成员。

  - 见证服务器必须与 DAG 位于同一个 Active Directory 林中。

  - 见证服务器必须运行受支持的 Windows Server 版本。有关详细信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 单个服务器可以充当多个 DAG 的见证。但是，每个 DAG 都需要其自己的见证目录。

无论将哪个服务器用作见证服务器，如果在预期的见证服务器上启用了 Windows 防火墙，则必须为文件和打印机共享启用 Windows 防火墙例外。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果指定的见证服务器不是 Exchange 2013 或 Exchange 2010 服务器，则必须在创建 DAG 之前将 Exchange 受信任子系统通用安全组 (USG) 添加到见证服务器上的本地 Administrators 组中。需要这些安全权限来确保 Exchange 可以根据需要在见证服务器上创建并共享目录。<br />
见证服务器使用 SMB 端口 445。</td>
</tr>
</tbody>
</table>


见证服务器和见证目录不需具有容错能力，也不需使用任何形式的冗余或高可用性。无需对见证服务器使用群集文件服务器或采用其他任何形式的恢复机制。其原因是多方面的。对于大型 DAG（例如，六个成员或更多），只有在发生多个故障时才需要见证服务器。由于六成员 DAG 可以承受多达两个投票者故障，而不会丢失仲裁，因此三个投票者发生故障后才需要见证服务器来维持仲裁。此外，如果故障影响到了当前的见证服务器（例如，由于硬件故障而丢失了见证服务器），则可以使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) cmdlet 配置新的见证服务器和见证目录（前提是拥有仲裁）。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果见证服务器丢失了存储内容，或有人更改了见证目录或共享权限，则还可以使用 <strong>Set-DatabaseAvailabilityGroup</strong> cmdlet 在原始位置配置见证服务器和见证目录。</td>
</tr>
</tbody>
</table>


## 见证服务器放置的注意事项

DAG 的见证服务器放置将取决于业务需求和组织的可用选项。Exchange 2013 支持在 Exchange 之前的版本中不推荐或不可用的新 DAG 配置选项。这些选项包括使用第三个位置，如第三个数据中心、分支机构或 Microsoft Azure 虚拟网络。

下表列出了不同部署方案中见证服务器放置的常规建议。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>部署方案</th>
<th>推荐</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在单个数据中心部署单个 DAG</p></td>
<td><p>查找相同数据中心中的见证服务器作为 DAG 成员</p></td>
</tr>
<tr class="even">
<td><p>在两个数据中心部署单个 DAG；没有其他可用位置</p></td>
<td><p>在 Microsoft Azure 虚拟网络上查找见证服务器来启用自动数据中心故障转移，或</p>
<p>在主数据中心查找见证服务器</p></td>
</tr>
<tr class="odd">
<td><p>在单个数据中心部署多个 DAG</p></td>
<td><p>查找相同数据中心中的见证服务器作为 DAG 成员。其他选项包括：</p>
<ul>
<li><p>为多个 DAG 使用相同的见证服务器</p></li>
<li><p>为不同的 DAG 使用 DAG 成员作为见证服务器</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>在两个数据中心中部署多个 DAG</p></td>
<td><p>在 Microsoft Azure 虚拟网络上查找见证服务器来启用自动数据中心故障转移，或</p>
<p>在数据中心查找视为每个 DAG 的主服务器的见证服务器。其他选项包括：</p>
<ul>
<li><p>为多个 DAG 使用相同的见证服务器</p></li>
<li><p>为不同的 DAG 使用 DAG 成员作为见证服务器</p>
<p></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>在两个以上数据中心部署单个或多个 DAG</p></td>
<td><p>在此配置中，见证服务器应位于您希望大多数仲裁投票位于其中的数据中心。</p></td>
</tr>
</tbody>
</table>


在两个数据中心中部署 DAG 后，Exchange 2013 中的新配置选项将使用第三个位置来托管见证服务器。如果组织具有带有网络基础结构的第三个位置，且该网络基础结构与影响部署了 DAG 的两个数据中心的网络故障分离开来，则可以在此第三个位置部署 DAG 的见证服务器，从而将 DAG 配置为可以自动将数据库故障转移到其他数据中心，以响应数据中心级别的故障事件。如果您的组织只有两个物理位置，则可以使用 Microsoft Azure 虚拟网络作为放置见证服务器的第三个位置。

## 在 DAG 创建过程中指定见证服务器和见证目录

创建 DAG 时，必须提供 DAG 的名称。您也可以选择指定见证服务器和见证目录。

创建 DAG 时，可以使用以下选项和行为组合：

  - 可以仅指定 DAG 的名称，将“见证服务器”和“见证目录”字段留空。在这种情况下，向导会在本地 Active Directory 站点中搜索没有安装邮箱服务器的客户端访问服务器，自动在该服务器上创建默认目录 (%SystemDrive%:\\DAGFileShareWitnesses\\\<*DAGFQDN*\>) 和默认共享 (\<*DAGFQDN*\>)，并将该客户端访问服务器用作见证服务器。例如，请考虑 CAS3 见证服务器，在其中的驱动器 C 上已安装了操作系统。在 contoso.com 域中名为 DAG1 的 DAG 使用默认见证目录 C:\\DAGFileShareWitnesses\\DAG1.contoso.com，该目录共享为 \\\\CAS3\\DAG1.contoso.com。

  - 可以指定 DAG 的名称、要使用的见证服务器以及要在见证服务器上创建并共享的目录。

  - 可以指定 DAG 的名称、要使用的见证服务器，并将“见证目录”字段留空。在这种情况下，向导会在指定的见证服务器上创建默认目录。

  - 可以指定 DAG 的名称、将“见证服务器”字段留空，并指定要在见证服务器上创建并共享的目录。在这种情况下，向导会搜索没有安装邮箱服务器的客户端访问服务器，自动在该服务器上创建指定的 DAG 并共享目录，并将该客户端访问服务器用作见证服务器。

DAG 形成后，最初使用多数节点仲裁模型。将第二个邮箱服务器添加到 DAG 后，仲裁将自动更改为多数节点和文件共享仲裁模型。发生此更改后，DAG 的群集将开始使用见证服务器来维持仲裁。如果见证目录不存在，Exchange 会自动创建该目录并将其共享，使 DAG 的 CNO 计算机帐户具有对该共享的完全控制权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支持使用属于分布式文件系统 (DFS) 命名空间的文件共享。</td>
</tr>
</tbody>
</table>


如果创建 DAG 之前在见证服务器上启用了 Windows 防火墙，那么防火墙可能会阻止创建 DAG。Exchange 使用 Windows Management Instrumentation (WMI) 在见证服务器上创建目录和文件共享。如果启用了见证服务器上的 Windows 防火墙，但没有针对 WMI 配置防火墙例外，那么 **New-DatabaseAvailabilityGroup** cmdlet 将会失败，并出现错误。如果指定了见证服务器，但未指定见证目录，则会收到以下错误消息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>该任务无法在服务器 &lt;<em>服务器名称</em>&gt; 上创建默认见证目录。请手动指定见证目录。</p></td>
</tr>
</tbody>
</table>


如果指定了见证服务器和见证目录，则会收到以下警告消息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>无法访问见证服务器“<em>服务器名称</em>”上的文件共享。更正此问题之前，数据库可用性组很容易发生故障。可以使用 Set-DatabaseAvailabilityGroup cmdlet 再次尝试该操作。错误:找不到网络路径。</p></td>
</tr>
</tbody>
</table>


如果在创建 DAG 之后但未添加服务器之前启用了见证服务器上的 Windows 防火墙，那么防火墙可能会阻止添加或删除 DAG 成员。如果启用了见证服务器上的 Windows 防火墙，但没有针对 WMI 配置防火墙例外，那么 **Add-DatabaseAvailabilityGroupServer** cmdlet 将会显示下列警告消息。


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>在见证服务器<em>“服务器名称”</em>上创建文件共享见证目录“C:\DAGFileShareWitnesses\DAG_FQDN”失败。更正此问题之前，数据库可用性组很容易发生故障。可以使用 Set-DatabaseAvailabilityGroup cmdlet 再次尝试该操作。错误:在服务器<em>“服务器名称”</em>上发生 WMI 异常：RPC 服务器不可用。（异常来自 HRESULT:0x800706BA）</p></td>
</tr>
</tbody>
</table>


要解决前面的错误和警告，请执行下列操作之一：

  - 在见证服务器上手动创建见证目录和共享，并为该目录和共享的 DAG 完全控制权分配 CNO。

  - 在 Windows 防火墙中启用 WMI 例外。

  - 禁用 Windows 防火墙。

创建 DAG

## DAG 成员身份

创建 DAG 之后，可以在 EAC 中使用管理数据库可用性组向导，或在命令行管理程序中使用 **Add-DatabaseAvailabilityGroupServer** 或 **Remove-DatabaseAvailabilityGroupServer** cmdlet 向 DAG 中添加服务器或从 DAG 中删除服务器。有关如何管理 DAG 成员身份的详细步骤，请参阅[管理数据库可用性组成员身份](manage-database-availability-group-membership-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>作为 DAG 成员的每个邮箱服务器也是 DAG 使用的基础群集中的一个节点。因此，在任何时候，邮箱服务器都只能是一个 DAG 的成员。</td>
</tr>
</tbody>
</table>


如果添加到 DAG 的邮箱服务器没有安装故障转移群集组件，则用于添加服务器的方法（例如，**Add-DatabaseAvailabilityGroupServer** cmdlet 或管理数据库可用性组向导）会安装故障转移群集功能。

将第一个邮箱服务器添加到 DAG 时，将发生以下操作：

  - 安装 Windows 故障转移群集组件（如果尚未安装）。

  - 使用 DAG 名称创建故障转移群集。此故障转移群集由 DAG 独占使用，并且此群集必须专用于 DAG。不支持将此群集用于任何其他用途。

  - 在默认计算机容器中创建 CNO。

  - DAG 的名称和 IP 地址在域名系统 (DNS) 中注册为主机 (A) 记录。

  - 服务器添加到 Active Directory 中的 DAG 对象中。

  - 使用装入到所添加服务器中的数据库的信息更新群集数据库。

在大型或多站点环境中，尤其是 DAG 扩展为多个 Active Directory 站点的环境中，必须等待包含第一个 DAG 成员的 DAG 对象 Active Directory 复制完成。如果在您的环境中未复制此 Active Directory 对象，则添加第二个服务器可能会导致为该 DAG 创建一个新的群集和新的 CNO。这是因为从添加的第二个成员的角度来看，该 DAG 对象看起来内容为空，因此即使这些对象已经存在，仍会导致 **Add-DatabaseAvailabilityGroupServer** cmdlet 为该 DAG 创建群集和 CNO。若要验证是否已复制了包含第一个 DAG 服务器的 DAG 对象，请在要添加的第二个服务器上使用 **Get-DatabaseAvailabilityGroup** cmdlet 来验证已添加的第一个服务器是否作为该 DAG 的成员列出。

将第二个及后续服务器添加到 DAG 时，将发生以下操作：

  - 服务器加入 DAG 的 Windows 故障转移群集中。

  - 仲裁模型自动进行调整：
    
      - 对于成员数为奇数的 DAG 采用多数节点仲裁模型。
    
      - 对于成员数为偶数的 DAG 采用多数节点和文件共享仲裁模型。

  - 需要时，Exchange 将自动创建见证目录和共享。

  - 服务器添加到 Active Directory 中的 DAG 对象中。

  - 使用已装入数据库的信息更新群集数据库。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>自动更改仲裁模型。如果仲裁模型没有自动更改为正确的模型，则可以运行仅包含 <em>Identity</em> 参数的 <strong>Set-DatabaseAvailabilityGroup</strong> cmdlet 来更正 DAG 仲裁设置。</td>
</tr>
</tbody>
</table>


## 预先暂存 DAG 的群集名称对象

CNO 是在 Active Directory 中创建的一个计算机帐户，与群集名称资源相关联。群集名称资源与 CNO 绑定，该 CNO 是支持 Kerberos 的对象，充当群集标识并提供群集的安全上下文。在将第一个成员添加到该 DAG 时形成了 DAG 基础群集以及该群集的 CNO。将第一个服务器添加到 DAG 时，远程 Powershell 将与正在添加的邮箱服务器上的 Microsoft Exchange 复制服务取得联系。如果还未安装故障转移群集功能，Microsoft Exchange 复制服务将安装该功能，并开始群集创建过程。Microsoft Exchange 复制服务在 LOCAL SYSTEM 安全上下文中运行，并且群集创建也正是在此上下文中执行。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您的 DAG 成员运行 Windows Server 2012，则必须在将第一个服务器添加到 DAG 中之前预先暂存 CNO。如果您的 DAG 成员运行 Windows Server 2012 R2，并且创建的 DAG 没有群集管理访问点，那么将不会创建 CNO，并且不需要为 DAG 创建 CNO。</td>
</tr>
</tbody>
</table>


如果计算机帐户的创建环境受限，或者计算机帐户创建于默认计算机容器之外的其他容器中，则可以预先暂存并设置 CNO。您可为 CNO 创建和禁用计算机帐户，然后执行以下操作之一：

  - 向您要添加到 DAG 的第一个邮箱服务器的计算机帐户分配对该计算机帐户的完全控制权限。

  - 向 Exchange 受信任子系统 USG 分配对该计算机帐户的完全控制权限。

向您要添加到 DAG 的第一个邮箱服务器的计算机帐户分配对该计算机帐户的完全控制权限，可确保 LOCAL SYSTEM 安全上下文能够管理预先暂存的计算机帐户。也可改为向 Exchange 受信任子系统 USG 分配对该计算机帐户的完全控制权限，因为该 Exchange 受信任子系统 USG 包含了域中所有 Exchange 服务器的计算机帐户。

有关如何预先暂存和设置 DAG 的 CNO 的详细步骤，请参阅[为数据库可用性组预留群集名称对象](pre-stage-the-cluster-name-object-for-a-database-availability-group-exchange-2013-help.md)。

## 从 DAG 中删除服务器

在 EAC 中使用管理数据库可用性组向导，或在命令行管理程序中使用 **Remove-DatabaseAvailabilityGroupServer** cmdlet 可以将邮箱服务器从 DAG 中删除。将邮箱服务器从 DAG 中删除之前，必须先从服务器中删除所有复制的邮箱数据库。如果试图从 DAG 中删除带有复制的邮箱数据库的邮箱服务器，任务将失败。

在某些情况下，必须先将邮箱服务器从 DAG 中删除才能执行特定操作。这些情况包括：

  - **执行服务器恢复操作**   如果邮箱服务器是 DAG 的成员，但发生了故障或丢失，且不可恢复并需要替换，则可以使用 **Setup /m:RecoverServer** 开关执行服务器恢复操作。但是，在执行恢复操作之前，必须首先使用包含 *ConfigurationOnly* 参数的 [Remove-DatabaseAvailabilityGroupServer](https://technet.microsoft.com/zh-cn/library/dd297956\(v=exchg.150\)) cmdlet 将服务器从 DAG 中删除。

  - **删除数据库可用性组**   在某些情况下，可能需要删除 DAG（例如，禁用第三方复制模式时）。如果需要删除 DAG，必须先删除 DAG 中的所有服务器。如果试图删除包含任何成员的 DAG，任务会失败。

创建 DAG

## 配置 DAG 属性

将服务器添加到 DAG 之后，可以使用 EAC 或命令行管理程序配置 DAG 的属性，包括 DAG 使用的见证服务器和见证目录以及分配给 DAG 的 IP 地址。

可配置的属性包括：

  - **见证服务器**   要用于为文件共享见证托管文件共享的服务器的名称。我们建议您指定客户端访问服务器作为见证服务器。这样系统可以根据需要自动对此共享进行配置、安全设置和使用，并使邮件管理员可以知道见证服务器的可用性。

  - **见证目录**   将用于存储文件共享见证数据的目录的名称。系统将自动在指定的见证服务器上创建此目录。

  - **数据库可用性组 IP 地址**   除非 DAG 成员运行 Windows Server 2012 R2 且创建的 DAG 没有 IP 地址，否则必须向 DAG 分配的一个或多个 IP 地址。或者，可以使用手动分配的静态 IP 地址配置 DAG 的 IP 地址，或在组织中使用 DHCP 服务器自动将它们分配给 DAG。

命令行管理程序不但使您能够配置 EAC 中不可用的 DAG 属性，例如 DAG IP 地址、网络加密和压缩设置、网络发现、用于复制的 TCP 端口以及备用见证服务器和见证目录设置，还能够启用数据中心激活协调模式。

有关如何配置 DAG 属性的详细步骤，请参阅[配置数据库可用性组属性](configure-database-availability-group-properties-exchange-2013-help.md)。

## DAG 网络加密

通过利用 Windows Server 操作系统的加密功能，DAG 支持加密。DAG 在 Exchange 服务器之间使用 Kerberos 身份验证。Microsoft Kerberos 安全支持提供程序 (SSP) EncryptMessage 和 DecryptMessage API 可处理 DAG 网络通信的加密。Microsoft Kerberos SSP 支持多种加密算法。（有关完整列表，请参阅 [Kerberos 协议扩展](https://go.microsoft.com/fwlink/p/?linkid=179131)的第 3.1.5.2 节“加密类型”）。Kerberos 身份验证握手会选择列表中支持的最强加密协议：通常为高级加密标准 (AES) 256 位，可能还包含基于 SHA 哈希的消息身份验证代码 (HMAC) 以维持数据的完整性。有关详细信息，请参阅 [HMAC](https://en.wikipedia.org/wiki/hmac)。

网络加密是 DAG 的属性，而非 DAG 网络的属性。可以在命令行管理程序中使用 **Set-DatabaseAvailabilityGroup** cmdlet 配置 DAG 网络加密。下表显示 DAG 网络通信的可能加密设置。

### DAG 网络通信加密设置

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已禁用</p></td>
<td><p>未使用网络加密。</p></td>
</tr>
<tr class="even">
<td><p>已启用</p></td>
<td><p>所有 DAG 网络上都使用了网络加密，用于复制和种子设定。</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>在不同子网间进行复制时，将在 DAG 网络上使用网络加密。这是默认设置。</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>所有 DAG 网络上都使用了网络加密，仅用于种子设定。</p></td>
</tr>
</tbody>
</table>


## DAG 网络压缩

DAG 支持内置压缩。启用压缩时，DAG 网络通信使用 XPRESS（LZ77 算法的 Microsoft 实现）。有关详细信息，请参阅 [Deflate 算法说明](http://www.zlib.net/feldspar.html)，及[线路格式协议规范](https://go.microsoft.com/fwlink/p/?linkid=179133)中的第 3.1.4.11.1.2.1 节“LZ77 压缩算法”。这与众多 Microsoft 协议中使用的压缩类型相同，尤其是 Microsoft Outlook 和 Exchange 之间的 MAPI RPC 压缩。

与网络加密一样，网络压缩也是 DAG 的属性，而非 DAG 网络的属性。在命令行管理程序中使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) cmdlet 可以配置 DAG 网络压缩。下表显示 DAG 网络通信的可能压缩设置。

### DAG 网络通信压缩设置

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>已禁用</p></td>
<td><p>未使用网络压缩。</p></td>
</tr>
<tr class="even">
<td><p>已启用</p></td>
<td><p>所有 DAG 网络上都使用了网络压缩，用于复制和种子设定。</p></td>
</tr>
<tr class="odd">
<td><p>InterSubnetOnly</p></td>
<td><p>在不同子网间进行复制时，将在 DAG 网络上使用网络压缩。这是默认设置。</p></td>
</tr>
<tr class="even">
<td><p>SeedOnly</p></td>
<td><p>所有 DAG 网络上都使用了网络压缩，仅用于种子设定。</p></td>
</tr>
</tbody>
</table>


创建 DAG

## DAG 网络

DAG 网络包含一个或多个用于复制流量或 MAPI 流量的子网。每个 DAG 包含最多一个 MAPI 网络，以及零个或多个复制网络。

## 单网络适配器配置

在单网络适配器配置中，同一网络同时用于 MAPI 流量和复制流量。为了降低复杂性，单网络适配器配置是针对 Exchange 服务器的推荐配置，因此同一网络上可以同时有 MAPI 流量和复制流量。

## 双网络适配器配置

通常情况下，只有当增加的网络流量有可能使单网络适配器饱和时，才需要使用双网络适配器。

在双网络适配器配置中，通常有一个网络专用于复制流量，另一个网络主要用于 MAPI 流量。还可以向每个 DAG 成员添加网络适配器，并将其他 DAG 网络配置为复制网络。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用多个复制网络时，无法指定网络使用优先顺序。Exchange 会从复制网络组中随机选择一个复制网络用于日志传送。</td>
</tr>
</tbody>
</table>


在 Exchange 2010 中，在许多情况下需要手动配置 DAG 网络。默认情况下，在 Exchange 2013 中，由系统自动配置 DAG 网络。因为您可以创建或修改 DAG 网络，所以必须首先通过运行以下命令启用手动 DAG 网络控制：

    Set-DatabaseAvailabilityGroup <DAGName> -ManualDagNetworkConfiguration $true

启用手动 DAG 网络配置之后，您即可在命令行管理程序中使用 **New-DatabaseAvailabilityGroupNetwork** cmdlet 创建 DAG 网络。有关如何创建 DAG 网络的详细步骤，请参阅[创建数据库可用性组网络](create-a-database-availability-group-network-exchange-2013-help.md)。

可以在命令行管理程序中使用 **Set-DatabaseAvailabilityGroupNetwork** cmdlet 配置 DAG 网络属性。有关如何配置 DAG 网络属性的详细步骤，请参阅[配置数据库可用性组网络属性](configure-database-availability-group-network-properties-exchange-2013-help.md)。需要配置每个 DAG 网络的必需和可选参数：

  - **网络名**   DAG 网络的唯一名称，最多 128 个字符。

  - **网络描述**   DAG 网络的可选描述，最多 256 个字符。

  - **网络子网**   使用 *IPAddress/Bitmask* 格式（例如，对于 Internet 协议版本 4 (IPv4) 子网为 192.168.1.0/24；对于 Internet 协议版本 6 (IPv6) 子网为 2001:DB8:0:C000::/64）输入的一个或多个子网。

  - **启用复制**   在 EAC 中，选中复选框使 DAG 网络专门用于复制通信，并阻止 MAPI 通信。清除此复选框可以阻止使用 DAG 网络进行复制通信，并启用 MAPI 通信。在命令行管理程序中，使用 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298008\(v=exchg.150\)) cmdlet 中的 *ReplicationEnabled* 参数可以启用和禁用复制。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 MAPI 网络上禁用复制并不保证系统不会将 MAPI 网络用于复制。当配置的所有复制网络都脱机、出现故障或由于其他原因而不可用，只有 MAPI 网络保留（该网络配置为禁用复制）时，系统使用 MAPI 网络进行复制。</td>
</tr>
</tbody>
</table>


系统创建的初始 DAG 网络（例如 MapiDagNetwork 和 ReplicationDagNetwork01）基于群集服务枚举的子网。每个 DAG 成员都必须具有相同数目的网络适配器，并且每个网络适配器都必须具有唯一子网上的 IPv4 地址（也可以具有 IPv6 地址）。多个 DAG 成员可以具有相同子网上的 IPv4 地址，但是特定 DAG 成员中的每个网络适配器和 IP 地址对必须处于唯一子网上。此外，只有用于 MAPI 网络的适配器才应配置有默认网关。复制网络不应配置有默认网关。

例如，请考虑 DAG1，这是一个两成员 DAG，其中每个成员都有两个网络适配器（一个专用于 MAPI 网络，另一个用于复制网络）。下表中显示了示例 IP 地址配置设置。

### 示例网络适配器设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器网络适配器</th>
<th>IP 地址/子网掩码</th>
<th>默认网关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1 (MAPI)</p></td>
<td><p>192.168.1.15/24</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX1（复制）</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>EX2 (MAPI)</p></td>
<td><p>192.168.1.16</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2（复制）</p></td>
<td><p>10.0.0.16</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


在下面的配置中，在 DAG 中配置了两个子网：192.168.1.0 和 10.0.0.0。在将 EX1 和 EX2 添加到 DAG 时，会枚举这两个子网，并会创建两个 DAG 网络：MapiDagNetwork (192.168.1.0) 和 ReplicationDagNetwork01 (10.0.0.0)。这些网络的配置如下表所示。

### 单子网 DAG 的枚举 DAG 网络设置

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>子网</th>
<th>接口</th>
<th>启用了 MAPI 访问</th>
<th>启用了复制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.1.15)</p>
<p>EX2 (192.168.1.16)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.0.16)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


若要完成作为专用复制网络的 ReplicationDagNetwork01 的配置，请通过运行下面的命令为 MapiDagNetwork 禁用复制。

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG1\MapiDagNetwork -ReplicationEnabled:$false

在为 MapiDagNetwork 禁用了复制之后，Microsoft Exchange 复制服务将 ReplicationDagNetwork01 用于连续复制。如果 ReplicationDagNetwork01 遇到故障，则 Microsoft Exchange 复制服务会恢复为使用 MapiDagNetwork 进行连续复制。这由系统主动进行，以维持高可用性。

## DAG 网络和多子网部署

在上面的示例中，即使 DAG 使用了两个不同的子网（192.168.1.0 和 10.0.0.0），DAG 仍被视为单子网 DAG，因为每个成员都使用相同的子网构成 MAPI 网络。当 DAG 成员将不同的子网用于 MAPI 网络时，DAG 称为“多子网 DAG”。在多子网 DAG 中，合适的子网会自动与每个 DAG 网络关联。

例如，请考虑 DAG2，这是一个两成员 DAG，其中每个成员都有两个网络适配器（一个专用于 MAPI 网络，另一个用于复制网络），并且每个 DAG 成员位于独立 Active Directory 站点中，其 MAPI 网络处于不同的子网上。下表中显示了示例 IP 地址配置设置。

### 多子网 DAG 的示例网络适配器设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器网络适配器</th>
<th>IP 地址/子网掩码</th>
<th>默认网关</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1 (MAPI)</p></td>
<td><p>192.168.0.15/24</p></td>
<td><p>192.168.0.1</p></td>
</tr>
<tr class="even">
<td><p>EX1（复制）</p></td>
<td><p>10.0.0.15/24</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>EX2 (MAPI)</p></td>
<td><p>192.168.1.15</p></td>
<td><p>192.168.1.1</p></td>
</tr>
<tr class="even">
<td><p>EX2（复制）</p></td>
<td><p>10.0.1.15</p></td>
<td><p>不适用</p></td>
</tr>
</tbody>
</table>


在下面的配置中，在 DAG 中配置了四个子网：192.168.0.0、192.168.1.0、10.0.0.0 和 10.0.1.0。在将 EX1 和 EX2 添加到 DAG 时，会枚举这四个子网，但是仅创建两个 DAG 网络：MapiDagNetwork (192.168.0.0, 192.168.1.0) 和 ReplicationDagNetwork01 (10.0.0.0, 10.0.1.0)。这些网络的配置如下表所示。

### 多子网 DAG 的枚举 DAG 网络设置

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>子网</th>
<th>接口</th>
<th>启用了 MAPI 访问</th>
<th>启用了复制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MapiDagNetwork</p></td>
<td><p>192.168.0.0/24</p>
<p>192.168.1.0/24</p></td>
<td><p>EX1 (192.168.0.15)</p>
<p>EX2 (192.168.1.15)</p></td>
<td><p>True</p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p>ReplicationDagNetwork01</p></td>
<td><p>10.0.0.0/24</p>
<p>10.0.1.0/24</p></td>
<td><p>EX1 (10.0.0.15)</p>
<p>EX2 (10.0.1.15)</p></td>
<td><p>False</p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


## DAG 网络和 iSCSI 网络

默认情况下，DAG 将执行所有已检测到并配置为供基础群集使用的网络的发现。这包括作为对一个或多个 DAG 成员使用 iSCSI 存储的结果的所有 Internet SCSI (iSCSI) 网络。最佳做法是，iSCSI 存储应使用专用的网络和网络适配器。这些网络不应由 DAG 或其群集管理，也不应用作 DAG 网络（MAPI 或复制）。相反，应手动禁止 DAG 使用这些网络，使之专用于 iSCSI 存储通信。若要禁止检测 iSCSI 网络并将其用作 DAG 网络，请使用 [Set-DatabaseAvailabilityGroupNetwork](https://technet.microsoft.com/zh-cn/library/dd298008\(v=exchg.150\)) cmdlet 配置 DAG 以忽略当前检测到的任何 iSCSI 网络，如此示例所示：

    Set-DatabaseAvailabilityGroupNetwork -Identity DAG2\DAGNetwork02 -ReplicationEnabled:$false -IgnoreNetwork:$true

此命令还会禁止群集使用该网络。虽然 iSCSI 网络会继续显示为 DAG 网络，但是在运行上面的命令之后不会将它们用于 MAPI 或复制通信。

创建 DAG

## 配置 DAG 成员

作为 DAG 成员的邮箱服务器的某些属性特定于高可用性，应按照以下各节所述配置这些属性：

  - 自动数据库装入拨号

  - 数据库副本自动激活策略

  - 最大的活动数据库数

## 自动数据库装入拨号

*AutoDatabaseMountDial* 参数指定数据库故障转移后的自动数据库装入行为。可以使用 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\)) cmdlet 将 *AutoDatabaseMountDial* 参数配置为具有以下任何值：

  - `BestAvailability`   如果指定此值，且复制队列长度小于或等于 12，则数据库会在故障转移后立即自动装入。复制队列长度是需要复制的被动副本识别的日志数量。如果复制队列长度大于 12，则数据库不会自动装入。在复制队列长度小于或等于 12 时，Exchange 会尝试将剩余日志复制到被动副本中，并装入数据库。

  - `GoodAvailability`   如果指定此值，且复制队列长度小于或等于 6，则数据库会在故障转移后立即自动装入。复制队列长度是需要复制的被动副本识别的日志数量。如果复制队列长度大于 6，则数据库不会自动装入。在复制队列长度小于或等于 6 时，Exchange 会尝试将剩余日志复制到被动副本中，并装入数据库。

  - `Lossless`   如果指定此值，则在将主动副本上生成的所有日志复制到被动副本之前，数据库不会自动装入。此设置还会使活动管理器最佳副本选择算法基于数据库副本的激活首选项值（而不是其副本队列长度），对进行激活的潜在候选对象进行排序。

默认值为 `GoodAvailability`。如果指定 `BestAvailability` 或 `GoodAvailability`，并且无法将主动副本中的所有日志复制到所激活的被动副本中，则可能会丢失一些邮箱数据。但是，安全网络功能（默认启用）将通过重新提交安全网络队列中的邮件来帮助防止大多数数据丢失。

## 示例：配置自动数据库装入拨号

下面的示例使用值为 `GoodAvailability` 的 *AutoDatabaseMountDial* 设置来配置邮箱服务器。

    Set-MailboxServer -Identity EX1 -AutoDatabaseMountDial GoodAvailability

## 数据库副本自动激活策略

*DatabaseCopyAutoActivationPolicy* 参数指定所选邮箱服务器上邮箱数据库副本可用的自动激活类型。可以使用 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\)) cmdlet 将 *DatabaseCopyAutoActivationPolicy* 参数配置为具有以下任何值：

  - `Blocked`   如果指定此值，则不能在所选邮箱服务器上自动激活数据库。

  - `IntrasiteOnly`   如果指定此值，则允许激活在同一个 Active Directory 站点中的服务器上的数据库副本。这可以防止跨站点故障转移或激活。此属性适用于传入邮箱数据库副本（例如，正被制作成主动副本的被动副本）。对于在另一个 Active Directory 站点中处于活动状态的数据库副本，无法在此邮箱服务器上为其激活数据库。

  - `Unrestricted`   如果指定此值，在所选邮箱服务器上激活邮箱数据库副本没有任何特殊限制。

## 示例：配置数据库副本自动激活策略

下面的示例使用值为 `Blocked` 的 *DatabaseCopyAutoActivationPolicy* 设置来配置邮箱服务器。

    Set-MailboxServer -Identity EX1 -DatabaseCopyAutoActivationPolicy Blocked

## 最大的活动数据库数

*MaximumActiveDatabases* 参数（也与 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\)) cmdlet 一起使用）指定可以在邮箱服务器上装入的数据库数。可以配置邮箱服务器以确保单个邮箱服务器不会过载，从而满足部署要求。

*MaximumActiveDatabases* 参数使用整数数值进行配置。达到最大数时，如果出现故障转移或切换，将不会激活服务器上的数据库副本。如果这些副本在服务器上已处于活动状态，则服务器不允许装入数据库。

## 示例：配置最大的活动数据库数

下面的示例将邮箱服务器配置为支持最多 20 个活动数据库。

    Set-MailboxServer -Identity EX1 -MaximumActiveDatabases 20

创建 DAG

## 对 DAG 成员执行维护

在 DAG 成员上执行任何类型的软件或硬件维护之前，应先将 DAG 成员置于维护模式中。这将从服务器移除所有活动数据库，并阻止活动数据库移动至该服务器。它还确保将服务器上可能存在的所有关键 DAG 支持功能（例如，主活动管理器 (PAM) 角色）都移动至其他服务器，并阻止这些功能移动回该服务器。具体而言，您应执行以下任务：

1.  要启动腾空传输队列的过程，请运行 `Set-ServerComponentState <ServerName> -Component HubTransport -State Draining -Requester Maintenance`

2.  要启动腾空传输队列的操作，则运行 `Restart-Service MSExchangeTransport`

3.  若要启动腾空所有统一消息呼叫的过程，则运行 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Draining -Requester Maintenance`

4.  要将本地队列中等待传递的邮件重定向到由目标参数指定的邮箱服务器，则运行 `Redirect-Message -Server <ServerName> -Target <MailboxServerFQDN>`

5.  要暂停群集节点（这将防止节点作为及成为 PAM），则运行 `Suspend-ClusterNode <ServerName>`

6.  要将 DAG 成员上当前托管的所有活动数据库都移动至其他 DAG 成员，则运行 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $True`

7.  要防止服务器托管主动数据库副本，则运行 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Blocked`

8.  要将服务器置于维护模式，则运行 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Inactive -Requester Maintenance`

要验证服务器是否准备好进行维护，则执行以下任务：

1.  要验证服务器是否已置入维护模式，则运行 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

2.  要验证服务器是否托管了任何主动数据库副本，则运行 `Get-MailboxServer <ServerName> | ft DatabaseCopy* -Autosize`

3.  要验证是否已暂停节点，则运行 `Get-ClusterNode <ServerName> | fl`

4.  要验证是否已腾空所有传输队列，则运行 `Get-Queue`

在维护完成且 DAG 成员准备好重新投入运行之后，可以通过执行以下任务使 DAG 成员脱离维护模式并将其重新投入生产：

  - 要指定服务器脱离维护模式，则运行 `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Maintenance`

  - 若要允许服务器接受统一消息呼叫，则运行 `Set-ServerComponentState <ServerName> -Component UMCallRouter -State Active -Requester Maintenance`

  - 要恢复群集中的节点，并启用服务器的完整群集功能，则运行 `Resume-ClusterNode <ServerName>`

  - 要允许数据库在服务器上变为活动状态，则运行 `Set-MailboxServer <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $False`

  - 要删除对自动激活的阻止，则运行 `Set-MailboxServer <ServerName> -DatabaseCopyAutoActivationPolicy Unrestricted`

  - 要启用传输队列，并允许服务器接受和处理邮件，则运行 `Set-ServerComponentState <ServerName> -Component HubTransport -State Active -Requester Maintenance`

  - 要恢复传输活动，则运行 `Restart-Service MSExchangeTransport`

要验证服务器是否准备好在生产中使用，则执行以下任务：

1.  要验证服务器不处于维护模式，则运行 `Get-ServerComponentState <ServerName> | ft Component,State -Autosize`

如果要安装 Exchange 更新，而更新进程失败，则会使某些服务器组件处于非活动状态，该状态将会在以上 Get-ServerComponentState cmdlet 的输出中显示。要解决此问题，请运行以下命令：

  - `Set-ServerComponentState <ServerName> -Component ServerWideOffline -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component Monitoring -State Active -Requester Functional`

  - `Set-ServerComponentState <ServerName> -Component RecoveryActionsEnabled -State Active -Requester Functional`

创建 DAG

## 关闭 DAG 成员

Exchange 2013 高可用性解决方案与 Windows 关闭进程集成在一起。如果 DAG 的装入数据库复制到了一个或多个 DAG 成员，则当管理员或应用程序对 DAG 中的 Windows 服务器启动关闭进程时，系统会在允许关闭进程完成前先尝试激活此装入数据库的另一个副本。

但是，此新行为并不能保证要关闭的服务器上的所有数据库都进行 `lossless` 激活。因此，最佳做法是在关闭 DAG 成员服务器之前先执行服务器切换。

创建 DAG

## 在 DAG 成员上安装更新

在 DAG 成员服务器上安装 Microsoft Exchange Server 2013 更新是相对简单的过程。在 DAG 成员服务器上安装更新时，一些服务将在安装过程中停止，包括所有 Exchange 服务以及群集服务。对 DAG 成员应用更新的一般过程如下所示：

1.  按照上述步骤将 DAG 成员置于维护模式中。

2.  安装更新。

3.  按照上述步骤使 DAG 成员脱离维护模式并将其重新投入生产。

4.  （可选）使用 RedistributeActiveDatabases.ps1 脚本在 DAG 间重新平衡主动数据库副本。

可以从 [Microsoft 下载中心](http://www.microsoft.com/downloads)下载 Exchange 2013 的最新更新。

创建 DAG

