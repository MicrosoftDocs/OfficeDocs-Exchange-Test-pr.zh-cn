---
title: '启动和停止 POP3 服务: Exchange 2013 Help'
TOCTitle: 启动和停止 POP3 服务
ms:assetid: 3d543921-d8c9-4d4b-99a1-82446b585ceb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997475(v=EXCHG.150)
ms:contentKeyID: 50490394
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启动和停止 POP3 服务

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-03-13_

默认情况下，Microsoft Exchange POP3 服务和 Microsoft Exchange POP3 后端服务这两项 POP3 服务在运行 MicrosoftExchange Server 2013 的计算机上并未启动。您必须启动这两项服务，才能让电子邮件客户端使用 POP3 连接到 Exchange。当这些服务运行时，Exchange 2013 使用安全套接字层 (SSL) 在端口 110 以及通过端口 995 接受不安全的 POP3 客户端通信。

Microsoft Exchange POP3 服务在运行客户端访问服务器角色的 Exchange 2013 计算机上运行。Microsoft Exchange POP3 后端服务在运行邮箱服务器角色的 Exchange 2013 计算机上运行。在同一计算机上运行客户端访问和邮箱角色的环境中，您可以在同一计算机上管理这两个服务。

有关与 POP3 和 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 和 IMAP4 权限”条目。

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


## 您想执行什么操作？

## 使用 Microsoft 管理控制台服务管理单元启动或停止 POP3 服务

要启动 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上单击“开始”，指向“程序”，指向“管理工具”，然后单击“服务”。右键单击“Microsoft Exchange POP3”，然后单击“启动”。

2.  在运行邮箱服务器角色的计算机上单击“开始”，指向“程序”，指向“管理工具”，然后单击“服务”。在结果窗格中，右键单击“Microsoft Exchange POP3 后端”，然后单击“启动”。

要停止 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上单击“开始”，指向“程序”，指向“管理工具”，然后单击“服务”。右键单击“Microsoft Exchange POP3”，然后单击“停止”。

2.  在运行邮箱服务器角色的计算机上单击“开始”，指向“程序”，指向“管理工具”，然后单击“服务”。右键单击“Microsoft Exchange POP3 后端”，然后单击“停止”。

## 使用命令行管理程序启动或停止 POP3 服务

要启动 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上，从命令行管理程序运行下列命令，以启动 Microsoft Exchange POP3 服务。
    
        Start-service MSExchangePOP3

2.  在运行邮箱服务器角色的计算机上，从命令行管理程序运行下列命令以启动 Microsoft Exchange POP3 后端服务。
    
        Start-service MSExchangePOP3BE

要停止 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上，从命令行管理程序运行下列命令，以停止 Microsoft Exchange POP3 服务。
    
        Stop-service MSExchangePOP3

2.  在运行邮箱服务器角色的计算机上，从命令行管理程序运行下列命令，以停止 Microsoft Exchange POP3 后端服务。
    
        Stop-service MSExchangePOP3BE

## 使用 net start 启动或停止 POP3 服务

要启动 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上，从命令提示符运行下列命令，以启动 Microsoft Exchange POP3 服务。
    
        Net Start msExchangePOP3

2.  在运行邮箱服务器角色的计算机上，从命令提示符运行下列命令，以启动 Microsoft Exchange POP3 后端服务。
    
        Net Start msExchangePOP3BE

要停止 POP3 服务，请执行以下操作：

1.  在运行客户端访问服务器角色的计算机上，从命令提示符运行下列命令，以停止 Microsoft Exchange POP3 服务。
    
        Net Stop MSExchangePOP3

2.  在运行邮箱服务器角色的计算机上，从命令提示符运行下列命令，以停止 Microsoft Exchange POP3 后端服务。
    
        Net Stop MSExchangePOP3BE

## 您如何知道这有效？

1.  在 Exchange 客户端访问服务器上，打开 Windows 任务管理器。如果 Microsoft Exchange POP3 服务正在运行，“服务”选项卡上的“MSExchangePOP3”的状态将显示为“正在运行”。

2.  在 Exchange 邮箱服务器上，打开 Windows 任务管理器。如果 Microsoft Exchange POP3 后端服务正在运行，“服务”选项卡上的“MSExchangePOP3BE”的状态将显示为“正在运行”。

