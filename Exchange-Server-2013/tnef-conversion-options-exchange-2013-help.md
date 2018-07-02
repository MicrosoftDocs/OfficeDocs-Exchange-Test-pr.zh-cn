---
title: 'TNEF 转换选项: Exchange 2013 Help'
TOCTitle: TNEF 转换选项
ms:assetid: 989a62fc-4bc1-448f-90c8-7c7b56fe1084
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb310786(v=EXCHG.150)
ms:contentKeyID: 52061386
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# TNEF 转换选项

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

可以指定是应当为离开 Exchange 组织的邮件保留传输中性封装格式 (TNEF) 还是删除该格式。TNEF（也称为 Outlook RTF 格式或 Exchange RTF 格式）是 Microsoft 特定的用于封装 MAPI 邮件属性的格式。MicrosoftOutlook 的所有版本都能完全理解 TNEF。Outlook Web App 将 TNEF 转换为 MAPI，并显示已设置格式的邮件。但是，不了解 TNEF 的其他电子邮件客户端通常将 TNEF 格式的邮件显示为带有 Winmail.dat 或 Win.dat 附件的纯文本邮件。

**目录**

远程域的 TNEF 转换选项

邮件用户和邮件联系人的 TNEF 转换选项

Outlook 中的 TNEF 转换选项

TNEF 转换选项的优先级顺序

## 远程域的 TNEF 转换选项

配置远程域的 TNEF 转换选项后，这些 TNEF 转换选项会应用于发送到该域的所有邮件。

  - 对于 Exchange Online 专用版，使用 Exchange 管理中心 (EAC) 在“邮件流”\>“远程域”\>“编辑” (![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")) \>“使用 Exchange RTF 格式”中设置远程域的 TNEF 转换选项。

  - 对于 Exchange Online 和 Exchange 2013，可以在 **Set-RemoteDomain** cmdlet 中使用 *TnefEnabled* 参数设置远程域的 TNEF 转换选项。

对于您组织中的远程域，TNEF 转换有以下配置选项：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>在 EAC 中</th>
<th>在 Shell 中</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用发送到远程域的所有邮件的 TNEF。</p></td>
<td><p><strong>Always</strong></p></td>
<td><p><code>$true</code></p></td>
</tr>
<tr class="even">
<td><p>从不使用发送到远程域的任何邮件的 TNEF。</p></td>
<td><p><strong>Never</strong></p></td>
<td><p><code>$false</code></p></td>
</tr>
<tr class="odd">
<td><p>不会明确允许或阻止发送到远程域中的收件人的 TNEF 邮件。TNEF 邮件是否发送给远程域中的收件人取决于邮件联系人或邮件用户的特定设置或发件人在 Outlook 中指定的设置。此值为默认值。</p></td>
<td><p><strong>Follow user settings</strong></p></td>
<td><p><code>$null</code>（空值）</p></td>
</tr>
</tbody>
</table>


有关远程域的详细信息，请参阅[远程域](remote-domains-exchange-2013-help.md)或 [Exchange Online 中的远程域](https://technet.microsoft.com/zh-cn/library/jj966211\(v=exchg.150\))。

返回顶部

## 邮件用户和邮件联系人的 TNEF 转换选项

配置邮件联系人或邮件用户的 TNEF 转换选项后，这些 TNEF 转换选项会应用于发送到此指定收件人的所有邮件。可以在 **Set-MailUser** 和 **Set-MailContact** cmdlet 中使用 *UseMapiRichTextFormat* 参数为邮件用户和邮件联系人配置 TNEF 转换选项。

对于组织中的邮件用户和邮件联系人，可用于 TNEF 转换的配置选项如下：

  - **始终**   TNEF 用于发送到收件人的所有邮件。*UseMapiRichTextFormat* 参数的对应值为 `Always`。

  - **从不**   TNEF 从不用于发送到收件人的任何邮件。*UseMapiRichTextFormat* 参数的对应值为 `Never`。

  - **使用默认设置**   尚未明确允许或阻止 TNEF 邮件用于邮件用户或邮件联系人。TNEF 邮件是否发送给收件人取决于相应远程域的特定设置或发件人在 Outlook 中指定的设置。*UseMapiRichTextFormat* 参数的对应值为 `UseDefaultSettings`。这是默认设置。

返回顶部

## Outlook 中的 TNEF 转换选项

发件人可以控制发送到 Exchange 组织外所有收件人的 TNEF 邮件的默认 TNEF 邮件转换选项。这些选项称为“Internet 邮件格式”选项。这些选项仅应用于远程收件人，不应用于 Exchange 组织中的收件人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>下列选项定义当包含 Outlook RTF 格式的邮件发送到外部收件人时如何处理这些邮件。如果使用的邮件格式是 HTML 或纯文本，则这些设置不适用。</td>
</tr>
</tbody>
</table>


在 Outlook 中有下列 TNEF 转换选项：

  - **转换为 HTML 格式**   这是默认选项。所有发送到远程收件人的 TNEF 邮件都转换为 HTML 格式。邮件中的格式应与原始邮件非常相似。许多（但并非所有）电子邮件客户端都支持 MIME 编码的 HTML 邮件。

  - **转换为纯文本格式**   所有发送到远程收件人的 TNEF 邮件都转换为纯文本格式。邮件中的所有格式都将丢失。

  - **以 Outlook RTF 格式发送**   所有发送到远程收件人的 TNEF 邮件仍是 TNEF 邮件。

可以在 Outlook 的下列位置配置这些选项：

  - **Outlook 2010 或 Outlook 2013**   “文件”\>“选项”\>“邮件”\>“邮件格式”。

  - **Outlook 2007**   “工具”\>“选项”\>“邮件格式”\>“Internet 格式”。

发件人还可以控制发送到 Exchange 组织外特定收件人的 TNEF 邮件的默认 TNEF 邮件转换选项。这些选项称为 *Internet 收件人邮件格式*选项。这些选项仅应用于“联系人”文件夹中的远程收件人，不应用于 Exchange 组织中的收件人。“联系人”文件夹中的远程收件人有下列 TNEF 转换选项：

  - **允许 Outlook 决定最佳发送格式**   这是默认设置。此设置强制 Outlook 使用默认 Internet 格式指定的 TNEF 转换选项。可以使用的值有“转换为 HTML 格式”、“转换为纯文本格式”或“以 Outlook RTF 格式发送”。所以，TNEF 邮件可以保留 TNEF 格式、转换为 HTML 格式或转换为纯文本格式。如果您希望确保该收件人的 TNEF 邮件保留 TNEF，则应将设置从“允许 Outlook 决定最佳发送格式”更改为“以 Outlook RTF 格式发送”。

  - **仅发送纯文本**   所有发送到收件人的 TNEF 邮件都转换为纯文本。邮件中的所有格式都将丢失。

  - **以 Outlook RTF 格式发送**   所有发送到远程收件人的 TNEF 邮件仍是 TNEF 邮件。

可以在 Outlook 的下列位置配置这些选项：

  - **Outlook 2010 或 Outlook 2013**   打开联系人卡片，双击电子邮件地址，单击“查看与此人互动的其他选项”图标，选择“Outlook 属性”。在“电子邮件属性”对话框中，选择“Internet 格式”。

  - **Outlook 2007**   打开联系人卡片，双击“电子邮件”字段，选择“Internet 格式”。

返回顶部

## TNEF 转换选项的优先级顺序

Exchange 使用以下列表介绍的优先级顺序来确定发送到 Exchange 组织以外收件人的传出邮件的 TNEF 转换选项。

1.  远程域设置

2.  邮件用户或邮件联系人设置

3.  Outlook 设置

该列表指定从最高级到最低级的优先级顺序。远程域上的 TNEF 设置覆盖了邮件用户、邮件联系人或 Outlook 中的 TNEF 设置。例如，假设您在 Outlook 中发送 RTF 格式邮件，但是某个域中的远程域经过特殊设置，因此该域中的收件人不允许接收 TNEF 格式的邮件。收件人接收的邮件将是纯文本或 HTML 格式，而不是 TNEF 格式。

而且，Exchange 从不将汇总传输中性编码格式 (STNEF) 邮件发送到外部收件人。只有 TNEF 邮件可以发送到 Exchange 组织外的收件人。

返回顶部

