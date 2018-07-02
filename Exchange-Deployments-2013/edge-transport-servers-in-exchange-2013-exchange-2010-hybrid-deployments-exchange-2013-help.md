---
title: 'Exchange 2013/Exchange 2010 混合部署中的边缘传输服务器: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合部署中的边缘传输服务器
ms:assetid: 924f895e-5987-48d0-b113-9d26dcbcdae0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn393965(v=EXCHG.150)
ms:contentKeyID: 59636471
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合部署中的边缘传输服务器

本主题正在进行。  

_<strong>适用于：</strong>Exchange Online, Exchange Server, Exchange Server 2013_

_<strong>上一次修改主题：</strong>2016-12-09_

使用 Microsoft Exchange 部署的边缘传输服务器部署在组织的内部部署外围网络中。它们是未加入域的计算机，可处理面向 Internet 的邮件流，并充当内部网络中的 Exchange 服务器的 SMTP 中继和智能主机。

对于想要使用边缘传输服务器的 Exchange 2013 组织，提供部署 Exchange Server 2013 边缘传输服务器或运行 Exchange 2010 Service Pack 3 (SP3) 的 Exchange 2010 边缘传输服务器的选项。如果您不想将内部 Exchange 2013 客户端访问或邮箱服务器直接暴露给 Internet，请使用边缘传输服务器。

可在以下位置了解 Exchange 2013 边缘传输服务器角色的详细信息：[边缘传输服务器](https://technet.microsoft.com/zh-cn/library/bb124701\(v=exchg.150\))。

有关 Exchange 2010 边缘传输服务器的详细信息，请参阅[边缘传输服务器角色概述](http://go.microsoft.com/fwlink/p/?linkid=183473)。

## 基于 Exchange 2013 的混合部署组织中的边缘传输服务器

在内部部署与混合部署中的 Exchange Online 组织之间路由的邮件要求 Microsoft Exchange Online Protection (EOP) 服务代表 Exchange Online 直接连接到运行 Exchange 2013 或 Exchange 2010 SP3 的边缘传输服务器。

> [!IMPORTANT]
> 如果您在其他位置具有其他 Exchange 2010 边缘传输服务器，但是这些服务器不处理混合传输，那么这些服务器无需升级到 Exchange 2010 SP3。然而，如果希望 EOP 在未来连接至混合传输的其他边缘传输服务器，那么这些服务器必须使用 Exchange 2010 SP3 升级或升级到 Exchange 2013 边缘传输服务器。


## 将边缘传输服务器添加到混合部署

当配置混合部署时，在内部部署组织中部署边缘传输服务器是可选项。当配置混合部署时，混合配置向导允许您选择一个或多个客户端访问和邮箱服务器用于混合邮箱传输，或选择一个或多个内部部署边缘传输服务器处理 Exchange Online 组织的混合邮件传输。

在将边缘传输服务器添加到混合部署时，混合配置向导将代表内部 Exchange 2013 客户端访问和邮箱服务器与 EOP 进行通信。边缘传输服务器作为内部部署邮箱服务器和 EOP 之间的中继，用于从内部部署组织到 Exchange Online 的出站邮件。边缘传输服务器还作为内部部署客户端访问服务器之间的中继，用于从 Exchange Online 组织到内部部署组织的入站邮件。所有以前由客户端访问服务器处理的连接安全性由边缘传输服务器处理。收件人查找、合规性策略和其他邮件检查继续由客户端访问服务器处理。

## 不使用边缘传输服务器的邮件流

以下过程与图表描述了在无边缘传输服务器部署时，内部部署组织与 Exchange Online 之间的邮件的路径：

1.  从内部部署组织到 Exchange Online 组织中收件人的出站邮件将从 Exchange 2010 邮箱服务器中的邮箱发送到 Exchange 2010 集线器传输服务器。

2.  Exchange 2010 集线器传输服务器将邮件发送到 Exchange 2013 邮箱服务器。

3.  Exchange 2013 邮箱服务器将邮件直接发送至 Exchange Online EOP 公司。

4.  EOP 将邮件传送给 Exchange Online 组织。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

从 Exchange Online 组织发送到内部部署组织中的收件人的邮件将遵循相反的路由。

**未部署边缘传输服务器的混合部署中的邮件流**

![没有边缘传输服务器的内部部署](images/Dn393965.37bbe430-b157-4f52-83da-6d44f4459425(EXCHG.150).png "没有边缘传输服务器的内部部署")

## 使用边缘传输服务器的邮件流

以下流程介绍了在部署边缘传输服务器后，邮件在内部部署组织与 Exchange Online 之间采用的路径。从内部部署组织到 Exchange Online 组织中收件人的邮件是从 Exchange 2010 邮箱服务器发送的：

1.  从内部部署组织到 Exchange Online 组织中收件人的出站邮件将从 Exchange 2010 邮箱服务器中的邮箱发送到 Exchange 2010 集线器传输服务器。

2.  Exchange 2010 集线器传输服务器将邮件发送到 Exchange 2013 邮箱服务器。

3.  Exchange 2013 邮箱服务器将邮件发送至 Exchange 2013 或 Exchange 2010 SP3 边缘传输服务器。

4.  边缘传输服务器将邮件发送到 Exchange Online EOP 公司。

5.  EOP 将邮件传送给 Exchange Online 组织。在此示例中，客户端访问和邮箱服务器角色安装在同一 Exchange 2013 服务器上。

从 Exchange Online 组织发送到内部部署组织中的收件人的邮件将遵循相反的路由。

**部署了 Exchange 2013 或 2010 SP3 边缘传输服务器的混合部署中的邮件流**

![具有边缘传输服务器的内部部署](images/Dn393965.f1039133-249b-401d-bd39-3672442a06c9(EXCHG.150).png "具有边缘传输服务器的内部部署")

