---
title: FIPS 运行状况设置疑难解答
TOCTitle: FIPS 运行状况设置疑难解答
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54652344
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# FIPS 运行状况设置疑难解答

 

_**适用于：** Exchange Server 2013, Project Server 2013_

_**上一次修改主题：** 2015-03-09_

**FIPS** 运行状况设置监视 Exchange 服务器上的联邦信息处理标准 (FIPS) 的设置的总体运行状况。有关 FIPS 140 的详细信息，请参阅 [FIPS 140 验证](http://go.microsoft.com/fwlink/p/?linkid=521913)。

如果您收到警报，指示 **FIPS** 运行状况设置不正常，这表示某个问题可能会阻止您的 Exchange 服务器使用与 FIPS 140 兼容的组件和进程。

## 说明

使用下列探测器和监视器监视 **FIPS** 服务。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>探测器</th>
<th>运行状况设置</th>
<th>关联监视器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>无（通知或检查）</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您收到指定 **FIPS** 运行状况设置不正常的警报时，请首先验证问题是否仍存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题

1.  识别警报中显示的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。在大多数情况下，消息详细信息提供足够的疑难解答信息以帮助识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如：若要检索关于 server1.contoso.com 的 **FIPS** 运行状况设置详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”值将为“不正常”。

