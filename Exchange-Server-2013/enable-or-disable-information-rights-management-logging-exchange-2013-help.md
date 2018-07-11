---
title: '启用或禁用信息权限管理日志记录: Exchange 2013 Help'
TOCTitle: 启用或禁用信息权限管理日志记录
ms:assetid: 6933bc65-4d98-4878-9167-0e9eaac68b6b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff686962(v=EXCHG.150)
ms:contentKeyID: 50490753
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用信息权限管理日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-12_

在Exchange Server 2013，您可以使用信息权限管理 (IRM) 日志监视并排除 IRM 操作。默认情况下启用 IRM 记录。

IRM 日志使用以下通用参数集：

  - *IrmLogEnabled*  启用或禁用 IRM 日志记录。默认值 ︰ `$true`。

  - *IrmLogMaxAge*  指定 IRM 日志文件的最长期限。删除早于指定存在时间的文件。默认值 ︰ 30 天。

  - *IrmLogMaxDirectorySize*  指定目录包含 IRM 日志最大的大小。当一个目录达到最大文件大小时，服务器将首先删除最旧的日志文件。默认值 ︰ 250 MB。

  - *IrmLogMaxFileSize*  指定每个 IRM 日志文件的最大大小。当日志文件达到指定的大小时，将创建新的日志文件。默认值 ︰ 10 MB。

  - *IrmLogPath*  指定 IRM 日志目录的位置。默认值 ︰ `%ExchangeInstallPath%Logging\IRMLogs`。

关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个过程的时间 ︰ 2-5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;配置 IRM 日志记录\&quot;条目。

  - 不能使用 Exchange 管理中心 (EAC) 来启用或禁用 IRM 服务器上的记录。您必须使用外壳程序

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序启用服务器上的 IRM 日志记录

本示例启用邮箱服务器上的 IRM 日志。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $true

有关语法和参数的详细信息，请参阅 [Set-TransportService](https://technet.microsoft.com/zh-cn/library/jj215682\(v=exchg.150\))。

## 使用命令行管理程序禁用服务器上的 IRM 日志记录

本示例禁用邮箱服务器上的 IRM 日志记录。

    Set-TransportService -Identity EXCH01 -IRMLogEnabled $false

有关语法和参数的详细信息，请参阅 [Set-TransportService](https://technet.microsoft.com/zh-cn/library/jj215682\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否在服务器上成功启用或禁用了 IRM 日志记录，请运行 [Get-TransportService](https://technet.microsoft.com/zh-cn/library/jj215746\(v=exchg.150\)) cmdlet 以检索 IRM 设置。

本示例检索服务器 EXCH01 上的所有 IRM 日志记录属性。

    Get-TransportService -Identity EXCH01 | Format-List IRMLog*

