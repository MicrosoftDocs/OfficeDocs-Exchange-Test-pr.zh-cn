---
title: 'Exchange 2013 系统要求: Exchange 2013 Help'
TOCTitle: Exchange 2013 系统要求
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50490183
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 系统要求

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

了解在安装 Exchange 2013 之前您需要知道的 Exchange 2013 要求。例如，您将了解有关硬件、网络和操作系统要求的信息。

安装 Microsoft Exchange Server 2013 之前，建议您查看本主题中的内容，以确保您的网络、硬件、软件、客户端和其他元素满足 Exchange 2013 的要求。此外，请确保了解支持 Exchange 2013 和较早版本的 Exchange 的共存方案。

## 支持的共存方案

下表列出了一些支持 Exchange 2013 与早期版本的 Exchange 共存的方案。

### Exchange 2013 和早期版本的 Exchange Server 共存

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 版本</th>
<th>Exchange 组织共存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 和更早版本</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>1组织中所有 Exchange 2007 服务器（包括边缘传输服务器）上的 Exchange 2007 Service Pack 3 (SP3) 更新汇总 10。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 累计更新 2 (CU2) 或更高版本。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>2组织中所有 Exchange 2010 服务器（包括边缘传输服务器）上的 Exchange 2010 SP3。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 CU2 或更高版本。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2010 和 Exchange 2007 的混合组织</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>1组织中所有 Exchange 2007 服务器（包括边缘传输服务器）上的 Exchange 2007 SP3 更新汇总 10。</p></li>
<li><p>2组织中所有 Exchange 2010 服务器（包括边缘传输服务器）上的 Exchange 2010 SP3。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 CU2 或更高版本。</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   如果您想要在 Exchange 2007 集线器传输服务器和 Exchange2013 SP1 边缘传输服务器之间创建 EdgeSync 订阅，您需要在 Exchange 2007 集线器传输服务器上安装 Exchange 2007 SP3 更新汇总 13 或更高版本。

2   如果您想要在 Exchange 2010 集线器传输服务器和 Exchange 2013 SP1 边缘传输服务器之间创建 EdgeSync 订阅，您需要在 Exchange 2010 集线器传输服务器上安装 Exchange 2010 SP3 更新汇总 5 或更高版本。

## 支持的混合部署方案

Exchange 2013 支持已升级到 Office 365 最新版本的 Office 365 租户进行混合部署。有关特定混合部署的详细信息，请参阅[混合部署先决条件](https://technet.microsoft.com/zh-cn/library/hh534377\(v=exchg.150\))。

## 网络和目录服务器

下表列出了对 Exchange 2013 组织中网络和目录服务器的要求。

**Exchange 2013 的网络和目录服务器要求**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>架构主机</p></td>
<td><p>默认情况下，架构主机在林中安装的第一个 Active Directory 域控制器上运行。架构主机必须运行以下一种操作系统：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise（32 位或 64 位）</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更高版本（32 位或 64 位）</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更高版本（32 位或 64 位）</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>全局编录服务器</p></td>
<td><p>在您计划安装 Exchange 2013 的每个 Active Directory 站点中，您都必须有至少一个运行以下一种操作系统的全局编录服务器：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise（32 位或 64 位）</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更高版本（32 位或 64 位）</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更高版本（32 位或 64 位）</p></li>
</ul>
<p>有关全局编录服务器的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/p/?linkid=178996">什么是全局编录</a>。</p></td>
</tr>
<tr class="odd">
<td><p>域控制器</p></td>
<td><p>在您计划安装 Exchange 2013 的每个 Active Directory 站点中，您都必须有至少一个运行以下一种操作系统的可写域控制器：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard 或 Enterprise SP1 或更高版本</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2008 Standard 或 Enterprise SP1 或更高版本（32 位或 64 位）</p></li>
<li><p>Windows Server 2008 Datacenter RTM 或更高版本</p></li>
<li><p>Windows Server 2003 Standard Edition Service Pack 2 (SP2) 或更高版本（32 位或 64 位）</p></li>
<li><p>Windows Server 2003 Enterprise Edition SP2 或更高版本（32 位或 64 位）</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Active Directory 林</p></td>
<td><p>Active Directory 必须处于 Windows Server 2003 林功能模式或更高级别模式2。</p></td>
</tr>
<tr class="odd">
<td><p>DNS 命名空间支持</p></td>
<td><p>Exchange 2013 支持以下域名系统 (DNS) 命名空间：</p>
<ul>
<li><p>连续命名空间</p></li>
<li><p>分离命名空间</p></li>
<li><p>单标签域</p></li>
<li><p>不连续命名空间</p></li>
</ul>
<p>有关 Exchange 支持的 DNS 命名空间的详细信息，请参阅 Microsoft 知识库文章 2269838 <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2269838">Microsoft Exchange 与单标签域、不连续命名空间和分离命名空间的兼容性</a>。</p></td>
</tr>
<tr class="even">
<td><p>IPv6 支持</p></td>
<td><p>在 Exchange 2013 中，仅当 IPv4 也已安装并启用时，才支持 IPv6。如果此配置中已部署 Exchange 2013，并且网络支持 IPv4 和 IPv6，则所有 Exchange 服务器均可在使用 IPv6 地址的设备、服务器和客户端上发送和接收数据。有关详细信息，请参阅 <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的 IPv6 支持</a>。</p></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 仅在 Exchange 2013 SP1 或更高版本中受支持。

2   Windows Server 2012 R2 林功能模式仅在 Exchange 2013 SP1 或更高版本中受支持。

## 目录服务器体系结构

使用 64 位 Active Directory 域控制器可以提高 Exchange 2013 的目录服务性能。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在多域环境的将 Active Directory 语言区域设置为日语的 Windows Server 2008 域控制器上，服务器可能不接收在入站复制期间存储在对象上的某些属性。有关详细信息，请参阅 Microsoft 知识库文章 949189 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=949189">使用日语语言区域设置配置的 Windows Server 2008 域控制器配置可能不会在入站复制期间将更新应用于对象的属性</a>。</td>
</tr>
</tbody>
</table>


## 在目录服务器上安装 Exchange 2013

出于安全和性能的考虑，建议仅在成员服务器上安装 Exchange 2013，而不要在 Active Directory 目录服务器上安装。但不能在运行 Exchange 2013 的计算机上运行 DCPromo。安装 Exchange 2013 后，不支持将其角色从成员服务器更改为目录服务器，反之亦然。

## 硬件

为 Exchange 2013 服务器推荐的硬件要求因许多因素而异，包括所安装的服务器角色和服务器上将放置的预期负载。

有关如何正确调整和配置您的部署的详细信息，请参阅 [Exchange 2013 大小调整和配置建议](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md)。

有关在虚拟化环境中部署 Exchange 的信息，请参阅[Exchange 2013 虚拟化](exchange-2013-virtualization-exchange-2013-help.md)。

**Exchange 2013 的硬件要求**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>要求</th>
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>处理器</p></td>
<td><ul>
<li><p>基于 x64 体系结构的计算机，具有支持 Intel 64 位体系结构（以前称为 Intel EM64T）的 Intel 处理器</p></li>
<li><p>支持 AMD64 平台的 AMD 处理器</p></li>
<li><p>Intel Itanium IA64 处理器不受支持</p></li>
</ul></td>
<td><p>有关支持的操作系统，请参阅本主题后面的“操作系统”一节。</p></td>
</tr>
<tr class="even">
<td><p>内存</p></td>
<td><p>因所安装的 Exchange 角色而异：</p>
<ul>
<li><p><strong>邮箱</strong>   最小 8 GB</p></li>
<li><p><strong>客户端访问</strong>   最小 4 GB</p></li>
<li><p><strong>邮箱和客户端访问组合</strong>   最小 8 GB</p></li>
<li><p><strong>边缘传输</strong>   最小 4GB</p></li>
</ul></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>页面文件大小</p></td>
<td><p>如果您使用超过 32 GB 的 RAM，最小和最大页面文件大小必须设置为物理 RAM 加 10 MB，最大值为 32778 MB。</p></td>
<td><p>有关详细的页面文件建议，请参阅 <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Exchange 2013 大小调整和配置建议</a>中的“页面文件”部分。</p></td>
</tr>
<tr class="even">
<td><p>磁盘空间</p></td>
<td><ul>
<li><p>安装 Exchange 的驱动器上至少要有 30 GB 的可用磁盘空间</p></li>
<li><p>对于您要安装的每个统一消息 (UM) 语言包，需要另外 500 MB 的可用磁盘空间</p></li>
<li><p>系统驱动器上具有 200 MB 的可用磁盘空间</p></li>
<li><p>存储邮件队列数据库的硬盘至少具有 500 MB 的可用空间。</p></li>
</ul></td>
<td><p>有关详细的存储建议，请参阅 <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Exchange 2013 存储配置选项</a>。</p></td>
</tr>
<tr class="odd">
<td><p>驱动器</p></td>
<td><p>DVD-ROM 驱动器（可从本地或网络访问）</p></td>
<td><p>无。</p></td>
</tr>
<tr class="even">
<td><p>屏幕分辨率</p></td>
<td><p>1024 x 768 像素或更高</p></td>
<td><p>无。</p></td>
</tr>
<tr class="odd">
<td><p>文件格式</p></td>
<td><p>格式化为 NTFS 文件系统的磁盘分区，这适用于下列分区：</p>
<ul>
<li><p>系统分区</p></li>
<li><p>存储由 Exchange 诊断日志生成的 Exchange 二进制文件或文件的分区</p></li>
</ul>
<p>包括以下文件类型的磁盘分区可以格式化为 ReFS：</p>
<ul>
<li><p>包含事务日志文件的分区</p></li>
<li><p>包含数据库文件的分区</p></li>
<li><p>包含内容索引文件的分区</p></li>
</ul></td>
<td><p>无。</p></td>
</tr>
</tbody>
</table>


## 操作系统

下表列出了用于 Exchange 2013 的受支持的操作系统。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支持在 Windows Server Core 模式中运行的计算机上安装 Exchange 2013。计算机必须运行 Windows Server 的完全安装。如果要在 Windows Server Core 模式中运行的计算机上安装 Exchange 2013，您必须通过执行以下某项操作，将服务器转换为 Windows Server 的完全安装：
<ul>
<li><p><strong>Windows Server 2008 R2</strong>   重新安装 Windows Server 并选择“完全安装”选项。</p></li>
<li><p><strong>Windows Server 2012 R2</strong> 或 <strong>Windows Server 2012</strong>   通过运行以下命令将 Windows Server Core 模式服务器转换为完全安装。</p>
<pre><code>Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart</code></pre></li>
</ul></td>
</tr>
</tbody>
</table>


**Exchange 2013 的受支持的操作系统**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>组件</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮箱、客户端访问和边缘传输服务器角色</p></td>
<td><p>下列内容之一：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>带有 Service Pack 1 (SP1) 的 Windows Server 2008 R2 Standard</p></li>
<li><p>带有 Service Pack 1 (SP1) 的 Windows Server 2008 R2 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更高版本</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>管理工具</p></td>
<td><p>下列内容之一：</p>
<ul>
<li><p>Windows Server 2012 R2 Standard 或 Datacenter1</p></li>
<li><p>Windows Server 2012 Standard 或 Datacenter</p></li>
<li><p>带有 SP1 的 Windows Server 2008 R2 Standard</p></li>
<li><p>带有 SP1 的 Windows Server 2008 R2 Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM 或更高版本</p></li>
<li><p>64 位版本的 Windows 8.12</p></li>
<li><p>64 位版本的 Windows 8</p></li>
<li><p>带有 Service Pack 1 的 Windows 7 的 64 位版本</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Windows Server 2012 R2 仅受 Exchange 2013 SP1 或更高版本支持。

2   Windows 8.1 仅受 Exchange 2013 SP1 或更高版本支持。

**Exchange 2013 支持的 Windows Management Framework 版本**

Exchange 2013 仅支持内置于你在其上安装 Exchange 的 Windows 发布的 Windows Management Framework 版本。不要在运行 Exchange 的服务器上安装可供独立下载的 Windows Management Framework 版本。

## .NET Framework

强烈建议您使用受您正在安装的 Exchange 版本所支持的 .NET Framework 的最新版本。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 版本</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU16</p></td>
<td><p> X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU15</p></td>
<td><p> X</p></td>
<td><p>X1,2 </p></td>
<td><p> X</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU13 和 CU14</p></td>
<td> </td>
<td><p>X1,2 </p></td>
<td><p>X</p></td>
</tr>
</tbody>
</table>


1如果想要在运行 Exchange 2013 CU13 的服务器上安装 .NET Framework 4.6.1，则其需要发布后的修补程序。有关详细信息，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

2 如果你正从 Exchange 2013 CU12 或更早版本升级到 Exchange 2013 CU13、CU14 或 CU15，我们强烈建议你在安装 .NET Framework 4.6.1 及其相关的发布后的修补程序前安装 Exchange 2013 CU13。

## 支持的客户端

Exchange 2013 支持 Outlook 和 Entourage for Mac 的下列版本：

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 for Mac Web Services Edition

  - Office 365 适用的 Outlook for Mac

  - Outlook for Mac 2011

有关 Exchange 支持的 Outlook 版本列表，请参阅 [Outlook 更新](https://go.microsoft.com/fwlink/p/?linkid=513459)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>强烈建议您安装最新可用的 Service Pack 和可用更新，以便您的用户在连接到 Exchange 时获得可能的最佳体验。</td>
</tr>
</tbody>
</table>


不支持版本低于 Outlook 2007 的 Outlook 客户端。不支持 Mac 操作系统上需要 DAV 的电子邮件客户端，例如 Entourage 2008 for Mac RTM 和 Entourage 2004。

Outlook Web App 在各种操作系统和设备上支持多种浏览器。有关详细信息，请参阅[Exchange 2013 中 Outlook Web App 的新增内容](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)。

