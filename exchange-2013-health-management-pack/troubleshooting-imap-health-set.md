---
title: 解决 IMAP 运行状况设置的问题
TOCTitle: 解决 IMAP 运行状况设置的问题
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53275696
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 IMAP 运行状况设置的问题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

IMAP 运行状况设置监视 IMAP4 代理基础结构在客户端访问服务器 (CAS) 上的可用性。IMAP 运行状况设置与以下运行状况设置密切相关：

[解决 IMAP.Protocol 运行状况设置的问题](troubleshooting-imap-protocol-health-set.md)

[IMAP.Proxy 运行状况设置疑难解答](troubleshooting-imap-proxy-health-set.md)

如果您收到指明 IMAP 运行状况不正常的警报，则表明存在问题，可能会导致用户无法使用 IMAP 访问自己的邮箱。

## 说明

IMAP4 服务受到以下探测器和监视器的监视：


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>邮箱服务器身份验证</p>
<p>高可用性</p>
<p>网络</p></td>
<td><p>ImapCTPMonitor（IMAP 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>身份验证</p></td>
<td><p>ImapProxyTestMonitor（IMAP.Proxy 运行状况设置）</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>身份验证</p>
<p>信息存储</p>
<p>高可用性</p></td>
<td><p>IMAP.Protocol（IMAP.Protocol 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>身份验证</p></td>
<td><p>IMAP.Protocol（IMAP.Protocol 运行状况设置）</p>
<p>AverageCommandProcessingTimeGt60sMonitor（IMAP 运行状况设置）</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行下列命令，以获取警报中提到的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要获取有关 server1.contoso.com 的 IMAP 运行状况设置详细信息，请运行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行处于不正常状态的监视器的关联探测器。请参阅说明部分中的表格，查找关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **ImapCTPMonitor**。与该监视器关联的探测器为 **ImapCTPProbe**。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## ImapTestDeepMonitor 和 ImapSelfTestMonitor 恢复操作

1.  重启后端服务器上的 Exchange IMAP4 服务。有关如何停止和启动 IMAP4 服务的详细信息，请参阅[启动和停止 IMAP4 服务](https://technet.microsoft.com/zh-cn/library/bb124022\(v=exchg.150\))。

2.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

3.  如果问题仍存在，您必须使用下列命令对邮箱服务器上托管的数据库进行故障转移：
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令输出显示服务器上无活动副本，重启服务器。

5.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

6.  如果探测器成功，运行下列命令，对数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## ImapCTPMonitor 恢复操作

CAS 服务器通常会发出此监视器警报。

1.  重启后端服务器上的 Exchange IMAP4 服务。有关如何停止和启动 IMAP4 服务的详细信息，请参阅[启动和停止 IMAP4 服务](https://technet.microsoft.com/zh-cn/library/bb124022\(v=exchg.150\))。

2.  按照验证问题是否仍然存在部分的步骤 2.c. 所示，重新运行关联探测器。

3.  如果问题仍然存在，必须启用 IMAP 协议日志记录来帮助解决问题。为此，请执行下列步骤：
    
    1.  在 Windows PowerShell 中，运行以下命令：
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  重启后端服务器上的 Exchange IMAP4 服务。有关如何停止和启动 IMAP4 服务的详细信息，请参阅[启动和停止 IMAP4 服务](https://technet.microsoft.com/zh-cn/library/bb124022\(v=exchg.150\))。
    
    3.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。
    
    4.  运行下列命令，然后确定日志文件的位置。为此，请运行下列命令：
        
            Get-ImapSettings -server <CAS server name>
    
    5.  确定提供此命令的邮箱。邮箱服务器的名称是错误消息中的 `_Mbx:` 值。
    
    6.  运行以下命令：
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **注意**   在此命令中，用实际的邮箱服务器名称替换 *mailbox1.contoso.com*。
    
    7.  如果命令输出中列出的任一监视器处于不正常状态，必须先解决这些监视器的问题。请按照ImapTestDeepMonitor 和 ImapSelfTestMonitor 恢复操作部分中概述的故障排除步骤操作。

4.  如果邮箱服务器被报告为正常，重新启动 CAS。

5.  按照验证问题是否仍然存在部分的步骤 2c 所示，在服务器重启后，重新运行关联探测器。

6.  关闭协议日志记录。为此，请运行下列 Windows PowerShell 命令：
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  重启 IMAP4 服务。

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## ImapProxyTestMonitor 恢复操作

1.  重启 IMAP4 服务。

2.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

3.  如果探测器仍失败，重启 CAS。

4.  按照验证问题是否仍然存在部分的步骤 2c 所示，在服务器重启后，重新运行关联探测器。

5.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor 恢复操作

CA 和邮箱服务器通常会发出此监视器警报。

1.  重启后端服务器或 CAS 上的 Exchange IMAP4 服务。有关如何停止和启动 IMAP4 服务的详细信息，请参阅[启动和停止 IMAP4 服务](https://technet.microsoft.com/zh-cn/library/bb124022\(v=exchg.150\))。

2.  等待 10 分钟，查看监视器是否处于正常运行状态。10 分钟后，运行下列命令：
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **注意**   在此命令中，用实际的服务器名称替换 *server1.contoso.com*。

3.  等待 10 分钟，然后重新运行第 2 步中显示的命令，观察监视器是否处于正常状态。

4.  如果问题仍然存在，必须重启服务器。如果服务器是 CAS，只需重启服务器即可。如果服务器是邮箱服务器，请执行下列操作：
    
    1.  对服务器上托管的数据库进行故障转移。为此，请运行下列命令：
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **注意**   在此代码示例以及所有后续代码示例中，用实际的服务器名称替换 *server1.contoso.com*。
    
    2.  验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        如果命令输出显示服务器上无活动副本，重启服务器。

5.  服务器重新启动之后，等待 10 分钟，然后再次运行步骤 2 中显示的命令，查看监视器是否处于正常状态。

6.  如果监视器处于正常状态，且服务器是邮箱服务器，请通过运行下列命令来对数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[POP3 和 IMAP4](https://technet.microsoft.com/zh-cn/library/jj657728\(v=exchg.150\))

[在 Exchange 2013 中启用 IMAP4](https://technet.microsoft.com/zh-cn/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/zh-cn/library/bb738126\(v=exchg.150\))

