---
title: '非连续命名空间应用场景: Exchange 2013 Help'
TOCTitle: 非连续命名空间应用场景
ms:assetid: 90101d49-6f45-44be-8a93-eeb2c8283e3b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb676377(v=EXCHG.150)
ms:contentKeyID: 50491162
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 非连续命名空间应用场景

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

本主题提供了有关脱节命名空间的概念以及用于在具有脱节命名空间的域中部署 Microsoft Exchange 2013 的受支持方案的信息。

**目录**

DNS 和 NetBIOS 域名

脱节命名空间

Exchange 2013 和脱节命名空间

允许 Exchange 2013 服务器访问脱节的域控制器

查看运行 Windows Server 2008 的计算机的 DNS 和 NetBIOS 名称信息

## DNS 和 NetBIOS 域名

首先，介绍一些背景知识。Internet 上的每台计算机都有域名系统 (DNS) 名称。该名称也称为“*计算机名称*”或“*主机名*”。每台运行 Windows 操作系统并具有联网功能的计算机还具有一个 NetBIOS 名称。

在 Active Directory 域中运行 Windows 的计算机同时拥有 DNS 域名和 NetBIOS 域名，如下所示：

  - **DNS 域名**   DNS 域名由一个或多个以圆点“**.**”分隔的子域组成，并以顶级域名结束。例如，在 DNS 域名 corp.contoso.com 中，子域为 corp 和 contoso，顶级域名为 com。

  - **NetBIOS 域名**   通常情况下，NetBIOS 域名是 DNS 域名的子域。例如，如果 DNS 域名是 contoso.com，则 NetBIOS 域名是 contoso。如果 DNS 域名是 corp.contoso.com，则 NetBIOS 域名是 corp。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要查找运行 Windows Server 2008 的计算机的 DNS 和 NetBIOS 信息，请参阅查看运行 Windows Server 2008 的计算机的 DNS 和 NetBIOS 名称信息。</td>
</tr>
</tbody>
</table>


Active Directory 域中的计算机还具有主 DNS 后缀，并且可以包含其他 DNS 后缀。默认情况下，主 DNS 后缀与 DNS 域名相同。有关如何更改主 DNS 后缀的详细步骤，请参阅本主题中后面部分的步骤。

配置 Active Directory 域中的第一个域控制器时，定义该域的 DNS 域名和 NetBIOS 域名。有关配置域控制器的详细信息，请参阅[域控制器角色](https://go.microsoft.com/fwlink/p/?linkid=268367)和 [Active Directory 域服务概述](https://go.microsoft.com/fwlink/p/?linkid=268366)。

## 脱节命名空间

在大多数域拓扑中，域中的计算机的主 DNS 后缀与 DNS 域名相同。

在某些情况下，可能要求这些命名空间各不相同。这称为“*脱节命名空间*”。例如，合并或收购可能会导致拓扑包含脱节命名空间。此外，如果在管理 Active Directory 的管理员与管理网络的管理员之间分配公司中的 DNS 管理任务，可能需要拓扑包含脱节命名空间。

脱节命名空间方案是一种计算机的主 DNS 后缀与该计算机所在的 DNS 域名不相符的情况。带有不相符的主 DNS 后缀的计算机被称为“*脱节*”。另一种脱节命名空间方案是域控制器的 NetBIOS 域名与 DNS 域名不相符。

## Exchange 2013 和脱节命名空间

Exchange 2013 支持下列三种在拥有脱节命名空间的域中部署 Exchange 的方案：

  - **主 DNS 后缀与 DNS 域名不相同**   域控制器的主 DNS 后缀与 DNS 域名不相同。作为域成员的计算机可以是脱节的，也可以是不脱节的。

  - **成员计算机脱节**   Active Directory 域中的成员计算机脱节，但域控制器不脱节。

  - **域控制器的 NetBIOS 名称与其 DNS 域名的子域不相同**   域控制器的 NetBIOS 域名与该域控制器的 DNS 域名的子域不相同。

下列各部分详细介绍了这些方案。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在本主题中所述的脱节命名空间方案中，支持运行 Exchange 2013。但是，如果脱节命名空间方案不是本主题所述方案之一，则必须使用 Microsoft 服务来部署 Exchange 2013。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=94845">Microsoft 服务</a>。</td>
</tr>
</tbody>
</table>


## 方案：主 DNS 后缀与 DNS 域名不相同

在该方案中，域控制器的主 DNS 后缀与 DNS 域名不同。该方案中的域控制器是脱节的。作为域成员的计算机（包括 Exchange 服务器和 Microsoft Outlook 客户端计算机）的主 DNS 后缀可以与域控制器的主 DNS 后缀相匹配，也可以与 DNS 域名相匹配。

## 方案：成员计算机是脱节的

在该方案中，安装了 Exchange 2013 的成员计算机的主 DNS 后缀与 DNS 域名不同，但是域控制器的主 DNS 后缀与 DNS 域名相同。在该方案中，有一个不脱节的域控制器和一个脱节的成员计算机。运行 Outlook 的成员计算机的主 DNS 后缀可以与脱节 Exchange 服务器的主 DNS 后缀相匹配，也可以与 DNS 域名相匹配。

## 方案：域控制器的 NetBIOS 名与其 DNS 域名的子域不相同

在该方案中，域控制器的 NetBIOS 域名与同一域控制器的 DNS 域名不同。

**NetBIOS 域名与 DNS 域名不相符**

![NetBIOS 域名与 DNS 域名不匹配](images/Bb676377.1ee18cb6-0296-4875-b572-0ddf33f65f7c(EXCHG.150).gif "NetBIOS 域名与 DNS 域名不匹配")

## 允许 Exchange 2013 服务器访问脱节的域控制器

要允许 Exchange 2013 服务器访问脱节的域控制器，必须修改域对象容器的 **msDS-AllowedDNSSuffixes**Active Directory 属性。必须将两个 DNS 后缀均添加到该属性中。有关如何修改该属性的详细步骤，请参阅[计算机的主 DNS 后缀与它所在域的 FQDN 不匹配](https://go.microsoft.com/fwlink/p/?linkid=98848)。

此外，为了确保 DNS 后缀搜索列表包含组织中部署的所有 DNS 命名空间，必须为域中每台脱节的计算机配置搜索列表。命名空间列表不仅要包含域控制器的主 DNS 后缀和 DNS 域名，还要包含 Exchange 可与之互操作的其他服务器（例如，监视服务器或第三方应用程序服务器）的所有其他命名空间。可以通过设置域的组策略完成此任务。有关组策略的详细信息，请参阅下列主题：

  - [组策略常见问题 (FAQ)](https://go.microsoft.com/fwlink/p/?linkid=100128)

  - [Windows Server 2003 中的新 DNS 组策略](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=294785)

  - [组策略](https://go.microsoft.com/fwlink/p/?linkid=268043)

有关如何配置 DNS 后缀搜索列表组策略的详细步骤，请参阅[为非连续命名空间配置 DNS 后缀搜索列表](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md)。

## 查看运行 Windows Server 2008 的计算机的 DNS 和 NetBIOS 名称信息

1.  单击“开始”，右键单击“计算机”，然后单击“属性”。

2.  在“**系统**”中，DNS 主机名和主 DNS 后缀显示在“**计算机名称、域和工作组设置**”下“**完整计算机名**”旁边。DNS 域名显示在“**域**”的旁边。

3.  单击“更改设置”。

4.  在“系统属性”的“计算机名称”选项卡上，单击“更改”。

5.  在“**计算机名称/域更改**”中，单击“**更多**”。主 DNS 后缀显示在“**此计算机的主 DNS 后缀**”下。NetBIOS 计算机名称显示在“**NetBIOS 计算机名称**”下。
    
    要更改主 DNS 后缀，在“此计算机的主 DNS 后缀”下键入新的主 DNS 后缀，然后单击“确定”。

6.  在命令提示符窗口中，键入 **set**。此时变量 USERDNSDOMAIN 将显示 DNS 域名。变量 USERDOMAIN 将显示 NetBIOS 域名。

