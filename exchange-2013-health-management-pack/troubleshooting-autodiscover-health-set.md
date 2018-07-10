---
title: 解决 Autodiscover 运行状况设置的问题
TOCTitle: 解决 Autodiscover 运行状况设置的问题
ms:assetid: bc933621-df73-4d1d-bdef-825b98be8e09
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.autodiscover(v=EXCHG.150)
ms:contentKeyID: 53275711
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 Autodiscover 运行状况设置的问题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

自动发现运行状况设置监视客户端自动发现服务的总体运行状况。

如果您接收到指示自动发现处于不正常状态的警报，则表示存在可能阻止用户使用自动发现进程访问其邮箱的问题。

## 说明

通过使用以下探测器和监视器对自动发现服务进行监视。


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
<td><p>AutodiscoverCtpProbe</p></td>
<td><p>Autodiscover</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverCtpMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

此监视器失败的常见原因可能包括：

  - 驻留在受监视的客户端访问服务器 (CAS) 上的自动发现应用程序池 (MSExchangeAutodiscoverAppPool) 未响应。或者，驻留在一个或多个邮箱服务器上的自动发现应用程序池未响应。

  - CAS 遇到网络问题，并且无法连接至邮箱服务器或域控制器。

  - 监视帐户的凭据不正确。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的自动发现运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover"}
    
    2.  查看命令输出，确定报告错误的监视器。发出警报的监视器的“AlertValue” 值为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **AutodiscoverCtpMonitor**。与该监视器关联的探测器为 **AutodiscoverCtpProbe**。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe Autodiscover\AutodiscoverCtpProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## AutodiscoverCtpMonitor 恢复操作

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的服务器名称

  - 该探测器正在监视的邮箱服务器的名称

  - 出现警报的时间和日期

  - 所使用的身份验证机制和凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息

您可以使用全部异常跟踪中的信息来帮助解决问题。探测器所生成的异常包含描述探测器失败原因的“故障原因”。例如，“故障原因”可能是下列原因之一：

  - **X-FEServer**   指示探测器在哪个 CAS 上运行

  - **X-CalculatedBETarget**   表示接收所路由的请求的邮箱服务器

  - **X-DiagInfo**   表示接收请求的邮箱服务器

要解决此问题，请执行下列步骤：

1.  检查 CA 和邮箱服务器上的协议日志。CAS 上的协议日志默认位于 ***\<exchange server installation directory\>*\\Logging\\HttpProxy\\Autodiscover** 文件夹中。邮箱服务器上的协议日志文件默认位于 ***\<exchange server installation directory\>*\\Logging\\Autodiscover** 文件夹中。

2.  创建测试用户帐户，然后使用该测试用户帐户登录 CAS。例如，使用以下帐户登录：https://*\<servername\>*/autodiscover/autodiscover.xml。
    
    如果测试用户帐户名称通过，则问题可能会影响托管受监视邮箱的邮箱服务器。
    
    尝试通过在邮箱服务器上使用测试帐户，来重复之前的步骤。如果尝试失败，尝试对另一台 CAS 执行此测试，以确定该问题是发生于特定的 CAS 上，而不发生于邮箱服务器上。

3.  验证 CA 和邮箱服务器之间的网络连接。使用 ping.exe 验证每个服务器是否都有响应。

4.  检查针对 Autodiscover.Proxy 运行状况设置发出的警报，其中可能指出存在影响特定邮箱服务器的问题。有关详细信息，请参阅[解决 Autodiscover.Proxy 运行状况设置的问题](troubleshooting-autodiscover-proxy-health-set.md)。

5.  检查针对 Autodiscover.Protocol 运行状况设置发出的警报，其中可能指出存在影响特定邮箱服务器的问题。有关详细信息，请参阅[Autodiscover.Protocol 运行状况设置疑难解答](troubleshooting-autodiscover-protocol-health-set.md)。

6.  启动 IIS 管理器，然后连接到报告问题的服务器。验证 **MSExchangeAutodiscoverAppPool** 应用程序池是否正在 CA 和邮箱服务器上运行。

7.  在 IIS 管理器中，单击“应用程序池”，然后在命令行管理程序中使用以下命令来再循环“MSExchangeAutodiscoverAppPool”应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

9.  如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

10. 按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

11. 如果问题仍存在，重启服务器。

12. 重启服务器后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

13. 如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

