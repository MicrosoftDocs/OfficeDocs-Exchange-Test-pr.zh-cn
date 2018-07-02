---
title: 'Exchange 2013 存储配置选项: Exchange 2013 Help'
TOCTitle: Exchange 2013 存储配置选项
ms:assetid: 37cdeacf-74f9-4399-9860-4d1dbec12bb1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee832792(v=EXCHG.150)
ms:contentKeyID: 50490316
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 存储配置选项

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

了解 Microsoft Exchange Server 2013 中的邮箱服务器角色的存储选项和要求是邮箱服务器存储设计解决方案的重要组成部分。

**目录**

存储结构

物理磁盘类型

支持的存储配置的最佳实践

## 存储结构

下表介绍支持的存储体系结构，并为每种类型的存储体系结构提供最佳实践指南（如果适用）。

### 支持的存储体系结构

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>存储体系结构</th>
<th>描述</th>
<th>最佳实践</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>直接附加存储 (DAS)</p></td>
<td><p>DAS 是一种直接附加到服务器或工作站（中间不使用存储网络）的数字存储系统。例如，DAS 传输包括串行附加小型计算机系统接口 (SCSI) 和串行附加高级技术附件 (ATA)。</p></td>
<td><p>不可用。</p></td>
</tr>
<tr class="even">
<td><p>存储区域网络 (SAN)：Internet 小型计算机系统接口 (iSCSI)</p></td>
<td><p>SAN 是一种将远程计算机存储设备（如磁盘阵列和磁带库）附加到服务器的体系结构，这样一来设备就像是在本地附加到操作系统（例如块存储）一样。iSCSI SAN 将 SCSI 命令封装在 IP 数据包内，使用标准网络基础结构作为存储传输（例如以太网）。</p></td>
<td><p>请勿与其他应用程序共享物理磁盘备份 Exchange 数据。</p>
<p>使用专用存储网络。</p>
<p>对独立配置使用多个网络路径。</p></td>
</tr>
<tr class="odd">
<td><p>SAN：光纤通道</p></td>
<td><p>光纤通道 SAN 将 SCSI 命令封装在光纤通道数据包内，通常利用专用光纤通道网络作为存储传输。</p></td>
<td><p>请勿与其他应用程序共享物理磁盘备份 Exchange 数据。</p>
<p>对独立配置使用多个光纤通道网络路径。</p>
<p>按照存储供应商的最佳实践调整光纤通道主机总线适配器 (HBA)，例如队列深度和队列目标。</p></td>
</tr>
</tbody>
</table>


网络附加存储 (NAS) 单元是连接到网络的自包含计算机，唯一用途是向网络上的其他设备提供基于文件的数据存储服务。NAS 单元上的操作系统和其他软件提供数据存储、文件系统和文件访问的功能，以及对这些功能（例如文件存储）的管理。

Exchange 用于存储 Exchange 数据的所有存储空间必须为块级存储空间，因为 Exchange 2013 不支持使用 NAS 卷，但在 [Exchange 2013 虚拟化](exchange-2013-virtualization-exchange-2013-help.md) 主题中所述的 SMB 3.0 情况下除外。此外，在虚拟化环境中，不支持通过虚拟机监控程序以块级存储形式向来宾提供的 NAS 存储。

不建议使用存储层，因为它可能会降低系统性能。出于此原因，请勿允许存储控制器自动将最常访问的文件移到“更快”的存储。

存储结构

## 物理磁盘类型

下表列出了支持的物理磁盘类型，并为每种物理磁盘类型提供最佳实践指南（如果适用）。

### 支持的物理磁盘类型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>物理磁盘类型</th>
<th>描述</th>
<th>支持的实践或最佳实践</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>串行 ATA (SATA)</p></td>
<td><p>SATA 是用于 ATA 和集成驱动电子设备 (IDE) 磁盘的串行接口。SATA 磁盘具有各种尺寸、速度和容量。</p>
<p>一般来说，如果您有以下设计要求，则可以为 Exchange 2013 邮箱存储选择 SATA 磁盘：</p>
<ul>
<li><p>高容量</p></li>
<li><p>中等性能</p></li>
<li><p>中等电源利用率</p></li>
</ul></td>
<td><p>支持：Windows Server 2008 和 Windows Server 2008 R2 支持 512 字节扇区磁盘。另外，具有以下内容的 Windows Server 2008 R2 支持 512e 磁盘：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知识库文章 982018</a>“现已推出可改善 Windows 7 和 Windows Server 2008 R2 与高级格式磁盘之间兼容性的更新”中介绍的修补程序。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更高版本支持本机 4 千字节 (KB) 扇区磁盘和 512e 磁盘。支持要求数据库的所有副本均位于同一类型的物理磁盘上。例如，以下配置不受支持：在 512 字节扇区磁盘上托管给定数据库的一个副本，而在 512e 磁盘或 4 K 磁盘上托管同一数据库的另一个副本。</p>
<p>最佳实践：考虑企业级 SATA 磁盘，这类磁盘通常具有更好的热量、震动和可靠性特征。</p></td>
</tr>
<tr class="even">
<td><p>串行附加 SCSI</p></td>
<td><p>串行附加 SCSI 是用于 SCSI 磁盘的串行接口。串行附加 SCSI 磁盘具有各种尺寸、速度和容量。</p>
<p>一般来说，如果您有以下设计要求，则可以为 Exchange 2013 邮箱存储选择串行附加 SCSI 磁盘：</p>
<ul>
<li><p>中等容量</p></li>
<li><p>高性能</p></li>
<li><p>中等电源利用率</p></li>
</ul></td>
<td><p>支持：Windows Server 2008 和 Windows Server 2008 R2 支持 512 字节扇区磁盘。另外，具有以下内容的 Windows Server 2008 R2 支持 512e 磁盘：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知识库文章 982018</a>“现已推出可改善 Windows 7 和 Windows Server 2008 R2 与高级格式磁盘之间兼容性的更新”中介绍的修补程序。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更高版本支持本机 4 千字节 (KB) 扇区磁盘和 512e 磁盘。支持要求数据库的所有副本均位于同一类型的物理磁盘上。例如，以下配置不受支持：在 512 字节扇区磁盘上托管给定数据库的一个副本，而在 512e 磁盘或 4 K 磁盘上托管同一数据库的另一个副本。</p>
<p>最佳实践：在没有 UPS 的情况下使用时，必须禁用物理磁盘写入缓存。</p></td>
</tr>
<tr class="odd">
<td><p>光纤通道</p></td>
<td><p>光纤通道是用于将磁盘连接到基于光纤通道的 SAN 的电气接口。光纤通道磁盘具有各种速度和容量。</p>
<p>一般来说，如果您有以下设计要求，则可以为 Exchange 2013 邮箱存储选择光纤通道磁盘：</p>
<ul>
<li><p>中等容量</p></li>
<li><p>高性能</p></li>
<li><p>SAN 连接</p></li>
</ul></td>
<td><p>支持：Windows Server 2008 和 Windows Server 2008 R2 支持 512 字节扇区磁盘。另外，具有以下内容的 Windows Server 2008 R2 支持 512e 磁盘：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知识库文章 982018</a>“现已推出可改善 Windows 7 和 Windows Server 2008 R2 与高级格式磁盘之间兼容性的更新”中介绍的修补程序。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更高版本支持本机 4 千字节 (KB) 扇区磁盘和 512e 磁盘。支持要求数据库的所有副本均位于同一类型的物理磁盘上。例如，以下配置不受支持：在 512 字节扇区磁盘上托管给定数据库的一个副本，而在 512e 磁盘或 4 K 磁盘上托管同一数据库的另一个副本。</p>
<p>最佳实践：在没有 UPS 的情况下使用时，必须禁用物理磁盘写入缓存。</p></td>
</tr>
<tr class="even">
<td><p>固态驱动器 (SSD)（闪存磁盘）</p></td>
<td><p>SSD 是使用固态内存存储永久性数据的数据存储设备。SSD 会模拟硬盘驱动器接口。SSD 磁盘具有各种速度（不同的 I/O 性能）和容量。</p>
<p>一般来说，如果您有以下设计要求，则可以为 Exchange 2013 邮箱存储选择 SSD 磁盘：</p>
<ul>
<li><p>低容量</p></li>
<li><p>极高的性能</p></li>
</ul></td>
<td><p>支持：Windows Server 2008 和 Windows Server 2008 R2 支持 512 字节扇区磁盘。另外，具有以下内容的 Windows Server 2008 R2 支持 512e 磁盘：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=982018">Microsoft 知识库文章 982018</a>“现已推出可改善 Windows 7 和 Windows Server 2008 R2 与高级格式磁盘之间兼容性的更新”中介绍的修补程序。</p></li>
<li><p>Windows Server 2008 R2 Service Pack 1 (SP1) 和 Exchange Server 2010 SP1。</p></li>
</ul>
<p>Exchange 2013 和更高版本支持本机 4 千字节 (KB) 扇区磁盘和 512e 磁盘。支持要求数据库的所有副本均位于同一类型的物理磁盘上。例如，以下配置不受支持：在 512 字节扇区磁盘上托管给定数据库的一个副本，而在 512e 磁盘或 4 K 磁盘上托管同一数据库的另一个副本。</p>
<p>最佳实践：在没有 UPS 的情况下使用时，必须禁用物理磁盘写入缓存。</p>
<p>Exchange 2013 邮箱服务器通常不需要 SSD 存储的性能特征。</p></td>
</tr>
</tbody>
</table>


## 选择磁盘类型时应考虑的因素

在为 Exchange 2013 存储选择磁盘类型时，需要进行一些权衡。正确的磁盘需要在性能（同时包括顺序和随机）与容量、可靠性、电源利用率和资金成本之间达到平衡。下表包含支持的物理磁盘类型，提供在考虑这些因素时对您有帮助的信息。

从性能角度来看，如果大型较慢的磁盘可以在负载下保持延迟为 20 毫秒的平均读写速度，则 Exchange 存储可以使用这些磁盘。

### 选择磁盘类型时应考虑的因素

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>磁盘速度 (RPM)</th>
<th>磁盘尺寸</th>
<th>接口或传输</th>
<th>容量</th>
<th>随机 I/O 性能</th>
<th>顺序 I/O 性能</th>
<th>电源利用率</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5,400</p></td>
<td><p>2.5 英寸</p></td>
<td><p>SATA</p></td>
<td><p>平均</p></td>
<td><p>较差</p></td>
<td><p>较差</p></td>
<td><p>极好</p></td>
</tr>
<tr class="even">
<td><p>5,400</p></td>
<td><p>3.5 英寸</p></td>
<td><p>SATA</p></td>
<td><p>极好</p></td>
<td><p>较差</p></td>
<td><p>较差</p></td>
<td><p>高于平均值</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>2.5 英寸</p></td>
<td><p>SATA</p></td>
<td><p>平均</p></td>
<td><p>平均</p></td>
<td><p>平均</p></td>
<td><p>极好</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>2.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>平均</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>极好</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5 英寸</p></td>
<td><p>SATA</p></td>
<td><p>极好</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
</tr>
<tr class="even">
<td><p>7,200</p></td>
<td><p>3.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>极好</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
</tr>
<tr class="odd">
<td><p>7,200</p></td>
<td><p>3.5 英寸</p></td>
<td><p>光纤通道</p></td>
<td><p>极好</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>平均</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>2.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>低于平均值</p></td>
<td><p>极好</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5 英寸</p></td>
<td><p>SATA</p></td>
<td><p>平均</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
</tr>
<tr class="even">
<td><p>10,000</p></td>
<td><p>3.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
<td><p>低于平均值</p></td>
</tr>
<tr class="odd">
<td><p>10,000</p></td>
<td><p>3.5 英寸</p></td>
<td><p>光纤通道</p></td>
<td><p>平均</p></td>
<td><p>高于平均值</p></td>
<td><p>高于平均值</p></td>
<td><p>低于平均值</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>2.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>较差</p></td>
<td><p>极好</p></td>
<td><p>极好</p></td>
<td><p>平均</p></td>
</tr>
<tr class="odd">
<td><p>15,000</p></td>
<td><p>3.5 英寸</p></td>
<td><p>串行附加 SCSI</p></td>
<td><p>平均</p></td>
<td><p>极好</p></td>
<td><p>极好</p></td>
<td><p>低于平均值</p></td>
</tr>
<tr class="even">
<td><p>15,000</p></td>
<td><p>3.5 英寸</p></td>
<td><p>光纤通道</p></td>
<td><p>平均</p></td>
<td><p>极好</p></td>
<td><p>极好</p></td>
<td><p>较差</p></td>
</tr>
<tr class="odd">
<td><p>SSD：企业级</p></td>
<td><p>不适用</p></td>
<td><p>SATA、串行附加 SCSI、光纤通道</p></td>
<td><p>较差</p></td>
<td><p>极好</p></td>
<td><p>极好</p></td>
<td><p>极好</p></td>
</tr>
</tbody>
</table>


存储结构

## 支持的存储配置的最佳实践

本节提供有关支持的磁盘和阵列控制器配置的最佳实践信息。

独立磁盘冗余阵列 (RAID) 通常用于提高各个磁盘的性能特征（通过在多个磁盘间使数据条带化）以及防范各个磁盘故障。随着 Exchange 2013 高可用性方面的改进，RAID 已不是 Exchange 2013 存储设计的必需组件。但是，对于针对独立服务器的 Exchange 2013 存储设计和需要存储容错功能的解决方案来说，RAID 仍然是一个基本组件。

**操作系统、系统或页面文件卷**

对于操作系统、系统或页面文件卷，推荐的配置是利用 RAID 技术保护该数据类型。虽然推荐的 RAID 配置为 RAID-1 或 RAID-1/0，但是支持所有的 RAID 类型。

**分开的邮箱数据库和日志卷**

如果您要部署独立的邮箱服务器角色体系结构，则邮箱数据库和日志卷需要 RAID 技术。对于邮箱卷的推荐 RAID 配置是 RAID-1/0（特别是如果您使用的是 5.4K 或 7.2K 磁盘）；但是支持所有的 RAID 类型。对于日志卷，推荐的 RAID 配置是 RAID-1 或 RAID-1/0。

针对操作系统、页面文件或 Exchange 数据卷使用 RAID-5 或 RAID-6 配置时，请注意以下内容：

  - 对于 RAID-5 配置（包括其变体如 RAID-50 和 RAID-51），每个阵列组应不多于 7 个磁盘，而且 RAID-5 配置应启用阵列控制器高优先级清理和表面扫描。

  - RAID-6 配置应启用阵列控制器高优先级清理和表面扫描。

虽然具有 3 个或更多高可用性数据库副本的高可用性体系结构支持 JBOD，但因为日志和邮箱数据库卷是分开的，所以不建议使用 JBOD。

**邮箱数据库和日志卷共用同一位置**

不建议在独立体系结构中使邮箱数据库和日志卷共用同一位置。在高可用性体系结构中，该方案有两种可能性：

1.  每个卷单个数据库

2.  每个卷多个数据库

**每个卷单个数据库**

对于 Exchange，JBOD 意味着将数据库及其关联日志同时存储在单个磁盘上。若要在 JBOD 上进行部署，必须至少部署三个高可用数据库副本。利用单个磁盘会成为单一故障点，因为当该磁盘发生故障时，驻留在该磁盘上的数据库副本会丢失。至少拥有三个数据库副本可确保实现容错能力，因为在一个副本（或一个磁盘）发生故障时还有其他两个副本。但是，三个高可用数据库副本的放置以及滞后数据库副本的使用可能会影响存储设计。下表显示了针对 RAID 或 JBOD 考虑事项的指导。

### RAID 或 JBOD 注意事项

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>数据中心服务器</th>
<th>两个高可用副本（总计）</th>
<th>三个高可用副本（总计）</th>
<th>每个数据中心具有两个或更多高可用副本</th>
<th>一个滞后副本</th>
<th>每个数据中心具有两个或更多滞后副本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主数据中心服务器</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD（2 个副本）</p></td>
<td><p>RAID 或 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD</p></td>
</tr>
<tr class="even">
<td><p>辅助数据中心服务器</p></td>
<td><p>RAID</p></td>
<td><p>RAID（1 个副本）</p></td>
<td><p>RAID 或 JBOD</p></td>
<td><p>RAID</p></td>
<td><p>RAID 或 JBOD</p></td>
</tr>
</tbody>
</table>


若要对主数据中心服务器在 JBOD 上进行部署，需要在 DAG 中包含三个或更多高可用数据库副本。如果在托管高可用数据库副本的同一个服务器上混合滞后副本（例如，不使用专用滞后数据库副本服务器），则至少需要两个滞后数据库副本。

若要使辅助数据中心服务器使用 JBOD，应在辅助数据中心中至少包含两个高可用数据库副本。辅助数据中心中的一个副本丢失不会导致需要跨 WAN 重新设定种子，也不会导致在激活辅助数据中心时形成单一故障点。如果在托管高可用数据库副本的同一个服务器上混合滞后数据库副本（例如，不使用专用滞后数据库副本服务器），则至少需要两个滞后数据库副本。

对于专用滞后数据库副本服务器，在数据中心中应至少有两个滞后数据库副本使用 JBOD。否则，丢失磁盘会导致丢失滞后数据库副本，以及丢失保护机制。

**每个卷多个数据库**

每个卷多个数据库是 Exchange 2013 中可用的新 JBOD 方案，允许在单个磁盘上混合主动和被动副本（包括滞后副本），从而实现更优的磁盘使用。但是，要以这种方式部署滞后副本，则必须启用自动滞后副本日志文件减少功能。下表显示用于每个卷多个数据库的 JBOD 注意事项指南。

### JBOD 注意事项

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>数据中心服务器</th>
<th>3 个或更多副本（总计）</th>
<th>每个数据中心具有两个或更多副本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主数据中心服务器</p></td>
<td><p>JBOD</p></td>
<td><p>JBOD</p></td>
</tr>
<tr class="even">
<td><p>辅助数据中心服务器</p></td>
<td><p>不适用</p></td>
<td><p>JBOD</p></td>
</tr>
</tbody>
</table>


下表提供有关 Exchange 2013 的存储阵列配置的指南。

### Exchange 2013 邮箱服务器角色支持的 RAID 类型

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>RAID 类型</th>
<th>描述</th>
<th>支持的做法或最佳做法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>磁盘阵列 RAID 带区大小 (KB)</p></td>
<td><p>条带大小是 RAID 集中每个磁盘的数据分布单位。条带大小也称为<em>块大小</em>。</p></td>
<td><p>最佳实践：256 KB 或更大。遵循存储供应商的最佳实践。</p></td>
</tr>
<tr class="even">
<td><p>存储阵列缓存设置</p></td>
<td><p>缓存设置由电池供电的缓存阵列控制器提供。</p></td>
<td><p>最佳实践：DAS 存储控制器 100% 的写入高速缓存（电池或闪存备份的缓存）位于 RAID 或 JBOD 配置中。75% 的写入高速缓存和 25% 的读取缓存（电池或闪存备份的缓存）用于其他类型的存储解决方案，如 SAN。如果您的 SAN 供应商在其平台上有针对不同缓存配置的最佳实践，请按照您的 SAN 供应商的指导进行操作。</p></td>
</tr>
<tr class="odd">
<td><p>物理磁盘写入缓存</p></td>
<td><p>可对每个磁盘设置该缓存。</p></td>
<td><p>支持：在没有 UPS 的情况下使用时，必须禁用物理磁盘写入缓存。</p></td>
</tr>
</tbody>
</table>


下表提供有关数据库和日志文件选项的指南。

### Exchange 2013 邮箱服务器角色的的数据库和日志文件选项

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>数据库和日志文件选项</th>
<th>描述</th>
<th>独立：支持的做法或最佳做法</th>
<th>高可用性：支持的做法或最佳做法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文件位置：数据库/日志隔离</p></td>
<td><p>数据库/日志隔离指将同一邮箱数据库中的数据库文件和日志放置在由不同物理磁盘支持的不同卷上。</p></td>
<td><p>最佳实践：为实现可恢复性，将同一数据库中的数据库 (.edb) 文件和日志移动到由不同物理磁盘备份的不同卷中。</p></td>
<td><p>支持：日志和数据库的隔离不是必需的。</p></td>
</tr>
<tr class="even">
<td><p>文件位置：数据库文件/卷</p></td>
<td><p>数据库文件/卷指如何在磁盘卷内或跨磁盘卷分布数据库文件。</p></td>
<td><p>最佳实践：基于您的备份方法。</p></td>
<td><p>支持：使用 JBOD 时，请为数据库和日志文件创建单个包含单独目录的卷。</p></td>
</tr>
<tr class="odd">
<td><p>文件位置：日志流/卷</p></td>
<td><p>日志流/卷指如何在磁盘卷内或跨磁盘卷分布数据库日志文件。</p></td>
<td><p>最佳实践：基于您的备份方法。</p></td>
<td><p>支持：使用 JBOD 时，请为数据库和日志文件创建单个包含单独目录的卷。</p>
<p>最佳实践：使用 JBOD 时，每卷利用多个数据库。</p></td>
</tr>
<tr class="even">
<td><p>数据库大小</p></td>
<td><p>数据库大小指磁盘数据库 (.edb) 文件大小。</p></td>
<td><p>支持：大约 16 TB。</p>
<p>最佳实践：</p>
<ul>
<li><p>200 GB 或更少。</p></li>
<li><p>按计算的最大数据库大小的 120% 设置。</p></li>
</ul></td>
<td><p>支持：大约 16 TB。</p>
<p>最佳实践：</p>
<ul>
<li><p>2 TB 或更少。</p></li>
<li><p>按计算的最大数据库大小的 120% 设置。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>日志截断方法</p></td>
<td><p>日志截断方法是截断并删除旧数据库日志文件的过程。有两种机制：</p>
<ul>
<li><p>循环日志记录，在这种机制中，Exchange 会删除日志。</p></li>
<li><p>日志截断，在完整或增量卷影复制服务 (VSS) 备份成功之后进行。</p></li>
</ul></td>
<td><p>最佳实践：</p>
<ul>
<li><p>使用备份执行日志截断（例如，禁用循环日志记录）。</p></li>
<li><p>按三天的日志生成容量设置。</p></li>
</ul></td>
<td><p>最佳实践：</p>
<ul>
<li><p>为使用 Exchange 本地数据保护功能的部署启用循环日志记录。</p></li>
<li><p>按超过重播延迟设置三天的日志生成容量设置。</p></li>
</ul></td>
</tr>
</tbody>
</table>


下表提供有关 Windows 磁盘类型的指南。

### Exchange 2013 邮箱服务器角色的 Windows 磁盘类型

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 磁盘类型</th>
<th>描述</th>
<th>独立：支持的做法或最佳做法</th>
<th>高可用性：支持的做法或最佳做法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>基本磁盘</p></td>
<td><p>初始化为基本存储的磁盘称为基本磁盘。基本磁盘包含基本卷，如主分区、扩展分区和逻辑驱动器。</p></td>
<td><p>支持。</p>
<p>最佳实践：使用基本磁盘。</p></td>
<td><p>支持。</p>
<p>最佳实践：使用基本磁盘。</p></td>
</tr>
<tr class="even">
<td><p>动态磁盘</p></td>
<td><p>初始化为动态存储的磁盘称为动态磁盘。动态磁盘包含动态卷，如简单卷、跨区卷、带区卷、镜像卷和 RAID-5 卷。</p></td>
<td><p>支持。</p></td>
<td><p>支持。</p></td>
</tr>
</tbody>
</table>


下表提供有关卷配置的指南。

### Exchange 2013 邮箱服务器角色的卷配置

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>卷配置</th>
<th>描述</th>
<th>独立：支持的做法或最佳做法</th>
<th>高可用性：支持的做法或最佳做法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GUID 分区表 (GPT)</p></td>
<td><p>GPT 是一种在旧式主启动记录 (MBR) 分区方案上扩展得到的磁盘体系结构。最大 NTFS 格式分区大小为 256 TB。</p></td>
<td><p>支持。</p>
<p>最佳实践：使用 GPT 分区。</p></td>
<td><p>支持。</p>
<p>最佳实践：使用 GPT 分区。</p></td>
</tr>
<tr class="even">
<td><p>MBR</p></td>
<td><p>MBR（或分区扇区）是作为已分区数据存储设备（如硬盘）的第一个扇区（LBA 扇区 0）的 512 字节启动扇区。最大 NTFS 格式分区大小为 2 TB。</p></td>
<td><p>支持。</p></td>
<td><p>支持。</p></td>
</tr>
<tr class="odd">
<td><p>分区对齐</p></td>
<td><p>分区对齐指将分区在扇区边界上对齐以获得最佳性能。</p></td>
<td><p>支持：Windows Server 2008 R2 和 Windows Server 2012 默认为 1 MB。</p></td>
<td><p>支持：Windows Server 2008 R2 和 Windows Server 2012 默认为 1 MB。</p></td>
</tr>
<tr class="even">
<td><p>卷路径</p></td>
<td><p>卷路径指访问卷的方式。</p></td>
<td><p>支持：驱动器号或装入点。</p>
<p>最佳实践：装入点主机卷必须启用 RAID。</p></td>
<td><p>支持：驱动器号或装入点。</p>
<p>最佳实践：装入点主机卷必须启用 RAID。</p></td>
</tr>
<tr class="odd">
<td><p>文件系统</p></td>
<td><p>文件系统是一种用于存储和组织计算机文件及其中包含的数据的方法，以便可轻松地查找和访问这些文件。</p></td>
<td><p>支持：NTFS 和 ReFS。</p></td>
<td><p>支持：NTFS 和 ReFS。</p></td>
</tr>
<tr class="even">
<td><p>NTFS 碎片整理</p></td>
<td><p>NTFS 碎片整理是一个用于减少 Windows 文件系统中碎片量的过程。此过程的具体操作为：以物理方式组织磁盘的内容，以便将每个文件的各部分紧密且连续地进行存储。</p></td>
<td><p>支持。</p>
<p>最佳实践：不要求并且不建议。在 Windows Server 2012 上，我们也建议禁用自动磁盘优化和碎片整理功能。</p></td>
<td><p>支持。</p>
<p>最佳实践：不要求并且不建议。在 Windows Server 2012 上，我们也建议禁用自动磁盘优化和碎片整理功能。</p></td>
</tr>
<tr class="odd">
<td><p>NTFS 分配单元大小</p></td>
<td><p>NTFS 分配单元大小表示可以分配用于存放文件的最小磁盘空间量。</p></td>
<td><p>支持：所有分配单元大小。</p>
<p>最佳实践：对于 .edb 和日志文件卷都为 64 KB。</p></td>
<td><p>支持：所有分配单元大小。</p>
<p>最佳实践：对于 .edb 和日志文件卷都为 64 KB。</p></td>
</tr>
<tr class="even">
<td><p>NTFS 压缩</p></td>
<td><p>NTFS 压缩是减小硬盘上存储的文件实际大小的过程。</p></td>
<td><p>支持：Exchange 数据库或日志文件不支持此配置。</p></td>
<td><p>支持：Exchange 数据库或日志文件不支持此配置。</p></td>
</tr>
<tr class="odd">
<td><p>NTFS 加密文件系统 (EFS)</p></td>
<td><p>用户使用 EFS 可以加密各个文件、文件夹或整个数据驱动器。由于 EFS 通过行业标准算法和公钥加密提供强加密，所以加密的文件可保持机密性，即使攻击者绕过系统安全保护也是如此。</p></td>
<td><p>支持：Exchange 数据库或日志文件不支持此配置。</p></td>
<td><p>Exchange 数据库或日志文件不支持此配置。</p></td>
</tr>
<tr class="even">
<td><p>Windows BitLocker（卷加密）</p></td>
<td><p>Windows BitLocker 是 Windows Server 2008 中的一种数据保护功能。BitLocker 可防止丢失或被盗的计算机上的数据失窃或泄露，并可在计算机停止使用时提供更加安全的数据删除。</p></td>
<td><p>支持：所有 Exchange 数据库和日志文件。</p></td>
<td><p>支持：所有 Exchange 数据库和日志文件。Windows 故障转移群集需要 Windows Server 2008 R2 或 Windows Server 2008 R2 SP1 以及以下修补程序：<a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=2446607">如果计算机是故障转移群集节点，则无法在 Windows Server 2008 R2 中的磁盘卷上启用 BitLocker</a>。运行早期版本的 Windows 的 Windows 故障转移群集上不支持启用了 Bitlocker 的 Exchange 卷。</p>
<p>有关 Windows 7 BitLocker 加密的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=220898">Windows 7 中的 BitLocker 驱动器加密：常见问题</a>。</p></td>
</tr>
<tr class="odd">
<td><p>服务器消息块 (SMB) 3.0</p></td>
<td><p>服务器消息块 (SMB) 协议是一项网络文件共享协议（在 TCP/IP 或其他网络协议之上），它允许计算机上的应用程序访问远程服务器上的文件和资源。它还允许应用程序与任何设置为接收 SMB 客户端请求的服务器程序进行通信。Windows Server 2012 中引入了新的 3.0 版本的 SMB 协议，其中包括下列功能：</p>
<ul>
<li><p>SMB 透明故障转移</p></li>
<li><p>SMB 横向扩展</p></li>
<li><p>SMB 多通道</p></li>
<li><p>SMB 直通</p></li>
<li><p>SMB 加密</p></li>
<li><p>适用于 SMB 文件共享的 VSS</p></li>
<li><p>SMB 目录租赁</p></li>
<li><p>SMB PowerShell</p></li>
</ul></td>
<td><p>有限支持。受支持的情况是在 SMB 3.0 共享的 VHD 上托管磁盘的硬件虚拟化部署。这些 VHD 通过一个虚拟机监控程序呈现给主机。有关详细信息，请参阅<a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虚拟化</a>。</p></td>
<td><p>有限支持。受支持的情况是在 SMB 3.0 共享的 VHD 上托管磁盘的硬件虚拟化部署。这些 VHD 通过一个虚拟机监控程序呈现给主机。有关详细信息，请参阅<a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虚拟化</a>。</p></td>
</tr>
<tr class="even">
<td><p>存储空间</p></td>
<td><p>存储空间是一个新的存储解决方案，实现 Windows Server 2012 的虚拟化功能。存储空间允许将物理磁盘组织为存储池，只需简单地增加磁盘，空间就能轻松地扩展。可以通过 USB、SATA 或 SAS 连接磁盘。也可以利用具有相关强大功能的虚拟磁盘（空间）（与物理磁盘的工作原理一样），例如精简设置以及从基础物理媒体故障中复原的功能。有关存储空间的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/hh831739.aspx">存储空间概述</a>。</p></td>
<td><p>支持。此主题列出了物理磁盘类型的一些限制。</p></td>
<td><p>支持。此主题列出了物理磁盘类型的一些限制。</p></td>
</tr>
<tr class="odd">
<td><p>复原文件系统 (ReFS)</p></td>
<td><p>ReFS 是一个为 Windows Server 2012 新设计的文件系统，它是在 NTFS 的基础上创建的。ReFS 保持 NTFS 的高兼容性，同时提供增强的数据验证和自动更正技术，以及集成的端到端损坏复原，与存储空间功能一起使用时尤为如此。有关 ReFS 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/hh831724.aspx">复原文件系统概述</a>。</p></td>
<td><p>支持包含 Exchange 数据库文件、日志文件和内容索引文件的卷。如果在 Windows Server 2012 上部署，请确保在 Windows Server 2012 上安装以下修补程序：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 和 Windows Server 2012 更新汇总：2013 年 4 月</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">虚拟磁盘服务或使用虚拟磁盘服务的应用程序在 Windows Server 2012 中崩溃或冻结</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">在 ReFS 卷上运行“dir”命令时基于 Windows 8 或基于 Windows Server 2012 的计算机冻结</a></p></li>
</ul>
<p>OS 卷不支持 ReFS。</p>
<p>最佳实践：必须禁用 Exchange 数据库 (.edb) 文件或托管这些文件的卷的数据完整性功能。</p></td>
<td><p>支持包含 Exchange 数据库文件、日志文件和内容索引文件的卷。如果在 Windows Server 2012 上部署，请确保在 Windows Server 2012 上安装以下修补程序：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717874">Windows 8 和 Windows Server 2012 更新汇总：2013 年 4 月</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717877">虚拟磁盘服务或使用虚拟磁盘服务的应用程序在 Windows Server 2012 中崩溃或冻结</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=717879">在 ReFS 卷上运行“dir”命令时基于 Windows 8 或基于 Windows Server 2012 的计算机冻结</a></p></li>
</ul>
<p>OS 卷不支持 ReFS。</p>
<p>最佳实践：必须禁用 Exchange 数据库 (.edb) 文件或托管这些文件的卷的数据完整性功能。</p></td>
</tr>
<tr class="even">
<td><p>重复数据删除</p></td>
<td><p>重复数据删除是优化 Windows Server 2012 存储利用的一项新技术。它是在不影响保真性或完整性的情况下，发现和删除重复数据的一种方法。其目标是通过将文件分割为各种尺寸的小区块、标识重复的区块并保留每个区块的单个副本，以使较少的空间能够存储更多的数据。多余的区块副本会用单个副本的引用替换，区块组织为容器文件，然后压缩容器文件，从而进一步优化空间。</p></td>
<td><p>不支持 Exchange 数据库文件。注意：适用于完全处于脱机模式的 Exchange 数据库文件（作为备份或存档）。</p></td>
<td><p>不支持 Exchange 数据库文件。注意：适用于完全处于脱机模式的 Exchange 数据库文件（作为备份或存档）。</p></td>
</tr>
</tbody>
</table>


存储结构

