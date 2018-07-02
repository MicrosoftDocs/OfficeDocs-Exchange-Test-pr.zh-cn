---
title: '规划使用 Active Directory 站点路由邮件: Exchange 2013 Help'
TOCTitle: 规划使用 Active Directory 站点路由邮件
ms:assetid: 0f697cee-bcaa-4c69-b80c-7a2afd1817d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996299(v=EXCHG.150)
ms:contentKeyID: 52061480
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 规划使用 Active Directory 站点路由邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-05-21_

Microsoft Exchange Server 2013 识别 Active Directory 站点和数据库可用性组 (DAG) 作为路由边界。但是，Exchange 2013 仍使用 Active Directory 站点拓扑来确定邮件在组织的不同 DAG 或不同站点的 Exchange 服务器中间传输的方式。有关详细信息，请参阅[邮件路由](mail-routing-exchange-2013-help.md)。

邮箱服务器上的传输服务提供 Exchange 组织内部的邮件传输。如果部署的是纯 Exchange 2013 组织，或向纯 Exchange 2013 组织中引入 Exchange Server 2010，则在林中建立路由时无需其他配置。

**目录**

Exchange 2013 使用 Active Directory 站点成员身份的方式

确定 Active Directory 站点成员身份

IP 站点链接概述

在 Active Directory 站点中部署 Exchange 2013

## Exchange 2013 使用 Active Directory 站点成员身份的方式

Exchange 2013 是站点感知应用程序。通过查询 Active Directory，站点感知应用程序可以确定其自身的 Active Directory 站点成员身份和其他服务器的 Active Directory 站点成员身份。Exchange 2013 使用站点成员身份确定处理 Active Directory 查询要使用哪些域控制器和全局编录服务器。此外，当运行 Exchange 的服务器必须确定另一个 Exchange 服务器的 Active Directory 站点成员身份时，前者可查询 Active Directory 以检索站点名称。

在 Exchange 2013 中，Microsoft Exchange Active Directory 拓扑服务负责更新 Exchange 服务器对象的站点属性。由于 Active Directory 站点成员身份为服务器对象属性，因此 Exchange 无需查询 DNS 即可解析与 Active Directory 站点相关联的子网的服务器地址。通过对 Exchange 服务器对象的 Active Directory 站点属性进行标记，可将 Active Directory 站点成员身份分配给非域成员的服务器（如订阅的边缘传输服务器）。

Exchange 2013 服务器使用 Active Directory 站点成员身份信息的情况如下所示：

  - **邮件提交**Exchange 2013 邮箱服务器上的邮箱传输提交服务使用 Active Directory 站点成员身份信息确定其他位于同一 Active Directory 站点中的 Exchange 2013 邮箱服务器。如果源邮箱服务器不属于 DAG，或 DAG 未跨越多个 Active Directory 站点，则源邮箱服务器上的“邮箱传输提交”服务提交邮件，然后将邮件路由并传输到位于同一 Active Directory 站点中的 Exchange 2013 邮箱服务器的传输服务。

  - **邮件传递**Exchange 2013 邮箱服务器上的传输服务执行收件人解析，并查询 Active Directory，使电子邮件地址与收件人帐户匹配。收件人帐户信息包括用户的邮箱数据库的完全限定域名 (FQDN)。传输服务查询 Active Directory，以确定用户的邮箱数据库的 Active Directory 站点。如果邮箱数据库不属于 DAG，则将邮件传递到该邮箱服务器。否则，它会将邮件中继到与目标邮箱服务器相同的站点内的另一个邮箱服务器进行传递。

  - **邮件路由**Exchange 2013 邮箱服务器上的传输服务从 Active Directory 检索信息，以确定邮件在组织内部路由的方式。Exchange 2013 使用“传递组”的概念确定邮件路由的位置和方式。邮件可根据目标路由到传输服务、Exchange 2013 邮箱服务器上的邮箱传输传递服务，或运行 Exchange 早期版本的集线器传输服务器上。有关详细信息，请参阅[邮件路由](mail-routing-exchange-2013-help.md)。

  - **统一消息邮件提交**Exchange 2013 邮箱服务器上的统一邮件服务使用 Active Directory 站点成员关系信息查找位于同一 Active Directory 站点中的其他邮箱服务器。统一邮件服务提交邮件以路由到位于同一 Active Directory 站点中的邮箱服务器上的传输服务。传输服务服务器执行收件人解析，并查询 Active Directory，使电话号码、E.164 号码或 SIP 地址与收件人帐户相匹配。收件人解析完成之后，传输服务器采用与常规电子邮件相同的方式将邮件发往目标邮箱。

  - **客户端与客户端访问服务器连接**   客户端访问服务器收到用户连接请求时，会查询 Active Directory，以确定哪个邮箱服务器承载用户的邮箱。然后，客户端访问服务器检索该邮箱服务器的 Active Directory 站点成员身份，并通过代理连接到邮箱服务器。

## 确定 Active Directory 站点成员身份

Active Directory 客户端通过将所分配的 IP 地址与 Active Directory 站点和服务中定义、并与 Active Directory 站点关联的子网相匹配，从而假设其站点成员身份。然后，客户端使用此信息确定该站点内存在哪些域控制器和全局编录服务器，并与这些目录服务器通信进行身份验证和授权。Exchange 2013 还利用此关系优先从与 Exchange 2013 服务器位于同一站点内的目录服务器检索有关收件人的信息。

如果网络连接高速可靠，则将属于同一 Active Directory 站点的所有计算机都视为连接状态良好。默认情况下，首次部署 Active Directory 林时，将只有一个名为 `Default-First-Site-Name` 的站点。如果管理员未手动配置其他站点，则该林中的所有服务器和客户端计算机都将被视为 `Default-First-Site-Name` 的成员。

如果定义了多个站点，则 Active Directory 管理员必须定义组织中现有的子网，并将这些子网与 Active Directory 站点相关联。

Microsoft Exchange Active Directory 拓扑服务在服务器启动时检查 Exchange 服务器对象上的站点成员身份属性。如果必须更新站点属性，Microsoft Exchange Active Directory 拓扑服务将使用新值来标记该属性。Microsoft Exchange Active Directory 拓扑服务每 15 分钟验证一次站点属性值，如果站点成员身份发生更改，还会更新该值。Microsoft Exchange Active Directory 拓扑服务使用网络登录服务获取当前站点成员身份。网络登录服务每五分钟更新一次站点成员身份。这表示在站点成员身份发生变化时与在站点属性上标记新值时之间最长可能有 20 分钟的延迟期。

## IP 站点链接概述

Active Directory 站点之间的关系由 IP 站点链接定义。IP 站点链接由两个或更多 Active Directory 站点组成。属于链接的所有 Active Directory 站点以相同的成本进行通信。IP 站点链接属性包括开销分配、日程安排以及间隔。日程安排和间隔属性仅用于确定 Active Directory 复制频率。当目标存在多个路径时，Exchange 2013 使用成本分配确定流量要遵循的最低成本路由。通过累计传输路径中所有站点链接的开销来确定路由的开销。Active Directory 管理员将根据相对网络速度和可用带宽（与其他可用连接相比）为链接分配成本。

默认情况下，邮箱服务器上的传输服务始终尝试直接连接到其他 Active Directory 站点中邮箱服务器上的传输服务或邮箱传输传递服务。传输中的邮件不会通过站点链接路径中每个邮箱服务器上的传输服务进行中继。但是，路由路径上中间 Active Directory 站点中的邮箱服务器可以在下列情况下执行邮件中继操作：

  - 当最低成本路由路径上存在中心站点时，在邮箱服务器之间不会发生直接中继。可以将 Active Directory 站点配置为中心站点，以便先将邮件路由到集线器站点，然后再将邮件中继到目标服务器。本主题稍后部分中将就集线器站点进行讨论。

  - 与目标 Active Directory 站点通信失败时，Exchange 2013 会使用从 IP 站点链接信息中得到的路由路径。如果目标 Active Directory 站点中没有邮箱服务器响应，则邮件传递将沿成本最低的路由路径回退，直到沿路由路径建立起与 Active Directory 站点中的邮箱服务器的连接。在该 Active Directory 站点中会对邮件进行排队，队列将处于重试状态。该行为称为“在故障点排队”。

  - 在不带 DAG 的 Exchange 2013 组织中，邮箱服务器上的传输服务还可使用 IP 站点链接信息来优化发送到多个收件人的邮件路由。邮件服务器将延迟邮件的收件人拆分，直至到达指向收件人的路由路径中的某个分支为止。经过收件人拆分的邮件将由代表单独路由路径中分支的 Active Directory 站点中的邮箱服务器中继到每个收件人目标位置。此功能称为“延迟扇出”。

## 指定中心站点

可使用 **Set-AdSite** cmdlet 将 Active Directory 站点配置为中心站点。当中心站点存在于两个传输服务器之间的最小成本路由路径时，邮件会先路由到中心站点进行处理，然后再中继到目标服务器。若要执行此路由操作，中心站点必须在两台传输服务器之间成本最少的路由路径上。应仅在网络拓扑需要此设置时才使用此配置，例如，因 Active Directory 站点间存在防火墙而阻碍 SMTP 通信的直接中继时。有关详细信息，请参阅[配置 Active Directory 中的 Exchange 邮件路由设置](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

## 对 IP 站点链接设置 Exchange 的特定开销

可在 Exchange 命令行管理程序中使用 **Set-AdSiteLink** cmdlet 将 Exchange 特定的成本设置为 Active Directory IP 站点链接。Exchange 特定的成本是一个单独的属性，用于代替 Active Directory 分配的成本以确定 Exchange 路由路径。当 Active Directory IP 站点链接成本无法得到最佳的 Exchange 邮件路由拓扑时，此配置将非常有用。有关详细信息，请参阅[配置 Active Directory 中的 Exchange 邮件路由设置](configure-exchange-mail-routing-settings-in-active-directory-exchange-2013-help.md)。

## 对 IP 站点链接设置邮件大小限制

默认情况下，Exchange 2013 对于在不同 Active Directory 站点中的邮箱服务器之间中继的邮件不施加最大邮件大小限制。如果使用 **Set-AdSiteLink** cmdlet 对 Active Directory IP 站点链接配置最大邮件大小，则路由将对大于最大邮件大小限制的任何邮件生成未送达报告 (NDR)，该最大邮件大小限制是针对最小成本路由路径中任何 Active Directory 站点链接配置的。如果要限制发送到必须通过低带宽连接进行通信的远程 Active Directory 站点的邮件大小，则此配置十分有用。

## 在 Active Directory 站点中部署 Exchange 2013

若要在 Exchange 2013 服务器之间正确地路由邮件，林中部署的所有 Exchange 服务器都必须属于 Active Directory 站点。请确保已分配的 IP 地址位于与 Active Directory 站点正确关联的子网中。

在规划 Active Directory 站点拓扑中的 Exchange 2013 服务器的部署过程中，第一步是记录当前拓扑。您的文档应包含以下内容：

  - 站点

  - 子网及其站点关联

  - IP 站点链接及其成员站点

  - IP 站点链接开销

  - 每个站点中的目录服务器

  - 物理网络连接

  - 防火墙位置

用图解法表示这些对象之后，即可规划 Exchange 服务器的部署。在确定服务器的放置位置时，请考虑以下信息：

  - 邮箱服务器需与全局编录服务器直接通信，以执行 Active Directory 查找。

  - 建议您在每个 Active Directory 站点中部署多个邮箱服务器，以提供负载平衡和容错功能。

  - DAG 与站点恢复

  - 邮箱服务器上的统一邮件服务将语音邮件提交到邮箱服务器上的传输服务，以便传递到邮箱。运行统一消息呼叫路由器服务的客户端访问服务器可能位于中心站点或者 IP 网关或 Voice over IP (VoIP) 网关、IP 专用交换机 (IP PBX)、启用了 SIP 的 PBX 或会话边界控制器 (SBC) 附近。具有与客户端访问服务器相同的站点成员关系的邮箱服务器上的传输服务将收到语音邮件，然后将邮件传输并路由到组织中其他邮箱服务器上的传输服务。

  - 客户端访问服务器将为远程访问 Exchange 的用户提供到达 Exchange 组织的连接点。客户端访问服务器必须部署在每个包含邮箱服务器的 Active Directory 站点中。

规划 Exchange 2013 服务器位置后，可确定可在哪些区域修改 Active Directory 站点拓扑以改善通信流。您可能需要调整 IP 站点链接和站点链接成本，以优化邮件传递。高效的 Active Directory 拓扑不需要任何更改即可支持 Exchange 2013。

