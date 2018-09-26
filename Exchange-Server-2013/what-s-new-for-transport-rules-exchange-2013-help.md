---
title: '传输规则新增内容: Exchange 2013 Help'
TOCTitle: 传输规则新增内容
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50489901
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 传输规则新增内容

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-10-03_

在 Exchange Server 2013 中，对传输规则进行了几处改进。本主题简要概述了一些重要更改和增强功能。有关传输规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

## 对数据丢失预防策略的支持

Exchange 2013 中的数据丢失预防 (DLP) 功能可以帮助组织减少敏感数据的意外泄露。传输规则已进行更新，可支持创建随 DLP 策略附带并强制执行 DLP 策略的规则。若要了解有关传输规则中的 DLP 支持的详细信息，请参阅下列主题：

[将敏感信息规则与传输规则集成](https://technet.microsoft.com/zh-cn/library/jj150583(v=exchg.150))

[数据丢失预防](https://technet.microsoft.com/zh-cn/library/jj150527(v=exchg.150))

## 新谓词和操作

通过添加新谓词和操作扩展了传输规则的功能。下面列出的每个谓词都可以在创建传输规则时用作条件或例外。

有关使用这些新谓词和操作的详细信息，请参阅[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)和[传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)。

## 新谓词

  -  **AttachmentExtensionMatchesWords**   用于检测包含具有特定扩展名的附件的邮件。

  -  **AttachmentHasExecutableContent**   用于检测包含具有可执行文件内容的附件的邮件。

  -  **HasSenderOverride** 用于检测发件人在其中选择替代 DLP 策略限制的邮件。

  -  **MessageContainsDataClassifications**   用于检测邮件正文和任何附件中的敏感信息。有关可用数据分类的完整列表，请参阅[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)。

  -  **MessageSizeOver**   用于检测整体大小大于或等于指定限制的邮件。

  -  **SenderIPRanges**   用于检测从一组特定 IP 地址范围发送的邮件。

## 新操作

  -  **GenerateIncidentReport**   生成发送给指定 SMTP 地址的事件报告。该操作还有一个名为 *IncidentReportOriginalMail* 的参数，该参数接受以下两个值之一：IncludeOriginalMail 或 DoNotIncludeOriginalMail。

  -  **NotifySender**   控制如何通知违反 DLP 策略的邮件的发件人。可以选择仅通知发件人并正常路由邮件，也可以选择拒绝邮件并通知发件人。

  -  **StopRuleProcessing**   停止对邮件处理所有后续规则。

  -  **ReportSeverityLevel**   在事件报告中设置指定严重性级别。此操作的值为：Informational、Low、Medium、High 和 Off。

  -  **RouteMessageOutboundRequireTLS**   在组织外部路由此邮件时需要传输层安全性 (TLS) 加密。如果不支持 TLS 加密，则会拒绝邮件，不进行传递。

## 传输规则中的其他更改

  - **支持扩展正则表达式语法**Exchange 2013 中的传输规则基于 Microsoft.NET Framework 正则表达式 (regex) 功能，现在支持扩展正则表达式语法。

  - **传输规则代理调用**Exchange 2013 中针对传输规则的关键体系结构更改是对 onResolvedMessage 调用传输规则代理。在以前版本的 Exchange 中，是对 onRoutedMessage 调用规则代理。此更改允许我们添加新操作，如需要 TLS，这可能会更改邮件的路由方式。若要了解有关 Exchange 2013 中的传输规则体系结构的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

  - **邮件跟踪日志中的详细传输规则信息**   有关传输规则的详细信息现在包含在邮件跟踪日志中。这些信息包括对特定邮件触发的规则以及由于处理这些规则而执行的操作。

  - **新规则监视功能**Exchange 2013 监视配置的传输规则并度量在创建规则时及常规操作过程中运行这些规则的成本。Exchange 可以检测在邮件传递中导致延迟的规则并针对这些规则生成警报。

