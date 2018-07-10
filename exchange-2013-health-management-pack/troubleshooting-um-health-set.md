---
title: UM 运行状况设置疑难解答
TOCTitle: UM 运行状况设置疑难解答
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53275717
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# UM 运行状况设置疑难解答

 

_**适用于：** Exchange Server 2013, Project Server 2013_

_**上一次修改主题：** 2015-03-09_

统一消息 (UM) 运行状况设置监视组织中 UM 服务的整体运行状况。

如果收到指示 UM 处于不正常状态的警报，则表示组织中存在可能阻止用户使用 UM 服务的问题。UM 运行状况设置与以下运行状况设置密切相关：

[解决 UM.CallRouter 运行状况设置的问题](troubleshooting-um-callrouter-health-set.md)

[UM.Protocol 运行状况设置疑难解答](troubleshooting-um-protocol-health-set.md)

## 说明

通过使用以下探测器和监视器来监视 UM 服务。


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>Active Directory 域服务 (AD DS)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
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
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，检索发布警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如：若要检索关于 server1.contoso.com 的 UM.Protocol 运行状况设置详细信息，请运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。
    
    3.  重新运行处于不正常状态的监视器的关联探测器。请参阅说明部分中的表格，查找关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为 **UMSelfTestMonitor**。与该监视器相关联的探测器为 **UMSelfTestProbe**。要在 server1.contoso.com 上运行该探测器，请运行下列命令：
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## 故障排除步骤

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的服务器名称

  - 警报发出的时间和日期

  - 所使用的身份验证机制和凭据信息

  - 上一次错误的全部异常跟踪，包括诊断数据和具体的 HTTP 头信息
    
    **注意**   可使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常中包含“失败原因”，它说明了探测失败的原因。

**UM 服务的 Sip 选项出现故障**

确定 UM 服务是否被禁用。如果 UM 服务未开启或被禁用，请重启 UM 服务。

**{0}% 以上的入站呼叫在上一小时内被 UM 服务拒绝。**

检查客户端访问服务器 (CAS) 上的事件日志以确定 UM 对象（例如“umipgateway”和“umhuntgroup”）是否得到正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**{0}% 以上的入站呼叫在上一小时内被 UM 工作进程拒绝。**

检查 CAS 上的事件日志以确定 UM 对象（例如“umipgateway”和“umhuntgroup”对象）是否得到正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**{0}% 以下的邮件在上一小时内得到成功处理。**

检查 CAS 上的事件日志以确定 UM 对象（例如“umipgateway”和“umhuntgroup”对象）是否得到正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**由于 UM 管道已满，Microsoft Exchange 统一消息服务拒绝呼叫**

检查 CAS 上的事件日志以确定 UM 对象（例如“umipgateway”和“umhuntgroup”对象）是否得到正确配置。

如果事件日志没有包含足够的信息，则您可能需要在专家级别启用 UM 事件日志，然后检查 UM 跟踪日志文件。

**A/V 边缘服务配置错误或无法运行**

1.  检查邮箱服务器上的事件日志，尝试确定 Lync Server 调用失败的原因。然后执行下列操作：
    
      - 确保 UM 服务选择的 Lync 池正常运行。
    
      - 若要使用特定的 Lync Server，请运行以下命令：
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**UM 服务器无法使用 Communications Server A/V 边缘服务成功地获得凭据**

检查事件日志以调查选择哪个 Lync 池，以及验证选择的 Lync 池是否正常运行。

**Communications Server 音频/视频边缘在尝试建立会话时无法打开端口或分配资源**

检查事件日志以调查选择哪个 Lync 池，以及验证选择的 Lync 池是否正常运行。

**Microsoft Exchange 统一消息服务证书即将过期**

在邮箱服务器上续订 UM 服务证书。

**其他故障排除步骤：** 

1.  启动 IIS 管理器，并将其连接到报告问题的服务器上以确定“MSExchangeServicesAppPool”应用程序池是否运行。

2.  在 IIS 管理器中，单击“应用程序池”，然后再循环“MSExchangeServicesAppPool”应用程序池。为此，请从 Exchange 命令行管理程序 运行下列命令：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  按照验证问题是否仍然存在部分步骤 2c 中所示，重新运行相关联的探测器。

4.  如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

5.  按照验证问题是否仍然存在部分步骤 2c 中所示，重新运行相关联的探测器。

6.  如果问题仍存在，重启服务器。

7.  重新启动服务器后，按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

8.  如果探测器仍然无法运行，可能需要寻求帮助来解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

