---
title: ActiveSync 运行状况设置疑难解答
TOCTitle: ActiveSync 运行状况设置疑难解答
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53275705
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# ActiveSync 运行状况设置疑难解答

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Exchange ActiveSync 运行状况设置监视组织中移动客户端的 ActiveSync 服务的总体运行状况。ActiveSync 运行状况设置与下列运行状况设置紧密相关：

[ActiveSync.Protocol 运行状况设置疑难解答](troubleshooting-activesync-protocol-health-set.md)

[ActiveSync.Proxy 运行状况设置疑难解答](troubleshooting-activesync-proxy-health-set.md)

如果您收到警报，警报中说明 ActiveSync 运行状况设置不正常，则表明可能发生一个问题，阻止用户使用 ActiveSync 访问其邮箱。

## 说明

使用下列探测器和监视器监视 ActiveSync 服务。


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>邮箱服务器身份验证</p>
<p>信息存储</p>
<p>高可用性</p>
<p>网络</p></td>
<td><p>ActiveSyncCTPMonitor（ActiveSync 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor（ActiveSync.Proxy 运行状况设置）</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>信息存储</p>
<p>高可用性</p></td>
<td><p>ActiveSyncDeepTestMonitor（ActiveSync 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>身份验证</p></td>
<td><p>ActiveSyncSelfTestMonitor（ActiveSync.Protocol 运行状况设置）</p>
<p>RequestsQueuedGt500Monitor（ActiveSync 运行状况设置）</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

可以在发出警报后恢复服务。因此，当您收到指定 ActiveSync 运行状况设置不正常的警报时，请首先验证问题是否仍存在。如果问题确实存在，请执行下面章节中所述的相应恢复操作。

## 验证问题

1.  识别警报中显示的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。在大多数情况下，消息详细信息提供足够的疑难解答信息以帮助识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  在 Exchange 命令行管理程序 上，运行下列命令检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 ActiveSync 运行状况设置详细信息，请运行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”值将为“不正常”。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行以下命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **ActiveSyncCTPMonitor**。与该监视器关联的探测器为 **ActiveSyncCTPProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，查看探测器的“结果”部分。如果值为“**Succeeded**”，则问题只是一个暂时错误，将不再存在。否则，请参考下面章节所述的恢复步骤。

## ActiveSyncDeepTestMonitor 和 ActiveSyncSelfTestMonitor 恢复操作

此监视器警报通常在邮箱服务器上发出。要执行恢复操作，请按照下列步骤操作：

1.  启动 IIS 管理器，然后连接到报告问题的服务器。单击“应用程序池”，然后回收名为“**MSExchangeSyncAppPool**”的 ActiveSync 应用程序池。

2.  按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

3.  如果问题仍存在，则使用 IISReset 实用程序回收整个 IIS 服务。

4.  按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

5.  如果问题仍存在，请重新启动服务器。为此，首先使用下列命令对服务器上托管的数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    在该示例和所有后续代码示例中，将 *server1.contoso.com* 替换为实际服务器名称。

6.  接下来，验证所有数据库是否均已从报告问题的服务器上转移。为此，请运行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  如果步骤 6 中的命令输出显示服务器上没有活动副本，请重新启动服务器。如果输出显示有活动副本，请再次运行步骤 5 和 6。

8.  在服务器重新启动后，按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

9.  如果探测器成功，则通过运行下列命令对数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. 如果探测器仍无法运行，您可能需要进一步帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## ActiveSyncCTPMonitor 恢复操作

此监视器警报通常在 CA 服务器 (CAS) 上发出。

1.  启动 IIS 管理器，然后连接到报告问题的服务器。单击“应用程序池”，然后回收名为“**MSExchangeSyncAppPool**”的 ActiveSync 应用程序池。

2.  按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

3.  如果问题仍存在，则使用 IISReset 实用程序回收整个 IIS 服务。

4.  按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

5.  如果问题仍存在，则必须验证相应邮箱服务器上的运行状况状态。邮箱服务器的名称是错误消息中给出的 `_Mbx:` 值。
    
    1.  针对相应的邮箱服务器运行下列命令。例如，对于名为 mailbox1.contoso.com 的邮箱服务器，运行下列命令：
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  如果报告命令输出中列出的任何监视器处于不正常状态，则必须首先解决这些监视器的问题。为此，请按照 ActiveSyncDeepTestMonitor 和 ActiveSyncSelfTestMonitor 恢复操作部分中所述的疑难解答步骤操作。

6.  如果邮箱服务器上的所有监视器运行状况均正常，请重新启动 CAS。

7.  在服务器重新启动后，按照验证问题部分中的步骤 2c 所示，重新运行关联探测器。

8.  如果探测器仍失败，您可以需要进一步帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## RequestsQueuedGt500Monitor 恢复操作

此监视器警报通常在 CA 服务器上发出。

1.  启动 IIS 管理器，然后连接到报告问题的服务器。单击“应用程序池”，然后回收名为“**MSExchangeSyncAppPool**”的 ActiveSync 应用程序池。

2.  等待 10 分钟，查看监视器是否保持正常运行。10 分钟后，针对相应的服务器运行下列命令。例如，针对 server1.contoso.com 运行下列命令：
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  如果问题仍存在，则使用 IISReset 实用程序回收整个 IIS 服务。

4.  等待 10 分钟，然后再次运行步骤 2 所示的命令，查看监视器是否仍运行正常。

5.  如果问题仍存在，请重新启动服务器。如果服务器为 CAS，只需重新启动服务器。如果服务器为邮箱服务器，请执行下列操作：
    
    1.  对服务器上托管的数据库进行故障转移。为此，请运行下列命令：
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注意**   在该示例和所有后续代码示例中，将 *server1.contoso.com* 替换为实际服务器名称。
    
    2.  验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        如果命令输出显示服务器上没有活动副本，请重新启动服务器。

6.  服务器重新启动后，等待 10 分钟，然后再次运行步骤 2 所示的命令，确定监视器是否仍运行正常。

7.  如果监视器仍运行正常，且服务器是邮箱服务器，则运行下列命令对数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  如果探测器仍失败，您可以需要进一步帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange ActiveSync](https://technet.microsoft.com/zh-cn/library/aa998357\(v=exchg.150\))

[移动设备](https://technet.microsoft.com/zh-cn/library/bb232129\(v=exchg.150\))

[Exchange ActiveSync 虚拟目录管理任务](https://technet.microsoft.com/zh-cn/library/bb125170\(v=exchg.150\))

