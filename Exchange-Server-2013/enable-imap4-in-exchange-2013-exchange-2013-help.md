---
title: '在 Exchange 2016 中启用 IMAP4: Exchange 2013 Help'
TOCTitle: 在 Exchange 2016 中启用 IMAP4
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50491606
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 2016 中启用 IMAP4

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-06-02_

了解如何使用 Microsoft 管理控制台 (MMC) 或 Exchange 命令行管理程序 (EMS) 在 Exchange 2016 中启用 IMAP4 客户端连接。

安装 Exchange Server 2016 时，IMAP4 客户端连接性未启用。要启用 IMAP4 客户端连接性，你需要启动两个 IMAP 服务、Microsoft Exchange IMAP4 服务以及 Microsoft Exchange IMAP4 Backend 服务。启用 IMAP4 之后，Exchange 2016 将使用安全套接字层 (SSL) 在端口 143 和端口 993 上接受不安全的 IMAP4 客户端通信。

你可以在同一台运行邮箱服务器角色的 Exchange 2016 计算机上同时管理 IMAP4 和 IMAP4 后端服务。在 Exchange 2016 中，客户端访问服务是邮箱服务器角色的一部分，这样你就无需单独管理这些服务。

有关如何设置 POP3 和 IMAP4 的详细信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 和 IMAP4 权限”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 Microsoft 管理控制台 (MMC) 来启用 IMAP4

在运行邮箱服务器角色的计算机上：

1.  在“服务”管理单元的控制台树中，单击“服务（本地）”。

2.  在结果窗格中，右键单击“Microsoft Exchange IMAP4”，然后单击“属性”。

3.  在结果窗格中，右键单击“Microsoft Exchange IMAP4 Backend”，然后单击“属性”。

4.  在“常规”选项卡上的“启动类型”下，选择“自动”，然后单击“应用”。

5.  在“服务状态”下，单击“启动”，再单击“确定”。

## 使用 Exchange 命令行管理程序 来启用 IMAP4

在运行邮箱服务器角色的计算机上：

1.  将 Microsoft Exchange IMAP4 服务设置为自动启动。
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  启动 Microsoft Exchange IMAP4 服务。
    
        Start-service msExchangeIMAP4

3.  将 Microsoft Exchange IMAP4 Backend 服务设置为自动启动。
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  启动 Microsoft Exchange IMAP4 Backend 服务。
    
        Start-service msExchangeIMAP4BE

## 您如何知道这有效？

在 Exchange 2016 邮箱服务器上，打开 Windows 任务管理器。如果启用了 IMAP4，在“**服务**”选项卡上，“**MSExchangeIMAP4**”和“**MSExchangeIMAP4BE**”的状态将显示为“**正在运行**”。

