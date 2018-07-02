---
title: '队列查看器: Exchange 2013 Help'
TOCTitle: 队列查看器
ms:assetid: db892f88-5c13-4607-a38c-8845b35ab8b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124789(v=EXCHG.150)
ms:contentKeyID: 50491673
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 队列查看器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-09-25_

队列查看器是一个 Microsoft 管理控制台的管理单元，安装于邮箱服务器或边缘传输服务器上。队列查看器位于 Exchange 工具箱控制台的\&quot;**邮件流工具**\&quot;部分。使用此工具，可以查看有关传输服务器上的队列以及这些队列中的邮件的信息，并对队列和邮件项目执行管理操作。队列查看器可用于解决邮件流问题和标识垃圾邮件。

使用队列查看器管理队列时，请考虑以下事项：

  - 必须连接到传输服务器。默认设置下，队列查看器在你将其打开的服务器上打开队列数据库。但是，你也可以连接到不同的服务器。有关详细信息，请参阅[使用队列查看器连接到服务器](connect-to-a-server-in-queue-viewer-exchange-2013-help.md)。

  - 队列和邮件的列表可能非常大，具体取决于当前邮件流，当邮件进入和离开服务器时，队列和邮件的列表会发生更改。可以配置队列查看器的选项，以控制队列和邮件列表的刷新间隔以及每页上显示的项目数。有关详细信息，请参阅[设置队列查看器选项](set-queue-viewer-options-exchange-2013-help.md)。

  - 可以创建筛选器，以显示要监视的特定队列或邮件集合。找到要监视的队列和邮件之后，可以查看这些队列和邮件的属性信息。此信息可以帮助你找出邮件流问题的原因。有关详细信息，请参阅[队列筛选器](queue-filters-exchange-2013-help.md)和[邮件筛选器](message-filters-exchange-2013-help.md)。

  - 可以使用操作窗格中的\&quot;**导出列表**\&quot;链接导出队列列表或邮件列表。有关详细信息，请参阅[从队列查看器中导出列表](export-lists-from-queue-viewer-exchange-2013-help.md)。

