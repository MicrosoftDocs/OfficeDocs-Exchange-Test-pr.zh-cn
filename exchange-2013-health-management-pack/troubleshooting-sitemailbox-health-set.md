---
title: 解决 SiteMailbox 运行状况设置的问题
TOCTitle: 解决 SiteMailbox 运行状况设置的问题
ms:assetid: ac00985c-c9a5-44bf-b152-4b99d8ae24ed
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.scom.sitemailbox(v=EXCHG.150)
ms:contentKeyID: 53275707
ms.date: 10/08/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 解决 SiteMailbox 运行状况设置的问题

 

_**适用于：** Exchange Server 2013, Project Server 2013_

_**上一次修改主题：** 2013-02-11_

SiteMailbox 运行状况设置监视组织中站点邮箱的整体运行状况以及辅助功能。

如果收到一条警报，指示 SiteMailbox 运行状况不正常，则说明用户邮箱的内容不处于同步状态。

## 说明

SiteMailbox 监视系统接收来自后台同步服务的被动同步结果。本系统不使用任何探测器。每次尝试同步之后，被动同步结果就被写入 SiteMailbox 监视系统中。下列事件发生时，也会触发同步：

  - 用户使用 Outlook 或 Outlook Web App 访问其站点邮箱

  - 运行“Update-SiteMailbox”命令

  - 打开 Outlook Web App 选项窗口，然后单击选定站点邮箱“同步状态”页面上的“开始同步”按钮

有关 Update-SiteMailbox cmdlet 的详细信息，请参阅：[Update-SiteMailbox](https://technet.microsoft.com/zh-cn/library/jj218690\(v=exchg.150\))

有关探测器和监视器的详细信息，请参阅[服务器运行状况和性能](https://technet.microsoft.com/zh-cn/library/jj150551\(v=exchg.150\))。

## 常见问题

发生站点范围传播的同步问题时，同步监视服务通常会触发警报。单个站点邮箱同步失败时，不会发送警报。要确定单个站点邮箱引发上限阈值警报的原因，建议您查看站点邮箱同步日志文件。

## 用户操作

发出警报后服务可能会恢复。因此，当您接收到指示运行状况设置不正常的警报时，首先要验证该问题是否仍然存在。若问题确实存在，执行以下部分介绍的相应恢复操作。

## 验证问题是否仍然存在

1.  识别警报中的运行状况设置名称和服务器名称。

2.  邮件详细信息提供了有关确切警报原因的信息。大部分情况下，邮件详细信息会提供充足的故障排除信息，用于识别根本原因。如果邮件详细信息不明确，请执行以下操作：
    
    1.  打开 Exchange 命令行管理程序，然后运行以下命令，以检索发出警报的运行状况设置的详细信息：
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        例如，若要检索 server1.contoso.com 上 SiteMailbox 运行状况设置的详细信息，运行以下命令：
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "SiteMailbox"}
    
    2.  检查命令输出，以确定报告了错误的监视器。发出警报的监视器的 **AlertValue** 值将为 `Unhealthy`。

## 故障排除步骤

从运行状况设置收到一条警报时，电子邮件包含以下信息：

  - 发送警报的服务器名称

  - 警报发出的时间和日期

  - 所用的身份验证机制，以及凭据信息

  - 上一个错误的全部异常跟踪，包括诊断数据和特定 HTTP 头信息  
    
    **注意**   可使用全部异常跟踪中的信息来帮助解决问题。探测器生成的异常中包含“失败原因”，它说明了探测失败的原因。

**后台同步错误**

后台同步过程失败时，您可能会收到类似以下内容的警报：

站点邮箱后台同步的失败率至少为 25%：87 次尝试中有 41 次失败。示例同步结果：

\[消息：远程服务器返回一个错误：(401) 未经授权。\]\[类型：System.Net.WebException\]

在前四个小时中不断有高百分比的同步失败发生时，就会触发该警报。为避免出现误报，仅当在前四个小时的连续 15 分钟内满足以下条件时，才会发送警报：

  - 在 15 分钟期限内至少发生 20 个失败。

  - 在 15 分钟期限内失败同步占总同步尝试的百分比超过 25%。

Exchange 中的每个站点邮箱都链接到 SharePoint 站点。对于托管邮箱角色的给定 Exchange 服务器上的每个站点邮箱，服务器都会同步来自 SharePoint 且与站点邮箱相关的信息。

此过程中会发生两种类型的同步：成员同步和文档同步。这些同步过程的元数据来自不同的 Web 服务。此外，给定 Exchange 服务器可能包含链接到多个 SharePoint 服务器或服务器场的站点邮箱。因此，警报可能来自多个邮箱服务器，具体取决于以下情况：

1.  组织中主动使用的站点邮箱如何分布

2.  主动使用的站点邮箱所链接的 SharePoint 服务器

3.  邮箱服务器是否有充足的同步容量来满足警报阈值

为了帮助解决此问题，警报中的示例同步结果可帮助确定失败原因。*\<exExchangeSvrNoVersion installation directory\>*Logging\\TeamMailbox 文件夹中记录了有关每个同步尝试成功和失败的详细信息。通过搜索“**失败**”这个词，可以查看有关失败的最新 Microsoft.Exchange.ServiceHost\_TeamMailboxSyncLog\* 文件。您还可以使用 **Test-OAuthConnectivity**、**Test-SiteMailbox** 和 **Get-SiteMailboxDiagnostics** cmdlet 进一步解决问题。

**MSExchangeServiceHost 服务未在运行**

如果 MSExchangeServiceHost 服务未在运行，您会收到类似以下内容的警报：

尝试恢复之后，“MSExchangeServiceHost”服务未在运行。该服务可能被禁用或处于崩溃循环状态。

若要解决此问题，请验证 MSExchangeServiceHost 服务是否正在发送警报的服务器上运行。如果服务正在运行，请查看 Windows 事件日志，了解服务之前未运行的原因，如手动服务控制或服务重复性崩溃。

**MSExchangeServiceHost 服务已崩溃**

如果 MSExchangeServiceHost 服务已崩溃，您会收到类似以下内容的警报：

MSExchangeServiceHost 进程在最近 60 分钟内至少发生 3 次崩溃。  
Watson 消息：

\<*消息*\>

若要解决此问题，请查看发送与 MSExchangeServiceHost 服务相关的“**4999**”事件的警报的服务器上的 Windows 应用程序事件日志。详细信息文本会提供有关问题发生原因的信息。

## 详细信息

[Exchange 2013 中的新增功能](https://technet.microsoft.com/zh-cn/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\))

