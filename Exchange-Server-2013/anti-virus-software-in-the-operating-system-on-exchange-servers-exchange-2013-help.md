---
title: '在 Exchange 服务器上的操作系统中的防病毒软件: Exchange 2013 Help'
TOCTitle: 在 Exchange 服务器上的操作系统中的防病毒软件
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50491065
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 服务器上的操作系统中的防病毒软件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-07-22_

本主题介绍文件级防病毒程序对运行 Microsoft Exchange Server 2013 的计算机的影响。如果按照本主题中所述的建议操作，可以帮助提高 Exchange 组织的安全性并改善运行状况。

文件级扫描程序经常使用。但是，如果配置不正确，可能会导致 Exchange 2013 出现问题。文件级扫描程序包括下列两种类型：

  - *驻留在内存中的文件级扫描* 是指文件级防病毒软件中始终加载在内存中的部分。该部分检查硬盘上以及计算机内存中使用的所有文件。

  - *按需运行的文件级扫描*是指文件级防病毒软件中可以配置为手动或按计划扫描硬盘上的文件的部分。某些版本的防病毒软件会在病毒定义更新后自动开始按需运行的扫描，以确保使用最新的定义扫描所有文件。

在 Exchange 2013 中使用文件级扫描程序时可能会出现下列问题：

  - 文件级扫描程序可能会在文件正在使用时扫描文件，也可能按计划的间隔扫描文件。这样可能会造成 Exchange 2013 尝试使用文件时，扫描程序锁定或隔离了相应的 Exchange 日志文件或数据库文件。此行为可能会导致 Exchange 2013 的严重故障，还可能会导致 -1018 事件日志错误。

  - 文件级扫描程序无法抵御电子邮件病毒（例如 Storm Worm）的攻击。Storm Worm 是通过电子邮件传播的后门特洛伊木马程序。这种蠕虫将受感染的计算机连接到僵尸网络，在这种网络中，计算机用于周期性、突发性地发送垃圾邮件。

## 在 Exchange 2013 中使用文件级扫描的建议

如果要在 Exchange 2013 服务器上部署文件级扫描程序，请确保为按内存驻留扫描和文件级扫描设置适当的排除规则（例如目录排除、进程排除和文件扩展名排除）。本节介绍建议的目录排除、进程排除和文件扩展名排除。

**目录**

目录排除

进程排除

文件扩展名排除

## 目录排除

必须为运行文件级防病毒扫描程序的每个 Exchange 服务器排除特定的目录。本节介绍应从文件级扫描中排除的目录。

  - **邮箱服务器**
    
      - **邮箱数据库**
        
          - Exchange 数据库、检查点文件和日志文件。默认情况下，这些文件位于 %ExchangeInstallPath%Mailbox 文件夹的子文件夹中。若要确定邮箱数据库、事务日志文件和检查点文件的位置，请运行以下命令：`Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - 数据库内容索引。默认情况下，这些文件与数据库文件位于同一文件夹中。
        
          - 组指标文件。默认情况下，这些文件位于 %ExchangeInstallPath%GroupMetrics 文件夹中。
        
          - 常用的日志文件，例如邮件跟踪日志文件和日历修复日志文件。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Logs 文件夹和 %ExchangeInstallPath%Logging 文件夹的子文件夹中。若要确定所使用的日志路径，请在 Exchange 命令行管理程序中运行以下命令： `Get-MailboxServer <servername> | Format-List *path*`
        
          - 脱机通讯簿文件。默认情况下，这些文件位于 %ExchangeInstallPath%ClientAccess\\OAB 文件夹下的子文件夹中。
        
          - %SystemRoot%\\System32\\Inetsrv 文件夹中的 IIS 系统文件。
        
          - 邮箱数据库临时文件夹：%ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **数据库可用性组的成员**
        
          - “邮箱数据库”列表中列出的所有项目以及 %Windir%\\Cluster 中存在的群集仲裁数据库。
        
          - 见证目录文件。这些文件位于环境中的其他服务器上，通常是未与邮箱服务器安装在同一台计算机上的客户端访问服务器。默认情况下，见证目录文件位于 %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\> 中。
    
      - **传输服务**
        
          - 日志文件，例如邮件跟踪和连接日志。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Logs 文件夹的子文件夹中。若要确定所使用的日志路径，请在 Exchange 命令行管理程序中运行以下命令： `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - 分拣和重播消息目录文件夹。默认情况下，这些文件夹位于 %ExchangeInstallPath%TransportRoles 文件夹中。若要确定所使用的日志路径，请在 Exchange 命令行管理程序中运行以下命令：`Get-TransportService <servername>| Format-List *dir*path*`
        
          - 队列数据库、检查点和日志文件。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Data\\Queue 文件夹中。
        
          - 发件人信誉数据库、检查点和日志文件。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation 文件夹中。
        
          - 用于执行转换的临时文件夹：
            
              - 默认情况下，在 Exchange 服务器的 %TMP% 文件夹中执行内容转换。
            
              - 默认情况下，在 %ExchangeInstallPath%\\Working\\OleConverter 文件夹中执行富文本格式 (RTF) 到 MIME/HTML 的转换。
        
          - 内容扫描组件由恶意软件代理和数据丢失预防 (DLP) 使用。默认情况下，这些文件位于 %ExchangeInstallPath%FIP-FS 文件夹中。
    
      - **邮箱传输服务**
        
          - 日志文件，例如连接日志。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox 文件夹的子文件夹中。若要确定所使用的日志路径，请在 Exchange 命令行管理程序中运行以下命令： `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **统一消息**
        
          - 不同区域的语法文件，例如 en-EN 或 es-ES。默认情况下，这些文件存储在 %ExchangeInstallPath%UnifiedMessaging\\grammars 文件夹的子文件夹中。
        
          - 语音提示、问候语和信息性消息文件。默认情况下，这些文件存储在 %ExchangeInstallPath%UnifiedMessaging\\Prompts 文件夹的子文件夹中
        
          - 暂时存储在 %ExchangeInstallPath%UnifiedMessaging\\voicemail 文件夹中的语音邮件文件。
        
          - 统一消息生成的临时文件。默认情况下，这些文件存储在 %ExchangeInstallPath%UnifiedMessaging\\temp 文件夹中。
    
      - **安装程序**
        
          - Exchange Server 安装程序的临时文件。这些文件通常位于 %SystemRoot%\\Temp\\ExchangeSetup。
    
      - **Exchange Search 服务**
        
          - 由 Exchange Search 服务和 Microsoft Filter Pack 在沙盒环境中执行文件转换时使用的临时文件。这些文件位于 %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\。

<!-- end list -->

  - **客户端访问服务器**
    
      - **Web 组件**
        
          - 对于使用 Internet 信息服务 (IIS) 7.0 的服务器，用于 Microsoft Outlook Web App 的压缩文件夹。默认情况下，IIS 7.0 的压缩文件夹的路径是 %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files。
        
          - %SystemRoot%\\System32\\Inetsrv 文件夹中的 IIS 系统文件
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET 文件中的子文件夹
    
      - **POP3 和 IMAP4 协议日志记录**
        
          - POP3 文件夹：%ExchangeInstallPath%Logging\\POP3
        
          - IMAP4 文件夹：%ExchangeInstallPath%Logging\\IMAP4
    
      - **前端传输服务**
        
          - 日志文件，例如连接日志和协议日志。默认情况下，这些文件位于 %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd 文件夹的子文件夹中。若要确定所使用的日志路径，请在 Exchange 命令行管理程序中运行以下命令： `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **安装程序**
        
          - Exchange Server 安装程序临时文件。这些文件通常位于 %SystemRoot%\\Temp\\ExchangeSetup 中。

在 Exchange 2013 中使用文件级扫描的建议

## 进程排除

现在，许多文件级扫描程序都支持进程扫描，如果扫描错误进程，可能对 Microsoft Exchange 带来负面影响。因此，应从文件级扫描程序中排除下列进程。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>进程</th>
<th>路径</th>
<th>注释</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>订阅的边缘传输服务器上的 Active Directory 轻型目录服务 (AD LDS)。</p></td>
<td><p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 传输服务工作进程</p></td>
<td><p>邮箱服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>恶意软件代理和 DLP 使用的内容扫描组件。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Microsoft Exchange 搜索主机控制器服务 (HostControllerService)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet 信息服务 (IIS)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 反垃圾邮件更新服务 (MSExchangeAntispamUpdate)</p></td>
<td><p>邮箱服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>内容筛选器代理</p></td>
<td><p>邮箱服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 诊断服务 (MSExchangeDiagnostics)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Active Directory 拓扑服务 (MSExchangeADTopology)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 凭据服务 (MSExchangeEdgeCredential)</p></td>
<td><p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange EdgeSync 服务 (MSExchangeEdgeSync)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 服务 (MSExchangeImap4)</p></td>
<td><p>客户端访问服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 后端服务 (MSExchangeIMAP4BE)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange POP3 服务 (MSExchangePop3)</p></td>
<td><p>客户端访问服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange POP3 后端服务 (MSExchangePOP3BE)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service 主机服务 (MSExchangeServiceHost)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange RPC 客户端访问服务 (MSExchangeRPC)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 搜索服务 (MSExchangeFastSearch)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Service 主机服务 (MSExchangeServiceHost)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Information Store 服务 (MSExchangeIS)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 信息存储服务工作进程</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange 统一消息呼叫路由器服务 (MSExchangeUMCR)</p></td>
<td><p>客户端访问服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange DAG 管理服务 (MSExchangeDagMgmt)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 邮箱传输交付服务 (MSExchangeDelivery)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 前端传输服务 (MSExchangeFrontEndTransport)</p></td>
<td><p>客户端访问服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 运行状况管理器服务 (MSExchangeHM)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 运行状况管理器服务工作进程</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 邮箱助理服务 (MSExchangeMailboxAssistants)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 邮箱复制服务 (MSExchangeMailboxReplication)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 迁移工作流服务 (MSExchangeMigrationWorkflow)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 复制服务 (MSExchangeRepl)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 邮箱传输提交服务 (MSExchangeSubmission)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 传输服务 (MSExchangeTransport)</p></td>
<td><p>邮箱服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 传输日志搜索服务 (MSExchangeTransportLogSearch)</p></td>
<td><p>邮箱服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 限制服务 (MSExchangeThrottling)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Microsoft Exchange 搜索服务 (MSExchangeFastSearch)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>将富文本格式 (RTF) 邮件转换为 MIME/HTML 以供外部收件人查看。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Microsoft Exchange 搜索服务 (MSExchangeFastSearch)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange Management Shell</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p>
<p>边缘传输服务器</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>恶意软件代理和 DLP 使用的内容扫描组件。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>恶意软件代理和 DLP 使用的内容扫描组件。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Outlook Web App 中的 WebReady 文档查看。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 统一消息服务 (MSExchangeUM)</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 统一消息服务工作进程</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>恶意软件代理和 DLP 使用的内容扫描组件。</p></td>
<td><p>邮箱服务器</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Internet 信息服务 (IIS)</p></td>
<td><p>邮箱服务器</p>
<p>客户端访问服务器</p></td>
</tr>
</tbody>
</table>


在 Exchange 2013 中使用文件级扫描的建议

## 文件扩展名排除

除了排除特定的目录和进程之外，如果目录排除失败或已从默认位置移动文件，则应排除下列特定于 Exchange 的文件扩展名。

  - 与应用程序有关的扩展名：
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - 与数据库有关的扩展名：
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - 与脱机通讯簿有关的扩展名：
    
      - .lzx

<!-- end list -->

  - 与内容索引有关的扩展名：
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - 与统一消息有关的扩展名：
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - 与组指标有关的扩展名：
    
      - .dsc
    
      - .txt

在 Exchange 2013 中使用文件级扫描的建议

