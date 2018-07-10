---
title: 解决 EWS 运行状况设置的问题
TOCTitle: 解决 EWS 运行状况设置的问题
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53275716
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 EWS 运行状况设置的问题

 

_**适用于：** Exchange Server 2013, Project Server 2013_

_**上一次修改主题：** 2015-03-09_

Exchange Web 服务 (EWS) 运行状况设置监视 EWS 服务的整体运行状况。EWS 运行状况设置与以下运行状况设置密切相关：

[EWS.Protocol 运行状况设置疑难解答](troubleshooting-ews-protocol-health-set.md)

[解决 EWS.Proxy 运行状况设置问题](troubleshooting-ews-proxy-health-set.md)

如果收到一条警报，指示 EWS 运行状况不正常，这说明可能出现了阻止用户与 Exchange 服务器通信的问题。

## 说明

EWS 通过以下探测器和监视器进行监视。


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>信息存储</p>
<p>Active Directory 域服务 (AD DS)</p></td>
<td><p>EwsCtpMonitor（EWS 运行状况设置）</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory 域服务 (AD DS)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>信息存储</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


该探测器使用监视帐户，执行从客户端访问服务器 (CAS) 到邮箱服务器的完整 EWS 登录过程。该探测器调用 EWS 上的 **GetFolder** 方法。有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

探测器运行失败的常见原因可能包括：

  - 探测器使用的身份验证机制和 CAS 虚拟目录上使用的身份验证机制之间存在不匹配的情况。

  - CAS 中受监视的 EWS 应用程序池未响应。

  - CAS 在连接到邮箱服务器时遇到网络问题。

  - CAS 在连接到域控制器时遇到通信问题。

  - 域控制器没有响应。

  - 驻留在一个或多个邮箱服务器上的 EWS 应用程序池未响应。

  - 用户的数据库未装入，或特定邮箱无法使用信息存储。

  - 一个或多个邮箱服务器上的信息存储遇到问题。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。
    
    收到来自运行状况设置的警报时，电子邮件将包含以下信息：
    
    1.  产生警报的 CAS 名称
    
    2.  探测器作为目标资源监视的邮箱服务器名称
    
    3.  上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    4.  事件发生的时间
    
    5.  所用的身份验证机制，以及凭据信息
    
    异常跟踪信息提供关于探测器运行失败原因的最重要线索。升级邮件也包含以下 HTTP 头：
    
    1.  **X-FEServer**   指示探测器在哪个 CAS 上运行
    
    2.  **X-TargetBEServer**   指示将请求路由到哪个 MBX
    
    3.  **X-DiagInfo**   指示收到请求的 MBX

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要检索 server1.contoso.com 上 EWS 运行状况设置的详细信息，运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        对于 EWS 运行状况设置，假定故障监视器为“EWSCtpMonitor”。与该监视器关联的探测器是“EWSCtpProbe”。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## EwsCtpMonitor 恢复操作

1.  启动 IIS 管理器，然后连接到报告问题的服务器，以确定“MSExchangeServicesAppPool”应用程序池是否在 CA 和邮箱服务器上运行。

2.  找到不正常探测器的 MailboxDatabase。然后验证邮箱服务器的邮箱数据库是否可用，以及信息存储是否处于正常状态。

3.  单击“应用程序池”，然后在命令行管理程序中运行以下命令，对“MSExchangeServicesAppPool”应用程序池进行再循环：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

5.  如果问题仍然存在，使用 IISReset 实用程序对整个 IIS 服务进行再循环。

6.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

7.  如果问题仍然存在，请查看 CA 和邮箱服务器上的协议日志文件。CAS 的协议日志位于 *\<exchange server installation directory\>\\Logging\\HttpProxy\\Ews* 文件夹中。邮箱服务器的日志位于 *\<exchange server installation directory\>\\Logging\\Ews* 文件夹中。

8.  创建一个测试用户帐户，然后使用此测试用户帐户登录给定的 CAS。例如，使用以下帐户登录：https:// \<servername\>/ews/exchange.asmx。如果问题仍然存在，则尝试不同的 CAS，以确定问题是否限于 CAS，而不涉及邮箱服务器。如果测试用户名称通过，则问题可能会影响带有监视邮箱的特定邮箱数据库或邮箱服务器。使用邮箱数据库中现有的测试帐户尝试重复此步骤。

9.  检查 CA 和邮箱服务器之间的网络连接。

10. 检查 EWS.Proxy 运行状况设置上是否有任何警报可能指示影响特定 CAS 的问题。

11. 检查 EWS.Protocol 运行状况设置上是否有任何警报可能指示影响特定邮箱服务器的问题。

12. 如果问题仍然存在，重新启动服务器。为此，请首先对服务器托管的数据库进行故障转移。为此，请运行下列命令：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **注意**   在本示例以及所有后续代码示例中，将 *server1.contoso.com* 替换为实际服务器名称。

13. 验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令输出显示服务器中无有效副本，则重新启动服务器。

14. 服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

15. 如果探测器运行成功，则通过以下命令将数据库故障转移回邮箱服务器。
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. 如果探测器仍然无法运行，可能需要通过协助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

