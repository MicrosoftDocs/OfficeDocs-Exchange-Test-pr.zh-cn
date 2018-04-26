---
title: UM.Protocol 运行状况设置疑难解答
TOCTitle: UM.Protocol 运行状况设置疑难解答
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53275700
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM.Protocol 运行状况设置疑难解答

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

UM.Protocol 运行状况设置监视邮件服务器上的统一消息 (UM) 协议。

如果收到一条警报，指示 UM.Protocol 不正常，表示组织中存在可能阻止用户使用 UM 服务的问题。UM.Protocol 运行状况设置与下列运行状况设置紧密相关：

[UM 运行状况设置疑难解答](troubleshooting-um-health-set.md)

[解决 UM.CallRouter 运行状况设置的问题](troubleshooting-um-callrouter-health-set.md)

## 说明

使用下列探测器和监视器监视 UM.Protocol 服务。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>探测器</th>
<th>运行状况设置</th>
<th>依存关系</th>
<th>关联监视器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory 域服务 (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，检索发布警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如：若要检索关于 server1.contoso.com 的 UM.Protocol 运行状况设置详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **UMSelfTestMonitor**。与该监视器相关联的探测器为 **UMSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## 故障排除步骤

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的服务器名称

  - 警报发出的时间和日期

  - 所使用的身份验证机制和凭据信息

  - 上一错误的完全异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    **注意**   可使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常中包含“失败原因”，它说明了探测失败的原因。

有关 UJM 警报消息疑难解答的详细信息，请参阅[UM 运行状况设置疑难解答](troubleshooting-um-health-set.md)

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

