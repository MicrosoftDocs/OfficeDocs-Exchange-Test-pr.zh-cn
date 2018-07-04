---
title: '从 Exchange 2013 导出 DLP 敏感信息类型: Exchange Online Help'
TOCTitle: 从 Exchange 导出 DLP 敏感信息类型
ms:assetid: 8f02fbc2-dd1c-4276-be1a-517a43fe39b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn479225(v=EXCHG.150)
ms:contentKeyID: 59636400
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从 Exchange 2013 导出 DLP 敏感信息类型

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-05-04_

您可以查看或不通过导出策略，将它们另存为 XML 文件，并修改该 XML 文件中使用Exchange 管理中心 (EAC) 或Exchange 命令行管理程序 cmdlet DLP 策略中更改的详细信息。通常您会然后 XML 文件重新导入Exchange。这种方式，策略可以编辑独立的Exchange。但是，他们必须满足特定格式的要求，也称为 XML 架构，才能正常工作。

有关与 DLP 相关的更多管理任务，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;数据丢失防护 (DLP)\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

EAC 无法将 DLP 策略或模板导出到外部文件。使用 Exchange 命令行管理程序 执行此任务。

## Exchange 命令行管理程序用于导出 DLP 敏感信息类型

本示例将所有 DLP 敏感信息类型及其属性导出到路径 C:\\My Documents\\exportedInformationTypes.xml 中的一个 XML 文件。我们建议对您当前的 DLP 敏感信息类型集进行备份。进行备份的一种方法是将其导出并立即复制，然后重命名该 XML 文件。

1.  打开 Exchange 命令行管理程序。

2.  键入 **Get-ClassificationRuleCollection**，您的组织的敏感信息类型应该会显示在屏幕上。如果您还没有创建您自己的敏感信息类型，您将仅看到默认的内置敏感信息类型集合\&quot;Microsoft 规则包\&quot;。

3.  键入 **$ruleCollections = Get-ClassificationRuleCollection**，将敏感信息类型存储在一个变量中。

4.  现在键入 **Set-Content -path "C:\\My Documents\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection**，创建包含所有这些数据的格式化 XML 文件。

现在您可以编辑 XML 文件，根据需要调整策略了。要了解如何自定义内置的敏感信息类型，请参阅[自定义内置 DLP 敏感信息类型](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)。有关将策略导入回 Exchange 的详细信息，请参阅[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)。

## 有关详细信息，请参阅以下内容：

[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

[自定义内置 DLP 敏感信息类型](customize-the-built-in-dlp-sensitive-information-types-exchange-2013-help.md)

[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

