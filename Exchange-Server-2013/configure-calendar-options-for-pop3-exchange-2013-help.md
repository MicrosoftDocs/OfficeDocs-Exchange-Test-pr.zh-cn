---
title: '配置 POP3 的日历选项: Exchange 2013 Help'
TOCTitle: 配置 POP3 的日历选项
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50556637
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 POP3 的日历选项

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-27_

可以使用命令行管理程序为使用 POP3 连接与其邮箱连接的用户配置日历访问设置。 指定的设置将确定 POP3 用户访问其日历以及与其他用户交换日历信息（例如，发送或响应会议请求）的方式。

有关与 POP3 相关的其他信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序设置 POP3 的日历选项

此示例使 POP3 用户能够使用 iCalendar 标准（一种日历信息交换标准）。

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar

此示例使 POP3 用户能够从内部服务器访问日历信息。

    Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

此示例使 POP3 用户能够从 Internet 访问外部服务器上的日历信息。

    Set-PopSettings -CalendarItemRetrievalOption InternetUrl

此示例使 POP3 用户能够使用直接的 Outlook Web App URL 访问日历信息。 如果要使用 `Custom`，必须使用 *OWAServerUrl* 参数指定一个 Outlook Web App URL。

    Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"

为 POP3 指定了日历选项之后，必须重新启动 POP3 服务。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功设置了日历选项，请执行以下操作：

在命令行管理程序中运行以下命令。

    Get-PopSettings | format-list

验证日历设置是否正确。

## 详细信息

在设置 POP3 的日历选项后，您可能还希望：

[配置 POP3 和 IMAP4 邮件检索格式选项](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[设置 POP3 的连接超时限制](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

