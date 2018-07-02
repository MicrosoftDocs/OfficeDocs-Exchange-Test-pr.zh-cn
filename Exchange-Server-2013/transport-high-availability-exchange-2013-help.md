---
title: '传输高可用性: Exchange 2013 Help'
TOCTitle: 传输高可用性
ms:assetid: e9ec6d05-f441-4cca-8592-8f7469948299
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657506(v=EXCHG.150)
ms:contentKeyID: 50491858
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 传输高可用性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-15_

在 Microsoft Exchange Server 2013 中，传输高可用性用于在成功传递邮件前后保留邮件的冗余副本。Exchange 2013 改善了在 Exchange Server 2010 中引入的传输高可用性功能（例如卷影冗余和传输暂放），以帮助确保邮件不会在传输中丢失。

这里给出了 Exchange 2013 中主要传输高可用改进的摘要：

  - 卷影冗余会在接受或确认邮件之前，在其他服务器上创建邮件的冗余副本。 发送服务器是否支持卷影冗余都与此无关。

  - 卷影冗余将数据库可用性组 (DAG) 和 Active Directory 站点识别为传输高可用性边界。 这样可减少保留邮件冗余副本的服务器数，并跨 DAG 或 Active Directory 站点消除不必要的冗余邮件维护流量。
    
    有关详细信息，请参阅[卷影冗余](shadow-redundancy-exchange-2013-help.md)。

  - 传输垃圾站已得到改进，并且现在称为“Safety Net”。 Safety Net 存储邮箱服务器上的传输服务成功处理的邮件。 Safety Net 最适用于 DAG 中的邮箱服务器，但是 Safety Net 也可用于不属于 DAG 的相同 Active Directory 站点中的多个邮箱服务器。

  - 当前在另一台服务器上使 Safety Net 本身冗余。 这对于避免 Exchange 2013 中的单点故障很重要，因为传输服务和邮箱数据库均位于邮箱服务器上。
    
    有关详细信息，请参阅[Safety Net](safety-net-exchange-2013-help.md)。

下图提供了传输高可用性如何在 Exchange 2013 中发挥作用的高级别概览。

![传输高可用性概述](images/JJ657506.88f2284d-8afe-4c8f-94a6-cd4c097a55d8(EXCHG.150).gif "传输高可用性概述")

1.  名为 Mailbox01 的 Exchange 2013 邮箱服务器从位于传输高可用性边界外的 SMTP 服务器接收邮件。 “传输高可用性边界”是非 DAG 环境中的 DAG 或 Active Directory 站点。 邮件可来自第三方 SMTP 服务器，来自通过客户端访问服务器代理的 Internet SMTP 服务器，或者来自另一个 Exchange 2013 服务器。

2.  在确认接收邮件之前，Mailbox01 会对另一个名为 Mailbox03 的 Exchange 2013 邮箱服务器启动新的 SMTP 会话，Mailbox03 位于传输高可用性边界内，并且会制作邮件的卷影副本。 在 DAG 环境中，远程 Active Directory 站点中的卷影服务器为首选。 Mailbox01 是保留主要邮件的主要服务器，Mailbox03 是保留卷影邮件的卷影服务器。

3.  Mailbox01 上的传输服务处理主要邮件。
    
    1.  在本例中，收件人的邮箱位于 Mailbox01，因此传输服务将邮件传输至本地邮箱传输服务。
    
    2.  邮箱传输服务将邮件传递到本地邮箱数据库。
    
    3.  Mailbox01 为 Mailbox03 安排丢弃状态，指示已成功处理主要邮件，并且 Mailbox01 将主要邮件的副本移动到本地 Primary Safety Net 中。请注意，邮件在同一个队列数据库内的队列之间移动。

4.  Mailbox03 就主要邮件状态定期轮询 Mailbox01。

5.  如果 Mailbox03 确定 Mailbox01 已成功处理主要邮件，Mailbox03 会将卷影邮件移动至本地 Shadow Safety Net。请注意，邮件在同一个队列数据库内的队列之间移动。

邮件保留在 Primary Safety Net 和 Shadow Safety Net 中，直至根据可配置的超时值，邮件过期。 如果在邮件到期前发生邮箱数据库故障转移，Mailbox01 上的 Primary Safety Net 会重新提交邮件。 如果 Mailbox01 不可用，Mailbox03 上的 Shadow Safety Net 将接管并重新提交邮件。

## 在客户端访问服务器上的前端传输服务中的邮件冗余

客户端访问服务器没有邮件队列。 其为无状态代理服务器，使用前端传输服务接收传入的 SMTP 连接，并在邮箱服务器上的传输服务中代理它们。 前端传输服务在发送服务器打开的情况下保持 SMTP 会话，同时主要邮件传输至邮箱服务器上的传输服务，并且由不同邮箱服务器上的传输服务在传输高可用性边界中制作邮件的卷影副本。 只有在成功创建主要邮件和卷影邮件之后，数据 SMTP 命令的末尾才会通过客户端访问服务器发送回发送 SMTP 服务器。

