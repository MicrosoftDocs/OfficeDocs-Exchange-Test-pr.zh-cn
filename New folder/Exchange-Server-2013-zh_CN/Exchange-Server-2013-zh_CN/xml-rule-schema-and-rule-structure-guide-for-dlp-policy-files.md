---
title: DLP 策略文件的 XML 规则架构和规则结构指南
TOCTitle: 开发 DLP 策略模板文件
ms:assetid: 4b263547-aef4-4ee8-aa4f-fa64a5863189
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674703(v=EXCHG.150)
ms:contentKeyID: 50490487
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 开发 DLP 策略模板文件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

本概述阐明了用于数据丢失防护 (DLP) 策略模板文件的 XML 架构定义组件，还提供了 XML 格式的示例策略文件。这有助于您在开始之前了解整个 DLP 体系结构和规则开发流程。有关详细信息，请参阅[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)和[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)。

为了便于采纳和管理数据丢失防护解决方案，Microsoft Exchange Server 2013 中引入了被称为 DLP 策略和策略模板的概念模型。DLP 策略模板为您预期的 DLP 策略提供初步设计。为了使策略更富有意义，DLP 策略模板必须封装为满足特定策略目标（如管理或业务需求）所需的所有指令和数据对象。该模板不针对特定环境。它只是一个策略定义或模型，可作为产品配置的一部分提供，或者由独立的软件供应商及合作伙伴提供。另一方面，DLP 策略是特定于开发环境的模板的运行时实例化。通过使用传输规则，现有消息策略框架可以包括 DLP 策略。传输规则在采纳和表达 DLP 解决方案的丰富性方面给予了很大的灵活性。

## 策略模板源和结构

DLP 策略模板通常受到许多源的影响，例如基于服务器的处理指令、客户端计算机策略，以及其他策略结构，如下图所示：

![影响策略模板的因素](images/JJ674703.12f48e4f-d7b8-4ddd-87e8-8477983252ec(EXCHG.150).gif "影响策略模板的因素")

通过 Exchange 命令行管理程序和基于 Internet 的界面，例如 Exchange 管理中心，简单的管理操作可用于 DLP 策略模板，这些操作包括导入、导出、删除和查询。在创建过程中引用 DLP 策略模板可以创建 DLP 策略。这些引用的 DLP 策略模板可以是系统中安装的策略所引用的模板（存储在 Active Directory 域服务中），也可以作为直接来自外部提供策略的输入。

DLP 策略模板表示为 XML 文档。Exchange 内部及外部提供的策略使用单个 XML 架构。XML 文档的概念结构如下表所示，其中显示了一些主要元素。策略组件定义集可以帮助您实现特定策略目标，例如管理或业务需求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>结构元素</th>
<th>含义或示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Publisher</p></td>
<td><p>Microsoft 或合作伙伴</p></td>
</tr>
<tr class="even">
<td><p>Version</p></td>
<td><p>15.0.1.0</p></td>
</tr>
<tr class="odd">
<td><p>Policy Name</p></td>
<td><p>PCI-DSS</p></td>
</tr>
<tr class="even">
<td><p>Description</p></td>
<td><p>PCI-DSS DLP 策略帮助检测 PCI 数据安全标准 (PCI DSS) 的信息（包括信用卡或借记卡号等信息）是否存在。使用此策略并不能确保遵守任何法规。在您的测试完成之后，请在 Exchange 中进行所需的配置更改，使信息传输符合您组织的策略。相关示例包括，配置已知业务合作伙伴的 TLS 或添加更多限制的传输规则操作，比如向包含此类型数据的邮件添加权限保护。</p></td>
</tr>
<tr class="odd">
<td><p>Metadata</p></td>
<td><p>用来描述地方法规、国家或地区、关键字以及其他信息的标记。</p></td>
</tr>
<tr class="even">
<td><p>Set of policy constructs</p></td>
<td><ol>
<li><p>传输规则定义，例如条件和操作。</p></li>
<li><p>通过交互式通知控制客户端体验的电子邮件客户端行为定义。</p></li>
<li><p>需要与客户端的特定环境设置相协调的配置参考（可选）。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Set of data classifications</p></td>
<td><ol>
<li><p>指定分类实体或相关性。</p></li>
<li><p>实体有计数和可信度；相关性只有可信度。</p></li>
<li><p>包括自身属性和分类架构的集合。</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 策略模板格式定义

DLP 策略模板表示为 XML 文档，该文档遵循以下架构。请注意，XML 区分大小写。例如，`dlpPolicyTemplates` 有效，但 `DlpPolicyTemplates` 无效。

    <?xml version="1.0" encoding="UTF-8"?>
    <dlpPolicyTemplates>
      <dlpPolicyTemplate id="F7C29AEC-A52D-4502-9670-141424A83FAB" mode="Audit" state="Enabled" version="15.0.2.0">
        <contentVersion>4</contentVersion>
        <publisherName>Microsoft</publisherName>
        <name>
          <localizedString lang="en">PCI-DSS</localizedString>
        </name>
        <description>
          <localizedString lang="en">Detects the presence of information subject to Payment Card Industry Data Security Standard (PCI-DSS) compliance requirements.</localizedString>
        </description>
        <keywords></keywords>
        <ruleParameters></ruleParameters>
        <ruleParameters/>
        <policyCommands>
          <!-- The contents below are applied/executed as rules directly in PS - -->
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP Policy."]]>
          </commandBlock>
          <commandBlock>
            <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "%%DlpPolicyName%%" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP Policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]>
          </commandBlock>
        </policyCommands>
        <policyCommandsResources></policyCommandsResources>
      </dlpPolicyTemplate>
    </dlpPolicyTemplates>

如果包含在 XML 文件中的任何元素的参数包含空格，该参数必须使用双引号括住，否则它将无法正常工作。在以下示例中，以 `-SentToScope` 开头的参数是可接受的，不需要使用双引号，因为它是一个不包含空格的连续字符串。但是，为 –`Comments` 提供的参数将不会在 Exchange 管理中心中显示，因为它没有使用双引号且包含空格。

    <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments Monitors payment card information sent inside the organization -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>

## localizedString 元素

通过模板格式可以将模板中的字符串本地化，以便向最终用户显示，例如可用于选择要安装哪些 DLP 策略模板。localizedString 元素可用于为“名称”和“描述”字段提供多种定义。

## ruleParameters 节点

这是在模板实例化阶段创建要映射到特定部署对象的 DLP 策略时，需要提供的可选参数集。例如部署中可用的实际通讯组。

## dlpPolicyTemplate 元素

这是 DLP 策略模板的根元素，每个模板都需要此元素。可用属性如下表所示：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>必需？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>是</p></td>
<td><p>此 DLP 策略模板文档使用的版本号。</p></td>
</tr>
<tr class="even">
<td><p>State</p></td>
<td><p>否</p></td>
<td><p>策略状态的默认配置（可选）。</p></td>
</tr>
<tr class="odd">
<td><p>Mode</p></td>
<td><p>否</p></td>
<td><p>策略模式的默认配置（可选）。</p></td>
</tr>
<tr class="even">
<td><p>Id</p></td>
<td><p>否</p></td>
<td><p>用来唯一标识此 DLP 策略模板定义的 GUID，格式如下所示：“A29C69BF-4F98-47F1-9A99-5771DFD2C27F”。</p></td>
</tr>
</tbody>
</table>


子元素包括以下一系列元素。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子元素</th>
<th>（最小值, 最大值）</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PublisherName</p></td>
<td><p>(1, 1)</p></td>
<td><p>此模板发布者的元数据</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>(1, 1)</p></td>
<td><p>此模板的本地化名称。</p></td>
</tr>
<tr class="odd">
<td><p>Description</p></td>
<td><p>(1, 1)</p></td>
<td><p>此模板的本地化描述。</p></td>
</tr>
<tr class="even">
<td><p>Keywords</p></td>
<td><p>(1, 1)</p></td>
<td><p>适用于此模板的关键字列表。模板可能会有一个空的关键字列表。</p></td>
</tr>
<tr class="odd">
<td><p>RuleParameters</p></td>
<td><p>(0, 1)</p></td>
<td><p>策略定义中使用的模板参数列表。</p></td>
</tr>
<tr class="even">
<td><p>PolicyCommands</p></td>
<td><p>(0, 1)</p></td>
<td><p>此策略的传输规则定义列表。这是可选元素。</p></td>
</tr>
</tbody>
</table>


## DLP 策略模板：PolicyCommands

此部分的策略模板包含用于实例化策略定义的 Exchange 命令行管理程序命令的列表。作为实例化过程的一部分，导入过程将执行每条命令。这里提供了一些策略命令示例。

    <PolicyCommands>
        <!-- The contents below are applied/executed as rules directly in PS - -->
          <CommandBlock> <![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Outside" -DlpPolicy "PCI-DSS" -SentToScope NotInOrganization -SetAuditSeverity High -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } -Comments "Monitors payment card information sent to outside the organization as part of the PCI-DSS DLP policy."]]></CommandBlock>
          <CommandBlock><![CDATA[ new-transportRule "PCI-DSS: Monitor Payment Card Information Sent To Within" -DlpPolicy "PCI-DSS" -Comments "Monitors payment card information sent inside the organization as part of the PCI-DSS DLP policy." -SentToScope InOrganization -SetAuditSeverity Low -MessageContainsDataClassifications @{Name="Credit Card Number"; MinCount="1" } ]]> </CommandBlock>
      </PolicyCommands> 

cmdlet 格式是所使用的 cmdlet 的标准 Exchange 命令行管理程序 cmdlet 语法。这些命令将按顺序执行。每个命令节点可以包含由多个命令组成的一个脚本块。以下示例表明了如何在 dlp 策略模板中嵌入分类规则包，并且作为策略创建过程的一部分来安装规则包。在策略模板中嵌入分类规则包，之后此规则包作为参数传输到模板中的 cmdlet：

``` 
<CommandBlock>
  <![CDATA[
$rulePack = [system.Text.Encoding]::Unicode.GetBytes('<?xml version="1.0" encoding="utf-16"?>
<rulePackage xmlns="http://schemas.microsoft.com/office/2011/mce">

  <RulePack id="c3f021a3-c265-4dc2-b3a7-41a1800bf518">
    <Version major="1" minor="0" build="0" revision="0"/>
    <Publisher id="e17451d3-9648-4117-a0b1-493a6d5c73ad"/>
    <Details defaultLangCode="en-us">
      <LocalizedDetails langcode="en-us">
        <PublisherName>Contoso</PublisherName>
        <Name>Contoso Sample Rule Pack</Name>
        <Description>This is a sample rule package</Description>
      </LocalizedDetails>
    </Details>
  </RulePack>

  <Rules>
    <Entity id="7cc35258-6b35-4415-baff-a76d1a018980" patternsProximity="300" recommendedConfidence="85" workload="Exchange">     

      <Pattern confidenceLevel="85">
        <IdMatch idRef="Regex_Contoso" />
        <Any minMatches="1">
          <Match idRef="Regex_conf" />
        </Any>
      </Pattern>
    </Entity>

    <Regex id="Regex_Contoso">(?i)(\bContoso\b)</Regex>
    <Regex id="Regex_conf">(?i)(\bConfidential\b)</Regex>

    <LocalizedStrings>
      <Resource idRef="7cc35258-6b35-4415-baff-a76d1a018980">
        <Name default="true" langcode="en-us">
          Confidential Information Rule
        </Name>
        <Description default="true" langcode="en-us">
          Sample rule pack - Detects Contoso confidential information
        </Description>
      </Resource>
    </LocalizedStrings>
  </Rules>

</RulePackage>

')


New-ClassificationRuleCollection -FileData $rulePack 
New-TransportRule -name "customEntity" -DlpPolicy "%%DlpPolicyName%%" -SentToScope NotInOrganization -MessageContainsDataClassifications @{Name="Confidential Information Rule"} -SetAuditSeverity High]]>
</CommandBlock> 
```

子元素包括以下有序元素序列。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>子元素</th>
<th>（最小值, 最大值）</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CommandBlock</p></td>
<td><p>(1, n)</p></td>
<td><p>在 PowerShell 中执行的命令块。每个命令块均按顺序执行。</p></td>
</tr>
</tbody>
</table>


## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[定义您自己的 DLP 模板和信息类型](define-your-own-dlp-templates-and-information-types-exchange-2013-help.md)

[从文件导入自定义 DLP 策略模板](import-a-custom-dlp-policy-template-from-a-file-exchange-2013-help.md)

