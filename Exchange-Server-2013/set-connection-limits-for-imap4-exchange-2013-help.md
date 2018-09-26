---
title: '设置 IMAP4 的连接限制: Exchange 2013 Help'
TOCTitle: 设置 IMAP4 的连接限制
ms:assetid: 8e3aa366-e77c-4c70-b78d-ddbb178cb521
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123712(v=EXCHG.150)
ms:contentKeyID: 50556614
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置 IMAP4 的连接限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-28_

可以使用 EAC 或命令行管理程序来管理组织的 IMAP4 连接限制。

指定 IMAP4 的连接限制时，可以选择服务器、IP 地址或特定用户的连接限制。

有关与 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“IMAP4 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 设置服务器、IP 地址或用户的 IMAP4 连接限制

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页上，单击“IMAP4”。

4.  向下滚动并单击“更多选项”。

5.  在“连接限制”下，使用下列设置：
    
      - **最大连接数**   指定所指定的服务器将接受的连接总数。 这包括通过身份验证和未通过身份验证的连接。默认值为 2,147,483,647。可能的值从 1 到 2,147,483,647。
    
      - **来自单个 IP 地址的最大连接数**   指定服务器将接受的来自单个 IP 地址的连接数。默认值为 2,147,483,647。可能的值从 1 到 2,147,483,647。
    
      - **来自单个 IP 用户的最大连接数**   指定服务器将接受的来自特定用户的最大连接数。默认值为 16。可能的值从 1 到 2,147,483,647。
    
      - **最大命令大小(字节)**   可以指定单个命令的最大大小。默认大小为 10,240。可能的值从 1,024 到 16,384。

6.  单击“应用”，然后单击“确定”保存更改。

设置了连接限制之后，必须重新启动 IMAP4 服务。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 使用命令行管理程序设置服务器、IP 地址或用户的 IMAP4 连接限制

本示例设置服务器的连接限制。

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnections Value
```

本示例设置 IP 地址的连接限制。

```powershell
Set-ImapSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value
```

本示例设置用户的连接限制。

```powershell
Set-ImapSettings -MaxConnectionsPerUser Value
```

此示例设置最大命令大小。

```powershell
Set-ImapSettings -MaxCommandSize Value
```

设置了连接限制之后，必须重新启动 IMAP4 服务。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\))。

## 您如何知道这有效？

若要检查是否成功创建了连接限制，请进行以下操作之一：

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页上，单击“IMAP4”。

4.  向下滚动并单击“更多选项”。

5.  在“连接限制”下，验证连接设置是不正确。

或

1.  在命令行管理程序中运行以下命令。
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  验证连接设置正确无误。

## 详细信息

设置服务器、IP 地址或用户的 IMAP4 连接限制之后，您可能还需要：

[在 Exchange 2016 中启用 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[为 IMAP4 设置连接超时限制](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

