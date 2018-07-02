---
title: '数据丢失预防: Exchange 2013 Help'
TOCTitle: 数据丢失预防
ms:assetid: 7c8ed3c1-ca91-4d9b-b16b-0a2b8ac89730
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150527(v=EXCHG.150)
ms:contentKeyID: 50489691
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 数据丢失预防

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

了解 Exchange Server 2013 和 Exchange Online 中的 DLP 策略，包括其中所包含的内容以及如何对其进行测试。您还将了解 Exchange DLP 中的新增功能。

由于将电子邮件大量用于包含敏感数据的业务关键通信，因此数据丢失预防 (DLP) 是企业邮件系统的一个重要问题。为了强制执行针对这类数据的遵从性要求并管理这类数据在电子邮件中的使用（而不影响工作人员的工作效率），DLP 功能使敏感数据的管理比以往更加简单。有关 DLP 的概念概述，请观看以下视频。

> [!VIDEO https://www.microsoft.com/zh-cn/videoplayer/embed/31f2b48e-93ed-4be3-b46d-e7230c0fed8f]

DLP 策略是包含条件集的简单数据包，这些数据包由您在 Exchange 管理中心 (EAC) 中创建然后激活以筛选电子邮件及附件的传输规则、操作和例外组成。可以创建 DLP 策略，但选择不激活它。这使您可以测试策略而不影响邮件流。DLP 策略可以使用现有传输规则的完整功能。事实上，已在 Microsoft Exchange Server 2013 和 Exchange Online 中创建了一些新传输规则类型，以便实现新 DLP 功能。传输规则的一个重要新功能是一种用于对可以并入到邮件流处理中的敏感信息进行分类的新方法。此新 DLP 功能通过关键字匹配、字典匹配、正则表达式计算和其他内容检查来执行深度内容分析，以检测违反组织 DLP 策略的内容。Exchange Online 和 Exchange 2013 SP1 的最新版本添加了[文档指纹](overview-of-document-fingerprinting-in-exchange.md)，它可以帮助您检测标准表单中的敏感信息。有关传输规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online) 和[将敏感信息规则与传输规则集成](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。您还可以通过使用 Exchange 命令行管理程序 cmdlet 来管理 DLP 策略。有关策略和遵从性 cmdlet 的详细信息，请参阅[策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\))。

除了可自定义的 DLP 策略本身之外，还可以通知电子邮件发件人他们可能将违反一个策略 — 甚至在发送有问题的邮件之前进行此操作。您可以通过配置策略提示来实现这点。策略提示类似于邮件提示，可配置为在 Microsoft Outlook 2013 客户端中提供简短说明，提供有关邮件创建者可能违反策略的信息。在 Exchange Online 的最新版本和 Exchange 2013 SP1 中，策略提示也会显示在 Outlook Web App 和 适用于设备的 OWA 中。有关详细信息，请参阅[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange Online：DLP 是一项高级功能，要求使用 Exchange Online 计划 2 订阅。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online Licensing</a>（Exchange Online 授权）。<br />
Exchange 2013：DLP 是一项高级功能，要求使用 Exchange 企业客户端访问许可证 (CAL)。有关 CAL 和服务器授权的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</a>（Exchange Server 授权）。<br />
<strong>Exchange Enterprise CAL with Services：</strong>如果您是拥有混合部署的 Exchange Enterprise CAL with Services 客户（即您的某些邮箱是本地的，某些邮箱位于 Exchange Online 中），则有一个需要注意的行为区分。DLP 策略在 Exchange Online 中应用。因此，从一个内部部署用户发送到另一个内部部署用户的邮件不应用 DLP 策略，因为该邮件没有离开内部部署基础结构。</td>
</tr>
</tbody>
</table>


要查找与数据丢失防护相关的管理任务吗？请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md) (Exchange 2013) 或 [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\)) (Exchange Online)。

**目录**

制定保护敏感数据的策略

DLP 策略中的敏感信息类型

与传统邮件分类一起检测敏感信息

使用文档指纹检测敏感的表单数据

策略提示向用户通知敏感内容预期

有关 DLP 处理的邮件的信息

安装先决条件

详细信息

## 制定保护敏感数据的策略

数据丢失防护可以帮助您标识和监视已在策略条件中定义的许多敏感信息类别，如私人身份证号码或信用卡号码。可以选择定义自己的自定义策略和传输规则，或使用 Microsoft 提供的预定义 DLP 策略模板来快速开始。有关包含的策略模板的详细信息，请参阅 [在 Exchange 中提供的 DLP 策略模板](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。*策略模板*包含一些您可以选择的条件、规则和操作，以便创建并保存可帮助您检查邮件的实际 DLP 策略。策略模板是一些模型，您可以选择这些模型或用于构建自己的特定规则，以创建满足您的数据丢失防护需求的策略。

可通过三种不同的方法开始使用 DLP：

1.  **应用 Microsoft 提供的现成模板。**   开始使用 DLP 策略的最快速方式是使用模板创建并实现新策略。这可使您省去从头构建新规则集的工作。您需要了解要检查的数据类型或是尝试应对的遵从性法规。您还需要了解处理这类数据的组织期望。有关详细信息，请参阅 [在 Exchange 中提供的 DLP 策略模板](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)和[从模板创建 DLP 策略](how-to-new-dlp-data-loss-prevention-policy-template.md)。

2.  **从组织外部导入预生成的策略文件。**   您可以导入独立软件供应商已在邮件环境外部创建的策略。通过此方式可以扩展 DLP 解决方案以满足您的业务要求。有关详细信息，请参阅[Microsoft 合作伙伴的策略模板](policy-templates-from-microsoft-partners-exchange-2013-help.md)、[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)和[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)。

3.  **创建不带任何预先存在的条件的自定义策略。**   您的企业可能具有自己监视邮件系统内已知存在的特定数据类型的要求。可以完全自己创建自定义策略，以便开始对自己独有的邮件数据进行检查和操作。需要了解在其中强制执行 DLP 策略的环境的要求和约束，以便创建这类自定义策略。有关详细信息，请参阅[创建自定义 DLP 策略](create-a-custom-dlp-policy-exchange-2013-help.md)。

在添加了策略之后，可以查看和更改其规则、使策略处于不活动状态或完全删除它。[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)主题中提供了这些操作的步骤。

## DLP 策略中的敏感信息类型

创建或更改 DLP 策略时，可以包含具有敏感信息检查的规则。[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)主题中列出的敏感信息类型可供您在策略中使用。在策略中建立的条件（如在执行某个操作之前必须发现某种内容的次数或是该操作的具体内容）可以在新自定义策略中进行自定义，以便满足特定策略要求。有关创建 DLP 策略的详细信息，请参阅[创建自定义 DLP 策略](create-a-custom-dlp-policy-exchange-2013-help.md)。有关整套传输规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)。

为了方便您使用敏感信息相关的规则，Microsoft 提供了已包括一些敏感信息类型的策略模板。但是不能将此处列出的所有敏感信息类型的条件都添加到策略模板中，因为这些模板旨在帮助您关注组织中最常见的合规性相关数据类型。有关预先生成的模板的详细信息，请参阅[在 Exchange 中提供的 DLP 策略模板](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。可以为组织创建大量 DLP 策略并全部启用，以便检查许多不同类型的信息。还可以创建不基于现有模板的 DLP 策略。若要开始创建这样一个策略，请参阅[创建自定义 DLP 策略](create-a-custom-dlp-policy-exchange-2013-help.md)。有关敏感信息类型的详细信息，请参阅[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)。

## 使用文档指纹检测敏感的表单数据

对于 Exchange 2013 SP1 和最新版本的 Exchange Online，您可以使用[文档指纹](overview-of-document-fingerprinting-in-exchange.md)轻松创建基于标准表单的敏感信息类型。若要了解如何保护表单数据，请参阅[使用文档指纹保护表单数据](protect-form-data-with-document-fingerprinting-exchange-2013-help.md)。

## 策略提示向用户通知敏感内容预期

您可以使用策略提示通知邮件在电子邮件发件人撰写电子邮件时通知他们可能的遵从性问题。在 DLP 策略中配置策略提示时，只有在发件人电子邮件中的某些内容符合策略中描述的条件时才显示通知邮件。策略提示类似于 Microsoft Exchange 2010 中引入的邮件提示。有关详细信息，请参阅[策略提示](technical-overview-of-policy-tips-in-exchange-online-and-exchange-2013.md)。

## 与传统邮件分类一起检测敏感信息

Exchange 2013 和 Exchange Online 提供一种新方法，帮助您在与传统邮件分类进行比较时管理邮件及附件数据。DLP 解决方案强大之处的一个重要因素是能够正确标识可能对组织、法规需求、地理位置或其他业务需求独有的机密或敏感内容。通过将新体系结构用于深入内容分析并使用您通过 DLP 策略中的规则建立的检测标准，Exchange 2013 可以实现这一点。在 Exchange 2013 中帮助防止数据丢失依赖于配置正确的敏感信息规则集，以便它们可提供高度防护，同时最大程度减少邮件流中断及误报和负面影响。这些规则类型在整个 DLP 信息内称为敏感信息检测，在传输规则提供的框架内工作以便启用 DLP 功能。

有关这些新功能的详细信息，请参阅[将敏感信息规则与传输规则集成](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)。传统邮件分类字段仍可应用于 Exchange 中的邮件，这些字段也可与新敏感信息检测一起组合到单个 DLP 策略，或并发运行以便在 Exchange 内单独对它们进行评估。若要详细了解旧版 Exchange 2010 邮件分类，请参阅 TechNet 库中的[了解邮件分类](https://go.microsoft.com/fwlink/?linkid=266612)。

## 有关 DLP 处理的邮件的信息

要让 Exchange 2013 可获取有关环境中的邮件和 DLP 策略检测的信息，请参阅 [查看 DLP 策略检测报告](view-dlp-policy-detection-reports-exchange-2013-help.md)和[创建 DLP 策略检测的事件报告](create-incident-reports-for-dlp-policy-detections-exchange-2013-help.md)。与 DLP 检测相关的数据会高度集成到 Exchange 2013 的送达报告邮件跟踪工具中。

有关 Exchange Online，请参阅 [查看 DLP 策略检测报告](https://technet.microsoft.com/zh-cn/library/dn904484\(v=exchg.150\))和[为 DLP 策略检测创建事件报告](https://technet.microsoft.com/zh-cn/library/dn904486\(v=exchg.150\))。

## 安装先决条件

要使用 DLP 功能，必须为 Exchange 2013 或 Exchange Online 配置至少一个发件人邮箱。数据丢失防护是一项高级功能，要求使用企业版客户端访问许可证 (CAL)。有关 Exchange 2013 入门的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。有关 Exchange Online 入门的详细信息，请参阅[Exchange Online](https://technet.microsoft.com/zh-cn/library/jj200580\(v=exchg.150\))。

## 详细信息

Exchange 2013

  - [邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md)

  - [DLP 过程](dlp-procedures-exchange-2013-help.md)

  - [查看 DLP 策略检测报告](view-dlp-policy-detection-reports-exchange-2013-help.md)

  - [文档指纹](overview-of-document-fingerprinting-in-exchange.md)

  - [策略和合规性 cmdlet](https://technet.microsoft.com/zh-cn/library/dd298082\(v=exchg.150\))

Exchange Online

  - [Exchange Online 的安全性和合规性](https://technet.microsoft.com/zh-cn/library/jj200706\(v=exchg.150\))

  - [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\))

  - [查看 DLP 策略检测报告](https://technet.microsoft.com/zh-cn/library/dn904484\(v=exchg.150\))

  - [文档指纹](overview-of-document-fingerprinting-in-exchange.md)

