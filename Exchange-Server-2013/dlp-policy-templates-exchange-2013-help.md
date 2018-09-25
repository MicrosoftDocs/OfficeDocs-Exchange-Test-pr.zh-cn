---
title: 'DLP 策略模板: Exchange 2013 Help'
TOCTitle: DLP 策略模板
ms:assetid: c7b1a8e4-30d9-4409-85c5-f85ae023737d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657730(v=EXCHG.150)
ms:contentKeyID: 50491680
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DLP 策略模板

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-01-14_

可使用数据丢失防护 (DLP) 策略模板在 Microsoft Exchange 2013 中开始使用 DLP 解决方案。DLP 策略模板是一个策略模型。您可以选择一个模板开始构建自己自定义的 DLP 策略的流程。在您的 DLP 策略中，可自定义规则来确保其符合您对数据丢失防护的业务需求。数个策略模板由 Microsoft 提供，但是这些模板并非在 Exchange 中实施数据丢失防护解决方案的唯一方式。

寻找与 DLP 策略模板相关的管理任务？请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md)。

**目录**

扩展模板和信息类型以满足您的需求

在分类规则包中创建自己的新 DLP 策略模板或自己的敏感信息类型

包括采用现有传输规则的 DLP 功能

使用 Microsoft 创建的 DLP 策略

详细信息

## 扩展模板和信息类型以满足您的需求

您可从 Microsoft 合作伙伴或从您自行开发的文件合并敏感内容定义和策略模板，作为 DLP 策略模板、信息类型和已在 Exchange 2013 中提供的规则的补充。在此提供了数种方式，通过这些方式您可添加自己的唯一 DLP 内容并扩展 DLP 功能。已经由 Microsoft 提供的模板是开始使用 DLP 解决方案的便利方法。要使用自己的唯一 DLP 策略模板文件扩展 DLP 功能，必须理解独立于 Exchange 创建的策略模板的 XML 架构要求。要了解有关与 DLP 策略模板关联的 Exchange Management Shell cmdlets 的详细信息，请参阅 [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\)) 中与 `Get-DlpPolicyTemplate` 相关的 cmdlets。此外，可在了解合并它们的格式和步骤之后，定义自己的敏感内容类型。要了解有关与 DLP 策略模板关联的 Exchange Management Shell cmdlets 的详细信息，请参阅 [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\)) 中与 `Get-ClassificationRuleCollection` 相关的 cmdlets。

> [!CAUTION]  
> 在生产环境中强制执行这些 DLP 策略之前，应在测试模式下启用这些策略。在此类测试中，我们建议配置示例用户邮箱并发送调用测试策略的测试邮件以便确认结果。


## 在分类规则包中创建自己的新 DLP 策略模板或自己的敏感信息类型

您可创建除 Exchange 之外的符合 Microsoft 提供的特定 XML 架构定义的 DLP 策略模板文件，然后将文件导入系统，从而可从中创建 DLP 策略。通过创建自己的模板文件，可定义 Microsoft 尚未提供的自己的 DLP 策略的模型。这与通过使用 Exchange 管理中心创建 DLP 策略不同，后者通常在策略模板可用后发生。如果创建独立于 Exchange 的策略模板，要将其导入方可使用它来扫描邮件。您也可创建除了 Microsoft 在 Exchange 中定义的敏感信息外，创建自己的敏感信息定义。存在一个 DLP 策略模板文件和分类规则包的单独 XML 架构定义。要开始了解这些信息，请参阅下列信息：

  -  [定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

  -  [从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

## 包括采用现有传输规则的 DLP 功能

您可将 DLP 检测功能与传统传输规则合并，无需创建新的 DLP 策略。如果在之前版本的 Exchange 中创建了复杂的规则组，并且您希望复制它们或者在 Exchange 2013 中添加敏感信息检测，则可使用 Exchange 管理中心中的传输规则编辑器或 Exchange 命令行管理程序来合并这两个功能。要开始了解这些信息，请参阅下列信息：

  -  [邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

  -  [Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)

  -  [管理邮件流规则](https://technet.microsoft.com/zh-cn/library/jj657505(v=exchg.150))
    
  -  [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\))

## 使用 Microsoft 创建的 DLP 策略

众多 DLP 政策由 Microsoft 提供。这是开始使用实施起来非常灵活和简便的 DLP 解决方案的最便利方式。您可以始终使用提供的策略作为启动，并进一步将其自定义，以满足自己的要求。要开始了解这些信息，请参阅下列信息：

  - [在 Exchange 中提供的 DLP 策略模板](https://technet.microsoft.com/zh-cn/library/jj150530(v=exchg.150))

  - [从模板创建 DLP 策略](https://technet.microsoft.com/zh-cn/library/jj150515(v=exchg.150))

## 详细信息

[数据丢失预防](https://technet.microsoft.com/zh-cn/library/jj150527(v=exchg.150))

