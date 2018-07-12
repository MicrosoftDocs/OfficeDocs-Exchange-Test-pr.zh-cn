---
title: '存储组驱动器规格为 missing_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: 存储组驱动器规格为 missing_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 50492029
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 存储组驱动器规格为 missing\_MailboxLogDriveDoesNotExist

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为灾难恢复安装程序无法访问此服务器以前安装所使用的存储组数据库驱动器规格，所以 Microsoft® Exchange Server 2007 灾难恢复安装程序不能继续进行。

Microsoft Exchange 灾难恢复安装程序要求，该服务器以前使用的同一存储组数据库驱动器规格在还原期间必须是可用的。

要解决此问题，请将驱动器配置为与原始逻辑驱动器配置相匹配，然后重新运行 Microsoft Exchange 灾难恢复安装程序。

分配或更改驱动器号

1.  打开\&quot;计算机管理(本地)\&quot;。

2.  在控制台树中，依次单击\&quot;计算机管理(本地)\&quot;、\&quot;存储\&quot;和\&quot;磁盘管理\&quot;。

3.  右键单击分区、逻辑驱动器或卷，然后单击\&quot;更改驱动器号和路径\&quot;。

4.  使用下列过程之一：
    
      - 要分配驱动器号，请依次单击\&quot;添加\&quot;、要使用的驱动器号和\&quot;确定\&quot;。
    
      - 要修改驱动器号，请依次单击相应的驱动器号、\&quot;更改\&quot;、要使用的驱动器号和\&quot;确定\&quot;。

有关如何将驱动器号分配的详细信息，请参阅"指派、 更改或删除驱动器号"([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764))。

