---
title: Autodiscover.Protocol 运行状况设置疑难解答
TOCTitle: Autodiscover.Protocol 运行状况设置疑难解答
ms:assetid: 06afdcc8-7920-4e88-b85a-98e67a19d221
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.autodiscover.protocol(v=EXCHG.150)
ms:contentKeyID: 53275690
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Autodiscover.Protocol 运行状况设置疑难解答

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Autodiscover.Protocol 运行状况设置可监视邮箱服务器上的自动发现通信协议。

如果收到一条警报，指示 Autodiscover.Protocol 运行状况不正常，说明可能会有阻止用户访问他们邮箱的问题。

## 说明

Autodiscover.Protocol 服务受到以下探测器和监视器的监视：


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
<td><p>AutodiscoverSelfTestProbe</p></td>
<td><p>Autodiscover.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>AutodiscoverSelfTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

探测器失败的常见原因可能包括：

  - 驻留在受监视的客户端访问服务器 (CAS) 上的自动发现应用程序池 (MSExchangeAutodiscoverAppPool) 未响应。或者，驻留在一个或多个邮箱服务器上的自动发现应用程序池未响应。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，检索发布警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 Autodiscover.Protocol 运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "Autodiscover.Protocol"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **AutodiscoverSelfTestMonitor**。与该监视器关联的探测器为 **AutodiscoverSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe Autodiscover.Protocol\AutodiscoverSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## AutodiscoverSelfTestProbe 恢复操作

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的邮箱服务器的名称

  - 受监视的邮箱服务器的名称

  - 警报发出的时间和日期

  - 使用的身份验证机制，以及凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息

您可以使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常包含说明探测器失败原因的“故障原因”。

要解决此问题，请执行下列步骤：

1.  查看邮箱服务器上的协议日志。邮箱服务器上的协议日志文件默认位于 ***\<exchange server installation directory\>*\\Logging\\Autodiscover** 文件夹中。

2.  创建一个测试用户帐户，然后通过在地址中使用测试用户帐户来登录邮箱服务器。例如，使用以下网址登录：https://*\<servername\>*:444/autodiscover/autodiscover.xml。
    
    如果测试用户帐户名称通过，则可能存在影响托管受监视邮箱的邮箱服务器的问题。

3.  尝试通过在邮箱服务器上使用测试帐户，来重复之前的步骤。

4.  检查针对 Autodiscover.Proxy 运行状况设置发出的警报，其中可能指出存在影响特定邮箱服务器的问题。有关详细信息，请参阅[解决 Autodiscover.Proxy 运行状况设置的问题](troubleshooting-autodiscover-proxy-health-set.md)。

5.  检查针对 Autodiscover 运行状况设置发出的警报，其中可能指出存在影响特定邮箱服务器的问题。有关详细信息，请参阅[解决 Autodiscover 运行状况设置的问题](troubleshooting-autodiscover-health-set.md)。

6.  启动 IIS 管理器，然后连接到报告问题的邮箱服务器。验证 **MSExchangeAutodiscoverAppPool** 应用程序池是否在该邮箱服务器上运行。

7.  在 IIS 管理器中，单击“应用程序池”，然后在命令行管理程序中使用以下命令来再循环“MSExchangeAutodiscoverAppPool”应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeAutodiscoverAppPool

8.  按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

9.  如果问题仍存在，使用 IISReset 实用程序或运行以下命令来再循环 IIS 服务：
    
        Iisreset /noforce

10. 按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

11. 如果问题仍然存在，请重新启动服务器。

12. 重新启动服务器后，按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

13. 如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

