---
title: EWS.Protocol 运行状况设置疑难解答
TOCTitle: EWS.Protocol 运行状况设置疑难解答
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53275698
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# EWS.Protocol 运行状况设置疑难解答

 

_**适用于：** Exchange Server 2013, Project Server 2013_

_**上一次修改主题：** 2015-03-09_

EWS.Protocol 运行状况设置监视邮箱服务器上的 Exchange Web 服务 (EWS) 通信协议。EWS.Protocol 运行状况设置与下列运行状况设置紧密相关：

[解决 EWS 运行状况设置的问题](troubleshooting-ews-health-set.md)

[解决 EWS.Proxy 运行状况设置问题](troubleshooting-ews-proxy-health-set.md)

如果您收到指定 EWS.Protocol 不正常的警报，这表示出现一个阻止用户访问 Exchange 的问题。

## 说明

EWS.Protocol 运行状况设置由下列探测器组成：

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe 不依赖信息存储。但是，EwsDeepTestProbe 探测器依赖信息存储。这两个探测器在邮箱服务器上执行 EWS 操作，它们使用与客户端访问服务器 (CAS) 同样的身份验证方法。EwsSeftTestProbe 调用 **ConvertId** 方法，EwsDeepTestProbe 调用 **GetFolder** 方法。


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>信息存储</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

当从此运行状况设置收到警报时，电子邮件包含下列信息：

1.  发出警报的邮箱服务器的名称

2.  上一错误的完全异常跟踪，包括诊断数据和特定 HTTP 头信息

3.  发生事件的时间

## 常见问题

此探测器可能因为下列任何常见问题出现故障：

  - 受监视的邮箱服务器上的 EWS 应用程序协议工作不正常。

  - 域控制器不响应，或者它们无法与邮箱服务器通信。

  - 用户的数据库未安装，或者信息存储对于特定邮箱不可用。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  在 Exchange 命令行管理程序 上，运行下列命令检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 EWS.Protocol 运行状况设置详细信息，请运行下列命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行处于不正常状态的监视器的关联探测器。请参阅说明部分中的表格，查找关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **EWSSelfTestMonitor**。与该监视器关联的探测器为 **EWSSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## EWSSelfTestMonitor 和 EWSDeepTestMonitor 恢复操作

此监视器警报通常在邮箱服务器上发出。

1.  启动 IIS 管理器，然后连接到报告问题的服务器以确定 MSExchangeServicesAppPool 是否在 CA 和邮箱服务器上运行。

2.  找到出现故障的探测器的 MailboxDatabase，然后确认已经针对 MailboxServer 激活 MailboxDatabase，且信息存储运行正常。

3.  单击“应用程序池”，然后通过从命令行管理程序运行下列命令再循环 **MSExchangeServicesAppPool** 应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

5.  如果问题仍存在，则使用 IISReset 实用程序重新启动 IIS 服务。

6.  按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

7.  如果问题仍存在，请查看邮箱服务器上的协议日志文件。在邮箱服务器上，日志驻留在 *\<exchange server installation directory\>*\\Logging\\Ews 文件夹中。

8.  创建测试用户帐户，然后使用该测试用户帐户登录端口 444 https://*\<servername\>*:444/ews/exchange.asmx 上的给定邮箱服务器。如果测试成功，则说明出现一个可能影响监视邮箱所在的特定邮箱数据库或邮箱服务器的问题。尝试使用该数据库上的测试帐户重复此步骤。

9.  检查 EWS.Protocol 运行状况设置中的任何指示影响特定邮箱服务器的问题的警报。

10. 如果问题仍存在，请重新启动服务器。为此，首先使用下列命令对服务器上托管的数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    在该示例和所有后续代码示例中，将 *server1.contoso.com* 替换为实际服务器名称。

11. 验证是否已将所有数据库从报告问题的服务器上删除。为此，请运行下列命令：
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    如果命令输出显示服务器上没有活动副本，则需要保存并重新启动服务器。重新启动服务器。

12. 在服务器重新启动后，按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

13. 如果探测器成功，则通过运行下列命令对数据库进行故障转移：
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. 如果探测器仍然无法运行，可能需要通过协助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

