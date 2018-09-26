---
title: '配置 IMAP4 的日历选项: Exchange 2013 Help'
TOCTitle: 配置 IMAP4 的日历选项
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50556593
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 IMAP4 的日历选项

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-27_

外壳程序可用于为您的用户连接到其邮箱使用 IMAP4 连接配置日历的访问设置。您指定的设置确定 IMAP4 用户访问他们的日历和 exchange 日历信息的方式 （例如，发送或响应会议请求） 与其他用户。

有关与 IMAP4 相关的其他信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;IMAP4 设置\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序设置 IMAP4 的日历选项

此示例可让 IMAP4 用户使用 iCalendar 标准，这是用于交换日历信息的标准。

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

此示例将使 IMAP4 用户能够从内部服务器访问日历信息。

  ```powershell
    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
  ```

此示例将使 IMAP4 用户能够通过 Internet 访问外部服务器上的日历信息。

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

本示例启用 IMAP4 访问日历信息的用户通过直接Outlook Web App URL。如果您正在使用`Custom`，则必须指定 Outlook Web App URL 使用*OWAServerUrl*参数。

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

您所指定的 IMAP4 日历选项后，您必须重新启动 IMAP4 服务。有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功设置了日历选项，请执行以下操作：

在命令行管理程序中运行以下命令。

```powershell
Get-ImapSettings | format-list
```

验证日历设置是否正确。

## 详细信息

为 IMAP4 设置日历选项之后，您可能还需要：

[配置 POP3 和 IMAP4 邮件检索格式选项](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[为 IMAP4 设置连接超时限制](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

