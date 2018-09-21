---
title: '邮件编码选项: Exchange 2013 Help'
TOCTitle: 邮件编码选项
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 50491608
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件编码选项

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Exchange 中可使用的邮件编码选项可指定邮件特性，例如 MIME 和非 MIME 字符集、二进制编码以及附件格式。您可以在以下位置指定邮件编码选项：

  - 远程域设置

  - 邮件用户和邮件联系人设置

  - Microsoft Outlook 设置
    
      - 邮件格式
    
      - Internet 邮件格式
    
      - Internet 收件人邮件格式
    
      - 邮件字符集编码选项

**内容**

发送到远程域的邮件的邮件编码选项

邮件用户和邮件联系人的邮件编码选项

Outlook 中可用的邮件编码选项

Outlook Web App 中可用的邮件编码选项

邮件编码选项的优先级顺序

详细信息

## 发送到远程域的邮件的邮件编码选项

配置远程域的邮件编码选项时，特定设置将应用于发送到该域的所有邮件。对于组织中的远程域，可用于邮件编码的配置选项如下。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>设置</strong></p></td>
<td><p><strong>在 Exchange Online 专用版中的 EAC 中可用</strong></p></td>
<td><p><strong>在命令行管理程序中可用</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>MIME 字符集：</strong>所指定的字符集将仅用于本身未指定字符集的 MIME 邮件。设置此参数不会覆盖已在传出邮件中指定的字符集。</p>
<p><strong>非 MIME 字符集</strong>   如果满足以下任一条件，则会使用该设置：</p>
<ul>
<li><p>来自远程域的传入邮件在 MIME Content-Type 中缺少 <em>charset=</em> 设置的值：头字段的值。</p></li>
<li><p>发送到远程域的传出邮件缺少 MIME 字符集值。</p></li>
</ul>
<p></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><strong>内容类型：</strong>可以为发送到远程域中收件人的 MIME 邮件指定内容类型。可以使用下列设置：</p>
<ul>
<li><p><strong>MimeHtmlText：</strong>所有邮件均转换为使用 HTML 格式的 MIME 邮件，除非原始邮件是文本邮件。如果原始邮件是文本邮件，则传出邮件将为使用文本格式的 MIME 邮件。这是默认设置。</p></li>
<li><p><strong>MimeText：</strong>所有邮件均转换为使用文本格式的 MIME 邮件。</p></li>
<li><p><strong>MimeHtml：</strong>所有邮件均转换为使用 HTML 格式的 MIME 邮件。</p></li>
</ul></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><strong>换行大小：</strong>可以指定电子邮件正文中一行文本可包含的最大字符数。更早的电子邮件客户端应用程序可能首选每行 78 个字符。仅通过使用命令行管理程序时，才能使用此选项。</p>
<p></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件用户和邮件联系人的邮件编码选项

配置邮件联系人或邮件用户的邮件编码选项后，选项将应用于发送到特定收件人的所有邮件。对于组织中的邮件联系人和邮件用户，可用于邮件编码的配置选项如下：

  - **UsePreferMessageFormat：** 此参数指定为邮件联系人配置的邮件格式设置是否覆盖为远程域配置的全局设置。如果禁用该设置，Exchange 将忽略该收件人的其他邮件编码选项并且由远程域的配置或邮件发送人配置的设置确定。

  - **MessageFormat：** 此参数指定邮件格式。可以指定 Text 或 Mime 作为邮件格式。此设置值依赖于 *MessageBodyFormat* 参数。如果邮件正文格式为 Html 或 TextAndHtml，则必须将此参数设置为 Mime。

  - **MessageBodyFormat：** 此参数指定邮件正文格式。可以指定 Text、Html 或 TextAndHtml。此设置值依赖于 *MessageFormat* 参数。如果邮件格式为 Text，则此参数也必须设置为 Text。

  - **MacAttachmentFormat：** 此参数指定邮件的 Apple Macintosh 操作系统附件格式。可以指定 BinHex、UuEncode、AppleSingle 或 AppleDouble。此设置值依赖于 *MessageFormat* 参数。如果邮件格式设置为 Text，则必须将此参数设置为 BinHex 或 UuEncode。如果邮件格式设置为 Mime，则必须将此参数设置为 BinHex、AppleSingle 或 AppleDouble。

您需要在 Exchange 命令行管理程序中使用这些参数为邮件用户和邮件联系人设置邮件编码选项。有关详细信息，请参阅下列主题：

  - [Enable-MailContact](https://technet.microsoft.com/zh-cn/library/aa996001\(v=exchg.150\))

  - [New-MailContact](https://technet.microsoft.com/zh-cn/library/bb124519\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-cn/library/aa995950\(v=exchg.150\))

  - [Enable-MailUser](https://technet.microsoft.com/zh-cn/library/aa996549\(v=exchg.150\))

  - [New-MailUser](https://technet.microsoft.com/zh-cn/library/aa996335\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-cn/library/aa995971\(v=exchg.150\))

返回顶部

## Outlook 中可用的邮件编码选项

作为发件人，可在以下任何阶段于 Outlook 中指定邮件编码选项：

  - 通过将默认邮件格式配置为纯文本或 HTML。

  - 撰写邮件时，通过使用“选项”选项卡中的“格式”区域将邮件格式设置为纯文本或 HTML。

  - 通过配置发送到 Exchange 组织以外所有收件人的邮件的邮件编码选项。这些选项称为“Internet 邮件格式”选项。这些选项仅应用于远程收件人，不应用于 Exchange 组织中的收件人。

  - 通过配置发送到 Exchange 组织以外特定收件人的邮件的邮件编码选项。这些选项称为“Internet 收件人邮件格式”选项。这些选项仅应用于“联系人”文件夹中的远程收件人，不应用于 Exchange 组织中的收件人。

默认情况下，Outlook 使用自动字符集邮件编码，它通过扫描传出邮件的整个文本来确定用于邮件的适当编码。此设置适用于发送到 Internet 收件人和 Exchange 组织内的收件人的邮件。但是，可以绕过此步骤，为传出邮件指定首选编码。

返回顶部

## Outlook Web App 中可用的邮件编码选项

作为发件人，您可在以下任何阶段于 Outlook Web App 中指定邮件编码选项：

  - 通过在“设置”\>“选项”\>“设置”页的“邮件格式”部分中将默认邮件格式配置为纯文本或 HTML。

  - 通过使用“更多选项” (…) 菜单，然后选择“切换到纯文本”或“切换到 HTML”将邮件撰写为纯文本或 HTML，从而达到设置邮件格式的目的。

返回顶部

## 邮件编码选项的优先级顺序

Exchange 使用以下列表介绍的优先级顺序来确定发送到 Exchange 组织以外收件人的传出邮件的邮件编码选项。

1.  远程域设置

2.  Outlook 或 Outlook Web App 设置

3.  邮件用户或邮件联系人设置

该列表指定从最低级到最高级的优先级顺序。较高级别的设置会覆盖较低级别的设置。

下表说明邮件字符集编码选项从最低优先级到最高优先级的优先级顺序。

### 邮件字符集编码选项从最低优先级到最高优先级的优先级顺序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>远程域条目设置，使用 EAC 或 <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>CharacterSet</em></p></td>
<td><p>已指定</p></td>
</tr>
<tr class="even">
<td><p>远程域条目设置，使用 EAC 或 <strong>Set-RemoteDomain</strong></p></td>
<td><p><em>NonMimeCharacterSet</em></p></td>
<td><p>已指定</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 设置</p></td>
<td><p>邮件字符集编码</p></td>
<td><ul>
<li><p>自动选择</p></li>
<li><p>已指定</p></li>
</ul></td>
</tr>
</tbody>
</table>


在为远程域设置非 MIME 字符集时，会向以下邮件类型分配字符集：

  - 发送到不包含指定字符集的已配置远程域的传出邮件。

  - 来自不包含指定字符集的已配置远程域的传入邮件。

传输服务器的 Windows ANSI 代码页的值用于将字符集分配到下列类型的邮件：

  - 不包含指定字符集的内部邮件。

  - 包含指定字符集但不包含指定服务器代码页的内部邮件。

如果邮件包含指定但无效的字符集，则传输服务器将尝试使用有效字符集替换该无效字符集。

下表说明纯文本邮件编码选项从最低优先级到最高优先级的优先级顺序。

### 纯文本邮件编码选项从最低优先级到最高优先级的优先级顺序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>源</th>
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>LineWrapSize</em></p></td>
<td><ul>
<li><p>0 至 132</p></li>
<li><p>不限制</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 设置</p></td>
<td><p>邮件格式</p></td>
<td><p>纯文本</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 设置</p></td>
<td><p>Internet 邮件格式</p></td>
<td><p>纯文本选项：</p>
<ul>
<li><p>发送纯文本邮件时以 UuEncode 格式对附件进行编码</p></li>
<li><p>文本在第 <em>nn</em> 个字符处自动换行</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 设置</p></td>
<td><p>Internet 收件人邮件格式</p></td>
<td><p>纯文本格式：</p>
<ul>
<li><p>以 UuEncode 附件格式对附件进行编码</p></li>
<li><p>使用 BinHex Mac 附件格式</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><ul>
<li><p><code>$true</code></p></li>
<li><p><code>$false</code></p></li>
</ul>
<p>如果值为 <code>$false</code>，或者收件人未定义为 Exchange 组织中的邮件用户或邮件联系人，则将忽略邮件用户或邮件联系人设置。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><p>Text</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>UuEncode</p></li>
</ul></td>
</tr>
</tbody>
</table>


下表说明 MIME 邮件编码选项从最低优先级到最高优先级的优先级顺序。

### MIME 邮件编码选项从最低优先级到最高优先级的优先级顺序

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>源</th>
<th>参数</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-RemoteDomain</strong></p></td>
<td><p><em>ContentType</em></p></td>
<td><ul>
<li><p><code>MimeHtmlText</code></p></li>
<li><p><code>MimeText</code></p></li>
<li><p><code>MimeHtml</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 或 Outlook Web App 设置</p></td>
<td><p>邮件格式</p></td>
<td><ul>
<li><p>纯文本</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 设置</p></td>
<td><p>Internet 收件人邮件格式</p></td>
<td><p>MIME 邮件格式</p>
<ul>
<li><p>纯文本</p></li>
<li><p>同时包含纯文本和 HTML</p></li>
<li><p>HTML</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>UsePreferMessageFormat</em></p></td>
<td><p><code>$true</code></p>
<p><code>$false</code></p>
<p>如果值为 <code>$false</code>，或者收件人未定义为 Exchange 组织中的邮件用户或邮件联系人，则将忽略邮件用户或邮件联系人设置。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageFormat</em></p></td>
<td><ul>
<li><p>文本</p></li>
<li><p>Mime</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MessageBodyFormat</em></p></td>
<td><ul>
<li><p><code>Text</code></p></li>
<li><p><code>Html</code></p></li>
<li><p><code>TextAndHtml</code></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailContact</strong></p></td>
<td><p><em>MacAttachmentFormat</em></p></td>
<td><ul>
<li><p>BinHex</p></li>
<li><p>AppleSingle</p></li>
<li><p>AppleDouble</p></li>
</ul></td>
</tr>
</tbody>
</table>


返回顶部

## 详细信息

[邮件编码选项](message-encoding-options-exchange-2013-help.md)

[TNEF 转换选项](tnef-conversion-options-exchange-2013-help.md)

[远程域](remote-domains-exchange-2013-help.md)

[Exchange Online 中的远程域](https://technet.microsoft.com/zh-cn/library/jj966211\(v=exchg.150\))

[管理邮件用户](https://docs.microsoft.com/zh-cn/exchange/recipients-in-exchange-online/manage-mail-users)

[管理邮件联系人](https://docs.microsoft.com/zh-cn/exchange/recipients-in-exchange-online/manage-mail-contacts)

[在 Outlook 中更改邮件格式](https://go.microsoft.com/fwlink/p/?linkid=397890)

