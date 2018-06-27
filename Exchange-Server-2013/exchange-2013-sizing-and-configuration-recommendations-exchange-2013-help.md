---
title: 'Exchange 2013 大小调整和配置建议: Exchange 2013 Help'
TOCTitle: Exchange 2013 大小调整和配置建议
ms:assetid: 4c4ba2fc-014a-46fb-949a-2dabba92c4a5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn879075(v=EXCHG.150)
ms:contentKeyID: 63892331
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 大小调整和配置建议

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2017-03-27_

与以前的 Exchange 版本相比，Exchange 2013 对系统资源要求更高。通过正确调整 Exchange 2013 的基础结构的大小以及对该基础结构内与 Exchange 相关的组件进行建议的配置，您可以为执行最佳部署打下坚实的基础。

## Exchange 2013 大小调整

正确调整 Exchange 2013 大小是防止性能问题最有效的方法之一。Exchange 2013 服务器角色要求计算器可在[此处获取](https://go.microsoft.com/fwlink/p/?linkid=523844)。最新版本是 6.6，但是我们建议定期检查更新。要正确使用此计算器，必须查看 [Exchange 2013 服务器角色要求计算器](https://go.microsoft.com/fwlink/p/?linkid=386677)和[调整 Exchange 2013 部署大小](https://go.microsoft.com/fwlink/p/?linkid=301990)博客文章中的指南。

在购买和部署硬件之前，首先使用计算器很重要；根据计算器结果，您首先应该确定整体的资源要求。您可以使用计算器输入组织的要求，并使用结果作为有关如何扩展硬件的指南。计算器不会告知您要使用多少台服务器，但是可允许您评估 Exchange 工作量对给定服务器集的影响。为了满足特定于您环境的硬件和业务需求，您应该对不同的配置进行试验，以查看这些配置对性能的影响。

为了简化部署并充分使用硬件，Exchange 产品组建议使用多角色服务器。使用多角色服务器可在客户端访问服务器 (CAS) 层为您提供更高的可用性，因为有更多的客户端访问服务器可用于在故障期间处理请求。Exchange 2013 的关键设计考虑因素是使用“更小”的商品类型服务器（横向扩展替代向上扩展）。设计和测试使用两台套接字计算机（包含最多 24 个处理器内核以及多达 96 千兆字节 (GB) 的 RAM）完成。如果您的硬件比这一配置要高，您应该考虑其他选择，例如将该硬件用于其他需求、为 Exchange 2013 环境购买较小的服务器或对其进行虚拟化。

最好是构建更多服务器（横向扩展），以向现有的较大服务器添加资源（向上扩展）。通过横向扩展，环境可以使用 Exchange 2013 中的内置高可用性功能。要了解建议使用此配置的原因，请查看[首选体系结构](https://go.microsoft.com/fwlink/p/?linkid=523782)和[站点恢复对可用性的影响](https://go.microsoft.com/fwlink/p/?linkid=523845)博客文章中的详细信息。

计算器不考虑在 Exchange 服务器上运行的第三方产品或与 Exchange（包括内部开发的应用程序）互动的产品，这表示您在调整大小期间必须考虑这些产品。例如，Lync Server 和第三方 Exchange Web 服务 (EWS) 应用程序以及 ActiveSync 设备都会大大提高每位用户的 CPU 要求。您可以参考第三方产品文档，了解这些产品将对 Exchange 产生何种影响。建议在实施第三方解决方案之前为 Exchange 创建性能基线。

## 建议的性能配置

建议对您的 Exchange 2013 环境进行以下性能优化。

## 电源

设置 BIOS，以允许操作系统 (OS) 对电源进行管理。

在 OS 中，打开高性能电源计划。

## 处理

关闭物理 Exchange 服务器上的超线程。如果进行虚拟化，虽然可能在物理服务器上启用超线程，但是应该只能为每个虚拟服务器分配所需数量的虚拟 CPU（不会过度分配虚拟 CPU），并且只能使用负责调整计算大小的物理处理器内核。

在 Exchange Server 2013 Service Pack 1 或更高版本中，您可以启用 SSL 卸载以帮助减少客户端访问服务器的 CPU 消耗，但是 SSL 卸载的配置过于复杂可能得不偿失。

## .NET Framework


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

如果无法安装 .net 4.5.2，请参阅 Microsoft 知识库文章 2995145 [连接到正在 Windows Server 中运行的 Exchange Server 2013 时的性能问题或延迟](https://go.microsoft.com/fwlink/p/?linkid=524159)。该文章中的修复程序是根据有关存储工作进程内存使用情况的内部调查开发出来的。通过应用这些修复程序，将减少所有管理的进程（包括存储工作进程）的整体内存消耗，并且将减少在 .NET 垃圾收集方面的整体 CPU 耗时。

## 修补程序

Exchange 性能团队建议安装以下所有与性能相关的修补程序。

  - [可改进 Windows Server 2012 中的群集恢复的更新现有推出](https://go.microsoft.com/fwlink/p/?linkid=524088)

  - [用于基于 Windows Server 2012 的故障转移群集的建议修补程序和更新](https://go.microsoft.com/fwlink/p/?linkid=524089)

  - [用于基于 Windows Server 2012 R2 的故障转移群集的建议修补程序和更新](https://go.microsoft.com/fwlink/p/?linkid=524090)

  - [具有多核处理器的基于 Windows 8 或 Windows Server 2012 的计算机上的 RSS 处理器分配不正确](https://go.microsoft.com/fwlink/p/?linkid=324140)

  - [连接到正在 Windows Server 中运行的 Exchange Server 2013 时的性能问题或延迟](https://go.microsoft.com/fwlink/p/?linkid=312962)

  - [Exchange 2013 中的 SSLOffloading 为“True”时的 Outlook 连接问题](https://go.microsoft.com/fwlink/p/?linkid=524091)

  - [Exchange Server 2013 中数据库故障转移后 Outlook 的服务器连接时间较长](https://go.microsoft.com/fwlink/p/?linkid=524092)

  - [Lync 与 Exchange Server 2013 集成时 Outlook Web App 中的性能下降](https://go.microsoft.com/fwlink/p/?linkid=524093)

  - [EMS 需要较长时间在 Exchange Server 2013 累积更新 5 环境中执行第一个命令](https://go.microsoft.com/fwlink/p/?linkid=524094)

  - [在 Exchange Server 2013 中启用 IPv6 时的邮件路由延迟](https://go.microsoft.com/fwlink/p/?linkid=524095)

  - [依赖 Windows Server 2008 R2 SP1 中 Microsoft LDAP 客户端的应用程序的 CPU 使用率高](https://go.microsoft.com/fwlink/p/?linkid=530287)

  - [当通过 Windows 8.1 或 Windows Server 2012 R2 中的 HTTP 协议使用 RPC 时，CPU 使用率会很高](https://go.microsoft.com/fwlink/p/?linkid=619127)

## 网络

对于 Exchange 2013，建议使用单个网络适配器，因为它无需拆分 MAPI 和复制网络。有关详细信息，请参阅[Network requirements](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)。

在可用的情况下使用默认的 SNP 卸载设置，并确保启用 RSS（Windows Server 2012 和更高版本中的默认设置）。RSS 有助于扩展 CPU 使用情况，尤其是在 10GbE 上。

验证 OS 没有关闭网卡以节省电源。

保持最新的 NIC 驱动程序。每月向您的供应商咨询是否有相关的驱动程序更新。

## Internet 信息服务 (IIS)

在安装期间，Exchange 修改针对 IIS 的某些连接限制。建议不要对 IIS 进行进一步调整。

无论何时都要避免进行自定义。Exchange 累积更新或 Windows 更新可能会覆盖对 web.config 或注册表项所做的任何更改。

## 存储

可以在 [Exchange 2013 存储配置选项](exchange-2013-storage-configuration-options-exchange-2013-help.md)中获取 Exchange 2013 存储的指南。

## 虚拟化

请查看[Requirements for hardware virtualization](exchange-2013-virtualization-exchange-2013-help.md)。此外，请注意 Exchange 不是非一致性内存访问 (NUMA) 感知型。因此，建议使用硬件制造商的默认 NUMA 设置。

## Active Directory

监视目录服务器性能，因为 Active Directory 查询直接影响 Exchange 部署。

对于 Active Directory 的运行状况，LDAP 搜索时间是要衡量的关键计时器。监视您的域控制器上的 CPU。域控制器上的 CPU 问题将呈现为对 Exchange 服务器的性能影响。

运行位于“数据采集器集”下性能监视器中的域控制器上内置的“Active Directory 诊断”，以帮助排除域控制器性能问题的原因。

在域控制器上规划出足够的 RAM，以缓存完整的 AD 数据库文件。

我们建议为处理有效负载的每 8 个邮箱内核（基于 64 位的全局编录内核）部署一个 Active Directory 全局编录内核。

## 负载平衡

所有客户端访问服务器应该接收大约相同数量的传入连接。

对于所有产品，Exchange 2013 不需要给定客户端访问服务器和负载平衡器之间的会话相关性。

应该将硬件或软件负载平衡器用于管理所有发往客户端访问服务器的入站通信。目标服务器的选择可通过多种方式实现，例如通过“轮询机制”，其中每个入站连接会到达循环列表中的下一个目标服务器；或者通过“最少连接”，其中负载平衡器会向当时建立了最少连接的服务器发送每个新的连接。[负载平衡](load-balancing-exchange-2013-help.md)中对这些方法有进一步的详细阐述。您还应考虑以下事项：

  - 轮循机制存在与长期连接（如 RPC/HTTP）集中缓慢的问题。作为一台联机的新计算机，在多台目标计算机之间提供的连接平衡需要很长时间才能集中。

  - 使用“最少连接”方法时，请注意客户端访问服务器在中断或修补维护期间可能超载和没有响应。对于 Exchange 性能，身份验证是一项高成本的操作。

由于在 Exchange 2013 环境中对 Windows 网络负载平衡进行了大量限制（[负载平衡](load-balancing-exchange-2013-help.md)中有详细阐述），因此我们不建议使用 Windows NLB。

## 用户和数据库分布

维持每个数据库的用户和每个服务器的活动数据库的平衡分布。平均分布数据库磁盘空间以及平衡所有数据库中的重负载用户。

必须配置您的用户群，以便于了解他们与 Exchange（设备、Outlook 和 OWA）的互动方式以及这些互动对性能造成的影响。请参阅第 2 部分中的计算器博客，以更好地了解如何配置每个用户的 Exchange 用法。

配置 DB 副本激活首选项和“MaximumPreferredActiveDatabases”（每服务器）设置，以维持故障转移或切换期间的平衡。

RedistributeActiveDatabases.ps1 脚本将重新平衡多个 DAG 节点之间的活动数据库。

请考虑强制执行与 Office 365 匹配的严格的项目计数。可以使用 Set-Mailbox cmdlet 和[邮箱文件夹限制](https://go.microsoft.com/fwlink/p/?linkid=398779)中提供的信息来执行这一操作。

## 页面文件

如果您使用的是大于 32 GB 的 RAM，请将页面文件的大小上限设置为 32778 MB。

页面文件应该托管在与 Exchange 数据库文件或数据库日志文件相同的驱动器上。

必须使用固定大小的页面文件，并且不允许 Windows 对其进行管理。当 Exchange 负荷过重时，增加页面文件可能是性能密集型任务并可能造成问题。

如果需要获取完整的内核转储，请使用 Microsoft 知识库文章 969028[如何在 Windows Server 2008 和 Windows Server 2008 R2 中生成内核或完整的内存转储文件](https://go.microsoft.com/fwlink/p/?linkid=524044)，获取专用的转储文件。

## Outlook 模式

建议使用缓存模式。要了解使用缓存模式的好处，请参阅[为 Outlook 2013 选择缓存的 Exchange 模式或联机模式](https://go.microsoft.com/fwlink/p/?linkid=524045)。

值得注意的是，服务器加载项和 Outlook 第三方加载项都可能对性能造成影响。当使用联机模式时，客户端可能在第三方加载项中遇到一些性能问题，如较高的项目计数、视图限制、访问邮箱的用户数量以及其他因素带来的问题。与 Outlook 2013 相比，旧版客户端可能在高项目计数和性能方面受到更大影响。

如果某个组织在联机模式下配置 Outlook 的主要原因是出于安全方面的考虑，请转为使用 BitLocker。

Outlook 2013 提供新的“同步滑块”功能，以尽可能减少下载时间和 OST 文件的大小。有关详细信息，请参阅[在 Outlook 2013 中配置缓存 Exchange 模式](https://go.microsoft.com/fwlink/p/?linkid=390456)。

每月检查一次您的环境中受支持的 Outlook 客户端更新。

## 第三方软件

作为最佳实践，在排除 Exchange 性能问题时，请卸载或禁用第三方软件。 以下列表包含 Microsoft 支持，但最常影响 Exchange 2013 性能的第三方软件类型。

  - 防病毒解决方案

  - 入侵防护软件

  - 备份软件

  - 适用于文件和用户的审核软件

  - 存档解决方案

