---
title: '创建自定义 DLP 策略: Exchange 2013 Help'
TOCTitle: 创建自定义 DLP 策略
ms:assetid: b3299a39-9663-41e4-b76e-9d2f7879d486
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150550(v=EXCHG.150)
ms:contentKeyID: 50489722
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建自定义 DLP 策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-03-18_

通过自定义数据丢失防护 (DLP) 策略，可以创建条件、规则和操作，借此可帮助满足预先存在的 DLP 模板之一中未涵盖的组织特定需求。

可供您在单个策略中使用的规则条件包括所有传统传输规则以及 [使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) 中显示的敏感信息类型。有关传输规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange 2013) 或[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生产环境中运行 DLP 策略时，应在测试模式下启用这些策略。在此类测试中，建议配置示例用户邮箱并发送调用测试策略的测试邮件以便确认结果。有关测试的详细信息，请参阅<a href="test-a-mail-flow-rule-exchange-2013-help.md">测试邮件流规则</a>。</td>
</tr>
</tbody>
</table>


有关创建自定义 DLP 策略的更多管理任务，请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md)(Exchange 2013) 或 [DLP 过程](https://technet.microsoft.com/zh-cn/library/jj938003\(v=exchg.150\)) (Exchange Online)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：60 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“数据丢失防护 (DLP)”条目。

  - 若要创建新的自定义 DLP 策略，必须按照 Exchange 2013 的安装说明执行。有关部署的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>由于客户环境存在着差异，所以 Microsoft 客户支持服务 (CSS) 无法参与自定义正则表达式脚本（“RegEx 脚本”）的开发或测试。对于 RegEX 自定义脚本的开发、测试和调试，Office 365 客户将需要依靠内部 IT 资源。此外，Office 365 客户可以选择使用外部咨询资源，如 Microsoft 咨询服务 (MCS)。无论脚本开发资源是什么，CSS EXO 和 EOP 支持工程师都不得帮助客户自定义 RegEx 脚本查询。</td>
</tr>
</tbody>
</table>


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


## 使用 EAC 创建自定义 DLP 策略，而无需任何现有规则

1.  在 EAC 中，导航至“符合性管理”\>“防止数据丢失”。配置的任何现有策略都会显示在一个列表中。

2.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 图标旁边的箭头，然后选择“新建自定义策略”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果单击“添加”<img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" /> 图标（而不是箭头），则会基于模板创建新策略。有关使用模板的详细信息，请参阅<a href="how-to-new-dlp-data-loss-prevention-policy-template.md">从模板创建 DLP 策略</a>。</td>
    </tr>
    </tbody>
    </table>


3.  在“新自定义策略”页上，填写下列字段：
    
    1.  “名称”   添加将此策略与其他策略进行区分的名称。
    
    2.  **描述**   添加概括此策略的可选说明。
    
    3.  **选择状态**   为此策略选择模式或状态。在指定应启用新策略之前，不会完全启用新策略。策略的默认模式为测试而不进行通知。

4.  单击“保存”可完成创建新策略参考信息。策略会添加到已配置的所有策略的列表中，尽管尚未有任何规则或操作与此新自定义策略关联。

5.  双击刚创建的策略或将其选中，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

6.  在“编辑 DLP 策略”页上，单击“规则”。
    
    单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 添加新空白规则。可以使用所有传统传输规则和敏感信息类型来创建条件。
    
    为了避免混淆，在选择提供自己的字符串时，请为策略或规则的每个部分提供唯一的名称。为您提供了几个附加选项：
    
    1.  单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 图标旁边的箭头可添加有关发件人通知或允许替代的规则。
    
    2.  若要删除规则，请突出显示该规则并单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。
    
    3.  单击“更多选项”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标") 可为此规则添加其他条件和操作，包括强制执行的时间限制或是对此策略中其他规则的影响。

7.  单击“保存”完成策略修改并保存更改。

DLP 策略模板是 Microsoft Exchange 中可以帮助为邮件环境设计和应用可靠策略和遵从性系统的一种功能类型。有关合规性功能的详细信息，请参阅[邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md) (Exchange 2013) 或 [Exchange Online 的安全性和合规性](https://technet.microsoft.com/zh-cn/library/jj200706\(v=exchg.150\))。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)Exchange 2013

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))Exchange Online

[将敏感信息规则与传输规则集成](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

