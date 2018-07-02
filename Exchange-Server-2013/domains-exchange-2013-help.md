---
title: '域: Exchange 2013 Help'
TOCTitle: 域
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 50490036
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 域

 

_**适用于：**Exchange Server 2013, Office 365_

_**上一次修改主题：**2012-10-11_

域表示为其设置电子邮件目录和邮箱的 SMTP 命名空间。通过配置与 Microsoft Exchange Server 2013 组织进行交互的域，可以配置 Exchange 如何处理与各个域往来的电子邮件。

## 接受域

接受的域是 Exchange 组织针对其发送或接收电子邮件的任何 SMTP 命名空间。接受的域包括 Exchange 组织是其权威的那些域以及内部中继域和外部中继域。当 Exchange 组织为接受域中的收件人处理邮件传递时，该组织即具有权威性。接受的域还包括 Exchange 组织针对其接收邮件然后中继到组织外部的电子邮件服务器的域。

有关接受域的详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

## 远程域

在 Exchange 2013 中，可创建远程域条目，以定义在您的 Exchange 组织和您的组织外部的域之间传输邮件时使用的设置。创建远程域条目时，将会控制发送到该域的邮件的类型。还可以将从组织中的用户发送的邮件格式策略和可接受的字符集应用到远程域中。

远程域的设置是用于 Exchange 组织的全局配置设置。在分类期间，远程域设置将应用于邮件。当发生收件人解析时，收件人域将与配置的远程域进行匹配。如果远程域的配置阻止特定类型的邮件发送到该域中的收件人，则将删除该邮件。如果为远程域指定特定的邮件格式，则将修改邮件头和邮件内容。这些设置适用于由 Exchange 组织处理的所有邮件。

有关远程域的详细信息，请参阅[远程域](remote-domains-exchange-2013-help.md)。

