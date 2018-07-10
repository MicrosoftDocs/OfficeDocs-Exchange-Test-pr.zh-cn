---
title: '邮件当前存在于一个或多个队列中_MessagesInQueue: Exchange 2013 Help'
TOCTitle: 邮件当前存在于一个或多个队列中_MessagesInQueue
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50490426
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 邮件当前存在于一个或多个队列中\_MessagesInQueue

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为尝试卸载传输角色可能会导致传输队列丢失数据，所以 Microsoft® Exchange Server 2007 安装程序显示该警告。

Exchange 2007 安装程序将进行检查以确保在删除与管理这些队列相关的角色之前，传输队列为空。

如果在仍处于传输队列中的邮件被传递之前就删除了传输角色，则这些邮件可能会无限期地留在该队列之中。

要解决此问题，请在继续安装之前，检查引用队列以确保其中没有邮件。

查看队列的内容

1.  打开 Exchange 管理控制台。

2.  在控制台树中，单击\&quot;工具箱\&quot;。

3.  在结果窗格中，单击\&quot;Exchange 队列查看器\&quot;。

4.  在操作窗格中，单击\&quot;打开工具\&quot;。

5.  在队列查看器中，单击\&quot;队列\&quot;选项卡。此时，系统会列出您连接到的服务器上的所有队列。

6.  右键单击所需的队列，然后选择\&quot;属性\&quot;查看此队列的属性。

查看队列中的邮件

1.  依照步骤 1 到 4 进行操作

2.  在队列查看器中，单击\&quot;邮件\&quot;选项卡。此时，系统会列出您连接到的服务器上的所有邮件。若要将视图调整为单个队列，请单击\&quot;队列\&quot;选项卡，双击队列名称，然后单击所显示的\&quot;服务器\\队列\&quot;选项卡。

3.  若要查看邮件的详细信息，请选择一个邮件，然后单击操作窗格中的\&quot;属性\&quot;。

