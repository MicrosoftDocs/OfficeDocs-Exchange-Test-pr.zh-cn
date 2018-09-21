---
title: '修改接收连接器上的 SMTP 标题: Exchange 2013 Help'
TOCTitle: 修改接收连接器上的 SMTP 标题
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52061559
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 修改接收连接器上的 SMTP 标题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

“SMTP 标题”是远程 SMTP 消息服务器连接到运行 Microsoft Exchange Server 2013 的计算机上配置的接收连接器之后收到的 SMTP 连接响应。

这是远程 SMTP 消息服务器连接到接收服务器上之后，远程 SMTP 消息服务器收到的默认响应：

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

当您在接收连接器上指定 SMTP 标题的自定义值时，连接到该 SMTP 接收连接器的远程 SMTP 消息服务器将收到以下响应。

```powershell
220 <Banner Text>
```

您可能想为面向 Internet 的 SMTP 接收器修改 SMTP 标题，以便服务器名称和消息服务器软件不会被 SMTP 标题泄露。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接收连接器”条目。

  - 只能使用命令行管理程序执行此过程。

  - 用于替换的 SMTP 标题文本字符串必须总是以 `220` 开头。根据 RFC 2821 中的定义，默认的服务就绪 SMTP 响应代码为 220。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序修改接收连接器上的 SMTP 标题

运行以下命令：

```powershell
Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"
```

此示例修改现有接收连接器“From the Internet”的 SMTP 标题，以便 SMTP 标题显示 `220 Contoso Corporation`。

```powershell
Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"
```

此示例删除了名为“From the Internet”的接收连接器上的自定义 SMTP 标题，这样 SMTP 标题返回为默认值。

```powershell
Set-ReceiveConnector "From the Internet" -Banner $null
```

## 您如何知道操作成功？

若要验证是否已成功修改了接收器上的 SMTP 标题，请执行以下操作：

1.  在可以访问接收连接器的计算机上打开 Telnet 客户端，并运行以下命令：
    
    ```powershell
open <Connector FQDN or IP address> <Port>
```

2.  验证来自接收连接器的响应是否包含您配置的 SMTP 标题。

请注意，这个程序只在允许匿名或基本身份验证的接收连接器上执行。有关详细信息，请参阅[使用 Telnet 测试 SMTP 通信](use-telnet-to-test-smtp-communication-exchange-2013-help.md)。

