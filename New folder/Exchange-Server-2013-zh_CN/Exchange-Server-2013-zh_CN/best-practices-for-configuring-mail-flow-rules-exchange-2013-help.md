---
title: '配置邮件流规则的最佳做法: Exchange Online Help'
TOCTitle: 配置邮件流规则的最佳做法
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65330365
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置邮件流规则的最佳做法

 

_**适用于：** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

请遵循下面推荐的这些 Exchange 传输规则最佳做法，以避免出现常见的配置错误。每条建议都有主题链接。单击链接后，可查看示例和分步操作说明。

## 测试您的规则

为了确保电子邮件不会出现意外状况，并确保您真正满足规则的业务、法律或合规性要求，请务必对其进行全面测试。由于选项有很多，而且规则也可以互相交互，因此请务必测试邮件，既测试与规则匹配的情况，也测试与规则不匹配的情况，以免因疏忽而导致规则过于宽泛。若要了解测试规则的所有选项，请参阅[测试邮件流规则](test-a-mail-flow-rule-exchange-2013-help.md)。

## 确定规则的范围

请确保您的规则仅适用于您预期的邮件。例如：

  - **限制规则仅应用于传入组织或从组织传出的邮件**
    
    默认情况下，新规则应用于由组织中人员发送或接收的邮件。因此，如果您希望仅通过一种方式应用规则，请务必在规则的条件中进行指定。有关示例，请参阅[常见的附件阻止方案](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)。

  - **根据发件人或收件人的域限制规则**
    
    默认情况下，新规则应用于从任何域发送或接收的邮件。有时，您希望将规则应用于除某个域以外的所有域，或只应用于某个域。有关示例，请参阅[使用传输规则创建基于域或基于用户的安全发件人或阻止发件人列表](https://technet.microsoft.com/zh-cn/library/dn198251\(v=exchg.150\))。

有关传输规则的所有条件和例外的完整列表，请参阅：

  - [在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\))

  - [传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [邮件流规则条件和例外 （谓语） 在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj919234\(v=exchg.150\))

## 了解何时需要两个规则

有时，需要两个规则才能执行相应的操作。由于传输规则是按顺序进行处理，因此可以将多个规则应用于同一邮件。例如，如果一个操作是要阻止邮件，同时您还要应用另一操作（如将邮件复制到发件人的管理器或更改通知邮件的主题），则需要使用两个规则。第一个规则可将邮件复制到发件人的管理器中并更改主题，第二个规则可阻止邮件。

如果您使用类似这样的两个规则，请确保条件完全相同。若要查看示例，请查看[常见邮件审批方案](common-message-approval-scenarios-exchange-2013-help.md)中的示例 3、[常见的附件阻止方案](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)中的示例 3 和[组织范围内的免责声明、签名、脚注或标头](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)。

## 请勿在对话中对每封电子邮件重复应用一个操作

对话中的电子邮件链可以包括许多单个邮件。如果对线程中的每封邮件都重复应用一个操作，可能会让人感到不耐烦。例如，如果您要执行一个操作（如添加免责声明），您可能希望仅将它应用于线程中的第一封邮件。如果是这样，请对已包含免责声明文本的邮件添加例外。 有关示例，请参阅[组织范围内的免责声明、签名、脚注或标头](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)。

## 了解何时停止规则处理

有时，在规则匹配时，有必要停止规则处理。例如，如果一个规则用于阻止包含附件的邮件，另一个规则用于向模式匹配的邮件插入免责声明，那么您可能应该在邮件遭到阻止后停止规则处理。无需执行其他操作。

若要在规则触发后停止规则处理，请选中规则中的\&quot;停止处理其他规则\&quot;复选框。

## 如果您有许多要匹配的关键字或模式，则可以通过文件加载它们。

例如，您不妨阻止发送包含不可接受或错误的字词列表的电子邮件。您可以创建一个包含这些字词和短语的文本文件，然后使用 Windows PowerShell 设置一个传输规则来阻止包含这些内容的邮件。

文本文件可以包含用于各种模式的正则表达式。这些表达式不区分大小写。常见的正则表达式包括：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>表达式</strong></p></td>
<td><p><strong>匹配</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>任何单个字符</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>任何其他字符</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>任何十进制数字</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p><em>character_group</em> 中的任何单个字符。</p></td>
</tr>
</tbody>
</table>


若要查看示例，了解包含正则表达式的文本文件和要使用的 Exchange 模块 Windows PowerShell 命令，请参阅[使用邮件流规则根据字词、短语或模式的列表路由电子邮件](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)。

若要了解如何使用正则表达式指定模式，请参阅[正则表达式参考](https://go.microsoft.com/fwlink/p/?linkid=532394)。

