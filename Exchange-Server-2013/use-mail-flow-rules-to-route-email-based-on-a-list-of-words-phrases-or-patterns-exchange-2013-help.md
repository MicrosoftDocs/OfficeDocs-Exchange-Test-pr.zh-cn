---
title: '使用邮件流规则根据字词、短语或模式的列表路由电子邮件: Exchange Online Help'
TOCTitle: 使用邮件流规则根据字词、短语或模式的列表路由电子邮件
ms:assetid: 4c5bee1b-58b5-4152-baef-86fa103050ae
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn951131(v=EXCHG.150)
ms:contentKeyID: 65330363
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用邮件流规则根据字词、短语或模式的列表路由电子邮件

 

_**适用于：** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上一次修改主题：** 2017-10-30_

为了帮助您满足您的组织的电子邮件策略的用户，可以使用Exchange传输规则来确定如何路由电子邮件包含特定的词或模式。对于短的单词或短语列表，您可以使用Exchange 管理中心。对于较长的列表，可能需要使用ExchangeWindows PowerShell的模块可以从文本文件中读取的列表。

  - Example 1: Use a short list of unacceptable words

  - Example 2: Use a long list of unacceptable words

如果您的组织使用数据丢失防护 (DLP)，请参阅[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)，了解用于识别和路由包含敏感信息的电子邮件的其他选项。

## 示例 1：使用包含不可接受字词的简短列表

如果您的词或短语列表很短，您可以创建使用Exchange 管理中心规则。例如，如果您想要确保没有人会发送电子邮件，使用错误的单词或拼错的公司名称，内部首字母缩写词或产品名称，可以创建一个规则来阻止该信息，并告诉发件人。请注意，单词、 短语和图案不区分大小写。

此示例可阻止含常见拼写错误的邮件。

![基于文本模式显示阻止某封邮件的规则](images/Dn951131.a8489cbb-be59-4890-ae30-1431703eeb88(EXCHG.150).png "基于文本模式显示阻止某封邮件的规则")

## 示例 2：使用包含不可接受字词的较长列表

如果单词、 短语或模式的列表很长，可以直接将它们放在文本文件中的每个单词、 短语或模式，在自己的行上。 使用Windows PowerShellExchange模块读入一个变量中的关键字列表，创建传输规则，并将与关键字的变量分配给传输规则条件。例如，以下脚本从名为 misspelled\_companyname.txt 的文件采用了拼写错误的列表。

    $keywords=Import-Content  .\misspelled_companyname.txt
    New-TransportRule -Name "Block messages with unacceptable words" -SubjectOrBodyContainsWords $keywords -SentToScope "NotInOrganization" -RejectMessageReasonText "Do not use internal acronyms, product names, or misspellings in external communications."

## 使用文本文件中的短语和模式

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


例如，此文本文件包含Microsoft的常见拼写错误。

    [mn]sft
    [mn]icrosft
    [mn]icro soft
    [mn].crosoft

若要了解如何使用正则表达式指定模式，请参阅[正则表达式参考](https://go.microsoft.com/fwlink/p/?linkid=532394)。

