---
title: 解决 POP 运行状况设置的问题
TOCTitle: 解决 POP 运行状况设置的问题
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53275699
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 POP 运行状况设置的问题

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

POP 运行状况设置监视 Microsoft Exchange POP3 服务和 POP3 客户端连接的整体运行状况和可用性。POP 运行状况设置与以下运行状况设置密切相关：

  - [解决 POP.Protocol 运行状况设置的问题](troubleshooting-pop-protocol-health-set.md)

  - [POP.Proxy 运行状况设置疑难解答](troubleshooting-pop-proxy-health-set.md)

如果收到一条警报，指示 POP 服务运行状况不正常，这说明出现了可能会阻止用户在 Exchange 环境中使用 POP3 访问邮箱的问题。

## 说明

POP 服务通过以下探测器和监视器进行监视。


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>邮箱服务器身份验证</p>
<p>信息存储</p>
<p>高可用性</p>
<p>网络</p></td>
<td><p>PopCTPMonitor（POP 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>无</p></td>
<td><p>PopProxyTestMonitor（POP.Proxy 运行状况设置）</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>信息存储</p>
<p>高可用性</p></td>
<td><p>PopDeepTestMonitor（POP.Protocol 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>无</p></td>
<td><p>PopSelfTestMonitor（POP.Protocol 运行状况设置）</p>
<p>AverageCommandProcessingTimeGt60sMonitor（POP 运行状况设置）</p></td>
</tr>
</tbody>
</table>


## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要检索 server1.contoso.com 上 POP 运行状况设置的详细信息，运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为“PopCTPMonitor”。与该监视器关联的探测器是“PopCTPProbe”。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## PopTestDeepMonitor 和 PopSelfTestMonitor 恢复操作

此监视器警报通常会在邮箱服务器上发出。

1.  重新启动 POP3 后端服务。有关详细信息，请参阅[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))。

2.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

3.  如果探测器仍然无法运行，使用以下命令对托管在邮箱服务器上的数据库进行故障转移：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  在所有数据库都从邮箱服务器移除后，您必须验证数据库是否已成功移动。为此，请运行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  确保服务器不保留数据库的任何主动副本。然后，重新启动服务器。

6.  服务器成功重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

7.  如果探测器成功运行，通过运行以下命令对数据库进行故障转移：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## POPCTPMonitor 恢复操作

此监视器警报通常会在 CA 服务器 (CAS) 上发出。

1.  在运行 CAS 角色的服务器上重新启动 POP3 服务。有关详细信息，请参阅[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))。

2.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

3.  如果问题仍然存在，在 Windows PowerShell 中运行以下命令：
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  在运行 CAS 角色的服务器上重新启动 POP3 服务。
    
    3.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。
    
    4.  运行以下命令，然后找到日志文件的位置：
        
            Get-PopSettings -server <CAS server name>
    
    5.  运行以下命令，通过比较探测器的时间戳确认哪个邮箱正在为该命令提供服务。
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  如果有任何服务器被报告为不正常，请按照 PopTestDeepMonitor 和 PopSelfTestMonitor 恢复操作部分列出的步骤操作。

4.  如果邮箱服务器被报告为正常，重新启动 CAS。

5.  服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

6.  通过运行以下命令关闭协议日志记录：
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  在运行 CAS 角色的服务器上重新启动 POP3 服务。有关详细信息，请参阅[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))。

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## PopProxyTestMonitor 恢复操作

1.  在运行 CAS 角色的服务器上重新启动 POP3 服务。有关详细信息，请参阅[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))。

2.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

3.  如果探测器仍然运行失败，请重新启动 CAS。

4.  服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

5.  如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## AverageCommandProcessingTimeGt60sMonitor 恢复操作

此监视器警报通常会在 CA 或邮箱服务器上发出。

1.  重新启动 CA 或邮箱服务器上的 POP3 服务。有关详细信息，请参阅[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))。

2.  等待 10 分钟，查看监视器是否处于正常运行状态。10 分钟后，运行以下命令（此示例使用 server1.contoso.com）。
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  如果问题仍然存在，需要重新启动服务器。如果服务器是 CAS，只需重新启动服务器。如果服务器是邮箱服务器，则必须对数据库进行故障转移，并验证结果。为此，请执行下列步骤：
    
    1.  通过以下命令对服务器托管的数据库进行故障转移：
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注意**   在本示例以及所有后续代码示例中，将 *server1.contoso.com* 替换为实际服务器名称。
    
    2.  验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        如果命令输出显示服务器中无有效副本，则重新启动服务器。

4.  服务器重新启动之后，等待 10 分钟，然后再次运行步骤 2 中显示的命令，查看监视器是否处于正常状态。

5.  如果监视器运行正常，并且是邮箱服务器，则通过运行以下命令将数据库故障转移回邮箱服务器：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[启动和停止 POP3 服务](https://technet.microsoft.com/zh-cn/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/zh-cn/library/bb738143\(v=exchg.150\))

