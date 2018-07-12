---
title: '接受域: Exchange 2013 Help'
TOCTitle: 接受域
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50491604
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 接受域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-06-16_

接受域是 Microsoft Exchange Server 2013 组织为其发送或接收电子邮件的任何 SMTP 命名空间。接受域包括那些 Exchange 组织对其有权威性的域。当 Exchange 组织为接受域中的收件人处理邮件传递时，该组织即具有权威性。接受域还包括 Exchange 组织为其接收邮件然后中继到组织外部的电子邮件服务器以便传递给收件人的域。

**目录**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## 配置接受域

接受域被配置为 Exchange 组织的全局设置。您需要将 Exchange 组织为其中继或传递邮件的每个域配置为所在组织的接受域。

存在三种类型的接受域：权威、内部中继和外部中继。在以下部分中描述这些接受域类型。

> [!NOTE]  
> 如果您已在外围网络中订阅了边缘传输服务器，请在 Exchange 组织中的邮箱服务器上配置接受的域。在 EdgeSync 同步期间，接受的域配置会复制到边缘传输服务器。有关详细信息，请参阅<a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>。


## 权威域

一个组织可能具有多个 SMTP 域。组织的电子邮件域集是权威域。在 Exchange 2013 中，如果 Exchange 组织为某 SMTP 域中的收件人驻留邮箱，则该接受域被视为权威域。

默认情况下，安装第一个 Exchange 2013 邮箱服务器之后，一个接受域将配置为 Exchange 组织的权威域。默认接受域是林根域的完全限定的域名 (FQDN)。通常，内部域名不同于外部域名。例如，虽然外部域名是 Contoso.com，但内部域名则可能是 Contoso.local。组织的 DNS 邮件交换器 (MX) 记录引用了 Contoso.com。Contoso.com 是在创建电子邮件地址策略时分配给用户的 SMTP 命名空间。您需要创建一个与外部域名匹配的接受域。

有关详细信息，请参阅：

  - [配置贵 Exchange 组织内的接受域为权威](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [将 Exchange 配置为接收多个权威域的邮件](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## 中继域

通常，大多数面向 Internet 的消息服务器配置为不允许通过它们中继其他域。但是，有时您可能希望合作伙伴或子公司通过您的 Exchange 服务器中继电子邮件。在 Exchange 2013 中，可以将接受域配置为中继域。您的组织收到电子邮件，然后将邮件中继到其他电子邮件服务器。

您可以将中继域配置为内部中继域或外部中继域。以下部分描述了这两种中继域类型。

## 内部中继域

配置内部中继域时，该域中的一些收件人或所有收件人在 Exchange 组织中没有邮箱。通过 Exchange 组织中的传输服务器为该域中继来自 Internet 的邮件。本部分介绍的方案中使用了此配置。

在两个或两个以上不同的消息系统之间，组织可能必须共享同一 SMTP 地址空间。例如，您可能需要在 Exchange 和第三方消息系统之间，或在不同的 Active Directory 林中配置的 Exchange 环境之间共享 SMTP 地址空间。在这些应用场景中，各个电子邮件系统中的用户都将同一域后缀作为其电子邮件地址的一部分。

若要支持这些应用场景，需要创建一个配置为内部中继域的接受域。还需要添加一个源于邮箱服务器并配置为将电子邮件发送至共享地址空间的发送连接器。如果接受域配置为权威域且 Active Directory 中没有收件人，则会向发送人返回未送达报告 (NDR)。配置为内部中继域的接受域首先会尝试发送到 Exchange 组织中的收件人。如果没有该收件人，则会将邮件路由到地址空间最匹配的发送连接器。

如果组织包含多个林并已配置全局地址列表 (GAL) 同步，则一个林的 SMTP 域可以配置为另一个林的内部中继域。Internet 上发送给内部中继域的收件人的邮件被中继到同一组织中的邮箱服务器。然后，接收邮箱服务器将邮件路由到收件人林中的邮箱服务器。将 SMTP 域配置为内部中继域以确保 Exchange 组织接受发往该域的电子邮件。组织的连接器配置确定邮件的路由方式。

有关详细信息，请参阅[为在贵 Exchange 组织之外具有邮箱的业务单位配置接受域](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md)。

## 外部中继域

配置外部中继域时，邮件中继到位于 Exchange 组织外部和该组织外围网络外部的电子邮件服务器。

有关详细信息，请参阅[为独立的业务单位配置接受域](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md)。

## 接受域和电子邮件地址策略

需要配置接受域，才能在电子邮件地址策略中使用该 SMTP 地址空间。创建接受域时，可以在地址空间使用通配符 ( \* )，指示 Exchange 组织还接受 SMTP 地址空间的所有子域。例如，要将 contoso.com 及其所有子域配置为接受域，请输入 **\*.contoso.com** 作为 SMTP 地址空间。该接受域条目自动在电子邮件地址策略中可用。

如果删除电子邮件地址策略中使用的接受域，则该策略不再有效，具有该 SMTP 域中电子邮件地址的收件人将无法发送或接收电子邮件。

