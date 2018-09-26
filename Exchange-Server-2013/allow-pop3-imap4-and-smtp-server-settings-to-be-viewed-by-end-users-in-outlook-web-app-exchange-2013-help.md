---
title: '允许最终用户在 Outlook Web App 中查看 POP3、IMAP4 和 SMTP 服务器设置: Exchange 2013 Help'
TOCTitle: 允许最终用户在 Outlook Web App 中查看 POP3、IMAP4 和 SMTP 服务器设置
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50556666
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 允许最终用户在 Outlook Web App 中查看 POP3、IMAP4 和 SMTP 服务器设置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-28_

如果有用户使用 POP3 或 IMAP4 连接其 MicrosoftExchange Server 2013 邮箱，这些用户需要知道连接所需的正确服务器设置。在进行了默认的 Exchange 2013 安装之后，用户无法查找自己的传入 POP3 或 IMAP4 服务器设置或者传出 SMTP 服务器设置。不过，你可以配置 Exchange，以便用户能够使用 MicrosoftOutlook Web App 查找自己的设置。

在执行了这些过程之后，用户可以在 Outlook Web App 中查找其服务器设置，如下所示：

1.  在 Outlook Web Access 中，单击“设置”\>“选项”。

2.  在“选项”中，单击“帐户”\>“我的帐户”\>“POP 或 IMAP 访问的设置”。

有关与 POP3 和 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行管理程序以允许 POP3 和 IMAP4 用户在 Outlook Web App 中查看其传入 POP3 和 IMAP4 设置

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”和“IMAP4 设置”条目。

此示例允许最终用户查看外部 POP3 服务器设置。

```powershell
Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}
```

有关语法和参数的详细信息，请参阅 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

此示例允许最终用户查看外部 IMAP4 服务器设置。

```powershell
Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}
```

有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\))。

若要应用这些更改，必须重启 IIS。无需重启 POP3 服务。若要重启 IIS，请在命令提示符处输入以下命令：

```powershell
iisreset
```

## 您如何知道这有效？

若要验证是否已将 Exchange 配置为允许用户查看其 POP3 服务器设置，请执行以下操作：

1.  在命令行管理程序中运行以下命令。
    
    ```powershell
    Get-PopSettings | format-list
    ```

2.  验证是否已设置 *ExternalConnectionSettings* 属性。

若要验证是否已将 Exchange 配置为允许用户查看其 IMAP4 服务器设置，请执行以下操作：

1.  在命令行管理程序中运行以下命令。
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  验证是否已设置 *ExternalConnectionSettings* 属性。

## 使用命令行管理程序以允许 POP3 和 IMAP4 用户在 Outlook Web App 中查看其传出 SMTP 设置

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接收连接器”条目。

此示例允许最终用户使用 Outlook Web App 查看内部和外部 SMTP 服务器设置。

```powershell
    Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 
```

有关详细的语法和参数信息，请参阅[Set-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125140\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已将 Exchange 配置为允许用户查看其 SMTP 服务器设置，请执行以下操作：

1.  在命令行管理程序中运行以下命令。
    
    ```powershell
    Get-ReceiveConnector | format-list
    ```

2.  如果 *AdvertiseClientSettings* 属性设置为 `true`，则用户可以在 Outlook Web App 中查看其 SMTP 服务器设置。如果 *AdvertiseClientSettings* 设置为 `false`，则用户无法在 Outlook Web App 中查看其 SMTP 服务器设置。

## 详细信息

在使用户可以查看其 POP3、IMAP4 和 SMTP 设置之后，您可能还需要：

[对用户启用或禁用 POP3 访问](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[对用户启用或禁用 IMAP4 访问](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

