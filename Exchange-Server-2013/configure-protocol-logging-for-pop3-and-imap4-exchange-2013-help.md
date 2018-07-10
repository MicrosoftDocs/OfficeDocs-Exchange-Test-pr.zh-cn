---
title: '配置 POP3 和 IMAP4 的协议日志记录: Exchange 2013 Help'
TOCTitle: 配置 POP3 和 IMAP4 的协议日志记录
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50556560
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 POP3 和 IMAP4 的协议日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-27_

您可以使用命令行管理程序为 POP3 和 IMAP4 启用、禁用或修改协议日志记录设置。 默认情况下不启用协议日志记录。

可以使用协议日志记录功能在 Exchange 环境中查看 POP3 和 IMAP4 连接。 如果要解决与 POP3 或 IMAP4 性能相关的问题，这可能很有用。 有关详细信息，请参阅[POP3 和 IMAP4 的协议日志记录](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)。 有关与 POP3 和 IMAP4 相关的更多信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”和“IMAP4 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行管理程序启用 POP3 或 IMAP4 的协议日志记录

此示例在客户端访问服务器 CAS01 上启用 IMAP4 或 POP3 的协议日志记录。

    Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true

> [!NOTE]
> 为 POP3 或 IMAP4 更改了协议日志记录设置之后，必须重新启动所使用的任何服务：POP3 或 IMAP4。有关如何重新启动 POP3 服务和 IMAP4 服务的信息，请参阅<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">启动和停止 POP3 服务</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">启动和停止 IMAP4 服务</a>。


有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\)) 和 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 使用命令行管理程序禁用 POP3 或 IMAP4 的协议日志记录

此示例在客户端访问服务器 CAS01 上禁用 IMAP4 或 POP3 的协议日志记录。

    Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
    Set-PopSettings -Server "CAS01" -protocolLogEnabled $false

> [!NOTE]
> 为 POP3 或 IMAP4 更改了协议日志记录设置之后，必须重新启动所使用的任何服务：POP3 或 IMAP4。有关如何重新启动 POP3 服务和 IMAP4 服务的信息，请参阅<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">启动和停止 POP3 服务</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">启动和停止 IMAP4 服务</a>。


有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\)) 和 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 使用命令行管理程序修改 POP3 或 IMAP4 的协议日志记录

若要修改 POP3 或 IMAP4 日志记录设置，请使用以下一个或多个参数运行 **Set-ImapSettings** 或 **Set-PopSettings** cmdlet。

  - *LogFileLocation*   此参数指定 POP3 或 IMAP4 协议日志文件的位置。默认情况下，POP3 协议日志文件位于 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3 目录下。 此示例在客户端访问服务器 CAS01 上打开 POP3 协议日志记录。 此外，还将 POP3 协议日志记录目录更改为 C:\\Pop3Logging。
    
        Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"

  - *LogFileRollOverSettings*   此参数定义 POP3 或 IMAP4 协议日志记录创建新日志文件的频率。 默认情况下，每天创建一个新的日志文件。 可能的值是：
    
    每小时
    
    每天
    
    每周
    
    每月
    
    此设置仅适用于将参数 *LogPerFileSizeQuota* 的值设置为零时。 此示例在客户端访问服务器 CAS01 上将 POP3 协议日志记录更改为每小时创建一个新的日志文件。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly

  - *LogPerFileSizeQuota*   此参数定义 POP3 或 IMAP4 协议日志文件的最大大小（字节）。 默认情况下，此值设置为零。 将此值设置为零时，将按 *LogFileRollOverSettings* 参数指定的频率创建新的协议日志文件。
    
    此示例在客户端访问服务器 CAS01 上将 POP3 协议日志记录更改为在日志文件达到 2 MB 时创建一个新的日志文件。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    
    此示例在客户端访问服务器 CAS01 上将 POP3 协议日志记录更改为使用相同日志文件，而不考虑其创建日期和大小。
    
        Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited

> [!NOTE]
> 为 POP3 或 IMAP4 更改了协议日志记录设置之后，必须重新启动所使用的任何服务：POP3 或 IMAP4。有关如何重新启动 POP3 服务和 IMAP4 服务的信息，请参阅<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">启动和停止 POP3 服务</a>和<a href="start-and-stop-the-imap4-services-exchange-2013-help.md">启动和停止 IMAP4 服务</a>。


有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\)) 和 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

在命令行管理程序中执行以下命令以验证 POP3 协议日志记录设置。 如果启用了 POP3 协议日志记录，则 *ProtocolLogEnabled* 参数的值为 `True`。 如果禁用了 POP3 协议日志记录，则其值为 `False`。 您也可以确保 *LogFileLocation*、*LogPerFileSizeQuota* 和 *LogFileRollOverSettings* 参数的值是正确的。

    Get-PopSettings | format-list

在命令行管理程序中执行以下命令以验证 IMAP4 协议日志记录设置。 如果启用了 IMAP4 协议日志记录，则 *ProtocolLogEnabled* 参数的值为 `True`。 如果禁用了 IMAP4 协议日志记录，则其值为 `False`。 您也可以确保 *LogFileLocation*、*LogPerFileSizeQuota* 和 *LogFileRollOverSettings* 参数的值是正确的。

    Get-ImapSettings | format-list

## 详细信息

配置 POP3 和 IMAP4 的协议日志记录设置之后，您可能还需要：

[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)

[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)

