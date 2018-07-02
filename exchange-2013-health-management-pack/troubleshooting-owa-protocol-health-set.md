---
title: 解决 OWA.Protocol 运行状况设置的问题
TOCTitle: 解决 OWA.Protocol 运行状况设置的问题
ms:assetid: fe172da8-65d3-43e0-ba62-d36a1b05fc11
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.owa.protocol(v=EXCHG.150)
ms:contentKeyID: 53275718
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 OWA.Protocol 运行状况设置的问题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

OWA.Protocol 运行状况设置监视邮箱服务器上的 Outlook Web App 协议。

如果收到一条警报，指示 OWA.Protocol 运行状况不正常，这说明出现了可能会阻止用户使用 Outlook Web App 访问邮箱的问题。

## 说明

OWA 服务通过以下探测器和监视器进行监视。


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
<td><p>OwaSelfTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>无</p></td>
<td><p>OwaSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>OwaDeepTestProbe</p></td>
<td><p>OWA.Protocol</p></td>
<td><p>Active Directory</p>
<p>信息存储</p></td>
<td><p>OwaDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


“OwaSelfTestProbe”探测器发送单个 HTTP 请求到以下地址：https://localhost:444/owa/exhealth.check。探测器通过返回状态代码“200 OK”，确认应用程序池可以做出响应。该探测器对任何其他 Exchange 组件都没有依存关系。

通过使用当前服务器上的副本，对每个邮箱数据库运行探测器“OwaDeepTestProbe”。探测器确定可以对该服务器进行完整的登录。为此，探测器对该特定服务器模拟客户端访问服务器 (CAS) 生成的通信类型。探测器依靠 Active Directory 域服务 (AD DS) 进行身份验证，依靠邮箱存储进行邮箱访问。有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

探测器运行失败的常见原因可能包括：

  - 受监视 CAS 上托管的 OWA 应用程序池无响应，或者邮箱服务器上托管的应用程序池无响应。

  - CA 或邮箱服务器遇到网络问题，无法连接到其他服务器或域控制器。

  - 监视帐户的凭据不正确。

  - 用户的数据库未安装，或该邮箱不能访问信息存储。

  - 信息存储没有响应。

  - 域控制器没有响应。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要检索 server1.contoso.com 上 OWA.Protocol 状况设置的详细信息，运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA.Protocol"}
    
    2.  检查命令输出，以确定报告错误的监视器。发出警报的监视器的“AlertValue”将为 `Unhealthy`。
    
    3.  重新运行不正常监视器的关联探测器。请参阅说明部分中的表格，找到关联探测器。为此，请运行下列命令：
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        例如，假定故障监视器为“OwaSelfTestMonitor”。与该监视器关联的探测器是“OwaSelfTestProbe”。要在 server1.contoso.com 上运行该探测器，请运行以下命令：
        
            Invoke-MonitoringProbe OWA.Protocol\OwaSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  在命令输出中，检查探测器的“结果”值。如果值为“成功”，则该问题是暂时性错误，且不再存在。否则，请参阅以下部分列出的恢复步骤。

收到来自运行状况设置的警报时，电子邮件将包含以下信息：

  - 发送警报的服务器名称

  - 故障探测器的类型（SelfTest 或 DeepTest）

  - 警报出现的时间和日期

  - 可以查找探测器完整 HTTP 请求跟踪的文件夹路径
    
      
    默认情况下，跟踪文件位于以下文件夹中：
    
      - SelfTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\ProtocolProbe
    
      - DeepTestProbe: \<*ExchangeServer*\>\\Logging\\Monitoring\\OWA\\MailboxProbe

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息  
    
    **注意**   您可以使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常包含故障原因，描述了探测器运行失败的原因。失败原因可能是以下任一原因：
    
      - **MissingKeyword**   服务器响应中找不到预期关键字。在这种情况下，异常包含预期关键字。
    
      - **NameResolution**   DNS 解析无法解析给定的服务器名称。
    
      - **NetworkConnection**   探测器在尝试连接到 CAFE 上的 OWA 应用程序池时，收到网络连接故障。
    
      - **UnexpectedHttpResponseCode**   响应包含了一个意外 HTTP 代码。例如，服务器返回 HTTP 代码“503”。
    
      - **RequestTimeout**   服务器响应客户端请求的时间太长。
    
      - **UnexpectedHttpResponseCode**   响应返回了一个意外 HTTP 代码。例如，服务器返回 HTTP 代码“503”。
    
      - **ScenarioTimeout**   探测器成功完成，但花费的时间超过一分钟。这通常说明系统过载。
    
      - **OwaErrorPage**   OWA 返回了一个错误页面。导致失败的错误的名称通常在异常消息中提供。
    
      - **OwaMailboxErrorPage**   OWA 返回一个错误页面，包含与邮箱存储相关的错误。这通常表示邮箱存储正在关闭或邮箱正在卸除等问题。
    
    此异常跟踪包含一个名为 **FailingComponent** 的重要字段，其中，探测器努力尝试确定失败并对失败进行分类。例如，探测器可能会返回以下任一值：
    
      - **Mailbox**   探测器可以访问 OWA，但无法连接到邮箱存储。在这种情况下，探测器运行失败，或者邮箱访问延迟导致探测器运行失败，并生成 **ScenarioTimeout** 错误。如果出现这些失败类型，应检查邮箱服务器的运行状况。
    
      - **Active Directory**   探测器可以访问 OWA，但无法连接到 AD DS。在这种情况下，探测器运行失败，或者 AD DS 调用延迟可能导致探测器超时。如果出现这些失败类型，应检查域控制器的运行状况，并检查 CA、邮箱服务器以及域控制器之间的网络连接。
    
      - **OWA**   通常意味着 OWA 层内部出现错误。如果出现这些失败类型，必须在 CA 和邮箱服务器上验证 OWA 进程的运行状况，并检查网络连接。
    
    该异常也包含探测器运行失败之前收到的最新 HTTP 请求和响应信息。  
      
    升级正文包含探测器日志的路径，可用于验证探测器运行失败时发送的完整 HTTP Web 请求和响应。此文件仅包含运行失败的探测器的数据，因为只会对失败的尝试进行记录。可以使用此信息全面了解测试失败的原因。

## OwaSelfTestProbe 的恢复操作

由于此探测器几乎不存在依存关系，所以故障通常会在 OWA 应用程序池进程无响应时发生。

要解决此问题，请执行下列步骤：

1.  单击警报电子邮件正文中的探测器跟踪日志 URL，验证是否正发生新的失败情况。

2.  在装入了邮箱的同一服务器上创建测试用户帐户。尝试登录，确定问题是否可以重现。

3.  检查 OWA 运行状况设置上的警报，可能指出影响特定邮箱服务器的问题。有关详细信息，请参阅[OWA 运行状况设置疑难解答](troubleshooting-owa-health-set.md)。

4.  启动 IIS 管理器，然后连接到报告问题的服务器，以确定“MSExchangeOwaAppPool”应用程序池是否在 CAS 上运行。

5.  在 IIS 管理器中，验证默认网站是否正在运行。

6.  在 IIS 管理器中，单击“应用程序池”，然后在 Exchange 命令行管理程序 中运行以下命令，对“MSExchangeOWAAppPool”应用程序池进行再循环：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

7.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

8.  如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

9.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

10. 如果问题仍然存在，重新启动服务器。

11. 服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

12. 如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## OwaDeepTestProbe 的恢复操作

1.  若要确定问题是否仍然存在，可以在装入了邮箱的同一服务器上创建测试用户帐户，然后尝试登录到 OWA。例如，尝试使用以下帐户登录：https:// *\<servername\>*/owa。

2.  检查 OWA 运行状况设置上的警报，可能指出影响特定邮箱服务器的问题。有关详细信息，请参阅[OWA 运行状况设置疑难解答](troubleshooting-owa-health-set.md)。

3.  启动 IIS 管理器，然后连接到报告问题的服务器，以确定“MSExchangeOwaAppPool”应用程序池是否在 CAS 上运行。

4.  在 IIS 管理器中，验证默认网站是否正在运行。

5.  找到失败探测器的邮箱数据库，并验证邮箱数据库在邮箱服务器上是否处于活动状态，以及邮箱存储是否运行正常。若要找到失败的数据库 GUID 信息，打开全部异常跟踪信息。每个故障应包含一个类似以下内容的条目：
    
    `Starting Owa probe with Target: https://localhost/owa/, Username:  HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com`

6.  复制 HealthMailbox GUID，然后在命令行管理程序中运行以下命令：
    
        Get-Mailbox -Monitoring -Identity <username>
    
    例如，运行以下命令：
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    在返回的对象中，可以找到用户的数据库名称，也可以确定当前活动数据库驻留的位置。

7.  在 IIS 管理器中，单击“应用程序池”，然后在命令行管理程序中运行以下命令，对“MSExchangeOWAAppPool”应用程序池进行再循环：
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

8.  按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

9.  如果问题仍然存在，使用 IISReset 实用程序或运行以下命令，对 IIS 服务进行再循环：
    
        Iisreset /noforce

10. 按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

11. 如果问题仍然存在，重新启动服务器。

12. 服务器重新启动后，按照验证问题是否仍然存在部分的步骤 2c 所示，重新运行关联探测器。

13. 如果探测器仍然无法运行，可能需要寻求帮助来解决这个问题。若要解决此问题，请与 Microsoft 支持专家联系。若要与 Microsoft 支持专家联系，请访问 [Exchange Server 解决方案中心](http://go.microsoft.com/fwlink/p/?linkid=180809)。在导航窗格中，单击“支持选项和资源”，然后使用“获取技术支持”下列出的一个选项与 Microsoft 支持专家联系。由于您的组织可能已有直接与 Microsoft 产品支持服务联系的特定流程，因此，请务必先查看您组织的准则。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

