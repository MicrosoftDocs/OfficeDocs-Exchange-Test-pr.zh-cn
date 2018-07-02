---
title: 解决 OWA.Proxy 运行状况设置的问题
TOCTitle: 解决 OWA.Proxy 运行状况设置的问题
ms:assetid: 1eaa26ad-b489-402a-ad2d-bfae3b083f42
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.owa.proxy(v=EXCHG.150)
ms:contentKeyID: 53275691
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 OWA.Proxy 运行状况设置的问题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

OWA.Proxy 运行状况设置监视 Outlook Web App 服务的整体运行状况。

如果收到指示 OWA.Proxy 处于不正常状态的警报，则表示存在可能阻止用户使用 Outlook Web App 服务的问题。

## 说明

通过使用以下探测器和监视器对 Outlook Web App 服务进行监视。


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
<td><p>OWAProxyTestProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OWAanonymouscalendarProbe</p></td>
<td><p>OWA.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>OWAProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

探测器运行失败的常见原因可能包括：

  - 驻留在受监视的客户端访问服务器 (CAS) 上的应用程序池未正常运行。

  - 监视帐户的凭据不正确。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，要检索有关 server1.contoso.com 的 OWA.Proxy 运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **OWAProxyTestMonitor**。与该监视器关联的探测器为 **OWAProxyTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## OWAProxyTestMonitor 恢复操作

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的 CAS 名称

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息  
    
    **注意**   您可以使用全部异常跟踪中的信息来帮助解决问题。

  - 问题出现的时间和日期

要解决此问题，请执行下列步骤：

1.  查看 CA 服务器上的协议日志。协议日志位于 CAS 的 *\<exchange server installation directory\>*\\Logging\\HttpProxy*\\\<protocol\>* 文件夹中。

2.  创建测试用户帐户，然后使用该测试用户帐户登录 CAS。例如，使用以下帐户登录：https:// *\<servername\>*/owa。

3.  启动 IIS 管理器，然后连接到报告问题的服务器，以确定 **MSExchangeServicesAppPools** 应用程序池是否在 CAS 上运行。

4.  单击“应用程序池”，然后通过在命令行管理程序中运行以下命令再循环“MSExchangeOWAAppPool”和“MSExchangeOWACalendarAppPool”应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle APPPOOL MSExchangeOWACalendarAppPool

5.  按照验证问题是否仍然存在部分中的步骤 2c 所示，返回关联探测器。

6.  如果问题仍然存在，通过使用 IISReset 实用程序再循环 IIS 服务。

7.  按照验证问题是否仍然存在部分中的步骤 2c 所示，返回关联探测器。

8.  如果问题仍然存在，请重新启动服务器。

9.  重启服务器后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

10. 如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

[管理 Outlook Web App](https://technet.microsoft.com/zh-cn/3814b665-01e8-4881-9a44-163f14789ee4\(exchg.150\)#managing)

