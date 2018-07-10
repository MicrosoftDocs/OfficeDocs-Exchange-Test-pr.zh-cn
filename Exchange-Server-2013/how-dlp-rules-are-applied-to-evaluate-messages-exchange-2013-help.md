---
title: '如何通过应用 DLP 规则来评估邮件: Exchange 2013 Help'
TOCTitle: 如何通过应用 DLP 规则来评估邮件
ms:assetid: 1ac77020-26ff-410c-ab09-4f28a99d67a1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn329050(v=EXCHG.150)
ms:contentKeyID: 56271405
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 如何通过应用 DLP 规则来评估邮件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

您可以在 Microsoft Exchange 数据丢失预防 (DLP) 策略内设置敏感信息规则，以检测电子邮件中非常具体的数据。本主题将帮助您了解如何应用这些规则以及如何评估邮件。如果您了解如何强制执行规则，则可以为您的电子邮件用户避免工作流中断，并获得高度准确的 DLP 检测。让我们使用 Microsoft 提供的信用卡信息规则作为示例。当您激活传输规则或 DLP 策略时，Exchange 传输规则代理将用户发送的所有邮件与您创建的规则集进行对比。

## 精确表达您的需求

假设您需要处理邮件中的信用卡信息。虽然找到它时执行的操作不属于本主题的内容，但您可以通过[联机在 Exchange 邮件流规则操作](https://technet.microsoft.com/zh-cn/library/jj919237\(v=exchg.150\))了解其详细信息。为保证最大程度的确定性，您需要确保在邮件中检测到的确实是信用卡数据，而不仅仅是合法使用的类似信用卡数据的数字组；例如，预订代码或车辆识别号码。为满足该要求，让我们明确表示以下信息应分类为信用卡。

**    Margie 的旅行，  
    我已收到更新的 Spencer 的信用卡信息。  
    Spencer Badillo  
    Visa：4111 1111 1111 1111  
    过期时间：2/2012  
    请更新他的旅行个人资料。**

让我们同时明确表示以下信息不应分类为信用卡。

**    Alex，你好，  
    我也将去夏威夷。我的预订代码是 1234 1234 1234 1234，我将于 2012 年 3 月到达。  
    此致，Lisa**

以下 XML 代码段显示当前如何在与 Exchange 一起提供的敏感信息规则中定义之前表达的需求，该代码段已嵌入提供的 DLP 策略模板之一。

    <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085" patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>

## 解决方案中的模式匹配

之前显示的 XML 规则定义包括模式匹配，模式匹配将提高规则仅检测重要信息而不检测相关模糊信息的可能性。有关用于 DLP 策略和模板的 XML 架构的详细信息，请参阅[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

在信用卡规则中，有一部分面向模式的 XML 代码，它包括主标识符匹配和一些其他的确定证据。关于全部三项要求的说明如下：

1.  `<IdMatch idRef="Func_credit_card" />  ` - 这要求匹配内部定义的名为“信用卡”的函数。该函数包括以下几个验证：
    
    1.  它匹配正则表达式（在本例中为 16 位），该表达式也可能包括一些变体（如空格分隔符），以便它同样匹配“4111 1111 1111 1111”，或者包括连字符分隔符，以便它同样匹配“4111-1111-1111-1111”。
    
    2.  它针对 16 位数字评估 Lhun 的校验和算法，以确保这是信用卡号的可能性较高。
    
    3.  它要求强制匹配，之后将评估确定证据。

2.  `<Any minMatches="1">  ` - 该部分表示至少要求存在以下证据项之一。

3.  确定证据可能匹配以下三项之一：
    
    `<Match idRef="Keyword_cc_verification" />`
    
    `<Match idRef="Keyword_cc_name" />`
    
    `<Match idRef="Func_expiration_date" />`
    
    这三项表明信用卡的关键字列表、信用卡名称或过期日期是必需的。过期日期将作为另一个函数在内部定义和评估。

## 根据规则评估内容的过程

此处的 5 个步骤代表了 Exchange 为比较您的规则和电子邮件而执行的操作。对于我们的信用卡规则示例而言，采取了以下步骤。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>步骤</th>
<th>操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1. 获取内容</p></td>
<td><p>Spencer Badillo</p>
<p>Visa：4111 1111 1111 1111</p>
<p>过期时间：2/2012</p></td>
</tr>
<tr class="even">
<td><p>2. 正则表达式分析</p></td>
<td><p>4111 1111 1111 1111 -&gt; 检测到一个 16 位的数字</p></td>
</tr>
<tr class="odd">
<td><p>3. 功能分析</p></td>
<td><ul>
<li><p>4111 1111 1111 1111 -&gt; 匹配校验和</p></li>
<li><p>1234 1234 1234 1234 -&gt; 不匹配</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>4. 其他证据</p></td>
<td><ol>
<li><p>关键字 Visa 位于数字旁。</p></li>
<li><p>日期 (2/2012) 的正则表达式位于数字旁。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>5. 结论</p></td>
<td><ol>
<li><p>有一个正则表达式与校验和匹配。</p></li>
<li><p>其他证据增加了可信度。</p></li>
</ol>
<p></p></td>
</tr>
</tbody>
</table>


Microsoft 设置该规则的方式强制要求将确定证据（如关键字）作为电子邮件内容的一部分，以便匹配该规则。因此，以下电子邮件内容将不会被检测为包含信用卡：

**    Margie 的旅行，  
    我已收到关于 Spencer 的更新信息。  
    Spencer Badillo  
    4111 1111 1111 1111  
    请更新他的旅行信息。**

您可以使用自定义规则，它将定义无需额外证据的模式，如下例所示。这将检测仅包含信用卡号而无确定证据的邮件。

``` 
      <Pattern confidenceLevel="85">
         <IdMatch idRef="Func_credit_card" />
      </Pattern>
    </Entity>
```

本文的信用卡示例也可扩展应用于其他敏感信息规则。若要查看 Exchange 中 Microsoft 提供的规则的完整列表，请按照以下方式使用 Exchange 命令行管理程序中的 [Get-ClassificationRuleCollection](https://technet.microsoft.com/zh-cn/library/jj218696\(v=exchg.150\)) cmdlet：

    $rule_collection = Get-ClassificationRuleCollection

    $rule_collection[0].SerializedClassificationRuleCollection | Set-Content oob_classifications.xml -Encoding byte

## 有关详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))

[将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))

[Exchange Online PowerShell](https://technet.microsoft.com/zh-cn/library/jj200677\(v=exchg.150\))

