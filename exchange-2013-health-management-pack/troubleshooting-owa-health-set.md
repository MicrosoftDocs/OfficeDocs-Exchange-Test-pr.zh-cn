---
title: OWA 运行状况设置疑难解答
TOCTitle: OWA 运行状况设置疑难解答
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53275714
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# OWA 运行状况设置疑难解答

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Outlook Web App (OWA) 运行状况设置监视 Outlook Web App 服务的整体运行状况。

如果收到一条警报，指示 Outlook Web App 运行状况不正常，说明可能会有阻止用户使用 Outlook Web App 访问他们邮箱的问题。

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
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>信息存储</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

该探测器无法运行的几个原因。以下是一些更为常见的原因：

  - 在监视的客户端访问服务器 (CAS) 上托管的 Outlook Web App 应用程序池没有响应，或在邮箱服务器上托管的应用程序池没有响应。

  - CAS 出现网络问题，并且不能连接到邮箱服务器上或域控制器上。

  - 监视帐户的凭据不正确。

  - 用户的数据库未安装，或该邮箱不能访问信息存储。

  - 信息存储没有响应。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，检索生成警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Outlook Web App 关于 server1.contoso.com 运行状况设置的详细信息，请执行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  检查命令输出，确定哪个监视器报告了错误。发出警报的监视器的“AlertValue”值为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，若要在 *server1.contoso.com* 上创建一个 Exchange ActiveSync 监视探测器，请执行以下命令：
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

## POPCTPMonitor Recovery Actions

运行状况设置中的电子邮件警报包含以下信息：

  - 发送警报的服务器名称

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息  
    
    **注意**   可使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常中包含“失败原因”，它说明了探测失败的原因。例如，异常情况包括以下：
    
      - **MissingKeyword**   服务器响应中找不到预期关键字。在这种情况下，异常包含预期关键字。
    
      - **NameResolution**   DNS 解析无法解析给定的服务器名称。
    
      - **NetworkConnection**   探测器在尝试连接到 CAFE 上的 OWA 应用程序池时，出现网络连接失败。
    
      - **UnexpectedHttpResponseCode**   响应有一个无法预期的 HTTP 代码。例如，服务器返回 HTTP 代码“503”。
    
      - **RequestTimeout**   服务器响应客户端请求的时间太长。
    
      - **ScenarioTimeout**   探测器成功完成，但需要花费至少一分钟来完成。这通常表明系统超负荷。
    
      - **OwaErrorPage**Outlook Web App 返回一个错误页面。导致失败的错误名称通常可在异常邮件中获取。
    
      - **OwaMailboxErrorPage**Outlook Web App 返回一个包含邮箱储存相关错误的错误页面。这通常表明邮箱储存完成或邮箱正被卸载。
    
    异常情况包括一个重要的名为 **FailingComponent** 的字段。探测器尝试确认错误，如以下示例：
    
      - **邮箱**   探测器可以达到 Outlook Web App，但不能连接到邮箱储存中。这种情况下，探测器探测失败，或邮箱访问延迟导致探测器探测失败并产生 **ScenarioTimeout** 错误。当这些失败出现时，应该检查邮箱服务器的运行状况。
    
      - **Active Directory**   探测器可到达 Outlook Web App，但不能连接到 Active Directory。这种情况下，探测器运行失败或 Active Directory 呼叫延迟可能导致了探测器超时。当这些失败类型出现时，应该检查域控制器的运行状况，也要检查 CA 和邮箱服务器的网络连接情况以及域控制器。
    
      - **Owa**   这通常指在 Outlook Web App 层出现错误。当这些类型的失败出现时，必须验证 CA 和邮箱服务器上的 Outlook Web App 进程的运行状况，同时检查网络连接情况。
    
    该异常也包含探测器运行失败之前收到的最新 HTTP 请求和响应信息。呈报正文包括探测日志的路径。您可以使用该信息来确认全部 HTTP 网络请求和探测器运行失败时发生的响应。此文件仅包含运行失败的探测器的数据，因为只会对失败的尝试进行记录。可以使用此信息全面了解测试失败的原因。

  - 可行性指标降低了多少 (x%)。

  - 该文件夹的完整路径包括探测器的完整 HTTP 请求记录。默认情况下，该信息位于 *\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe 文件夹中。

  - 警报发出的时间和日期

要解决此问题，请执行下列步骤：

1.  创建测试用户帐户，然后使用该测试用户帐户登录 CAS。例如，使用 https:// *\<servername\>*/owa 登录。
    
    如果失败，可使用不同的 CA 服务器来验证该问题出于特定的 CAS，而不是邮箱服务器。

2.  验证 CA 和邮箱服务器的网络连接情况。使用 ping.exe 验证每个服务器是否都有响应。

3.  检查针对 OWA.Protocol 运行状况设置发出的警报，其中可能指出存在影响特定邮箱服务器的问题。有关详细信息，请参阅[解决 OWA.Protocol 运行状况设置的问题](troubleshooting-owa-protocol-health-set.md)。

4.  启动 IIS 管理器，然后将其连接到报告问题的服务器上，以验证 MSExchangeOwaAppPool 应用程序池正在 CAS 上运行。

5.  在 IIS 管理器中，验证默认网站是否正在运行。

6.  查找失败探测器的邮箱数据库，并验证邮箱数据库在邮箱服务器上处于活动状态，且邮箱储存正常运行。若要找到失败的数据库 GUID 信息，打开全部异常跟踪信息。每一个失败应该包含一个与以下示例类似的条目：
    
    从以下目标启动 Owa 探测器：https://localhost/owa/，用户名：*HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  复制 HealthMailbox GUID，然后在命令行管理程序中运行以下命令：
    
        Get-Mailbox -Monitoring -Identity <username>
    
    例如，运行以下命令：
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    在返回的对象中，可以找到用户的数据库名称，也可以确定当前活动数据库驻留的位置。

8.  如果在站点间配置了重定向，可能会出现探测器运行失败以及产生 MissingKeyword 的错误。这个情况出现的原因是，默认情况下，CA 探测器会对任何位置的帐户都进行探测，也因为探测器在使用重定向时不会尝试对不同站点测试 CAS。若要解决这个问题，应确保每个站点的服务器都包含在监视组中。给定监视组中的 CA 服务器仅与同一组的邮箱服务器一起测试。
    
    若要确认服务器的监视组，请运行以下命令：
    
        Get-ExchangeServer | ft MonitoringGroup
    
    若要修改服务器上的监视组，请结合使用 *MonitoringGroup* 参数和 **Set-ExchangeServer** cmdlet。例如，使用如下内容：
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  在 IIS 管理器中，单击“应用程序池”，然后在 Exchange 命令行管理程序 中运行以下命令，对“MSExchangeOWAAppPool”应用程序池进行再循环：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. 按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

11. 如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

12. 按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

13. 如果问题仍存在，重启服务器。

14. 重新启动服务器后，按照验证问题是否仍然存在部分步骤 2c 所示，重新运行相关联的探测器。

15. 如果探测器仍然运行失败，可能需要寻求协助，以解决此问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

