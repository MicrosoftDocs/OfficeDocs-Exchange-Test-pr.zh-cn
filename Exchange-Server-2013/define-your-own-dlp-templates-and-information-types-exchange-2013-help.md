---
title: '定义您自己的 DLP 模板和信息类型: Exchange 2013 Help'
TOCTitle: 定义您自己的 DLP 模板和信息类型
ms:assetid: f4622dba-3347-4758-b4a2-f01b043c908c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674310(v=EXCHG.150)
ms:contentKeyID: 50491936
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 定义您自己的 DLP 模板和信息类型

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-01-14_

您可以制作独立于 Microsoft Exchange Server 2013 的数据丢失防护 (DLP) 策略模板为 XML 文件，然后使用 Exchange 管理中心或 Exchange 命令行管理程序导入它们。该部分介绍创作和调整 DLP XML 文件以在 DLP 解决方案内使用的流程和详细信息。您无需制作自己的 DLP XML 文件，因为 Exchange 管理中心提供了让您快速使用现有 DLP 策略模板和传输规则扫描邮件的方式。

寻找与 DLP 策略模板相关的管理任务？请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) 或 [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\)) (Exchange Online)。

> [!NOTE]  
> Exchange 2013：DLP 是一项高级功能，要求使用 Exchange 企业客户端访问许可证 (CAL)。有关 CAL 和服务器授权的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</a>（Exchange Server 授权）。
> Exchange Online：DLP 是一项高级功能，要求使用 Exchange Online 计划 2 订阅。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online Licensing</a>（Exchange Online 授权）。


> [!IMPORTANT]  
> 这超出本文档范围，推荐了有关敏感信息规则的文件打包或部署指导的业务模式，或讨论如何分发此类规则。此外，本文档不会讨论保护机制，如自定义开发规则的加密，也不会讨论如何部署此类机制。


## 扩展信息类型以满足您的需要

以下部分介绍了您必须了解的概念和 XML 架构定义，以开始为 DLP 策略模板和敏感数据规则包创建您自己的 XML 文件，这可导入 Exchange 2013 并用作 DLP 策略。

Microsoft Exchange 中的 DLP 帮助您将组织特定的策略应用于敏感信息中。DLP 解决方案强大之处的一个重要因素是能够正确标识可能对组织、法规需求、地理位置或其他业务方面独有的机密或敏感信息。尽管 Microsoft 在产品内提供了策略模板和敏感信息类型让您开始使用，但是您的独特业务需求可能需要自定义数据丢失防护解决方案。出于这个原因，Microsoft 提供了方式让您在分类规则包内创建和导入自己的 DLP 策略模板或自己的敏感信息定义。精确的 DLP 解决方案依赖于配置正确的规则集用于敏感信息检测引擎，提供更高级别的保护，同时最大程度减少误报和负面影响。

## 开发自己的 DLP 策略模板

您可以编写自己的 DLP 策略模板 XML 文件并导入它。Exchange 中提供的这种 DLP 解决方案扩展方法将允许您构建完全匹配您的 DLP 要求的 DLP 策略。

管理自定义模板及其相关策略与管理您基于 Microsoft 所提供模板创建的 DLP 策略类似。在典型的 DLP 策略生命周期中，您将执行以下操作：

1.  创建您自己的 DLP 策略模板，即自定义 XML 文件。若要了解详细信息，请参阅[开发 DLP 策略模板文件](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

2.  导入自定义模板。若要了解详细信息，请参阅[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)。

3.  创建基于自定义模板的 DLP 策略。若要了解详细信息，请参阅[从模板创建 DLP 策略](https://technet.microsoft.com/zh-cn/library/jj150515(v=exchg.150))。

4.  重复步骤 1 和 2，更新您的自定义模板。

5.  删除自定义模板。若要了解详细信息，请参阅[Remove-DlpPolicyTemplate](https://technet.microsoft.com/zh-cn/library/jj215739\(v=exchg.150\))。

有关 XML 架构定义以及与开发您自己的模板相关的概念详细清晰，请参阅[开发 DLP 策略模板文件](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

## 在分类规则包中开发您自己的敏感信息类型和匹配逻辑

您可以在分类规则包中编写您自己的敏感信息定义，这是一个 XML 文件并可作为您的 DLP 解决方案一部分导入。敏感信息检测引擎提供深入内容分析能力以识别敏感信息，如信用卡号、社会保障号和公司知识产权。该引擎由可配置说明或规则集控制，以扫描和分析内容。该规则被组合到分类规则包，这是一个遵照标准化规则包 XML 架构定义的 XML 文档。下面介绍了如何开发自己的规则。

1.  创建您自己的敏感信息类型，即自定义 XML 文件。若要了解详细信息，请参阅[开发敏感信息规则包](technical-description-of-xml-schema-for-dlp-rule-packages.md)。

2.  导入您的敏感信息类型。若要了解详细信息，请参阅[New-ClassificationRuleCollection](https://technet.microsoft.com/zh-cn/library/jj218619\(v=exchg.150\))。

3.  创建基于您的信息类型的自定义模板。若要了解详细信息，请参阅[开发敏感信息规则包](technical-description-of-xml-schema-for-dlp-rule-packages.md)。

4.  重复步骤 1 和 2，更新您的自定义模板。

5.  删除自定义模板。若要了解详细信息，请参阅[Remove-ClassificationRuleCollection](https://technet.microsoft.com/zh-cn/library/jj218670\(v=exchg.150\))。

有关规则包的详细信息，请参阅[开发敏感信息规则包](technical-description-of-xml-schema-for-dlp-rule-packages.md)和[规则包的匹配方法和技术](technical-description-of-xsd-rule-matching-for-dlp-rule-packages.md)。

## 了解规则包中的规则类型

规则包内的规则配置了检测定义明确的内容特性的过程，例如，查找驾驶执照编号的规则。可以使用两种主要的规则类型：实体和相关性。

*实体*规则定位于定义明确（以及固定时间的）标识符，如美国社会保障号。实体代表可计算模式的集合。模式使用明确的主匹配标识符定义匹配集合。实体示例是驾驶执照。

*相关性*规则定位于某些类型的文件，如公司财务报表。相关性代表独立证据的集合。证据是某个相关性内的所需匹配聚合。相关性的一个示例是美国《萨班斯-奥克斯利法案》。

## 详细信息

[数据丢失预防](https://technet.microsoft.com/zh-cn/library/jj150527(v=exchg.150))

[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

[New-ClassificationRuleCollection](https://technet.microsoft.com/zh-cn/library/jj218619\(v=exchg.150\))

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange Server 2013

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))Exchange Online

[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

