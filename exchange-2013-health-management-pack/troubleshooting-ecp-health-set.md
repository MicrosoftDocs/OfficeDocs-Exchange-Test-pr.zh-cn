---
title: ECP 运行状况设置疑难解答
TOCTitle: ECP 运行状况设置疑难解答
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53275689
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ECP 运行状况设置疑难解答

 

_**适用于：**Exchange Server 2013, Project Server 2013_

_**上一次修改主题：**2015-03-09_

Exchange 控制面板 (ECP) 运行状况设置监视 Exchange 管理中心 (EAC) 和 Outlook Web App (OWA) 用户设置服务的整体运行状况。ECP 运行状况设置与以下运行状况设置密切相关：

[解决 ECP.Proxy 运行状况设置的问题](troubleshooting-ecp-proxy-health-set.md)

如果收到一条警报，指示 ECP 运行状况设置不正常，则说明可能出现了阻止用户访问 EAC 的问题。

## 说明

通过使用以下探测器和监视器来监视 EAC 服务。


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的服务器名称

  - 警报发出的时间和日期

  - 验证和凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    **注意**   可使用全部异常跟踪中的信息来帮助解决问题。

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  消息详细信息提供了警报的确切原因信息。在大多数情况下，消息详细信息会提供充分的疑难解答信息来确定问题的根本原因。如果消息详细信息不够明确，请按照以下步骤操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，检索发布警报的运行状况设置的详细信息：
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        例如：要检索关于 server1.contoso.com 的 ECP 运行状况设置详细信息，请运行以下命令：
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        例如，假定故障监视器为 **EacSelfTestMonitor**。与该监视器关联的探测器为 **EacSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## EacSelfTestMonitor 和 EacDeepTestMonitor 的恢复操作

1.  启动 IIS 管理器，然后连接到报告问题的服务器。单击“应用程序池”，然后再循环名为“**MSExchangeECPAppPool**”的 ECP 应用程序池。

2.  按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

3.  如果问题仍然存在，则通过 IISReset 实用程序再循环整个 IIS 服务。

4.  按照验证问题是否仍然存在部分步骤 2c 中所示，重新运行相关联的探测器。

5.  如果服务终止失败，则重新启动服务器

6.  重新启动服务器后，按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

7.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

[Exchange 2013 中的 Exchange 管理中心](https://technet.microsoft.com/zh-cn/library/jj150562\(v=exchg.150\))

