---
title: '规则包的匹配方法和技术: Exchange 2013 Help'
TOCTitle: 规则包的匹配方法和技术
ms:assetid: 09fe9278-d077-452c-b7e5-729b3dc70b1b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674702(v=EXCHG.150)
ms:contentKeyID: 50489888
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 规则包的匹配方法和技术

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-07-28_

本主题介绍用于匹配数据丢失预防 (DLP) XML 文件（该文件旨在包含您自己的自定义敏感信息类型规则包）中的模式和证据元素的方法。在创建了标准格式的 XML 文件之后，可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序导入文件，以便帮助创建 Microsoft Exchange Server 2013 DLP 解决方案。应当已启动 DLP XML 文件，才能使用此处介绍的匹配方法。有关定义自己的 DLP 模板和 XML 文件的详细信息，请参阅[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

## Match 元素

`Match` 元素在 `Pattern` 和 `Evidence` 元素中用于表示要匹配的基本关键字、正则表达式或函数。匹配本身的定义存储在 `Rule` 元素外部，通过必需的 `idRef` 属性进行引用。多个 `Match` 元素可以包含在模式定义中，而该定义可以直接包含在 `Pattern` 元素中或是使用 `Any` 元素进行合并以定义匹配语义。

```XML
    <?xml version="1.0" encoding="utf-8"?>
    <Rules packageId="...">
            ...
    <Entity id="...">
      <Pattern confidenceLevel="85">
                 <IdMatch idRef="FormattedSSN" />
                 <Match idRef="USDate" />
                 <Match idRef="USAddress" />
      </Pattern>
    </Entity>
            ...
             <Keyword id="FormattedSSN "> ... </Keyword>
             <Regex id=" USDate "> ... </Regex>
             <Regex id="USAddress"> ... </Regex>
            ...
    
    </Rules>
```

## 定义基于关键字的匹配

常用规则要求是基于已知关键字字符串表达式进行匹配。这通过使用 `Keyword` 元素来实现。Keyword 元素具有一个“id”属性，该属性在对应的实体或关联规则中用作引用。单个 Keyword 元素可以在多个实体和关联规则中引用。

可以使用完全匹配或基于文字匹配的算法来执行匹配。完全匹配使用区分大小写的算法，该算法在特定语言中搜索文本。文字匹配基于文字边界应用匹配算法。要匹配的项可以使用 Term 子元素内嵌在 Keyword 定义中。

> [!TIP]  
> 使用 regex 的基于常量的匹配风格以获得更出色的效率和性能。仅在基于常量的匹配不充分并且需要正则表达式的灵活性时使用 regex 匹配。

```XML
    <Keyword id="Word_Example">
        <Group matchStyle="word">
           <Term>card verification</Term>
           <Term>cvn</Term>
           <Term>cid</Term>
           <Term>cvc2</Term>
           <Term>cvv2</Term>
           <Term>pin block</Term>
           <Term>security code</Term>
        </Group>
    </Keyword>
    ...
    <Keyword id="String_Example">
        <Group matchStyle="string">
           <Term>card</Term>
           <Term>pin</Term>
           <Term>security</Term>
        </Group>
    </Keyword>
```

## 定义基于正则表达式的匹配

另一种常用匹配方法基于正则表达式。正则表达式匹配的灵活性使之成为实现如驾驶证号码、地址这类数据匹配的常见选择。常用正则表达式语法用于定义正则表达式模式。此处的表提供一些可以使用的最常用正则表达式令牌的示例。

> [!TIP]  
> 使用 regex 的基于常量的匹配风格以获得更出色的效率和性能。仅在基于常量的匹配不充分并且需要正则表达式的灵活性时使用 regex 匹配。



<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>符号</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>c</p></td>
<td><p>匹配文字字符 c 一次，除非它是特殊字符之一。</p></td>
</tr>
<tr class="even">
<td><p>^</p></td>
<td><p>匹配行的开头。</p></td>
</tr>
<tr class="odd">
<td><p>.</p></td>
<td><p>匹配任何不是换行符的字符。</p></td>
</tr>
<tr class="even">
<td><p>$</p></td>
<td><p>匹配行的末尾。</p></td>
</tr>
<tr class="odd">
<td><p>|</p></td>
<td><p>表达式之间的逻辑或。</p></td>
</tr>
<tr class="even">
<td><p>()</p></td>
<td><p>组子表达式。</p></td>
</tr>
<tr class="odd">
<td><p>[]</p></td>
<td><p>定义字符类。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>匹配前面的表达式零次或更多次。</p></td>
</tr>
<tr class="odd">
<td><p>+</p></td>
<td><p>匹配前面的表达式一次或更多次。</p></td>
</tr>
<tr class="even">
<td><p>?</p></td>
<td><p>匹配前面的表达式零次或一次。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n</em>}</p></td>
<td><p>匹配前面的表达式 <em>n</em> 次。</p></td>
</tr>
<tr class="even">
<td><p>{<em>n,</em>}</p></td>
<td><p>匹配前面的表达式至少 <em>n</em> 次。</p></td>
</tr>
<tr class="odd">
<td><p>{<em>n, m</em>}</p></td>
<td><p>匹配前面的表达式至少 <em>n</em> 次，至多 <em>m</em> 次。</p></td>
</tr>
<tr class="even">
<td><p>\d</p></td>
<td><p>匹配数字。</p></td>
</tr>
<tr class="odd">
<td><p>\D</p></td>
<td><p>匹配不是数字的字符。</p></td>
</tr>
<tr class="even">
<td><p>\w</p></td>
<td><p>匹配字母字符，包括下划线。</p></td>
</tr>
<tr class="odd">
<td><p>\W</p></td>
<td><p>匹配不是字母字符的字符。</p></td>
</tr>
<tr class="even">
<td><p>\s</p></td>
<td><p>匹配空白字符（任何 \t、\n、\r 或 \f）。</p></td>
</tr>
<tr class="odd">
<td><p>\S</p></td>
<td><p>匹配非空白字符。</p></td>
</tr>
<tr class="even">
<td><p>\t</p></td>
<td><p>制表符。</p></td>
</tr>
<tr class="odd">
<td><p>\n</p></td>
<td><p>换行符。</p></td>
</tr>
<tr class="even">
<td><p>\r</p></td>
<td><p>回车符。</p></td>
</tr>
<tr class="odd">
<td><p>\f</p></td>
<td><p>换页符。</p></td>
</tr>
<tr class="even">
<td><p>\<em>m</em></p></td>
<td><p>转义 <em>m</em>，其中 <em>m</em> 是上面介绍的元字符之一：^, .、$、|、()、[]、*、+、?、\ 或 /。</p></td>
</tr>
</tbody>
</table>


Regex 元素具有一个“id”属性，该属性在对应的实体或关联规则中用作引用。单个 Regex 元素可以在多个实体和关联规则中引用。正则表达式定义为 Regex 元素的值。

```XML
    <Regex id="CCRegex">
         \bcc\#\s|\bcc\#\:\s
    </Regex>
    ...
    <Regex id="ItinFormatted">
        (?:^|[\s\,\:])(?:9\d{2})[- ](?:[78]\d[-       ]\d{4})(?:$|[\s\,]|\.\s)
    </Regex>
    ...
    <Regex id="NorthCarolinaDriversLicenseNumber">
        (^|\s|\:)(\d{1,8})($|\s|\.\s)
    </Regex>
```

## 合并多个匹配元素

一种用于提高匹配置信度的常用方法是在多个 Match 元素之间定义语义，例如需要发生一次或多次匹配。通过 Any 元素可以在多个匹配之间实现基于逻辑的定义。Any 元素可以在 Pattern 元素中用作子元素。它包含一个或多个 Match 子元素并定义它们之间的匹配逻辑。请参阅下文以了解针对具有所有匹配、“非”逻辑和完全匹配计数的 Any 元素的 XML 代码示例。

可选 minMatches 属性可以用于（默认值 = 1）定义为符合匹配而必须满足的最小 Match 元素数。同样，可选 maxMatches 属性可以用于（默认值 = 子 Match 元素数）定义为符合匹配而必须满足的最大 Match 元素数。这些条件基于 minMatches 和 maxMatches 属性的用法，通过逻辑运算符进行合并，从而可以实现以下语义：

  - 匹配所有子 Match 元素
    
    不匹配任何子 Match 元素
    
    匹配任何子 Match 元素的精确子集

<!-- end list -->
```XML
    <Any minMatches="3" maxMatches="3">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```

```XML
    <Any maxMatches="0">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```

```XML
    <Any minMatches="1" maxMatches="1">
        <Match idRef="USDate" />
        <Match idRef="USAddress" />
        <Match idRef="Name" />
    </Any>
```

## 使用更多证据提高置信度级别

对于实体基础规则，另一个提高置信度的选择是定义多个 Pattern 元素，每个元素都具有更多确定证据。通过对 Any 元素使用 minMatches 和 maxMatches 以创建基于更多确定证据而提高置信度级别的独立模式，可以实现此目标。例如：

  - 如果找到一件确定证据：可信度为 65 %

  - 如果找到两件：可信度为 75%

  - 如果找到三件：可信度为 85%

<!-- end list -->

```XML
    <Entity id="..." patternsProximity="300" >
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Any maxMatches="1">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="75">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="2" maxMatches="2">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
        <Pattern confidenceLevel="85">
            <IdMatch idRef="UnformattedSSN" />
            <Any minMatches="3">
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity>
```

## 示例：美国社会保险规则

本节包含创作匹配美国社会保险号码的规则的介绍性描述。首先，开始介绍如何识别包含社会保险号码的内容。如果满足以下条件，则找到社会保险号码：

1.  正则表达式与格式化 SSN 匹配（并且它处于有效 SSN 范围内）

2.  确定证据   附近必须出现以下情况之一：
    
    1.  关键字匹配 {Social Security、Soc Sec、SSN、SSNS、SSN\#、SS\#、SSID}
    
    2.  表示美国地址的文本
    
    3.  代表日期的文本
    
    4.  表示姓名的文本

接下来，将描述转换为规则架构表示形式：

```XML
    <Entity id="a44669fe-0d48-453d-a9b1-2cc83f2cba77"
             patternsProximity="300" RecommendedConfidence="85">
        <Pattern confidenceLevel="85">
          <IdMatch idRef="FormattedSSN" />
          <Any minMatches="1">
              <Match idRef="SSNKeywords" />
              <Match idRef="USDate" />
              <Match idRef="USAddress" />
              <Match idRef="Name" />
          </Any>
        </Pattern>
    </Entity>
```

## 详细信息

[数据丢失预防](https://technet.microsoft.com/zh-cn/library/jj150527(v=exchg.150))

[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

