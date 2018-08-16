---
title: '对用户启用或禁用 POP3 访问: Exchange 2013 Help'
TOCTitle: 对用户启用或禁用 POP3 访问
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 50490633
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 对用户启用或禁用 POP3 访问

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-01-06_

可以对用户启用或禁用 POP3。

> [!NOTE]  
> 对用户启用或禁用了 POP3 之后，必须重新启动 Microsoft Exchange POP3 服务和 Microsoft Exchange POP3 后端服务。有关如何重新启动 POP3 服务的详细信息，请参阅<a href="start-and-stop-the-pop3-services-exchange-2013-help.md">启动和停止 POP3 服务</a>。


有关管理用户邮箱的其他信息，请参阅[管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)。

有关与 POP3 和 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 对用户启用或禁用 POP3

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在结果窗格中，选择要对其启用或禁用 POP3 的用户，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“用户邮箱”对话框中的控制台树中，单击“邮箱功能”。
    
    在结果窗格的“电子邮件连接”下，执行以下操作之一：
    
      - 若要对用户禁用 POP3，请在“POP3: **已启用”**下，单击“禁用”。
    
      - 若要对用户启用 POP3，请在“POP3: **已禁用”**下，请单击“启用”。

4.  单击“保存”。

## 使用命令行管理程序对用户启用或禁用 POP3

本示例对用户 John Smith 启用 POP3。

    Set-CASMailbox -Identity "John Smith" -POPEnabled $true

本示例对用户 John Smith 禁用 POP3。

    Set-CASMailbox -Identity "John Smith" -POPEnabled $false

## 您如何知道这有效？

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在结果窗格中，选择要对其启用或禁用 POP3 的用户，然后单击“编辑”。

3.  在“用户邮箱”对话框中的控制台树中，单击“邮箱功能”。
    
    在结果窗格中，查看“电子邮件连接”下的内容。
    
      - 如果对用户启用了 POP3，则会看到“POP3: **已启用”**。
    
      - 如果对用户禁用了 POP3，则会看到<strong>“POP3:已禁用”</strong>。

4.  单击“保存”。

