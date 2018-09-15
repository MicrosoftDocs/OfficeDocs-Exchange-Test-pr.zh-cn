---
title: '使用传输规则检查邮件附件: Exchange 2013 Help'
TOCTitle: 使用传输规则检查邮件附件
ms:assetid: c0de687e-e33c-4e8a-b253-771494678795
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674307(v=EXCHG.150)
ms:contentKeyID: 50491594
ms.date: 02/08/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用传输规则检查邮件附件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-27_

您可以通过设置传输规则，在组织中检查电子邮件附件。Exchange 提供传输规则，作为邮件安全性和合规性的一部分，这些传输规则可以提供检查电子邮件附件的功能。当您检查附件时，您可以根据这些附件的内容或特征对经过检查的邮件采取操作。以下是您使用传输规则可以执行的一些与附件相关的任务：

  - 搜索压缩附件中的文件，如 .zip 和 .rar 文件，如果有任何文本与您指定的模式匹配，则在邮件的结尾添加免责声明。

  - 检查附件中的内容，如果有任何您指定的关键词，则将邮件重定向到仲裁人进行审批，然后再传递。

  - 检查包含无法检查的附件的邮件，然后阻止整个邮件的发送。

  - 检查超出特定大小的附件；如果选择阻止邮件传递，则通知发件人该问题。

  - 创建通知，在用户发送与传输规则匹配的邮件时警告用户。

  - 阻止包含附件的所有邮件。有关示例，请参阅[常见的附件阻止方案](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)。

Exchange 管理员可以通过转到“Exchange 管理中心”\>“邮件流”\>“规则”，来创建传输规则。您必须先获得权限，然后才能执行此过程。开始创建新规则后，单击“在以下情况应用此规则”下方的“更多选项”\>“任何附件”，便可查看与附件相关的条件的完整列表。与附件相关的选项如下图所示。

![用于选择与附件相关的规则的对话框](images/JJ674307.2ae4a179-bfd2-4a0e-abe1-53ed4e9e3368(EXCHG.150).jpg "用于选择与附件相关的规则的对话框")

有关传输规则的详细信息，包括您可以选择的全部条件与操作，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。Exchange Online Protection (EOP) 和混合客户可以从[配置 EOP 的最佳实践](https://technet.microsoft.com/zh-cn/library/jj723164\(v=exchg.150\))中提供的传输规则最佳实践中获益。如果您已经准备好要开始创建规则，请参阅[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)。

## 检查附件中的内容

您可以使用下表中的传输规则条件检查邮件附件的内容。这些条件只检查附件的前 150 KB。要在检查邮件时开始使用这些条件，您需要将它们添加到传输规则。要了解如何创建或更改规则，可参阅[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件名称</th>
<th>命令行管理程序中的条件名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件内容包含这些词语中的任何一个</strong></p></td>
<td><p><code>AttachmentContainsWords</code></p></td>
<td><p>此条件会匹配受支持的文件类型附件包含指定的字符串或一组字符的邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件内容与这些文本模式匹配</strong></p></td>
<td><p><code>AttachmentMatchesPatterns</code></p></td>
<td><p>此条件会匹配受支持的文件类型附件包含的文本模式与指定正则表达式匹配的邮件。</p></td>
</tr>
</tbody>
</table>


在此处列出的条件的 Exchange 命令行管理程序 名称为需要 `TransportRule` cmdlet 的参数。

  -  要了解有关该 cmdlet 的详细信息，可参阅 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\))。

  -  要了解这些条件的属性类型的详细信息，可参阅[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

传输规则只检查受支持类型文件的内容。如果传输规则代理遇到的附件不在受支持的文件类型的列表内，则将触发 `AttachmentIsUnsupported` 条件。下一节列出了受支持的文件类型。任何未列出的文件将触发 `AttachmentIsUnsupported` 条件。

## 压缩的存档文件

如果邮件包含压缩的存档文件，例如 .zip 或 .cab 文件，那么传输规则代理将检查附件中包含的各个文件。处理此类邮件的方式与处理具有多个附件的邮件类似。不检查压缩存档文件的属性。例如，如果容器文件类型支持注释，则不检查该字段。

## 传输规则内容检查支持的文件类型

下表列出了传输规则支持的文件类型。系统自动检测文件类型，方法是检查文件属性，而不是实际的文件扩展名，从而防止恶意黑客通过重命名文件扩展名来绕过传输规则筛选。拥有可执行代码，可以在传输规则情境中进行检查的文件类型列表可参见本主题后面部分。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Category</th>
<th>文件扩展名</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 2013、Office 2010 和 Office 2007</p></td>
<td><p>.docm, .docx, .pptm, .pptx, .pub, .one, .xlsb, .xlsm, .xlsx</p></td>
<td><p>默认情况下，不支持 Microsoft OneNote 和 Microsoft Publisher 文件。可以使用 IFilter 集成实现对这些文件类型的支持。有关详细信息，请参阅<a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">向 Exchange 2013 注册 Filter Pack IFilter</a>。</p>
<p>同时还会检查这些文件类型中包含的任何嵌入式部件的内容。但是，不检查任何未嵌入的对象（例如，链接的文档）。</p></td>
</tr>
<tr class="even">
<td><p>Office 2003</p></td>
<td><p>.doc, .ppt, .xls</p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>其他 Office 文件</p></td>
<td><p>.rtf, .vdw, .vsd, .vss, .vst</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>Adobe PDF</p></td>
<td><p>.pdf</p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p>.html</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>.xml, .odp, .ods, .odt</p></td>
<td><p>无</p></td>
</tr>
<tr class="odd">
<td><p>文本</p></td>
<td><p>.txt, .asm, .bat, .c, .cmd, .cpp, .cxx, .def, .dic, .h, .hpp, .hxx, .ibq, .idl, .inc、inf, .ini、inx, .js, .log, .m3u, .pl, .rc, .reg, .txt, .vbs, .wtx</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument</p></td>
<td><p>.odp, .ods, .odt</p></td>
<td><p>不处理 .odf 文件的任何部分。例如，如果 .odf 文件包含嵌入式文档，则不检查该嵌入式文档的内容。</p></td>
</tr>
<tr class="odd">
<td><p>AutoCAD 绘图</p></td>
<td><p>.dxf</p></td>
<td><p>不支持 AutoCAD 2013 文件。</p></td>
</tr>
<tr class="even">
<td><p>图像</p></td>
<td><p>.jpg, .tiff</p></td>
<td><p>仅检查与这些图像文件关联的元数据文本。没有任何光学字符识别。</p></td>
</tr>
</tbody>
</table>


## 检查附件的文件属性

以下传输规则条件将检查附加到邮件中的文件的属性。要在检查邮件时开始使用这些条件，您需要将它们添加到传输规则。拥有可执行代码，可以在传输规则情境中进行检查的受支持文件类型如下所列。有关创建或更改规则的详细信息，请参阅[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件名称</th>
<th>命令行管理程序中的条件名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件文件名匹配这些文本模式</strong></p></td>
<td><p><code>AttachmentNameMatchesPatterns</code></p></td>
<td><p>当邮件的附件为支持的文件类型，并且附件的名称中包含您指定的字符时，则匹配此条件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件的文件扩展名包含这些词</strong></p></td>
<td><p><code>AttachmentExtensionMatchesWords</code></p></td>
<td><p>当邮件的附件为支持的文件类型，并且附件的文件扩展名与您所指定的扩展名匹配时，则匹配此条件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件大小大于或等于</strong></p></td>
<td><p><code>AttachmentSizeOver</code></p></td>
<td><p>当邮件的附件为支持的文件类型，并且附件的大小超出您所指定的大小时，则匹配此条件。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件未完成扫描</strong></p></td>
<td><p><code>AttachmentProcessingLimitExceeded</code></p></td>
<td><p>当邮件附件未经过传输规则代理的检查时，则匹配此条件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件具有可执行内容</strong></p></td>
<td><p><code>AttachmentHasExecutableContent</code></p></td>
<td><p>此条件会匹配包含可执行文件作为附件的邮件。这里列出了受支持的文件类型。</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件采用密码保护</strong></p></td>
<td><p><code>AttachmentIsPasswordProtected</code></p></td>
<td><p>当邮件的附件为支持的文件类型，并且附件采用密码保护，则匹配此条件。</p></td>
</tr>
</tbody>
</table>


在此处列出的条件的 Exchange 命令行管理程序 名称为需要 `TransportRule` cmdlet 的参数。

  -  要了解有关该 cmdlet 的详细信息，可参阅 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\))。

  -  要了解这些条件的属性类型的详细信息，可参阅[Conditions and exceptions for mail flow rules on Mailbox servers](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

## 传输规则检查支持的可执行文件类型

传输代理通过检查文件属性（而不仅仅是文件扩展名）来使用真正的类型检测。这会帮助阻止恶意黑客通过重命名文件扩展名来绕过您的规则。下表列出了这些条件支持的可执行文件类型。如果发现了未在此处列出的文件，将触发 `AttachmentIsUnsupported` 条件。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件类型</th>
<th>本机扩展</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 WinRAR 存档程序创建的自解压存档文件。</p></td>
<td><p>.rar</p></td>
</tr>
<tr class="even">
<td><p>使用动态链接库扩展名的 32 位 Windows 可执行文件。</p></td>
<td><p>.dll</p></td>
</tr>
<tr class="odd">
<td><p>自解压的可执行程序文件。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>Java 存档文件。</p></td>
<td><p>.jar</p></td>
</tr>
<tr class="odd">
<td><p>卸载可执行文件。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="even">
<td><p>程序快捷方式文件。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>已编译的源代码文件或 3-D 对象文件或序列文件。</p></td>
<td><p>.obj</p></td>
</tr>
<tr class="even">
<td><p>32 位 Windows 可执行文件。</p></td>
<td><p>.exe</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Visio XML 绘图文件。</p></td>
<td><p>.vxd</p></td>
</tr>
<tr class="even">
<td><p>OS/2 操作系统文件。</p></td>
<td><p>.os2</p></td>
</tr>
<tr class="odd">
<td><p>16 位 Windows 可执行文件。</p></td>
<td><p>.w16</p></td>
</tr>
<tr class="even">
<td><p>磁盘操作系统文件。</p></td>
<td><p>.dos</p></td>
</tr>
<tr class="odd">
<td><p>欧洲计算机研究所防病毒研究标准防病毒测试文件。</p></td>
<td><p>.com</p></td>
</tr>
<tr class="even">
<td><p>Windows 程序信息文件。</p></td>
<td><p>.pif</p></td>
</tr>
<tr class="odd">
<td><p>Windows 可执行程序文件。</p></td>
<td><p>.exe</p></td>
</tr>
</tbody>
</table>


## 扩展受支持的文件类型的数目

本主题中列出的受支持的文件类型可以随时使用 IFilter 集成进行修改。有关详细信息，请参阅[向 Exchange 2013 注册 Filter Pack IFilter](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md)。

使用此过程添加的文件类型变为受支持的文件类型，并且不再触发 `AttachmentIsUnsupported` 条件。

## 数据丢失预防策略和附件传输规则

为了帮助您管理电子邮件中的重要业务信息，您可以将任何与附件相关的条件包含在数据丢失预防 (DLP) 策略的规则内。例如，您可能会希望允许发送包含护照号码的邮件，条件是仅当护照号码在密码保护的附件内。为实现这一目的，请执行下列操作：

  - 创建 DLP 策略，检查邮件中的与密码相关的敏感信息。有关详细信息，请参阅 [DLP 过程](dlp-procedures-exchange-2013-help.md)。

  - 在“即使…”传输规则区域添加“任何附件采用密码保护”例外。

  - 定义要对包含护照编号，且护照号码不在受保护文件内的邮件执行的操作。

DLP 策略和与附件相关的条件可以通过将您的业务需求定义为传输规则条件、例外和操作，来帮助您满足这些需求。当您将敏感信息检查包含在 DLP 策略中时，会对任何邮件附件仅针对该信息进行扫描。但是，不包含与附件相关的条件，例如大小或文件类型，除非您添加本主题中列出的条件。DLP 并非对所有版本的 Exchange 都可用；要了解更多信息，请访问[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)。

## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Use mail flow rules to inspect message attachments in Office 365](https://technet.microsoft.com/zh-cn/library/jj919236\(v=exchg.150\)) 位于 Exchange Online

