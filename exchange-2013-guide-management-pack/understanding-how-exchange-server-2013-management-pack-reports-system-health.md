---
title: 了解 Exchange Server 2013 管理包报告系统运行状况的方式
TOCTitle: 了解 Exchange Server 2013 管理包报告系统运行状况的方式
ms:assetid: 6ca8847f-93fe-458d-bd43-7afad7fdd2f4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn195910(v=EXCHG.150)
ms:contentKeyID: 53275724
ms.author:dstrome
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解 Exchange Server 2013 管理包报告系统运行状况的方式

 

_**上一次修改主题：** 2015-03-09_

本主题提供有关 Exchange Server 2013 管理包如何监视和报告 Exchange 系统运行状况的信息。在 Exchange 2013 管理包中，运行状况信息以简单方式汇总。每当运行状况设置出现问题并触发升级应答器时，Windows 事件日志就会记录以下事件：

## 托管可用性

我们对 Exchange Server 2013 进行了一些架构更改。其中一个重要的更改就是*托管可用性*功能，所有 Exchange 2013 组件都含有可检测问题并尝试恢复服务可用性的内置监视器。Exchange 2013 管理包需要依靠此功能。任何无法自动恢复的问题都会作为警报升级至 Exchange 2013 管理包。Exchange 2013 中的各组件使用探测器、监视器和应答器这三个基本组件对自身状态进行监视。

![托管可用性](images/Dn195910.dd5febae-d05e-4089-a3f5-1691b2d9a3d7(EXCHG.150).png "托管可用性")

  - **探测器**   可以对各种组件进行测量的一组数据收集器。探测器有三种不同的类型：
    
      - 可对测量实际流量的综合端到端用户操作和检查进行测量的综合事务。
    
      - 可对实际客户流量进行测量的检查。
    
      - 可允许 Exchange 立即采取措施的通知。在证书到期时触发的通知就是一个很好的示例。

  - **监视器**   探测器收集的数据会传递给监视器，以便针对特定状况分析数据，并根据相应状况判断某个组件状态是否良好。

  - **应答器**   如果监视器认为某一组件运行状况不佳，就会触发应答器。如果该问题可以修复，应答器会尝试使用内置逻辑修复该组件。每个组件都有几个可用的应答器，但是与 Exchange 2013 管理包相关的应答器是*升级应答器*。当触发升级应答器后，它会生成 Exchange 2013 管理包可以识别的事件，并将相应信息提交至该警报，向管理员提供解决问题所必需的信息。

Exchange 2013 中的各组件使用特定的一组探测器、监视器和应答器来对自身状态进行监视。这些探测器和监视器被称为*运行状况设置*。例如，有大量探测器可用于收集与 ActiveSync 服务各方面有关的数据。该数据由一组指定的监视器进行处理，可触发相应的应答器以修复其在 ActiveSync 服务中检测到的问题。这些组件合起来就组成了 ActiveSync 运行状况设置。

Exchange 中的运行状况设置分为以下与管理包仪表板对应的四类：

  - 客户接触点

  - 服务组件

  - 服务器资源

  - 关键依存项

有关 Exchange 运行状况设置的完整列表，请参阅[Appendix A: Exchange health sets](appendix-a-exchange-health-sets.md)。

有关托管可用性的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 运行状况的汇总方式

本主题提供有关 Exchange Server 2013 管理包如何监视和报告 Exchange 系统运行状况的信息。在 Exchange 2013 管理包中，运行状况信息以简单方式汇总。每当运行状况设置出现问题并触发升级应答器时，Windows 事件日志就会记录以下事件：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>日志名称</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>来源</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日期</p></td>
<td><p>&lt;<em>事件日期和时间</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>事件 ID</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p>任务类别</p></td>
<td><p>监视</p></td>
</tr>
<tr class="even">
<td><p>级别</p></td>
<td><p>错误</p></td>
</tr>
<tr class="odd">
<td><p>关键字</p></td>
<td><p>&lt;<em>none</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>User</p></td>
<td><p>系统</p></td>
</tr>
<tr class="odd">
<td><p>计算机</p></td>
<td><p>&lt;<em>Exchange 服务器的 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>说明</p></td>
<td><p>&lt;<em>由升级应答器动态生成</em>&gt;</p></td>
</tr>
</tbody>
</table>


管理包代理可以检测和处理该事件。通过使用该事件，托管可用性可以在 SCOM 内生成警报。当相应问题解决之后，运行状况设置会返回正常状态，Windows 事件日志会记录以下事件：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>日志名称</p></td>
<td><p>Microsoft-Exchange-ManagedAvailability/Monitoring</p></td>
</tr>
<tr class="even">
<td><p>来源</p></td>
<td><p>ManagedAvailability</p></td>
</tr>
<tr class="odd">
<td><p>日期</p></td>
<td><p>&lt;<em>事件日期和时间</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>事件 ID</p></td>
<td><p>1</p></td>
</tr>
<tr class="odd">
<td><p>任务类别</p></td>
<td><p>监视</p></td>
</tr>
<tr class="even">
<td><p>级别</p></td>
<td><p>信息</p></td>
</tr>
<tr class="odd">
<td><p>关键字</p></td>
<td><p>&lt;<em>none</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>User</p></td>
<td><p>系统</p></td>
</tr>
<tr class="odd">
<td><p>计算机</p></td>
<td><p>&lt;<em>Exchange 服务器的 FQDN</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>说明</p></td>
<td><p>&lt;<em>由升级应答器动态生成</em>&gt;</p></td>
</tr>
</tbody>
</table>


对 Exchange 早期版本进行监视的管理包已完全集中。各 Exchange 服务器上的代理会收集数据，中央关联引擎会比较和评估这些代理报告的所有数据，以判断服务的总体运行状况。在大型环境中，此过程会产生复杂的关联，进而延迟警报的生成。Exchange 2013 不再使用警报关联。相反，各服务器自行执行监视，并在必要时向 SCOM 发出警报，适用于高度可扩展的架构。

根据事件的影响以及触发事件的运行状况设置，问题会显示在 SCOM 控制台的不同类型中。如果事件对用户造成影响，那么客户接触点指示灯会显示为不正常。如果事件导致整个组件（如 OWA）不可用，那么服务组件指示灯会显示为不正常。如果这是特定服务器的问题，那么相应的服务器运行状况指示灯会显示为不正常。最后，如果问题与 Exchange 依赖的资源相关，那么关键依存项指示灯会显示为不正常。有关这些类别的详细信息，请参阅[Exchange Server 2013 Management Pack 入门](getting-started-with-exchange-server-2013-management-pack.md)。

