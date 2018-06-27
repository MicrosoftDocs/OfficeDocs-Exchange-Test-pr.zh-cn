---
title: '由 Exchange 搜索编制索引的文件格式: Exchange 2013 Help'
TOCTitle: 由 Exchange 搜索编制索引的文件格式
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 52061560
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 由 Exchange 搜索编制索引的文件格式

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-07-21_

MicrosoftExchange Server 2013 和 Exchange Online、Exchange Search 包含用于索引最常见的邮件附件文件格式的筛选器。您也可以安装用于索引其他文件类型的筛选器。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，安装并注册 Microsoft Office Filter Pack 并不是一项强制性要求。</td>
</tr>
</tbody>
</table>


管理或使用 Exchange Search 以及独立功能（如 [就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)）时，请注意不可搜索的项目和已禁用索引功能或不包含可以索引的内容的文件格式的区别：

  - **不可搜索的项目**   当 Exchange Search 因任何原因（例如，未安装筛选器）而无法索引特定文件类型时，您将无法搜索此文件类型。包含此类附件的邮件被标记为“部分编制索引”。可以使用 [Get-FailedContentIndexDocuments](https://technet.microsoft.com/zh-cn/library/dd351154\(v=exchg.150\)) cmdlet 检索不可搜索的项目。将就地电子数据展示搜索结果复制到发现邮箱或将搜索结果导出到 PST 文件时，您可以将不可搜索项目包括在内。有关详细信息，请参阅[Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)。

  - **不包含可以索引的内容的文件格式**   某些文件类型不包含可以索引的内容，因此自身也无法索引，如 Windows Media 视频 (WMV)。包含此类文件类型的附件的邮件也会在就地电子数据展示搜索中作为不可搜索的项目返回。

  - **已禁用的文件格式** 在本地组织中，管理员可以禁用指定文件格式的索引。包含此类已禁用格式的附件的邮件也会作为不可搜索的项目返回。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管邮件附件可能不可搜索或者使用不能编制索引的文件格式，但仍可对邮件正文和其他元数据编制索引，以便能在搜索结果中返回邮件。</td>
</tr>
</tbody>
</table>


有关与本地组织中的 Exchange Search 相关的其他管理任务，请参阅[Exchange 搜索过程](exchange-search-procedures-exchange-2013-help.md)。

## 默认筛选器

下表列出了在 Exchange 2013 邮箱服务器上和 Exchange Online 中安装的默认搜索筛选器。您可以使用 [Get-SearchDocumentFormat](https://technet.microsoft.com/zh-cn/library/jj873755\(v=exchg.150\)) cmdlet 获取默认筛选器列表。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>筛选器</th>
<th>文件扩展名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>电子邮件</p></td>
<td><p>.eml</p></td>
</tr>
<tr class="even">
<td><p>图形交换格式</p></td>
<td><p>.gif</p></td>
</tr>
<tr class="odd">
<td><p>JPEG</p></td>
<td><p>.jpeg</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Excel</p></td>
<td><p>.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb</p></td>
</tr>
<tr class="odd">
<td><p>Excel 文件</p></td>
<td><p>odbcexcel</p></td>
</tr>
<tr class="even">
<td><p>Microsoft InfoPath</p></td>
<td><p>.infopathml</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Office Binder</p></td>
<td><p>.obt, .obd</p></td>
</tr>
<tr class="even">
<td><p>Microsoft PowerPoint</p></td>
<td><p>.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Publisher</p></td>
<td><p>.pub</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Word</p></td>
<td><p>.doc, .docm, .dotx, .dotm, .dot, .docx</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft XML 纸张规范</p></td>
<td><p>.xps</p></td>
</tr>
<tr class="even">
<td><p>OneNote</p></td>
<td><p>.one</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 演示文稿</p></td>
<td><p>.odp</p></td>
</tr>
<tr class="even">
<td><p>OpenDocument 电子表格</p></td>
<td><p>.ods</p></td>
</tr>
<tr class="odd">
<td><p>OpenDocument 文本</p></td>
<td><p>.odt</p></td>
</tr>
<tr class="even">
<td><p>Outlook 项</p></td>
<td><p>.msg</p></td>
</tr>
<tr class="odd">
<td><p>Portable Document Format</p></td>
<td><p>.pdf</p></td>
</tr>
<tr class="even">
<td><p>RTF 格式</p></td>
<td><p>.rtf</p></td>
</tr>
<tr class="odd">
<td><p>文本</p></td>
<td><p>.txt</p></td>
</tr>
<tr class="even">
<td><p>vCalendar</p></td>
<td><p>.vcs</p></td>
</tr>
<tr class="odd">
<td><p>vCard</p></td>
<td><p>.vcf</p></td>
</tr>
<tr class="even">
<td><p>Visio</p></td>
<td><p>.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx</p></td>
</tr>
<tr class="odd">
<td><p>Web 档案</p></td>
<td><p>.mhtml</p></td>
</tr>
<tr class="even">
<td><p>网页</p></td>
<td><p>.html</p></td>
</tr>
<tr class="odd">
<td><p>XML 文档</p></td>
<td><p>.xml</p></td>
</tr>
<tr class="even">
<td><p>ZIP 存档</p></td>
<td><p>.zip</p></td>
</tr>
</tbody>
</table>


## 已禁用的文件格式

下表列出了在 Exchange 2013 邮箱服务器上和 Exchange Online 中默认禁用索引编制的搜索筛选器。在 Exchange 2013 中，管理员可以通过使用 [Set-SearchDocumentFormat](https://technet.microsoft.com/zh-cn/library/jj873756\(v=exchg.150\)) cmdlet 禁用或重新启用受支持的索引文件格式。此 cmdlet 在 Exchange Online 中不可用。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>筛选器</th>
<th>文件扩展名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AVI</p></td>
<td><p>.avi</p></td>
</tr>
<tr class="even">
<td><p>位图</p></td>
<td><p>.bmp</p></td>
</tr>
<tr class="odd">
<td><p>MP3</p></td>
<td><p>.mp3</p></td>
</tr>
<tr class="even">
<td><p>MPEG</p></td>
<td><p>.mpeg</p></td>
</tr>
<tr class="odd">
<td><p>PNG</p></td>
<td><p>.png</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows 波形音频</p></td>
<td><p>.wav</p></td>
</tr>
</tbody>
</table>

