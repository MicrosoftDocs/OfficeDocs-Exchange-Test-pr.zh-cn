---
title: '自定义内置 DLP 敏感信息类型: Exchange 2013 Help'
TOCTitle: 自定义内置 DLP 敏感信息类型
ms:assetid: 3f8bf141-2e7c-4ea7-b102-dfd6c41539da
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn781122(v=EXCHG.150)
ms:contentKeyID: 62757547
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自定义内置 DLP 敏感信息类型

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-05-26_

在电子邮件中查找敏感信息时，您需要使用所谓的*规则*来描述此信息。数据丢失预防 (DLP) 包括针对您可能会立即用到的最常见敏感信息类型的 51 个规则。要使用这些规则，您必须将其包含在策略中。您可能会发现需要调整这些内置规则以满足组织的特定需求，您可以通过创建自定义敏感信息类型来实现这一点。本主题介绍如何自定义包含现有规则集的 XML 文件，以检测更广泛的潜在信用卡信息。

您可以此为例，并将其应用于其他内置敏感信息类型。有关默认敏感信息类型和 XML 定义的列表，请参阅[使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)主题。

本主题将指导您完成 XML 规则自定义的下列过程：

  - 导出当前规则的 XML 文件

  - 查找您想在 XML 中修改的规则

  - 修改 XML 并创建新的敏感信息类型

  - 从敏感信息类型中删除确定证据要求

  - 查找特定于您的组织的关键字

  - 上载您的规则

要了解有哪些不同的规则部分以及它们的功能，请参阅本主题结尾的术语表。

## 导出当前规则的 XML 文件

要导出 XML，您需要使用 Exchange 命令行管理程序。对于 Exchange Server 2013，参阅 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。对于 Exchange Online，参阅 [使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))。

1.  在 Exchange 命令行管理程序 或 Exchange Online PowerShell 中，键入 **Get-ClassificationRuleCollection** 以在屏幕上显示您的组织的规则。如果您还没有创建您自己的规则，您将仅看到默认的内置规则“Microsoft 规则包”。

2.  键入 **$ruleCollections = Get-ClassificationRuleCollection**，将组织的规则存储在一个变量中。将规则存储在变量中，可使其稍后以适用于远程 PowerShell 命令的格式快速提供。

3.  键入 **Set-Content -path "C:\\custompath\\exportedRules.xml" -Encoding Byte -Value $ruleCollections.SerializedClassificationRuleCollection**，创建包含所有这些数据的格式化 XML 文件。(**Set-content** 是将 XML 写入文件的 cmdlet 部分。）
    
    > [!IMPORTANT]  
    > 确保使用规则包实际存储的文件位置。<strong>C:\custompath\ </strong> 是占位符。


## 查找您想在 XML 中修改的规则

上述 cmdlet 导出整个*规则集*，其中包含我们提供的 51 个默认规则。接下来您将需要专门查找您想要修改的“信用卡号”规则。

1.  使用文本编辑器打开您在前一节中导出的 XML 文件。

2.  向下滚动到 **\<Rules\>** 标记，这是包含 DLP 规则的部分的开头。（因为该 XML 文件包含整个规则集的信息，除了滚动获取规则所需的信息外，它还包含其他信息。）

3.  查找 **Func\_credit\_card**，以查找信用卡号规则定义。（在 XML 中，规则名称不能包含空格，因此空格通常用下划线替代，规则名称有时会进行缩写。例如美国社会保险号码规则，其缩写为“SSN”。信用卡号规则 XML 应该如以下代码示例所示。
    
    ```xml
        <Entity id="50842eb7-edc8-4019-85dd-5a5c1f2bb085"
               patternsProximity="300" recommendedConfidence="85">
              <Pattern confidenceLevel="85">
               <IdMatch idRef="Func_credit_card" />
                <Any minMatches="1">
                  <Match idRef="Keyword_cc_verification" />
                  <Match idRef="Keyword_cc_name" />
                  <Match idRef="Func_expiration_date" />
                </Any>
              </Pattern>
            </Entity>
    ```

现在您已在 XML 中找到信用卡号规则定义，您可以自定义规则的 XML 以满足您的需求。（要刷新 XML 定义，请参阅本主题结尾的术语表。）

## 修改 XML 并创建新的敏感信息类型

首先，您需要创建新的敏感信息类型，因为您无法直接修改默认规则。您可以使用自定义敏感信息类型执行多种操作，如[开发敏感信息规则包](technical-description-of-xml-schema-for-dlp-rule-packages.md)中所述。在此示例中，我们使其尽量简单，仅删除确定证据，并将关键字添加到信用卡号规则。

所有 XML 规则定义基于以下通用模板构建。您需要在模板中复制和粘贴信用卡号定义，修改某些值（请注意以下示例中的“.. .” 占位符），然后将修改后的 XML 作为可用于策略的新规则进行上载。

```xml
    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id=". . .">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id=". . ." /> 
        <Details defaultLangCode=". . .">
          <LocalizedDetails langcode=" . . . ">
             <PublisherName>. . .</PublisherName>
             <Name>. . .</Name>
             <Description>. . .</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
       <!-- Paste the Credit Card Number rule definition here.--> 
    
          <LocalizedStrings>
             <Resource idRef=". . .">
               <Name default="true" langcode=" . . . ">. . .</Name>
               <Description default="true" langcode=". . ."> . . .</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>
```

现在，您的 XML 应该如下所示。因为规则包和规则使用它们的唯一 GUID 表示，您需要生成两个 GUID：一个用于规则包，一个用于替换信用卡号规则的 GUID。（以下代码示例中实体 ID 的 GUID 用于我们的内置规则定义，您需将其替换为新的 GUID。）有多种方法可以生成 GUID，但您可以通过键入 **\[guid\]::NewGuid()**，在 PowerShell 中轻松生成 GUID。

```xml
    <?xml version="1.0" encoding="utf-16"?>
    <RulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">
      <RulePack id="8aac8390-e99f-4487-8d16-7f0cdee8defc">
        <Version major="1" minor="0" build="0" revision="0" />
        <Publisher id="8d34806e-cd65-4178-ba0e-5d7d712e5b66" />
        <Details defaultLangCode="en">
          <LocalizedDetails langcode="en">
            <PublisherName>Contoso Ltd.</PublisherName>
            <Name>Financial Information</Name>
            <Description>Modified versions of the Microsoft rule package</Description>
          </LocalizedDetails>
        </Details>
      </RulePack>
      
     <Rules>
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f"
           patternsProximity="300" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    
          <LocalizedStrings>
             <Resource idRef="db80b3da-0056-436e-b0ca-1f4cf7080d1f"> 
    <!-- This is the GUID for the preceding Credit Card Number entity because the following text is for that Entity. -->
               <Name default="true" langcode="en-us">Modified Credit Card Number</Name>
               <Description default="true" langcode="en-us">Credit Card Number that looks for additional keywords, and another version of Credit Card Number that doesn't require keywords (but has a lower confidence level)</Description>
             </Resource>
          </LocalizedStrings>
    
       </Rules>
    </RulePackage>
```

## 从敏感信息类型中删除确定证据要求

现在您具有可上载到 Exchange 环境的新敏感信息类型，下一步是将规则设置得更加具体。对规则进行修改，使其仅查找通过校验和但不需要额外的（确定）证据（例如关键字）的 16 位数字。为此，您需要删除查找确定证据的 XML 部分。确定证据对于减少误报非常有用，因为信用卡号附近通常有特定的关键字或过期日期。如果您删除该证据，您还应该通过降低 **confidenceLevel**（本示例中为 85），调整您对某个信用卡号的信心。

```xml
    <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="300"
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
          </Pattern>
        </Entity>
```

## 查找特定于您的组织的关键字

您可能需要确定证据，但需要不同或额外的关键字，您可能想要更改在何处查找该证据。您可以调整 **patternsProximity**，以扩展或收缩围绕 16 位数字的确定证据的窗口。要添加您自己的关键字，您需要定义关键字列表并在您的规则中进行引用。以下 XML 添加关键字“company card”和“Contoso card”，以便在信用卡号的 150 个字符内包含这些短语的任何邮件均将识别为信用卡号。

```xml
    <Rules>
    <! -- Modify the patternsProximity to be "150" rather than "300." -->
        <Entity id="db80b3da-0056-436e-b0ca-1f4cf7080d1f" patternsProximity="150" recommendedConfidence="85">
          <Pattern confidenceLevel="85">
            <IdMatch idRef="Func_credit_card" />
            <Any minMatches="1">
              <Match idRef="Keyword_cc_verification" />
              <Match idRef="Keyword_cc_name" />
    <!-- Add the following XML, which references the keywords at the end of the XML sample. -->
              <Match idRef="My_Additional_Keywords" />
              <Match idRef="Func_expiration_date" />
            </Any>
          </Pattern>
        </Entity>
    <!-- Add the following XML, and update the information inside the <Term> tags with the keywords that you want to detect. -->
        <Keyword id="My_Additional_Keywords">
          <Group matchStyle="word">
            <Term caseSensitive="false">company card</Term>
            <Term caseSensitive="false">Contoso card</Term>
          </Group>
        </Keyword>
```

## 上载您的规则

要上载您的规则，需执行以下操作：

1.  使用 Unicode 编码将其另存为 .xml 文件。这一点很重要，因为如果文件使用其他编码保存，将无法正常运行。

2.  连接到 Exchange 命令行管理程序 或 Exchange Online PowerShell。对于 Exchange Server 2013，参阅 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。对于 Exchange Online，参阅 [使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))。

3.  在 Exchange 命令行管理程序 或 Exchange Online PowerShell 中，键入 **New-ClassificationRuleCollection -FileData (Get-Content -Path "C:\\custompath\\MyNewRulePack.xml " -Encoding Byte)**。
    
    > [!IMPORTANT]  
    > 确保使用规则包实际存储的文件位置。<strong>C:\custompath\ </strong> 是占位符。


4.  要确认，请键入“Y”，然后按“Enter”键。

5.  键入 **Get-DataClassification**，确认您的新规则已上载，现在它将显示您的规则的名称。

要开始使用新规则检测敏感信息，您需将规则添加到 DLP 策略。要了解如何将规则添加到策略，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。

## 术语表

下面您在此过程中遇到的术语的定义。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>术语</th>
<th>定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>实体</p></td>
<td><p>实体是我们称为敏感信息类型的项目，例如信用卡号。每个实体都有一个唯一的 GUID 作为其 ID。如果您复制 GUID 并在 XML 中搜索它，您将找到 XML 规则定义以及该 XML 规则的所有本地化翻译。您也可以通过查找翻译的 GUID 并搜索该 GUID 来查找此定义。</p></td>
</tr>
<tr class="even">
<td><p>函数</p></td>
<td><p>XML 文件引用 <strong>Func_credit_card</strong>，这是一个采用编译代码的函数。函数用于运行复杂的 regex 并确认校验和与我们的内置规则相符。）因为这会在代码中发生，某些变量不会显示在 XML 文件中。</p></td>
</tr>
<tr class="odd">
<td><p>IdMatch</p></td>
<td><p>这是尝试匹配的模式的标识符，例如信用卡号。您可以在<a href="technical-description-of-xml-schema-for-dlp-rule-packages.md">Entity rules</a>中阅读关于此标识符和<strong>匹配</strong>标记的详细信息。</p></td>
</tr>
<tr class="even">
<td><p>关键字列表</p></td>
<td><p>XML 文件还会引用 <strong>keyword_cc_verification</strong> 和 <strong>keyword_cc_name</strong>，这是关键字列表，我们可从中为实体查找 <strong>patternsProximity</strong> 中的匹配。这些匹配当前不会显示在 XML 中。</p></td>
</tr>
<tr class="odd">
<td><p>模式</p></td>
<td><p>模式包含敏感类型所查找内容的列表。这包括关键字、regex 和内部函数（执行验证校验和之类的任务）。敏感信息类型可能具有多个模式，每个模式均具有唯一的可信度。这在创建敏感信息类型时非常有用：当它找到确定证据时，返回高可信度；当未找到确定证据时，则返回较低的可信度。</p></td>
</tr>
<tr class="even">
<td><p>模式可信度</p></td>
<td><p>这是指 DLP 引擎找到匹配的可信度。如果满足模式的要求，则可信度与模式匹配有关。这是当您使用 Exchange 传输规则 (ETR) 时应考虑的可信度衡量标准。</p></td>
</tr>
<tr class="odd">
<td><p>patternsProximity</p></td>
<td><p><strong>patternsProximity</strong> 是指当我们找到疑似信用卡号的模式时，我们要查找确定证据的数字周围区域。</p></td>
</tr>
<tr class="even">
<td><p>recommendedConfidence</p></td>
<td><p>这是我们为此规则推荐的可信度。建议可信度适用于实体和关联。对于实体，永远不会针对模式的 <strong>confidenceLevel</strong> 评估此数字。它只是在您需要时帮助您选择可信度的一个建议。对于关联，模式的 <strong>confidenceLevel</strong> 必须高于 <strong>recommendedConfidence</strong> 数值，才能调用 ETR 操作。<strong>recommendedConfidence</strong> 是调用操作的 ETR 中所用的默认可信度。您可以根据需要，手动更改要调用的 ETR，以与模式的可信度互补。</p></td>
</tr>
</tbody>
</table>


## 详细信息

  - [如何通过应用 DLP 规则来评估邮件](how-dlp-rules-are-applied-to-evaluate-messages-exchange-2013-help.md)

  - [创建自定义 DLP 策略](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/data-loss-prevention/create-custom-dlp-policy)

  - [使用 Exchange 中的敏感信息类型查找什么](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md)

