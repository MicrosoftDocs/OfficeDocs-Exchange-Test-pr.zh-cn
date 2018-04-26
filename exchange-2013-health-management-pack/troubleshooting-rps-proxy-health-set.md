---
title: 解决 RPS.Proxy 运行状况设置的问题
TOCTitle: 解决 RPS.Proxy 运行状况设置的问题
ms:assetid: a5058323-5d86-438a-ad4a-fa4292310e98
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.rps.proxy(v=EXCHG.150)
ms:contentKeyID: 53275704
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 RPS.Proxy 运行状况设置的问题

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

RPS.Proxy 运行状况设置监视远程 PowerShell 服务的整体运行状况。

如果收到一条警报，指示 RPS.Proxy 运行状况不正常，这说明可能出现了阻止您使用远程 PowerShell 访问 Exchange 的问题。

## 说明

RPS 服务通过以下探测器和监视器进行监视：


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
<td><p>RPSProxyTestProbe</p></td>
<td><p>RPS.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>RPSProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

如果探测器运行失败，导致这个问题的原因有很多。以下包括了一些更常见的问题：

  - 驻留在受监视的 CAS 服务器上的应用程序池运行不正常。

  - 监视帐户的凭据不正确。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关导致警报出现的准确原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于确定根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序并运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要检索 server1.contoso.com 上 RPS.Proxy 状况设置的详细信息，运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "RPS.Proxy"}
    
    2.  检查命令输出，并确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 将读取 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为“**RPSProxyTestMonitor**”。与该监视器关联的探测器是“**RPSProxyTestProbe**”。要在服务器 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe RPS.Proxy\RPSProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“**结果**”。如果值为“**Succeeded**”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## RPSProxyTestMonitor 恢复操作

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的 CAS 服务器名称。

  - 全部异常跟踪，包括错误邮件、诊断数据和特定 HTTP 头信息。全部异常跟踪中的信息可用于帮助解决问题。

  - 问题发生的时间和日期。

若要帮助解决该问题，请执行以下步骤：

1.  检查 CAS 服务器上的协议日志。协议日志位于 CAS 服务器的 *\<exchange server installation directory\>*\\Logging\\HttpProxy*\\\<protocol\>* 文件夹中。

2.  创建一个测试用户帐户，然后使用该测试用户帐户登录到 CAS 服务器，例如，https:// *\<servername\>*/owa

3.  启动 IIS 管理器，并连接到报告问题的服务器，验证 MSExchangePowerShellFrontEndAppPool 是否在 CAS 服务器上运行。

4.  单击“应用程序池”，然后在 Exchange 命令行管理程序中运行以下命令，对 **MSExchangePowerShellFrontEndAppPool** 应用程序池进行再循环：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangePowerShellFrontEndAppPool

5.  按照验证问题是否仍然存在部分的步骤 2.c. 所示，重新运行关联探测器。

6.  如果该问题仍然存在，使用 IISReset 实用程序对 IIS 服务进行再循环。

7.  按照验证问题是否仍然存在部分的步骤 2.c. 所示，重新运行关联探测器。

8.  如果问题仍然存在，重新启动服务器。

9.  服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

10. 如果探测器仍然无法运行，可能需要协助才能解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

