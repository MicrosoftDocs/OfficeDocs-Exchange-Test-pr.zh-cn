---
title: 'Exchange Server 2013 中的 POP3 和 IMAP4: Exchange 2013 Help'
TOCTitle: POP3 和 IMAP4
ms:assetid: a7dc91ee-2919-4db3-ae9c-cd665d2e09ea
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657728(v=EXCHG.150)
ms:contentKeyID: 50491347
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 中的 POP3 和 IMAP4

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-08-16_

了解 Exchange Server 2013 中 POP3 和 IMAP4 协议之间的区别，以及如何配置从各个电子邮件程序访问 Exchange 2013 邮箱的选项。

默认情况下，Exchange Server 2013 中禁用 POP3 和 IMAP4。为了支持仍依赖于这些协议的 POP3 客户端，需要启动两种 POP3 服务：Microsoft Exchange POP3 服务和 Microsoft Exchange POP3 后端服务。为了支持仍依赖于这些协议的 IMAP4 客户端，需要启动两种 IMAP4 服务：Microsoft Exchange IMAP4 服务和 Microsoft Exchange IMAP4 后端服务。

有关启用 POP3 和 IMAP4 服务的详细步骤，请参阅[在 Exchange 2013 中启用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)和[在 Exchange 2016 中启用 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)。

默认情况下，在运行 Exchange 2013 的计算机上拥有邮箱的用户可以使用 Outlook、Outlook Web App、Exchange ActiveSync 或 Outlook Voice Access 访问他们的邮箱。通过 Outlook、Outlook Web App 和 Outlook Voice Access 功能，电子邮件用户可以使用为用户提供的全面功能集，这些用户在 Exchange 2016 服务器上拥有邮箱。

**目录**

POP3 和 IMAP4 功能概述

POP3 和 IMAP4 跨站点连接

通过 POP3 和 IMAP4 使用非标准帐户

了解 POP3 和 IMAP4 的区别

发送和接收 POP3 和 IMAP4 电子邮件应用程序的选项

POP3 和 IMAP4 应用程序

用于配置 POP3 或 IMAP4 对用户 Exchange 2013 邮箱访问权限的用户设置

## POP3 和 IMAP4 功能概述

本节介绍 Exchange 2013 的 POP3 和 IMAP4 功能。

POP3 和 IMAP4 协议具有下列优点和局限性：

  - **POP3**   POP3 用于支持脱机邮件处理。使用 POP3 时，如果未将客户端设置为在服务器上保留邮件，电子邮件将从服务器中删除并存储在本地 POP3 客户端上。这会使数据管理和安全责任都转由用户负责。POP3 不提供高级协作功能，例如日历、联系人和任务。

  - **IMAP4**   IMAP4 可提供脱机和联机访问功能，但与 POP3 一样，IMAP4 不提供高级协作功能，例如日历、联系人和任务。

POP3 和 IMAP4 电子邮件应用程序不使用 POP3 和 IMAP4 向电子邮件服务器发送邮件；它们依赖 SMTP 协议来发送邮件。安装 Exchange 时会自动创建用于从使用 POP3 或 IMAP4 的客户端应用程序接收电子邮件提交的连接器。有关连接器的详细信息，请参阅[接收连接器](receive-connectors-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每次用户使用基于 POP 或 IMAP 的电子邮件程序打开 Office 365 电子邮件时，都可能遇到几秒钟的延迟。延迟是由代理服务器所致，因为这会给身份验证带来额外的跃点。代理服务器首先查找分配的 pod 服务器（客户端访问服务器），然后再对此服务器进行身份验证。</td>
</tr>
</tbody>
</table>


## POP3 和 IMAP4 跨站点连接

在 Exchange 的早期版本中，当 POP3 和 IMAP4 客户端的邮箱位于组织中的其他站点时，必须执行手动配置步骤才能允许这些客户端从组织中的某个站点连接到其邮件。默认情况下，Exchange 2013 自动从一个站点中的客户端访问服务器代理到正确的服务器。

## 通过 POP3 和 IMAP4 使用非标准帐户

无法使用匿名帐户或来宾帐户通过 POP3 或 IMAP4 登录到 Exchange 2016 邮箱。匿名帐户将被阻止，是因为使用非标准帐户进行 POP3 和 IMAP4 访问时存在安全漏洞。另外，无法通过 POP3 或 IMAP4 连接到管理员邮箱。此限制是有意识地包括在 Exchange 2013 中的，目的是增强管理员邮箱的安全。若要访问管理员邮箱，必须使用 Outlook 或 Outlook Web App。

## 了解 POP3 和 IMAP4 的区别

**POP3** POP3 是一个常用的电子邮件 Internet 协议。默认情况下，当 POP3 电子邮件应用程序将电子邮件下载到客户端计算机后，下载的邮件将从服务器上删除。如果未在电子邮件服务器上保留用户电子邮件的副本，则用户无法从多台计算机上访问相同的电子邮件。但是可以将某些 POP3 电子邮件应用程序配置为在服务器上保留邮件副本，以便可以从另一台计算机访问相同的电子邮件。POP3 客户端应用程序只能用于将邮件从电子邮件服务器下载到客户端计算机上的某个文件夹（通常为收件箱）。POP3 协议无法将电子邮件服务器上的多个文件夹与客户端计算机上的多个文件夹同步。

**IMAP4** 与使用 POP3 的电子邮件客户端应用程序相比，使用 IMAP4 的电子邮件客户端应用程序更为灵活，通常提供的功能更多。默认情况下，当 IMAP4 电子邮件应用程序将电子邮件下载到客户端计算机，下载邮件的副本会保留在电子邮件服务器上。正是由于用户的电子邮件副本保留在电子邮件服务器上，用户可以从多台计算机上访问相同的电子邮件。使用 IMAP4 电子邮件，用户可以访问并创建电子邮件服务器上的多个电子邮件文件夹。然后用户可以从位于多个位置的计算机上访问服务器上的任何邮件。例如，大多数 IMAP4 应用程序可以配置为在服务器上保留用户已发送项目的副本，以便他们可以从任何其他计算机上查看他们的已发送项目。IMAP4 支持大多数 IMAP4 应用程序支持的其他功能。例如，某些 IMAP4 应用程序包含的一项功能可让用户仅查看服务器上电子邮件的邮件头（发件人和主题），然后仅下载要阅读的邮件。IMAP4 也不支持公用文件夹访问。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>IMAP4 和 POP3 客户端对 Exchange 日历信息的访问也受到限制。有关详细信息，请参阅 <a href="configure-calendar-options-for-pop3-exchange-2013-help.md">配置 POP3 的日历选项</a> 和 <a href="configure-calendar-options-for-imap4-exchange-2013-help.md">配置 IMAP4 的日历选项</a>。</td>
</tr>
</tbody>
</table>


## 发送和接收 POP3 和 IMAP4 电子邮件应用程序的选项

通过 POP3 和 IMAP4 电子邮件应用程序，用户可以选择需要连接到服务器发送和接收电子邮件的时间。此部分介绍了一些最常见的连接选项，并提供了一些用户在选择其 POP3 和 IMAP4 电子邮件应用程序中可用的连接选项时需考虑的因素。

## 常见配置设置

可以在 POP3 或 IMAP4 客户端应用程序上设置的常见连接设置有以下三个：

  - 每次启动电子邮件应用程序时发送和接收邮件。使用此选项时，仅在用户启动电子邮件应用程序时发送和接收邮件。

  - 手动发送和接收邮件。使用此选项时，仅在用户单击客户端用户界面中的“发送和接收”选项时发送和接收邮件。

  - 定时发送和接收邮件。用户设置此选项时，客户端应用程序定时连接到服务器以发送邮件并下载所有新邮件。

有关如何配置所使用的电子邮件应用程序的这些设置的信息，请参阅各个电子邮件应用程序提供的帮助文档。

## 设置发送/接收选项时的注意事项

如果运行 POP3 或 IMAP4 电子邮件应用程序的设备或计算机始终连接到 Internet，则用户可能需要将电子邮件应用程序配置为定时发送和接收邮件。通过定时连接到服务器，用户可使其电子邮件应用程序与服务器上的最新信息保持同步。然而，如果运行 POP3 或 IMAP4 电子邮件应用程序的设备或计算机不是始终连接到 Internet，则用户可能需要将电子邮件应用程序配置为手动发送和接收邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果用户使用的是与 IMAP4 兼容的电子邮件应用程序（支持 IMAP4 IDLE 命令），则用户几乎可以实时将电子邮件发送到他们的 Exchange 邮箱并从其邮箱接收电子邮件。要使这种连接方法正常工作，电子邮件服务器应用程序和客户端应用程序必须都支持 IMAP4 IDLE 命令。大多数情况下，用户不必配置其 IMAP4 应用程序的任何设置即可使用此连接方法。</td>
</tr>
</tbody>
</table>


## POP3 和 IMAP4 应用程序

由于 Exchange 2013 支持 POP3 和 IMAP4，用户可以使用任何支持 POP3 和 IMAP4 客户端应用程序的应用程序来连接到 Exchange 2013。这些应用程序包括 Outlook、Outlook Web App、Windows Live Mail、Outlook Express、Entourage 和许多第三方应用程序（如 Gmail、Mozilla Thunderbird 和 Eudora）。每个电子邮件客户端应用程序支持的功能都不同。有关特定 POP3 和 IMAP4 客户端应用程序提供的特定功能的信息，请参阅每个应用程序附带的文档。

## 用于配置 POP3 或 IMAP4 对用户 Exchange 2013 邮箱访问权限的用户设置

启用 POP3 和 IMAP4 客户端访问后，需要为用户提供将其电子邮件程序连接到其 Exchange 2016 邮箱所需的信息。

要从企业网络内进行连接，用户将需要以下信息：

  - 内部 POP3 或 IMAP4 服务器名称

  - 内部 POP3 或 IMAP4 端口号

  - 内部 POP3 或 IMAP4 加密方法

  - 内部 SMTP（发送服务器）名称

  - 内部 SMTP（发送服务器）端口号

  - 内部 SMTP（发送服务器）加密方法

要从 Internet 进行连接，用户将需要以下信息：

  - 外部 POP3 或 IMAP4 服务器名称

  - 外部 POP3 或 IMAP4 端口号

  - 外部 POP3 或 IMAP4 加密方法

  - 外部 SMTP（发送服务器）名称

  - 外部 SMTP（发送服务器）端口号

  - 外部 SMTP（发送服务器）加密方法

可通过电子邮件或其他手动通信方法向用户提供这些设置。还可配置 Exchange，以使用户可使用 Outlook Web App 查找其自己的设置。

**配置 Exchange 以使用户可查找其 POP3、IMAP4 和 SMTP 服务器设置**

默认情况下，用户无法通过 Outlook Web App 查找其 POP3、IMAP4 和 SMTP 服务器设置。为使用户能够执行此操作，你需要使用 **Set-PopSettings** 和 **Set-ImapSettings** cmdlet。为使用户能够查找其 SMTP（传出）服务器设置，必须使用 **Set-ReceiveConnector** cmdlet。

执行下列操作以允许用户查找其自己的 POP3、IMAP4 和 SMTP 设置：

  - **POP3 设置**   运行带有 *ExternalConnectionSettings* 参数的 **Set-POPSettings** cmdlet。格式为 `Set-POPSettings -ExternalConnectionSetting {<FQDN>:995:SSL}`。例如，如果希望通过服务器与 FQDN Dublin01.Contoso.com 连接的客户端可以查找自己的 POP 设置，则运行 `Set-PopSettings -ExternalConnectionSetting {Dublin01.Contoso.com:995:SSL}`。
    
    在应用此设置后，必须重新启动 IIS。

  - **IMAP4 设置**   运行带有 *ExternalConnectionSettings* 参数的 **Set-IMAPSettings** cmdlet。格式为 `Set-ImapSettings -ExternalConnectionSetting {<FQDN>:993:SSL}`。例如，如果希望通过服务器与 FQDN Dublin01.Contoso.com 连接的客户端可以查找自己的 IMAP 设置，则运行 `Set-IMAPSettings -ExternalConnectionSetting {Dublin01.Contoso.com:993:SSL}`。
    
    在应用此设置后，必须重新启动 IIS。

  - **SMTP 设置**   运行带有 *AdvertiseClientSettings* 参数的 **Set-ReceiveConnector** cmdlet。格式为 `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN <FQDN>`。例如，如果希望通过服务器与 FQDN Dublin01.Contoso.com 连接的客户端可以查找自己的 SMTP 设置，则运行 `Set-ReceiveConnector "Client Frontend <Server Name>" -AdvertiseClientSettings $True -FQDN Dublin01.Contoso.com`。
    
    在应用此设置后，必须重新启动 IIS。

通过运行 **Set-POPSettings**、**Set-IMAPSettings** 和 **Set-ReceiveConnector** cmdlet 更改默认设置后，用户可以在 Outlook Web App 中查找其外部 POP、IMAP 和 SMTP 服务器设置，具体操作为单击“设置”\>“选项”\>“帐户”\>“我的帐户”\>“POP 或 IMAP 访问的设置”。

**在服务器上保留邮件副本**

某些电子邮件程序上的默认设置在检索邮件后会在服务器上删除这些邮件。务必建议用户将其电子邮件程序设置为在服务器上保留客户端检索的所有邮件的副本。通过在服务器上保留邮件的副本，用户可通过其他电子邮件程序访问其邮件。

