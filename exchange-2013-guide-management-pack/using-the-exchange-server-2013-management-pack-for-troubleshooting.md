---
title: 使用 Exchange Server 2013 管理包进行故障排除
TOCTitle: 使用 Exchange Server 2013 管理包进行故障排除
ms:assetid: c9672dad-1e67-4f07-bad9-539a67f2ac70
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn195913(v=EXCHG.150)
ms:contentKeyID: 53275727
ms.author: dstrome
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用 Exchange Server 2013 管理包进行故障排除

 

_**上一次修改主题：** 2013-04-09_

[Exchange Server 2013 Management Pack 入门](getting-started-with-exchange-server-2013-management-pack.md)概述了管理包主控板。本主题将引导您了解该管理包如何帮助您对问题进行故障排除。该过程最好通过一个具体的示例说明。以如下方案为例：

Rob Fielder 是 Contoso 的 Exchange 管理员。他打开 SCOM 控制台并单击 Exchange Server 2013 主控板上的“服务器运行状况”，以检查 Exchange 服务器的状态。他发现一个 CAS 服务器上的“服务组件”处于紧急状态。

![故障的 CAS 服务器](images/Dn195913.32a265d9-68e0-4d8c-9f83-1d10cdda1f84(EXCHG.150).png "故障的 CAS 服务器")

Rob 双击服务器，打开“运行状况资源管理器”窗口。在此窗口中，他可以看到处于未正常运行状态的服务组件是 OWA.Proxy 运行状况设置。他单击该组件，查看与此运行状况设置相关的信息。

![故障的 CAS 服务器 healthset 详细信息](images/Dn195913.8e4d05a6-9128-40d8-b262-e60e9affc973(EXCHG.150).png "故障的 CAS 服务器 healthset 详细信息")

外部知识资源下提供的链接将 Rob 转到[解决 OWA.Proxy 运行状况设置的问题](https://technet.microsoft.com/zh-cn/library/jj737712\(v=exchg.150\))主题。在此文章中，Rob 查看到，首先要做的事是验证问题是否仍存在。按照指示的步骤进行操作，他运行以下命令，以验证命令行管理程序中 OWA.Proxy 运行状况设置的当前状态。

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

运行此命令，得出以下输出：

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Unhealthy  OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

Rob 发现问题在于 OWA 应用程序池。下一步是重新运行对处于未正常运行状态监视器的相关探测器。通过使用“对 OWA.Proxy 运行状况设置进行故障排除”主题中的表格，他确定需要重新运行的探测器是 OWAProxyTestProbe。他运行以下命令：

    Invoke-MonitoringProbe OWA.Proxy\OWAProxyTestProbe -Server Server1.contoso.com | Format-List

他扫描了 ResultType 值的输出，发现探测器失败了：

    ResultType : Failed

他继续进行文章中的“OWAProxyTestMonitor 恢复操作”部分。他连接到使用 IIS 管理器的 Server1，看看 MSExchangeOWAAppPool 是否在 IIS 服务器上运行。他确认在运行后，下一个步骤引导他再循环 MSExchangeOWAAppPool：

    C:\Windows\System32\Inetsrv\Appcmd recycle APPPOOL MSExchangeOWAAppPool

看到 MSExchangeOWAAppPool 成功循环后，他返回到重新运行使用 Invoke-MonitoringProbe cmdlet 的探测器，验证问题是否仍存在，这次的结果是成功的。然后，他运行以下命令，验证运行状况设置是否再一次报告为“正常”：

    Get-ServerHealth Server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Proxy"}

这次，他看到问题解决了。

    Server          State           Name                 TargetResource       HealthSetName   AlertValue ServerComp
                                                                                                         onent
    ------          -----           ----                 --------------       -------------   ---------- ----------
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWAAppPool OWA.Proxy       Healthy    OwaProxy
    Server1         Online          OWAProxyTestMonitor  MSExchangeOWACale... OWA.Proxy       Healthy    OwaProxy

他返回到 SCOM 控制台，验证问题是否已解决。

![服务器运行状况](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "服务器运行状况")

以上所述情景是您查看 SCOM 控制台提醒时故障排除工作流程的简单说明。即使详细步骤有所不同，但您一般都会对控制台报告的每个问题按照一个类似的故障排除工作流程进行操作。

