---
title: '在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器: Exchange 2013 Help'
TOCTitle: 在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50491569
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 2013 中使用 Exchange 2010 或 2007 边缘传输服务器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 Service Pack 1 (SP1) 中提供了边缘传输服务器。然而，您可以继续使用现有 Exchange Server 2007 或在外围网络中部署的 Exchange Server 2010 边缘传输服务器。或者，您可以为新的或升级的 Exchange 2013 组织，在外围网络中安装新的 Exchange 2007 或 Exchange 2010 边缘传输服务器。

下面是您需要知道的一些情况：

  - Exchange 2007 或 Exchange 2010 边缘传输服务器预期到集线器传输服务器的连接。在 Exchange 2013 中，传输服务存在于邮箱服务器上。因此，邮箱服务器和边缘传输服务器上的传输服务之间的 Internet 邮件流将有效绕过 Exchange 2013 客户端访问服务器。

  - 您可以将 Exchange 2007 或 Exchange 2010 边缘传输服务器订阅到只包含 Exchange 2013 服务器的 Active Directory 站点。您可以导入边缘订阅文件并在独立的 Exchange 2013 邮箱服务器上运行 EdgeSync，或将该文件导入到在同一计算机上装有邮箱服务器和客户端访问服务器的服务器。不能导入边缘订阅文件或在独立的 Exchange 2013 客户端访问服务器上运行 EdgeSync。

  - 在您的 Exchange 2013 组织上部署新 Exchange 2007 或 Exchange 2010 边缘传输服务器的程序基本与 Exchange 的之前版本一样。然而，任何在集线器传输服务器上执行过的任何程序都将在 Exchange 2013 中的邮箱服务器上执行。所使用的程序为：
    
      - [配置通过所订阅的边缘传输服务器的 Internet 邮件流](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [在不使用 EdgeSync 的情况下配置边缘传输服务器和集线器传输服务器之间的邮件流](https://go.microsoft.com/fwlink/p/?linkid=276661)

