---
title: 解决 UM.CallRouter 运行状况设置的问题
TOCTitle: 解决 UM.CallRouter 运行状况设置的问题
ms:assetid: 444a9038-0952-4823-98fb-99fa59f4a378
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.um.callrouter(v=EXCHG.150)
ms:contentKeyID: 53275697
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 UM.CallRouter 运行状况设置的问题

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Microsoft Exchange 统一消息 (UM) 呼叫路由器运行状况设置监视 UM 呼叫路由器服务的整体运行状况。

如果收到指示 UM 处于不正常状态的警报，则表示组织中存在可能阻止用户使用 UM 服务的问题。UM 运行状况设置与以下运行状况设置密切相关：

[UM 运行状况设置疑难解答](troubleshooting-um-health-set.md)

[UM.Protocol 运行状况设置疑难解答](troubleshooting-um-protocol-health-set.md)

## 说明

通过使用以下探测器和监视器监视 UM.Protocol 服务


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
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>Active Directory 域服务 (AD DS)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
        
        例如，若要检索有关 server1.contoso.com 的 UM.CallRouter 运行状况设置的详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.CallRouter"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”值将为 `Unhealthy`。
    
    3.  重新运行处于不正常状态的监视器的关联探测器。请参阅解释部分中的表格，查找关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定失败的监视器为“UMCallRouterTestMonitor”。与该监视器相关联的探测器是“UMCallRouterTestProbe”。要对 server1.contoso.com 运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe UM.CallRouter\UMCallRouterTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## 故障排除步骤

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的服务器名称

  - 出现警报的时间和日期

  - 使用的身份验证机制，以及凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息
    
    **注意**   您可以使用全部异常跟踪中的信息来帮助解决问题。探测器所生成的异常包含描述探测器失败原因的“故障原因”。

**UM 呼叫路由器服务的 SIP 选项失败**

确定 UM 呼叫路由器服务是否已禁用。如果 UM 呼叫路由器服务尚未启动或已禁用，则重新启动 UM 服务。

**在过去一小时内，UM 呼叫路由器拒绝了超过 50% 的入站呼叫**

检查客户端访问服务器 (CAS) 上的事件日志以确定 UM 对象（例如“umipgateway”和“umhuntgroup”）是否得到正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**在过去一小时内，UM 呼叫路由器中有超过 {0}% 的未接来电通知代理失败**

检查 CAS 上的事件日志，以确定诸如“umipgateway”和“umhuntgroup”之类的 UM 对象是否已正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**Microsoft Exchange 统一消息呼叫路由器证书即将过期**

续订 CAS 上的 UM 呼叫路由器服务证书。

**其他故障排除步骤：**

1.  启动 IIS 管理器，然后连接到报告问题的服务器，以确定 **MSExchangeServicesAppPool** 应用程序池是否正在运行。

2.  在 IIS 管理器中，单击“应用程序池”，然后在命令行管理程序中使用以下命令来再循环“MSExchangeServicesAppPool”应用程序池：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

4.  如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

5.  按照验证问题是否仍然存在部分中的步骤 2c 所示，重新运行关联探测器。

6.  如果问题仍然存在，请重新启动服务器。

7.  重启服务器后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

