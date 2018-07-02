---
title: 方法：新 DLP（数据丢失保护）策略模板
TOCTitle: 从模板创建 DLP 策略
ms:assetid: 4432ef8b-6108-48d3-b2af-43ef5b40d2bc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150515(v=EXCHG.150)
ms:contentKeyID: 50489660
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 从模板创建 DLP 策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-01-14_

在 Microsoft Exchange Server 2013 中，可以使用数据丢失预防 (DLP) 策略模板帮助满足组织的邮件策略和遵从性需求。这些模板包含预先生成的规则集，有助于管理与几个常见法律和法规要求关联的邮件数据。要查看 Microsoft 提供的所有模板的列表，请参阅 [在 Exchange 中提供的 DLP 策略模板](dlp-policy-templates-supplied-in-exchange-exchange-2013-help.md)。所提供的示例 DLP 模板可以帮助您管理：

  - 格雷姆-里奇-比利雷法案 (GLBA) 数据

  - 支付卡行业数据安全标准 (PCI-DSS)

  - 美国个人身份信息（美国 PII)

您可以自定义或按原样使用任何 DLP 模板。DLP 策略模板基于包含新条件或谓词和操作的传输规则。DLP 策略支持类型齐全的传统传输规则，而且您可以在建立 DLP 策略之后添加额外的规则。有关策略模板的详细信息，请参阅 [DLP 策略模板](dlp-policy-templates-exchange-2013-help.md)。若要了解有关传输规则功能的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013) 或[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)。开始强制执行策略后，您可以通过参阅以下主题来了解如何查看结果：

Exchange 2013: [查看 DLP 策略检测报告](view-dlp-policy-detection-reports-exchange-2013-help.md)

Exchange Online: [查看 DLP 策略检测报告](https://technet.microsoft.com/zh-cn/library/dn904484\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生产环境中运行 DLP 策略时，应在测试模式下启用这些策略。在此类测试中，建议配置示例用户邮箱并发送调用测试策略的测试邮件以便确认结果。</td>
</tr>
</tbody>
</table>


有关通过模板创建 DLP 策略的其他管理任务，请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md) (Exchange Server 2013) 或 [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\)) (Exchange Online)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟

  - 确保按[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)中所述设置 Exchange 2013。

  - 在组织中配置管理员和用户帐户并验证基本邮件流。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“数据丢失防护 (DLP)”条目

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用 EAC 通过模板配置 DLP 策略

1.  在 EAC 中，导航到“合规管理”\>“数据丢失防护”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您也可以通过其他方法选择此操作：单击“添加”<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /> 图标旁边的箭头，然后从下拉菜单中选择“根据模板新建 DLP 策略”。</td>
    </tr>
    </tbody>
    </table>


2.  在“根据模板新建 DLP 策略”页面上，填写下列字段：
    
    1.  **名称**   添加一个可将此策略与其他策略区分开来的名称。
    
    2.  **描述**   添加概括此策略的可选说明。
    
    3.  **选择模板**   选择适当的模板开始创建新策略。
    
    4.  **更多选项**   选择模式或状态。在指定应启用新策略之前，不会完全启用新策略。策略的默认模式为测试而不进行通知。
    
    5.  单击“保存”可完成策略创建。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除了特定模板中的规则之外，组织可能还具有应用于邮件环境中监管数据的其他期望或公司策略。Exchange 2013 使您可以方便地更改基本模板，以便添加操作，从而使 Exchange 邮件环境符合自己的要求。</td>
</tr>
</tbody>
</table>


在 Exchange 2013 环境中保存了策略之后，可以通过编辑这些策略中的规则来修改策略。示例规则更改可能包括使特定人员从策略中排除，或是在发现邮件包含敏感内容时发送通知并阻止邮件传递。有关编辑策略和规则的详细信息，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。

如果要更改已在 Exchange 2013 中创建的 DLP 策略，必须导航到“编辑 DLP 策略”页面上的特定策略的规则集，并使用此页上提供的工具。

某些策略允许添加为邮件调用 RMS 的规则。在添加操作以使用这些类型的规则之前，必须在 Exchange 服务器上配置 RMS。

对于任何 DLP 策略，可以更改规则、操作、例外、强制执行时间段或是否强制执行策略中的其他规则，并且可以为每个策略添加自己的自定义条件。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[DLP 策略模板](dlp-policy-templates-exchange-2013-help.md)

