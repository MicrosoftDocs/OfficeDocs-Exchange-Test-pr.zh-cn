---
title: '混合部署中的边缘传输服务器: Exchange 2013 Help'
TOCTitle: 混合部署中的边缘传输服务器
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50492072
ms.date: 04/16/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 混合部署中的边缘传输服务器

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2018-04-16_

边缘传输服务器角色是通常部署在位于 Exchange 组织外围网络中的计算机上的可选角色，旨在使组织的受攻击面降到最小。边缘传输服务器角色可处理所有面向 Internet 的邮件流，并为组织中的内部部署 Exchange 服务器提供 SMTP 中继和智能主机服务。

## 基于 Exchange 的混合部署组织中的边缘传输服务器

想要使用边缘传输服务器的 Exchange 2016 组织可以选择部署 exExchange2k16 边缘传输服务器或运行最新版本的 Exchange 2016 及更高版本、Exchange 2013 或 Exchange 2010 的边缘传输服务器。如果您不想直接向 Internet 公开内部 Exchange 服务器，请使用边缘传输服务器。在混合部署中部署边缘传输服务器时，Exchange Online 将通过 Exchange Online Protection 服务连接到边缘传输服务器传送邮件。然后，边缘传输服务器将把邮件传递到收件人邮箱所在的内部部署 Exchange 邮箱服务器。

> [!IMPORTANT]
> 不要在处理或修改 SMTP 通信的内部部署 Exchange 服务器和 Office 365 之间放置任何服务器、服务或设备。内部部署 Exchange 组织和 Office 365 之间的安全邮件流取决于组织之间发送的邮件中包含的信息。支持允许 TCP 端口 25 上的 SMTP 通信通过而无需修改的防火墙。如果服务器、服务或设备处理内部部署 Exchange 组织和 Office 365 之间发送的邮件，此信息将被删除。如果发生这种情况，该邮件将不再被视为组织内部邮件，并且将会对其应用反垃圾邮件筛选、 传输和日记规则以及可能不适用于它的其他策略。


> [!IMPORTANT]
> 如果您在其他位置具有其他 Exchange 边缘传输服务器，但是这些服务器不处理混合传输，那么这些服务器进行升级以支持混合部署。不过，如果希望 EOP 将来连接到其他边缘传输服务器以实现混合传输，则这些服务器必须运行最新版本的 Exchange 2016 及更高版本、Exchange 2010 或 Exchange 2013。


## 向混合部署添加边缘传输服务器

配置混合部署时，您可以视需要选择在内部部署组织中部署边缘传输服务器。配置混合部署时，您可以使用混合配置向导，选择一个或多个内部部署 Exchange 服务器，或选择一个或多个内部部署边缘传输服务器处理 Exchange Online 组织的混合邮件传输。

在将边缘传输服务器添加到混合部署时，混合配置向导将代表内部 Exchange 服务器与 EOP 进行通信。边缘传输服务器作为内部 Exchange 服务器和 EOP 之间的中继，用于从内部部署组织到 Exchange Online 组织的出站邮件。边缘传输服务器还作为内部 Exchange 服务器之间的中继，用于从 Exchange Online 组织到内部部署组织的入站邮件。所有以前由内部 Exchange 服务器处理的连接安全性由边缘传输服务器处理。收件人查询、遵从性策略和其他邮件检查继续由内部 Exchange 服务器处理。

如果将边缘传输服务器添加到了混合部署，那么不需要通过该服务器路由内部部署用户与 Internet 收件人之间发送的邮件。只有在内部部署与 Exchange Online 组织之间发送的邮件才会通过边缘传输服务进行路由。

## 不使用边缘传输服务器的邮件流

下面的流程和图表展示了在没有部署边缘传输服务器时，本地组织与 Exchange Online 之间的邮件路径：

1.  从内部部署组织到 Exchange Online 组织中的收件人的出站邮件从内部 Exchange 服务器上的邮箱进行发送。

2.  Exchange 服务器直接将邮件发送至 EOP。

3.  EOP 将邮件传递到 Exchange Online 组织。

从 Exchange Online 组织发送到本地组织中收件人的邮件遵循相反的路由。

**未部署边缘传输服务器的混合部署中的邮件流**

![不使用边缘传输服务器的混合邮件流](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "不使用边缘传输服务器的混合邮件流")

## 使用边缘传输服务器的邮件流

以下流程介绍了在部署边缘传输服务器后，邮件在内部部署组织与 Exchange Online 之间采用的路径。从内部部署组织到 Exchange Online 组织中收件人的邮件是从内部 Exchange 服务器发送的：

1.  从内部部署组织到 Exchange Online 组织中的收件人的邮件从内部 Exchange 服务器上的邮箱进行发送。

2.  Exchange 服务器将邮件发送到运行版本受支持的 Exchange 发行版边缘传输服务器。

3.  边缘传输服务器将邮件发送至 EOP。

4.  EOP 将邮件传递到 Exchange Online 组织。

从 Exchange Online 组织发送到本地组织中收件人的邮件遵循相反的路由。

**部署了边缘传输服务器的混合部署中的邮件流**

![使用边缘传输服务器的混合邮件流](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "使用边缘传输服务器的混合邮件流")

