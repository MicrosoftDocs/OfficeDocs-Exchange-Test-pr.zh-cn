---
title: '开发敏感信息规则包: Exchange 2013 Help'
TOCTitle: 开发敏感信息规则包
ms:assetid: c4ab8707-0839-4855-9390-3dbcb43475a7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674704(v=EXCHG.150)
ms:contentKeyID: 50491493
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 开发敏感信息规则包

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-07-28_

本主题中的 XML 架构和指导会帮助你开始创建自己的基本数据丢失预防 (DLP) XML 文件，这些文件在一个分类规则包中定义你自己的敏感信息类型。创建一个格式正确的 XML 文件后，可使用 Exchange 管理中心或 Exchange 命令行管理程序将其导入，以帮助创建一个 Microsoft Exchange Server 2013 DLP 解决方案。XML 文件是一个自定义的 DLP 策略模板，可包含作为你的分类规则包的 XML。有关将你自己的 DLP 模板定义为 XML 文件的概述，请参阅[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

**目录**

规则创作过程的概述

规则说明

基本规则结构

在您的 XML 文件中使用当地语言

分类规则包 XML 架构定义

详细信息

## 规则创作过程的概述

规则创作过程由以下一般步骤组成。

1.  准备一系列代表其目标环境的测试文档。对于这一系列测试文档需要考虑的关键特性包括：包含为其创作规则的实体或相关性的一个文档子集，以及不包含为其创作规则的实体或相关性的一个文档子集。

2.  确定满足接受要求（精度和调用）的规则以确定合格的内容。这可能要求在一个规则内开发多个条件，通过布尔逻辑约束，共同满足最低匹配要求以确定目标文档。

3.  为基于接受要求（精度和调用）的规则建立推荐的可信度。推荐的可信元素可被视为规则的默认可信度。

4.  通过将策略实例化并监视示例测试内容可验证规则。根据结果调整规则或可信度，以将检测内容最大化，同时将误报和负面影响最小化。继续验证循环和规则调整，直到正面和负面示例均达到内容检测的满意水平。

有关策略模板文件的 XML 架构定义的信息，请参阅[开发 DLP 策略模板文件](xml-rule-schema-and-rule-structure-guide-for-dlp-policy-files.md)。

## 规则说明

可为 DLP 敏感信息检测引擎创作两种主要的规则类型：实体和相关性。如之前部分所述，选择的规则类型基于应该应用到内容处理的处理逻辑类型。规则定义在一个 XML 文档中配置，格式如标准化规则 XSD 中所述。规则描述介绍匹配代表目标内容的要匹配的内容类型和可信度。可信度指定如果在内容中发现一种模式而要显示的实体的概率，或如果在内容中发现证据而要显示的相关性的概率。

## 基本规则结构

规则定义包括三个主要组件：

1.  **实体**   定义该规则的匹配和计数逻辑

2.  **相关性**   定义规则的匹配逻辑

3.  **本地化字符串**   规则名称及其说明的本地化

使用其他三个支持元素定义主要组件中处理和引用的详细信息：关键字、正则表达式和函数。使用引用，可在多个实体或相关性规则中使用支持元素的一个单独定义，如社会保险号。XML 格式的基本规则结构如下所示。

   ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
    
      <RulePack id="DAD86A92-AB18-43BB-AB35-96F7C594ADAA">
        <Version major="1" minor="0" build="0" revision="0"/>
        <Publisher id="619DD8C3-7B80-4998-A312-4DF0402BAC04"/>
        <Details defaultLangCode="en-us">
          <LocalizedDetails langcode="en-us">
            <PublisherName>DLP by EPG</PublisherName>
            <Name>CSO Custom Rule Pack</Name>
            <Description>This is a rule package for a EPG demo.</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
    
      <Rules>
    
        <!-- Employee ID -->
        <Entity id="E1CC861E-3FE9-4A58-82DF-4BD259EAB378" patternsProximity="300" recommendedConfidence="75">
          <Pattern confidenceLevel="75">
            <IdMatch idRef="Regex_employee_id" />
            <Match idRef="Keyword_employee" />
          </Pattern>
        </Entity>
    
        <Regex id="Regex_employee_id">(\s)(\d{9})(\s)</Regex>
        <Keyword id="Keyword_employee">
          <Group matchStyle="word">
            <Term>Identification</Term>
            <Term>Contoso Employee</Term>
          </Group>
        </Keyword>
    
    
        <LocalizedStrings>
    
          <Resource idRef="E1CC861E-3FE9-4A58-82DF-4BD259EAB378">
            <Name default="true" langcode="en-us">
              Employee ID
            </Name>
            <Description default="true" langcode="en-us">
              A custom classification for detecting Employee ID's
            </Description>
          </Resource>
    
        </LocalizedStrings>
      </Rules>
    </RulePackage>
```    

## 实体规则

实体规则针对定义正确的标识符，例如社会保险号，并且由一组可计数模式表示。实体规则返回一个计数和匹配的可信度，其中计数是发现的实体实例的总数，可信度是给定文档中存在的给定实体的概率。实体包含作为其唯一标识符的“id”属性。该标识符用于本地化、版本控制和查询。实体 id 必须是一个 GUID，并且不应在其他实体或相关性中重复。在本地化的字符串部分引用它。

实体规则包含可选的 patternsProximity 属性（默认 = 300），在应用布尔逻辑指定满足匹配条件所需的多个模式的邻接时使用它。Entity 元素包含 1 个或多个子 Pattern 元素，每个模式都是实体的明确表示，如信用卡实体或驾驶证实体。Pattern 元素拥有所需的 confidenceLevel 属性，代表基于示例数据集的模式的精度。Pattern 元素可以有三个子元素：

1.  IdMatch - 这是必要元素。

2.  匹配

3.  任意

如果任何 Pattern 元素返回“true”，则满足该模式。Pattern 元素的计数等于所有检测到的 Pattern 计数的总和。

![实体计数的的数学公式](images/JJ674704.25309939-98bc-4460-8f89-8560bbad7981(EXCHG.150).gif "实体计数的的数学公式")

其中 k 是实体模式元素的数量。

一个 Pattern 元素必须只有一个 IdMatch 元素。IdMatch 代表模式要匹配的标识符，例如一个信用卡号或 ITIN 号。模式计数是与 Pattern 元素匹配的 IdMatch 的数量。IdMatch 元素为 Pattern 元素锚定邻近感应窗口。

Pattern 元素的另一个可选子元素是 Match 元素，代表通过匹配以支持查找 IdMatch 元素所需的确凿证据。例如，除了查找信用卡号，更高的可信规则可能需要信用卡邻近感应窗口中的文档内存在其他项目，如地址和姓名。这些其他项目将通过 Match 元素或 Any 元素代表（在“匹配方法和技巧”部分中对这些有详细说明）。多个 Match 元素可包括在一个 Pattern 定义中，它可直接包括在 Pattern 元素中或使用 Any 元素组合以定义匹配语法。如在围绕 IdMatch 内容锚定的邻近感应窗口中找到一个匹配，则返回 true。

IdMatch 和 Match 元素均不定义需要匹配的内容的详细信息，而是通过 idRef 属性引用它。这提高了定义在多个模式结构中的可重用性。

```xml  
    <Entity id="..." patternsProximity="300" > 
        <Pattern confidenceLevel="85">
            <IdMatch idRef="FormattedSSN" />
            <Any minMatches="1">
                <Match idRef="SSNKeyword" />
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>  
        <Pattern confidenceLevel="65">
            <IdMatch idRef="UnformattedSSN" />
            <Match idRef="SSNKeyword" />
            <Any minMatches="1">        
                <Match idRef="USDate" />
                <Match idRef="USAddress" />
                <Match idRef="Name" />
            </Any>
        </Pattern>
    </Entity> 
``` 

在之前的 XML 中用“…“代表的实体 id 元素应该是一个 GUID，并且它在本地化字符串部分中引用。

## 实体模式接近窗口

实体保留用于查找模式的可选 patternsProximity 属性值（整数，默认 = 300）。对于每种模式，属性值为该模式指定的所有其他匹配定义与 IdMatch 位置的距离（采用 Unicode 字符）。邻近感应窗口通过 IdMatch 位置锚定，窗口扩展到 IdMatch 的左右。

![已调出匹配元素的文本模式](images/JJ674704.65d52989-f50f-4097-b39a-9612f860d727(EXCHG.150).gif "已调出匹配元素的文本模式")

下面的示例介绍了，SSN IdMatch 元素需要至少 1 个地址、名称或日期确认匹配时，邻近感应窗口如何影响匹配算法。只有 SSN1 和 SSN4 匹配，这是因为，对于 SSN2 和 SSN3，在邻近感应窗口中没有或只发现部分确认证据。

![邻近度规则匹配和不匹配示例](images/JJ674704.8117deb3-d8c8-4d4e-a011-ac5f9990b08e(EXCHG.150).gif "邻近度规则匹配和不匹配示例")

请注意，邮件正文和各个附件视为独立的项目。这意味着邻近感应窗口不会扩展到上述各个项目结尾之外。对于每个项目（附件或正文），idMatch 和确凿证据需要驻留在每个项目中。

## 实体可信度

Entity 元素的可信度是所有满意的模式可信度的组合。它们使用以下公式组合：

![实体可信度级别的的数学公式](images/JJ674704.9b8bb9c8-3ded-4ea5-a609-71d8034b1017(EXCHG.150).gif "实体可信度级别的的数学公式")

其中 k 是实体的模式元素的数量，而不匹配的模式返回可信度 0。

追溯到示例实体元素结构代码示例，如果匹配两种模式，根据以下计算方法得出实体的可信度为 94.75%：

CLEntity= 1-\[(1-CLPattern1) x (1-CLPattern1)\]

*= 1-\[(1-0.85) x (1-0.65)\]*

*= 1-(0.15 x 0.35)*

*= 94.75%*

同理，如果只有第二种模式匹配，根据以下计算方法得出实体的可信度为 65%：

CLEntity= 1 – \[(1 – CLPattern1) X (1 – CLPattern1)\]

*= 1 – \[(1 – 0) X (1 – 0.65)\]*

*= 1 – (1 X 0.35)*

*= 65%*

这些可信值按照单个模式的规则进行分配，基于验证为规则创作过程一部分的一系列测试文档。

## 相关性规则

相关性规则针对没有良好定义标识符的内容，例如 Sarbanes-Oxley 或公司财务内容。对于此类内容，无法找到单独一致的标识符，而是分析需要确定是否存在一组证据。相关性规则不返回一个计数，而是返回是否找到以及相关的可信度。相关性内容由一组独立证据表示。证据是某个相关性内的所需匹配聚合。对于相关性规则，邻近感应由 evidencesProximity 属性（默认为 600）定义，而最低可信度由 thresholdConfidenceLevel 属性定义。

相关性规则包含其用于本地化、版本管理和查询的唯一标志符的 id 属性。与实体规则不同，由于相关性规则不依靠良好定义的标识符，因此它们不包含 IdMatch 元素。

每个相关性规则都包含一个或多个子 Evidence 元素，定义要发现的证据以及对相关性规则发挥作用的可信度。如果产生的可信度低于阈值，则不认为发现相关性。每种证据都在逻辑方面代表这种文档“类型”的确凿证据，并且 confidenceLevel 属性是该证据在测试数据集上的精度。

Evidence 元素有一个或多个 Match 或 Any 子元素。如所有子 Match 和 Any 元素匹配，则会发现证据并且可信度对规则可信度计算起作用。在实体规则方面，相同的说明适用于实体规则的 Match 或 Any 元素。

```PowerShell
    <Affinity id="..." 
              evidencesProximity="1000"
              thresholdConfidenceLevel="65">
        <Evidence confidenceLevel="40">
            <Any> 
                <Match idRef="AssetsTerms" /> 
                <Match idRef="BalanceSheetTerms" /> 
                <Match idRef="ProfitAndLossTerms" /> 
            </Any> 
        </Evidence>
        <Evidence confidenceLevel="40">
            <Any minMatches="2"> 
                <Match idRef="TaxTerms" /> 
                <Match idRef="DollarAmountTerms" /> 
                <Match idRef="SECTerms" /> 
                <Match idRef="SECFilingFormTerms" /> 
                <Match idRef="DollarTotalRegex" /> 
            </Any> 
        </Evidence>
    </Affinity>
```

## 相关性接近窗口

相关性的邻近感应窗口和实体模式的计算方法不同。相关性邻近感应遵循一种滑动窗口模式。相关性邻近感应算法尝试在给定窗口中找到匹配证据的最大数量。邻近感应窗口中证据的可信度必须大于为要找到的相关性规则定义的阈值。

![关联性规则匹配邻近文本](images/JJ674704.2601ec86-0094-43fa-8d22-9d97f7465942(EXCHG.150).gif "关联性规则匹配邻近文本")

## 相关性可信度

相关性可信度等于相关性规则的邻近感应窗口中找到证据的组合。类似于实体规则的可信度，关键差异是邻近感应窗口的应用。和实体规则类似，Affinity 元素的可信度是所有满意的证据可信度的组合，但是对于相关性规则，它只代表在邻近感应窗口中找到的 Evidence 元素的最高组合。证据可信度使用以下公式组合：

![关联规则可信度的的数学公式](images/JJ674704.8a5da4ca-af02-4c5a-ab60-0072dc7e7a0f(EXCHG.150).gif "关联规则可信度的的数学公式")

其中 k 是接近窗口中匹配相关性的证据元素的数量。

追溯到“图 4 示例相关性”规则结构，如果全部三个证据在邻近感应滑动窗口中都匹配，根据以下计算方法得出相关性可信度为 85.6%。这超过了产生规则匹配的相关性规则阈值 65。

CL相关性= 1 – \[(1 – CL证据 1) X (1 – CL证据 2) X (1 – CL证据 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0.4) X (1 – 0.4)\]*

*= 1 – (0.4 X 0.6 X 0.6)*

*= 85.6%*

![关联性规则匹配示例（高可信度）](images/JJ674704.e17b2e22-18c3-40c4-8f19-0993bb556675(EXCHG.150).gif "关联性规则匹配示例（高可信度）")

使用相同的示例规则定义，如果因为第二个证据超出接近窗口而只有第一个证据匹配，则根据下面的计算最高相关性可信度为 60%，并且相关性规则不匹配，因为没有满足阈值 65。

CL相关性= 1 – \[(1 – CL证据 1) X (1 – CL证据 2) X (1 – CL证据 2)\]

*= 1 – \[(1 – 0.6) X (1 – 0) X (1 – 0) \]*

*= 1 – (0.4 X 1 X 1)*

*= 60%*

![关联性规则匹配示例（低可信度）](images/JJ674704.077095b1-6eb0-40df-b254-f33437725720(EXCHG.150).gif "关联性规则匹配示例（低可信度）")

## 微调可信度

规则创作过程的关键方面之一是为实体和相关性规则微调可信度。创建规则定义后，根据代表内容运行规则并收集准确数据。根据测试文档的预计结果，对比每个模式或证据返回的结果。

![包含规则匹配可信度比较的表](images/JJ674704.25a7d9a1-d02f-447e-a88b-8e78bdc0413a(EXCHG.150).gif "包含规则匹配可信度比较的表")

如规则满足接受要求，即模式或证据的可信比率超过既定的阈值（如 75%）— 匹配表达式完整并可进入下一步。

如模式或证据不匹配可信度，则重新创作它（如添加更多确信证据，删除或添加其他模式/证据等）并重复此步骤。

然后，根据上一步的结果微调你的规则中每个模式或证据的可信度。对于每个模式或证据，汇总误报 (TP) 的数量、包含创作规则并产生匹配和误报 (FP) 数量的实体或相关性的文档子集、不包含创作规则并也返回匹配的实体或相关性的文档子集。为使用以下计算的每个模式/证据设置可信度：

*可信度 = 真正的误报 /（真正的误报 + 误报）*


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>模式或证据</th>
<th>真正的误报</th>
<th>误报</th>
<th>可信度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>P1或 E1</p></td>
<td><p>4</p></td>
<td><p>1</p></td>
<td><p>80%</p></td>
</tr>
<tr class="even">
<td><p>P2或 E2</p></td>
<td><p>2</p></td>
<td><p>2</p></td>
<td><p>50%</p></td>
</tr>
<tr class="odd">
<td><p>Pn或 En</p></td>
<td><p>9</p></td>
<td><p>10</p></td>
<td><p>47%</p></td>
</tr>
</tbody>
</table>


## 在您的 XML 文件中使用当地语言

规则架构支持每个 Entity 元素和 Affinity 元素的本地化名称和说明的存储。每个 Entity 元素和 Affinity 元素必须在 LocalizedStrings 部分中包含一个相应的元素。要本地化每个元素，包括作为 LocalizedStrings 元素的子元素的 Resource 元素，以便为每个元素的多个地区存储名称和说明。Resource 元素包括所需的 idRef 属性，匹配本地化的每个元素的相应 idRef 属性。Resource 元素的 Locale 子元素包含每个指定地区的本地化名称和说明。

```PowerShell
    <LocalizedStrings>
        <Resource idRef="guid">
            <Locale langcode="en-US" default="true"> 
                <Name>affinity name en-us</Name> 
                <Description>
                    affinity description en-us
                </Description> 
            </Locale> 
            <Locale langcode="de"> 
                <Name>affinity name de</Name> 
                <Description>
                    affinity description de
                </Description> 
            </Locale> 
        </Resource>
    </LocalizedStrings>
```    

## 分类规则包 XML 架构定义

```xml
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:mce="http://schemas.microsoft.com/office/2011/mce"
               targetNamespace="http://schemas.microsoft.com/office/2011/mce" 
               xmlns:xs="http://www.w3.org/2001/XMLSchema"
               elementFormDefault="qualified"
               attributeFormDefault="unqualified"
               id="RulePackageSchema">
      <xs:simpleType name="LangType">
        <xs:union memberTypes="xs:language">
          <xs:simpleType>
            <xs:restriction base="xs:string">
              <xs:enumeration value=""/>
            </xs:restriction>
          </xs:simpleType>
        </xs:union>
      </xs:simpleType>
      <xs:simpleType name="GuidType" final="#all">
        <xs:restriction base="xs:token">
          <xs:pattern value="[0-9a-fA-F]{8}\-([0-9a-fA-F]{4}\-){3}[0-9a-fA-F]{12}"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulePackageType">
        <xs:sequence>
          <xs:element name="RulePack" type="mce:RulePackType"/>
          <xs:element name="Rules" type="mce:RulesType">
            <xs:key name="UniqueRuleId">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueProcessorId">
              <xs:selector xpath="mce:Regex|mce:Keyword"></xs:selector>
              <xs:field xpath="@id"/>
            </xs:key>
            <xs:key name="UniqueResourceIdRef">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:key>        
            <xs:keyref name="ReferencedRuleMustExist" refer="mce:UniqueRuleId">
              <xs:selector xpath="mce:LocalizedStrings/mce:Resource"/>
              <xs:field xpath="@idRef"/>
            </xs:keyref>
            <xs:keyref name="RuleMustHaveResource" refer="mce:UniqueResourceIdRef">
              <xs:selector xpath="mce:Entity|mce:Affinity"/>
              <xs:field xpath="@id"/>
            </xs:keyref>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="RulePackType">
        <xs:sequence>
          <xs:element name="Version" type="mce:VersionType"/>
          <xs:element name="Publisher" type="mce:PublisherType"/>
          <xs:element name="Details" type="mce:DetailsType">
            <xs:key name="UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="mce:LocalizedDetails"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:keyref name="DefaultLangCodeMustExist" refer="mce:UniqueLangCodeInLocalizedDetails">
              <xs:selector xpath="."/>
              <xs:field xpath="@defaultLangCode"/>
            </xs:keyref>
          </xs:element>
          <xs:element name="Encryption" type="mce:EncryptionType" minOccurs="0" maxOccurs="1"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="VersionType">
        <xs:attribute name="major" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="minor" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="build" type="xs:unsignedShort" use="required"/>
        <xs:attribute name="revision" type="xs:unsignedShort" use="required"/>
      </xs:complexType>
      <xs:complexType name="PublisherType">
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="LocalizedDetailsType">
        <xs:sequence>
          <xs:element name="PublisherName" type="mce:NameType"/>
          <xs:element name="Name" type="mce:RulePackNameType"/>
          <xs:element name="Description" type="mce:OptionalNameType"/>
        </xs:sequence>
        <xs:attribute name="langcode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="DetailsType">
        <xs:sequence>
          <xs:element name="LocalizedDetails" type="mce:LocalizedDetailsType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="defaultLangCode" type="mce:LangType" use="required"/>
      </xs:complexType>
      <xs:complexType name="EncryptionType">
        <xs:sequence>
          <xs:element name="Key" type="xs:normalizedString"/>
          <xs:element name="IV" type="xs:normalizedString"/>
        </xs:sequence>
      </xs:complexType>
      <xs:simpleType name="RulePackNameType">
        <xs:restriction base="xs:token">
          <xs:minLength value="1"/>
          <xs:maxLength value="64"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="NameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="1"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="OptionalNameType">
        <xs:restriction base="xs:normalizedString">
          <xs:minLength value="0"/>
          <xs:maxLength value="256"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="RestrictedTermType">
        <xs:restriction base="xs:string">
          <xs:minLength value="1"/>
          <xs:maxLength value="512"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RulesType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Entity" type="mce:EntityType"/>
            <xs:element name="Affinity" type="mce:AffinityType"/>
          </xs:choice>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Regex" type="mce:RegexType"/>
            <xs:element name="Keyword" type="mce:KeywordType"/>
          </xs:choice>
          <xs:element name="LocalizedStrings" type="mce:LocalizedStringsType"/>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="EntityType">
        <xs:sequence>
          <xs:element name="Pattern" type="mce:PatternType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="patternsProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="recommendedConfidence" type="mce:ProbabilityType"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="PatternType">
        <xs:sequence>
          <xs:element name="IdMatch" type="mce:IdMatchType"/>
          <xs:choice minOccurs="0" maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="AffinityType">
        <xs:sequence>
          <xs:element name="Evidence" type="mce:EvidenceType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="mce:GuidType" use="required"/>
        <xs:attribute name="evidencesProximity" type="mce:ProximityType" use="required"/>
        <xs:attribute name="thresholdConfidenceLevel" type="mce:ProbabilityType" use="required"/>
        <xs:attribute name="workload" type="mce:WorkloadType"/>
      </xs:complexType>
      <xs:complexType name="EvidenceType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="confidenceLevel" type="mce:ProbabilityType" use="required"/>
      </xs:complexType>
      <xs:complexType name="IdMatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="MatchType">
        <xs:attribute name="idRef" type="xs:string" use="required"/>
      </xs:complexType>
      <xs:complexType name="AnyType">
        <xs:sequence>
          <xs:choice maxOccurs="unbounded">
            <xs:element name="Match" type="mce:MatchType"/>
            <xs:element name="Any" type="mce:AnyType"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="minMatches" type="xs:nonNegativeInteger" default="1"/>
        <xs:attribute name="maxMatches" type="xs:nonNegativeInteger" use="optional"/>
      </xs:complexType>
      <xs:simpleType name="ProximityType">
        <xs:restriction base="xs:positiveInteger">
          <xs:minInclusive value="1"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="ProbabilityType">
        <xs:restriction base="xs:integer">
          <xs:minInclusive value="1"/>
          <xs:maxInclusive value="100"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:simpleType name="WorkloadType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Exchange"/>
          <xs:enumeration value="Outlook"/>
        </xs:restriction>
      </xs:simpleType>
      <xs:complexType name="RegexType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="id" type="xs:token" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="KeywordType">
        <xs:sequence>
          <xs:element name="Group" type="mce:GroupType" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="id" type="xs:token" use="required"/>
      </xs:complexType>
      <xs:complexType name="GroupType">
        <xs:sequence>
          <xs:choice>
            <xs:element name="Term" type="mce:TermType" maxOccurs="unbounded"/>
          </xs:choice>
        </xs:sequence>
        <xs:attribute name="matchStyle" default="word">
          <xs:simpleType>
            <xs:restriction base="xs:NMTOKEN">
              <xs:enumeration value="word"/>
              <xs:enumeration value="string"/>
            </xs:restriction>
          </xs:simpleType>
        </xs:attribute>
      </xs:complexType>
      <xs:complexType name="TermType">
        <xs:simpleContent>
          <xs:extension base="mce:RestrictedTermType">
            <xs:attribute name="caseSensitive" type="xs:boolean" default="false"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="LocalizedStringsType">
        <xs:sequence>
          <xs:element name="Resource" type="mce:ResourceType" maxOccurs="unbounded">
            <xs:key name="UniqueLangCodeUsedInNamePerResource">
              <xs:selector xpath="mce:Name"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
            <xs:key name="UniqueLangCodeUsedInDescriptionPerResource">
              <xs:selector xpath="mce:Description"/>
              <xs:field xpath="@langcode"/>
            </xs:key>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:complexType name="ResourceType">
        <xs:sequence>
          <xs:element name="Name" type="mce:ResourceNameType" maxOccurs="unbounded"/>
          <xs:element name="Description" type="mce:DescriptionType" minOccurs="0" maxOccurs="unbounded"/>
        </xs:sequence>
        <xs:attribute name="idRef" type="mce:GuidType" use="required"/>
      </xs:complexType>
      <xs:complexType name="ResourceNameType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
      <xs:complexType name="DescriptionType">
        <xs:simpleContent>
          <xs:extension base="xs:string">
            <xs:attribute name="default" type="xs:boolean" default="false"/>
            <xs:attribute name="langcode" type="mce:LangType" use="required"/>
          </xs:extension>
        </xs:simpleContent>
      </xs:complexType>
    </xs:schema>
```    

## 详细信息

[数据丢失预防](https://technet.microsoft.com/zh-cn/library/jj150527(v=exchg.150))

[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

