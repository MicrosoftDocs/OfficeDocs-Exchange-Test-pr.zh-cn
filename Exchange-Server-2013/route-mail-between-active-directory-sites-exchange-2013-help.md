---
title: '在 Active Directory 站点之间路由邮件: Exchange 2013 Help'
TOCTitle: 在 Active Directory 站点之间路由邮件
ms:assetid: 86b423e3-7bec-4430-9a5a-4f84ce9d82ea
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ916681(v=EXCHG.150)
ms:contentKeyID: 52061524
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Active Directory 站点之间路由邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Active Directory 站点是基于网络物理方面的逻辑配置组件。创建 Active Directory 站点的主要目的是定义网络中的哪些子网通过优化 Active Directory 复制通信控制的方式建立连接。Microsoft Exchange Server 2013 将数据库可用性组 (DAG) 和 Active Directory 站点识别为路由边界，Exchange 2013 服务器根据 Active Directory 站点拓扑制定路由决策。

默认情况下，Active Directory 林只包含一个 Active Directory 站点。此 Active Directory 站点的默认名称为 `Default-First-Site-Name`。如果未创建其他 Active Directory 站点，则林中所有域成员计算机为 `Default-First-Site-Name` 的成员。不必配置子网与站点的关联。如果创建了其他 Active Directory 站点，则需要指定为该 Active Directory 站点分配的子网。

**目录**

确定站点成员身份

IP 站点链接

控制 IP 站点链接开销

实现中心站点

拓扑发现

## 确定站点成员身份

每个 Active Directory 站点与一个或多个 IP 子网关联。管理员将 Active Directory 站点成员身份分配给配置为域控制器和全局目录服务器的计算机。如果其他域成员计算机（如 Exchange 服务器）配置为使用与 Active Directory 站点关联的 IP 子网中的 IP 地址，会自动为这些计算机分配 Active Directory 站点成员身份。拥有相同 Active Directory 站点成员身份的计算机被认为具有良好的网络连接性。服务器始终是一个 Active Directory 站点的成员。

如果应用程序可以确定安装该应用程序的计算机和林中其他计算机的 Active Directory 站点成员身份，然后使用该信息控制通信流，则该应用程序是站点感知应用程序。如果站点感知应用程序必须使用其他服务器（例如域控制器或全局编录服务器）的服务，则为与请求这些服务的计算机拥有相同 Active Directory 站点成员身份的服务器分配优先级。

Exchange 2013 是站点感知应用程序，它将 Active Directory 拓扑用于邮件路由并与其他 Exchange 2013 计算机上运行的服务进行通信。Active Directory 站点不仅是路由边界，它还是服务发现边界。

确定域成员计算机的站点成员身份取决于一系列 DNS 查询，这些查询将本地 IP 地址与已定义的子网进行比较，然后确定相应的站点成员身份关联。为了降低与 DNS 查询关联的开销，Exchange 2013 Active Directory 架构添加内容包括了 Exchange 服务器对象的 **msExchServerSite** 特性。此特性的值是 Exchange 服务器的 Active Directory 站点的可分辨名称。此特性是每个 Exchange 服务器对象的属性。如果站点成员身份关联存储为服务器对象的属性，则可以从 Active Directory 直接读取当前拓扑，而不必依靠 DNS 查询，并对非域计算机（例如订阅了站点的边缘传输服务器）启用站点成员身份关联。

Microsoft Exchange Active Directory 拓扑服务将填充 **msExchServerSite** 特性的值并保持该值最新。基于 Windows 的计算机启动时，网络登录服务将确定该计算机的站点成员身份。网络登录服务使用该信息查找与本地计算机位于同一个 Active Directory 站点的域控制器，然后将授权请求和身份验证请求传递到这些服务器。Microsoft Exchange Active Directory 拓扑服务使用 **DsGetSiteName** API 调用从网络登录服务检索站点成员身份值，然后将 Active Directory 站点的可分辨名称写入 Active Directory 中 Exchange 服务器对象的 **msExchServerSite** 特性。

下表说明组织如何定义 Active Directory 站点。在此示例，定义了三个 Active Directory 站点，每个 Active Directory 站点与多个 IP 子网关联。

**Active Directory 站点与子网的关联的示例**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 站点名</th>
<th>关联的 IP 子网</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>站点 A</p></td>
<td><p>192.168.1.0/24</p>
<p>192.168.2.0/24</p></td>
</tr>
<tr class="even">
<td><p>站点 B</p></td>
<td><p>192.168.3.0/24</p>
<p>192.168.4.0/24</p></td>
</tr>
<tr class="odd">
<td><p>站点 C</p></td>
<td><p>192.168.5.0/24</p>
<p>192.168.6.0/24</p></td>
</tr>
</tbody>
</table>


如果名为 Mailbox01 的服务器的 IP 地址为 192.168.1.1，则它是站点 A 的成员。通过更改服务器的 IP 地址可以更改其站点成员身份。如果将 Mailbox01 的 IP 地址更改为 192.168.2.1，它不会更改服务器的 Active Directory 站点成员身份，因为该子网还与站点 A 关联。不过，如果您移动服务器且 IP 地址更改为 192.168.3.1，则应将服务器视为站点 B 的成员。

如果更改子网与 Active Directory 站点的关联，则站点成员身份也会发生更改。例如，如果删除子网 192.168.3.0 与站点 B 的关联，而将其与站点 A 关联，则具有 IP 地址 192.168.3.1 的服务器的站点成员身份也更改为站点 A。当站点成员身份发生更改时，Exchange 必须更新其配置数据，以便当 Exchange 制定路由决策时考虑此更改。更改 Active Directory 站点成员身份与完全传播拓扑更改之间会存在一定的延迟。

返回顶部

## IP 站点链接

站点链接是 Active Directory 站点之间的逻辑路径。站点链接对象代表一组站点，这些站点可以利用统一开销进行通信。站点链接与物理网络上网络数据包的实际传输路径并不对应。但是，管理员为站点链接分配的开销通常与基础网络的可靠性、速度和可用带宽有关。例如，Active Directory 管理员为速度为 100 Mbps 的网络连接分配的开销将低于为速度为 10 Mbps 的网络连接分配的开销。

默认情况下，所有站点链接都是递次的。这意味着如果站点 A 具有与站点 B 的链接，站点 B 具有与站点 C 的链接，则站点 A 可以递次链接到站点 C。站点 A 与站点 C 之间的递次链接也称为*站点链接桥*。

Exchange 仅使用 IP 站点链接来确定其 Active Directory 站点路由拓扑。计算路由表时，Exchange 的路由组件将考虑为 IP 站点链接分配的开销。这些开销用于计算通向邮件最终目标开销最低的路由路径。

每个 Active Directory 站点必须至少与一个 IP 站点链接相关联。有一个默认 IP 站点链接，名为 `DEFAULTIPSITELINK`。当创建 Active Directory 站点时，需要将该站点与 IP 站点链接关联。可以创建其他 IP 站点链接以实现所需的拓扑，也可以将每个 Active Directory 站点与 `DEFAULTIPSITELINK` 关联。每个作为 IP 站点链接一部分的 Active Directory 站点可以利用统一的开销与该链接中的每个其他站点直接进行通信。

在下图中，林中配置了四个 Active Directory 站点。每个站点已经与 `DEFAULTIPSITELINK` 关联。因此，每个 Active Directory 站点可以利用相同的开销与每个其他站点直接进行通信。指示了多个通信路径，但是只定义一个 IP 站点链接。

**具有单个 IP 站点链接的完全网状拓扑**

![具有单个 IP 站点链接的完全网状拓扑](images/JJ916681.af38d41d-e768-4221-ab4b-b782aa388b73(EXCHG.150).gif "具有单个 IP 站点链接的完全网状拓扑")

在下图中，林中配置了四个 Active Directory 站点。在此拓扑中，管理员已经配置 IP 站点链接以创建 Active Directory 站点的*中心分支拓扑*。每个分支站点可以与中心站点直接进行通信，分支站点之间可以使用递次 IP 站点链接相互进行通信。

**Active Directory IP 站点链接的中心分支拓扑**

![IP 站点链接的中心辐射型拓扑](images/JJ916681.eca6cd51-8c2e-4996-81ea-070cd9766ef8(EXCHG.150).gif "IP 站点链接的中心辐射型拓扑")

请务必注意，Exchange 在确定开销最低路径时使用站点链接，但是会始终尝试将邮件直接传递到目标 Exchange 服务器。例如，如果上图拓扑中站点 B 中的用户将邮件发送到站点 C 中的另一个用户，则站点 B 中的邮箱服务器将直接与站点 C 中的邮箱服务器连接。如果希望强制邮件通过站点 A，则必须将该站点启用为中心站点。有关中心站点的详细信息，请参阅本主题后面的“实现中心站点”。

Active Directory 管理员实现最能代表林的连接和通信需求的拓扑。由于 Exchange 使用相同的拓扑，因此您需要确保当前拓扑支持有效邮件传递通信。

站点链接的默认开销是 100。有效的站点链接开销可以是从 1 到 99,999 之间的任意数字。如果指定冗余链接，将始终首选分配的开销最低的链接。Exchange 组织管理员可以为 IP 站点链接分配 Exchange 特定的开销。如果为 IP 站点链接分配 Exchange 开销，Exchange 将使用该开销。否则，将使用 Active Directory 开销。有关如何设置 IP 站点链接上的 Exchange 开销的详细信息，请参阅本主题后面的“控制 IP 站点链接开销”。拥有 Enterprise Administrators 组成员身份的管理员可创建其他 IP 站点链接。

有关 Active Directory 站点配置的详细信息，请参阅[设计站点拓扑](https://go.microsoft.com/fwlink/p/?linkid=33551)。

返回顶部

## 控制 IP 站点链接开销

Active Directory IP 站点链接开销基于相对网络速度（与 WAN 中的所有网络连接相比），并且可以生成可靠、高效的复制拓扑。因此，在大多数情况下，现有 IP 站点链接开销应当适用于 Exchange 邮件路由。不过，如果记录现有 Active Directory 站点和 IP 站点链接拓扑后，确认 Active Directory IP 站点链接开销和通信流模式不适用于 Exchange，则必须对 Exchange 评估的开销进行调整。使用 Active Directory 工具更改分配给 IP 站点链接的开销会影响整个环境。而是应该在 Exchange 命令行管理程序中使用 **Set-AdSiteLink** cmdlet 为 IP 站点链接分配 Exchange 特定的开销。例如，要在名为 SITELINKAB 的 IP 站点链接上配置 Exchange 特定开销值 25，请在命令行管理程序中运行以下命令：`Set-AdSiteLink SITELINKAB -ExchangeCost 25`。`Set-AdSiteLink SITELINKAB -ExchangeCost 25`.

为 IP 站点链接分配了 Exchange 特定的开销后，Exchange 开销在选择邮件路由时覆盖 Active Directory 开销，路由在评估开销最低路由路径时仅考虑 Exchange 开销。

当邮件路由拓扑必须脱离 Active Directory 复制拓扑时，调整 IP 站点链接开销非常有用。Exchange 开销可用于强制所有邮件路由使用中心站点。Exchange 开销还可用于控制当与 Active Directory 站点的通信失败时在何处对邮件排队。下图显示了具有四个站点的 Active Directory 拓扑。

**为 IP 站点链接配置了 Exchange 开销的拓扑**

![在 IP 站点链接上有 Exchange 成本的拓扑](images/JJ916681.56ac2bab-99de-4ddf-b968-80cd34ab8c21(EXCHG.150).gif "在 IP 站点链接上有 Exchange 成本的拓扑")

在上图中，站点 C 与站点 D 之间的网络连接是仅用于 Active Directory 复制的低带宽连接，不应当用于邮件路由。不过，Active Directory IP 站点链接开销会导致该链接包括在从任何其他 Active Directory 站点到站点 D 的开销最低路由路径中。因此，邮件传递到站点 C 中的站点 D 队列。Exchange 管理员倾向于开销最低路由路径包括站点 B，因此如果站点 D 不可用，邮件将在站点 B 排队。在站点 C 与站点 D 之间的 IP 站点链接上配置高 Exchange 开销会阻止该 IP 站点链接包括在通往站点 D 的开销最低路由路径中。

Exchange 支持对 Active Directory IP 站点链接配置最大邮件大小限制。默认情况下，对于在不同 Active Directory 站点中的 Exchange 服务器之间中继的邮件，Exchange 不施加最大邮件大小限制。如果使用 **Set-AdSiteLink** cmdlet 在 Active Directory IP 站点链接上配置最大邮件大小，则路由会为大于最大邮件大小限制（在开销最低路由路径中的任何 Active Directory 站点链接上配置的值）的任何邮件生成未送达报告 (NDR)。此配置对于限制发送到必须通过低带宽连接进行通信的远程 Active Directory 站点的邮件大小非常有用。有关详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

返回顶部

## 实现中心站点

在 Exchange 组织中，可能需要强制所有邮件通过特定 Active Directory 站点传递。可以使用命令行管理程序将 Active Directory 站点指定为中心站点。执行此操作时，由于邮件传递中涉及到更多服务器，会导致额外总体开销。例如，考虑从站点 A 发送到站点 E 的邮件。如果开销最低路由路径是站点 A - 站点 B - 站点 C - 站点 D - 站点 E，且将站点 C 指定为中心站点，则邮件从站点 A 中继到站点 C，然后从站点 C 中继到站点 E。

可以使用 **Set-AdSite** cmdlet 将 Active Directory 站点指定为中心站点。当开销最低路由路径中存在用于邮件传递的中心站点时，邮件先排队，并由中心站点中的服务器上的传输服务进行处理，然后再中继到最终目标。

选择开销最低路由路径后，路由确定该路由路径中是否存在中心站点。如果配置了中心站点，则邮件在中心站点中的邮件服务器处停留，然后再中继到目标。如果开销最低路由路径中存在多个中心站点，则邮件在路由路径中的每个中心站点上停留。

只有开销最低的路由路径上存在中心站点，直接中继路由的这种变化形式才有效。下图显示中心站点的正确用法。在此图中，站点 B 配置为中心站点。从站点 A 中继到站点 D 的邮件通过站点 B 中继，然后再传输到站点 D。

**使用中心站点进行邮件传递**

![使用中心站点进行邮件传递](images/JJ916681.93238bcb-6bbc-4a48-aeb0-09342a421b5b(EXCHG.150).gif "使用中心站点进行邮件传递")

下图显示 IP 站点链接开销对通向中心站点的路由的影响。在此方案中，站点 B 已指定为中心站点。不过，在任何其他站点间的开销最低路由路径中，站点 B 不存在。因此，从站点 A 中继到站点 D 的邮件从不通过站点 B 中继。如果 Active Directory 站点在两个其他站点间的开销最低路由路径中不存在，则 Active Directory 站点从不用作中心站点。

**配置错误的中心站点**

![配置错误的中心站点](images/JJ916681.c010d4d8-5cd3-4b79-b7db-0367ba3cc287(EXCHG.150).gif "配置错误的中心站点")

可以将任何 Active Directory 站点配置为中心站点。但是，为了让此配置正常工作，中心站点中必须至少存在一个邮箱服务器。

返回顶部

## 拓扑发现

Exchange 可以通过下列必需元素使用 Active Directory 拓扑：

  - Microsoft Exchange Active Directory 拓扑服务。

  - Microsoft Exchange 传输服务中的拓扑发现模块。

Microsoft Exchange Active Directory 拓扑服务在所有 Exchange 2013 客户端访问服务器和邮箱服务器上运行。这些服务器使用 Microsoft Exchange Active Directory 拓扑服务发现 Exchange 服务器可用来读取和写入 Active Directory 数据的域控制器和全局目录服务器。当 Exchange 必须在 Active Directory 中读取和写入时，Exchange 2013 绑定到标识的目录服务器。

拓扑发现模块是 Microsoft Exchange 传输服务的一部分，它将有关 Active Directory 拓扑的信息提供给 Exchange 服务器。此 API 在组织中发现 Exchange 服务器和角色，并确定它们与 Active Directory 配置对象的关系。配置数据从 Active Directory 检索，然后进行缓存，以便它可供该计算机上运行的 Exchange 服务访问。

拓扑发现模块执行下列步骤以生成 Exchange 路由拓扑：

1.  从 Active Directory 读取数据。检索所有下列对象：
    
      - Active Directory 站点。
    
      - IP 站点链接。
    
      - 所有 Exchange 服务器。

2.  使用步骤 1 中检索到的数据创建初始拓扑，并开始链接和映射相关的配置对象。

3.  Exchange 服务器通过从 Active Directory 中存储的 Exchange 服务器对象检索站点特性值来映射到 Active Directory 站点。

4.  使用检索到的信息集合更新路由表。

此过程使每个 Exchange 2013 服务器可以感知到组织中的其他 Exchange 服务器以及 Exchange 服务器与其他服务器的接近程度。

返回顶部

