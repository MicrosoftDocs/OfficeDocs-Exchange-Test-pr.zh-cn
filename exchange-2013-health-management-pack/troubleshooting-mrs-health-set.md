---
title: 解决 MRS 运行状况设置的问题
TOCTitle: 解决 MRS 运行状况设置的问题
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53275694
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 MRS 运行状况设置的问题

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

邮箱复制访问 (MRS) 运行状况设置可监视 MRS 服务的总体运行状况。

## 说明

通过使用以下探测器和监视器监视 MRS 服务。


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
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>信息存储</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 MRS 运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行处于不正常状态的监视器的关联探测器。请参阅说明部分中的表格，查找关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **MRSServiceCrashingMonitor**。与该监视器相关联的探测器为 **MRSServiceCrashingProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## 常见问题

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的服务器名称

  - 出现警报的时间和日期

  - 使用的身份验证机制，以及凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    您可以使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常包含说明探测器失败原因的“故障原因”。

**邮箱已锁定**

当邮箱锁定时，您可能会收到类似于以下内容的警报：

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: Primary (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, Protected Database: exampledb-db089 Exception: MapiExceptionADUnavailable: Unable to prepopulate the cache for user …*

这表明邮箱已锁定。要对邮箱进行解锁，请运行以下命令：

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**注意**   在此命令中，使用电子邮件中提供的邮箱名称（为 **MailboxIdentity**）替换 \<*mailboxIdentity*\>。如果邮箱是存档邮箱，则必须包括 **–Archive** 标志。您可以通过查看警报中的 **MailboxGuid** 字段来确定邮箱是主邮箱还是存档邮箱。

**损坏的迁移作业**

出现损坏的迁移作业时，您可能会收到类似于以下内容的警报：

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

当迁移元数据遇到问题时，会出现损坏。一旦出现损坏，Microsoft 便会收到即将进行调查的 Watson 报告。要从此问题进行恢复，您必须删除迁移批处理，然后重新创建该批处理。为此，请执行下列步骤：

1.  若要损坏的批处理，请运行以下命令：
    
        Remove-MigrationBatch -Identity

2.  若重新创建损坏的批处理，请运行以下命令：
    
        New-MigrationBatch -Local -Name

有关详细信息，请参阅 [Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

**MailboxMigration 警报：CriticalError**

如果在邮件迁移期间出现严重错误，您可能会收到类似于以下内容的警报：

*Notification thrown by MailboxMigration at 9/7/2012 9:08:32 PM. Details: Diagnostic Information: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

要解决此问题，必须重试迁移。为此，请运行以下命令或按 Exchange 管理中心 (EAC) 上的“开始”按钮。

    Call start-migrationbatch -Identity batchName

出现此问题时，系统会向 Microsoft 发送 Dr. Watson 邮件，以便进行调查。

**迁移 Exchange 复制访问未在运行。**

查看此错误原因时，您可以通过运行以下命令来验证服务的运行状况：

    Test-MRSHealth <servername> -MonitoringContext:$true

您也可以通过运行以下命令来尝试启动服务：

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping Failed**

查看此错误原因时，您可能会收到类似于以下内容的警报：

*An issue with MRS was detected at 6/26/2012 6:08:47 AM. Details: MRS RPC Ping check for server \<ServerName\> failed with the following error: The RPC endpoint for the Microsoft Exchange Mailbox Replication service couldn't respond:*

出现此问题后，您可以通过运行以下命令来验证服务的运行状况：

    Test-MRSHealth <servername> -MonitoringContext:$true

您也可以通过运行以下命令来尝试重启服务：

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication Service is repeatedly crashing**

当 MSExchangeMailboxReplication 服务崩溃或停止响应时，您可能会收到类似于以下内容的警报：

*The MRS process has crashed at least 3 times in last 01:00:00. \<b\>Watson Message:\</b\> Watson report about to be sent for process id: 41432, with parameters: E12, \<ServerName\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

出现此问题后，您可以通过运行以下命令来验证服务的运行状况：

    Test-MRSHealth <servername> -MonitoringContext:$true

您也可以通过运行以下命令来尝试重启服务：

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication is not scanning MDB queues**

当 MSExchangeMailboxReplication 服务无法扫描队列时，您可能会收到类似于以下内容的警报：

*An issue with MRS was detected at 6/12/2012 6:20:44 PM. Details: MRS queue scan check for server \<servername\> failed with the following error: The Microsoft Exchange Mailbox Replication Service isn't scanning mailbox database queues for jobs. Last scan age: 04:38:02.1959439..*

出现此问题后，您可以通过运行以下命令来验证服务的运行状况：

    Test-MRSHealth <servername> -MonitoringContext:$true

您也可以通过运行以下命令来尝试重启服务：

    Restart-Service msexchangemailboxreplication

**其他故障排除步骤**

1.  启动 IIS 管理器，然后连接到报告问题的服务器，以验证 **MSExchangeServicesAppPool** 应用程序池是否正在运行。

2.  在 IIS 管理器中，单击“应用程序池”，然后在命令行管理程序中使用以下命令来再循环“MSExchangeServicesAppPool”应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

4.  如果问题仍然存在，则通过使用 IISReset 实用程序或运行以下命令来回收 IIS 服务：
    
        Iisreset /noforce

5.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

6.  如果问题仍然存在，请重新启动服务器。

7.  重启服务器后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

