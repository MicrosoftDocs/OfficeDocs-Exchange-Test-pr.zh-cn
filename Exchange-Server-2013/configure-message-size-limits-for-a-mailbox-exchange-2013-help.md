---
title: '配置邮箱的邮件大小限制: Exchange 2013 Help'
TOCTitle: 配置邮箱的邮件大小限制
ms:assetid: d1220685-14c0-4c4f-abb2-3920f3046212
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124708(v=EXCHG.150)
ms:contentKeyID: 50556676
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置邮箱的邮件大小限制

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-12_

可以使用 EAC 和命令行管理程序以配置用户邮箱的邮件大小限制。这些限制控制用户可以发送和接收的邮件的大小。默认情况下，创建了邮箱时，系统不会对发送和接收的邮件的大小进行限制。

请记住，Exchange 组织中还有其他设置能确定邮箱发送和接收的最大邮件大小（例如，在邮箱服务器上配置的最大邮件大小）。若要了解有关 Exchange 中邮件大小的限制（包括邮件大小限制类型、作用域和优先顺序）的详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

有关与用户邮箱相关的其他管理任务，请参阅[管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)。

> [!NOTE]
> 还可以控制邮件用户发送和接收的邮件的大小，以及来自共享邮箱的邮件的大小。


## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;收件人设置权限\&quot;部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置邮件大小限制

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在用户邮箱列表中，单击要更改其邮件大小限制的邮箱，然后单击\&quot;**编辑**\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱功能\&quot;。

4.  在\&quot;**邮件大小限制**\&quot;下，单击\&quot;**查看详情**\&quot;以查看并更改以下邮件大小限制：
    
      - \&quot;已发送消息\&quot;   要指定该用户发送的消息的最大大小，可选择\&quot;最大消息大小 (KB)\&quot;复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户发送大于该指定大小的邮件，则会将该邮件返回至用户，并向其显示一条描述性的错误消息。
    
      - \&quot;已收到消息\&quot;   要指定该用户接收的消息的最大大小，可选择\&quot;最大消息大小 (KB)\&quot;复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户收到大于指定大小的邮件，则该邮件将返回至发件人，并向其显示一条描述性的错误消息。

5.  单击\&quot;**确定**\&quot;，然后单击\&quot;**保存**\&quot;以保存你的更改。

## 使用命令行管理程序配置邮件大小限制

此示例将 Debra Garcia 邮箱能发送的最大邮件大小设置为 25 MB，并将能接收的最大邮件大小设置 35 MB。

    Set-Mailbox "Debra Garcia" -MaxSendSize 25mb -MaxReceiveSize 35mb

有关详细的语法和参数信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否为邮箱成功配置了邮件大小限制，请执行下列操作之一：

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在用户邮箱列表中，单击要验证其邮件大小限制的邮箱，然后单击\&quot;**编辑**\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱功能\&quot;。

4.  在\&quot;**邮件大小限制**\&quot;下，单击\&quot;**查看详情**\&quot;以验证邮箱的邮件大小限制。

或

在命令行管理程序中运行以下命令。

    Get-Mailbox <identity> | fl MaxSendSize,MaxReceiveSize

