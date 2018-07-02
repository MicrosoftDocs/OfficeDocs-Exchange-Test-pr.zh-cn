---
title: '将敏感信息规则与传输规则集成: Exchange 2013 Help'
TOCTitle: 将敏感信息规则与传输规则集成
ms:assetid: feb014a7-89dd-4f2d-a06d-52806ce435d4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150583(v=EXCHG.150)
ms:contentKeyID: 50489809
ms.date: 02/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将敏感信息规则与传输规则集成

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-01-14_

在 Microsoft Exchange 中，您可以创建 DLP 策略，其中不仅包含传统消息分类的规则和现有传输规则，而且还组合了这些与消息内的敏感消息的规则。现有传输规则框架会提供丰富的定义邮件策略的功能，包括软切换到硬切换的整个范围。示例包括：

  - 限制收件人与发件人之间的交互，包括组织内的部门组之间的交互。

  - 在组织内外，应用独立的通信策略。

  - 防止不适当的内容进入或离开组织。

  - 筛选机密信息。

  - 对特定个人发送或接收的邮件进行跟踪或存档。

  - 在传递之前重定向入站和出站邮件以便进行检查。

  - 对通过组织的邮件应用免责声明。

传输规则允许您应用消息策略到电子邮件消息，该消息通过邮箱服务器和边缘传输服务器上的传输服务中的传输管道传输。这些规则允许系统管理员加强邮件策略、有助于保持邮件更加安全、有助于保护邮件系统，且有助于防止事故信息丢失。有关传输规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) 或[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)。

## 传输规则框架内的敏感信息规则

通过引入您可以自定义的条件，敏感信息规则可以与传输规则框架集成：** 如果消息包含......敏感信息**。本条件可以使用消息内包含的一个或多个敏感信息类型配置。当使用该条件配置策略内的多个 DLP 策略或规则时，在任何条件匹配时将满足策略或规则。Exchange 策略规则将检查邮件的主题、正文和任何附件。如果规则匹配任何邮件组件，将应用规则操作。

敏感消息条件可以与任意已有传输规则组合来定义邮件策略。如果进行了组合，条件便与其他规则共同工作，并提供 AND 语法。例如，两个不同的条件将与 AND 语句一起添加，以使这两个都匹配要应用的操作。任意传输规则操作均可配置为包含敏感信息类型匹配的规则结果。通过传输规则代理可以扫描许多不同的文件类型，这将扫描邮件以强制执行传输规则。要了解有关支持的文件类型的详细信息，请参阅[使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md) (Exchange Server 2013) 或[Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/zh-cn/library/jj919236\(v=exchg.150\)) (Exchange Online)。

规则还可用于规则定义的例外定义。它们在例外定义中的使用独立于它们在规则内作为一个条件使用。这将提供定义规则的灵活性，该规则制定将多个信息类型应用为条件一部分，同时还区分条件中的信息类型。这将允许匹配特定传统消息分类规则等策略，但在执行您在策略内定义的操作之前不匹配其他敏感信息类型。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))Exchange Online

[创建自定义 DLP 策略](create-a-custom-dlp-policy-exchange-2013-help.md)

