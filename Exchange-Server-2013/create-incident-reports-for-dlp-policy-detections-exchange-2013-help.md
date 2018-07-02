---
title: '创建 DLP 策略检测的事件报告: Exchange 2013 Help'
TOCTitle: 创建 DLP 策略检测的事件报告
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 50489770
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建 DLP 策略检测的事件报告

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

在 Exchange Server 2013 中，可以建立用于在 DLP 策略规则集中创建事件报告的操作。此外，还可以指示应向其发送报告的人员以及要对原始邮件执行的操作。事件报告可以包含以下任何信息。

## 事件管理报告的内容

用户使用“生成事件报告”操作可以将事件报告发送给事件管理邮箱。仅当在策略中应用了“生成事件报告”操作时，才会为每封邮件生成一个事件报告。

以下是事件报告模板中的行名称的完整列表。“格式”列描述如何识别报告中的每个字段。“可选字段”列为每个规则匹配指定可以不包含在报告中的字段。“特定于 DLP”列显示了因为 DLP 功能而存在的字段。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>行</strong> <strong>名称</strong></p></td>
<td><p><strong>描述</strong></p></td>
<td><p><strong>格式</strong></p></td>
<td><p><strong>可选字段</strong></p></td>
<td><p><strong>特定于 DLP</strong></p></td>
</tr>
<tr class="even">
<td><p>邮件 Id</p></td>
<td><p>原始已发送邮件的 ID</p></td>
<td><p>邮件 Id：邮件的 ID</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>发件人</p></td>
<td><p>原始邮件的实际发件人</p></td>
<td><p>发件人：发件人的电子邮件地址</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>主题</p></td>
<td><p>原始邮件的主题</p></td>
<td><p>主题：最终用户输入主题字符串</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>收件人</p></td>
<td><p>原始邮件的一个或多个收件人</p>
<p>每个“收件人”行仅包含一个收件人，事件报告中最多可以显示 10 个收件人。如果存在其他收件人，则下一个“收件人”行会显示剩余数量的收件人。</p></td>
<td><p>收件人：收件人的电子邮件地址</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>抄送</p></td>
<td><p>原始邮件的“抄送”电子邮件地址；该行是可选的</p>
<p>每个“抄送”行仅包含一个抄送电子邮件地址，事件报告中最多可以显示 10 个抄送电子邮件地址。如果存在其他抄送地址，则下一个“抄送”行会显示剩余数量的抄送电子邮件地址。</p></td>
<td><p>抄送：抄送收件人的电子邮件地址</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>密件抄送</p></td>
<td><p>原始邮件的“密件抄送”电子邮件地址；该行是可选的</p>
<p>每个“密件抄送”行仅包含一个密件抄送电子邮件地址，事件报告中最多可以显示 10 个密件抄送地址。如果存在其他密件抄送电子邮件地址，则后续“密件抄送”行会显示剩余数量的密件抄送电子邮件地址。</p></td>
<td><p>密件抄送：密件抄送收件人的电子邮件地址</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>严重性</p></td>
<td><p>规则命中的审核严重性；命中多个规则时显示最高严重性。</p></td>
<td><p>严重性：低、中或高</p></td>
<td><p>可选</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>首选参数</p></td>
<td><p>显示是否为邮件报告了替代，以及替代理由（如果提供）。</p></td>
<td><p>替代：是，理由：IW 输入理由字符串</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>误报</p></td>
<td><p>显示是否为邮件报告了误报。</p></td>
<td><p>误报：是</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>数据分类</p></td>
<td><p>原始邮件中发现的检测到的数据分类；该行是可选的。</p>
<p>每个数据分类行仅包含一个检测到的分类及其计数、可信度和建议的最低可信度级别。最多在事件报告中显示 5 个检测到的分类。如果检测到的分类是相关性，则不应用并且不会显示计数值。</p></td>
<td><p>数据分类：敏感信息类型，计数：邮件中发现的敏感信息的实例，可信度：百分比值，建议最低可信度：百分比值</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>规则命中</p></td>
<td><p>显示命中原始邮件的所有规则。</p>
<p>包含命中的规则的名称、规则所在的 DLP 策略（可选）、由于规则而对邮件执行的操作、规则中导致命中规则的数据分类以及规则定义。</p></td>
<td><p>规则命中：规则名称，DLP 策略：DLP 策略名称（如果适用），操作：单个操作，数据分类：敏感信息类型，定义：规则定义（如果适用）</p></td>
<td><p>强制</p></td>
<td><p>否</p></td>
</tr>
<tr class="odd">
<td><p>ID 匹配</p></td>
<td><p>显示匹配的数据分类、邮件中的准确匹配内容以及数据分类匹配的主要证据；该行是可选的。</p></td>
<td><p>ID 匹配：敏感信息类型，值：敏感数据的实际值，上下文：邮件中敏感数据周围的文本</p></td>
<td><p>可选</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 详细信息

[查看 DLP 策略检测报告](view-dlp-policy-detection-reports-exchange-2013-help.md)

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

