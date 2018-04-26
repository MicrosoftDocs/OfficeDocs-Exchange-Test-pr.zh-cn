---
title: 解决 DataProtection 运行状况设置的问题
TOCTitle: 解决 DataProtection 运行状况设置的问题
ms:assetid: cde3cc34-2076-4e30-8d3c-265b66d00ae8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.dataprotection(v=EXCHG.150)
ms:contentKeyID: 53275710
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 DataProtection 运行状况设置的问题

 

_**适用于：**Exchange Server 2013, Project Server 2013_

_**上一次修改主题：**2015-03-09_

DataProtection 运行状况设置监视数据库可用性组 (DAG) 中数据库的冗余。

如果收到一条警报，指示 DataProtection 运行状况不正常，这说明出现了可能影响复制或群集组件的问题，并会阻止对 Exchange 数据库的访问。

## 说明

DataProtection 运行状况服务通过以下探测器和监视器进行监视。


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
<td><p>ClusterEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterGroupProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterGroupMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ClusterNetworkProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterNetworkMonitor</p></td>
</tr>
<tr class="even">
<td><p>ClusterServiceCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ClusterServiceCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerOneCopyProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Director</p></td>
<td><p>ServerOneCopyMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServerOneCopyInternalMonitorProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerOneCopyInternalMonitorMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServiceHealthMSExchangeReplEndpointProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplEndpointMonitor</p></td>
</tr>
<tr class="even">
<td><p>ServiceHealthMSExchangeReplCrashProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServiceHealthMSExchangeReplCrashMonitor</p></td>
</tr>
<tr class="odd">
<td><p>ServerSiteFailureProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>ServerSiteFailureMonitor</p></td>
</tr>
<tr class="even">
<td><p>StorageApparentControllerIssuesProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>StorageApparentControllerIssuesMonitor</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseHealthTooManyMountedDatabaseProbe</p></td>
<td><p>DataProtection</p></td>
<td><p>Active Directory</p></td>
<td><p>DatabaseHealthTooManyMountedDatabaseMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 Autodiscover.Protocol 运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
        
        检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    2.  确定监视器基于哪个探测器。注意，大部分探测器都具有相同的名称前缀。使用前面的示例，搜索“**ClusterNetwork\***”：
        
            Get-MonitoringItemIdentity -Identity DataProtection -Server server1.contoso.com | ?{$_.Name -like "ClusterNet ItemType  
            work*"}
        
        返回的结果应该与下列内容相似。
        
        
        <table>
        <colgroup>
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        <col style="width: 25%" />
        </colgroup>
        <tbody>
        <tr class="odd">
        <td><p><code>ItemType</code></p></td>
        <td><p><code>HealthSetName</code></p></td>
        <td><p><code>Name</code></p></td>
        <td><p><code>TargetResource</code></p></td>
        </tr>
        <tr class="even">
        <td><p><code>Probe</code></p></td>
        <td><p><code>DataProtection</code></p></td>
        <td><p><code>ClusterNetworkProbe</code></p></td>
        <td><p><code>MSExchangeRepl</code></p></td>
        </tr>
        </tbody>
        </table>
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **AutodiscoverSelfTestMonitor**。与该监视器关联的探测器为 **AutodiscoverSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## 故障排除步骤

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的服务器名称

  - 警报出现的时间和日期

  - 所用的身份验证机制，以及凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    您可以使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常包含故障原因，描述了探测器运行失败的原因。

对于高可用性环境中出现的大部分问题，可以运行 **Test-ReplicationHealth** cmdlet 帮助对 cluster/networking/ActiveManager/services 进行故障排除。其他 HealthSet/组件具有不同的 Test-\* cmdlet。

例如：

    Test-ReplicationHealth <ServerName>

返回的结果将与下列内容相似：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><code>Server</code></p></td>
<td><p><code>Check</code></p></td>
<td><p><code>Result</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>ClusterService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>ReplayService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>ActiveManager</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>TasksRpcListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>TcpListener</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>ServerLocatorService</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DagMembersUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>ClusterNetwork</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>QuorumGroup</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>FileShareQuorum</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DatabaseRedundancyCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DatabaseAvailabilityCheck</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBCopySuspended</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBCopyFailed</code></p></td>
<td><p>已通过</p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBInitializing</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBDisconnected</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="even">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBLogCopyKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
<tr class="odd">
<td><p><em>&lt;ServerName&gt;</em></p></td>
<td><p><code>DBLogReplayKeepingUp</code></p></td>
<td><p><code>Passed</code></p></td>
</tr>
</tbody>
</table>


如果所有组件的“结果”栏中都显示“已通过”，尝试按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

如果问题仍然存在，重新启动服务器。服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

