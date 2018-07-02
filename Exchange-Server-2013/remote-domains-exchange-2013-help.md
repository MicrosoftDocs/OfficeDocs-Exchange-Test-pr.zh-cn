---
title: '远程域: Exchange 2013 Help'
TOCTitle: 远程域
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 50490020
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 远程域

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

可以创建远程域条目，以定义在 Microsoft Exchange Server 2013 组织和 Exchange 组织以外的域之间传输邮件时使用的设置。创建远程域条目时，将会控制发送到该域的邮件的类型。还可以将从组织中的用户发送的邮件格式策略和可接受的字符集应用到远程域中。远程域的设置是 Exchange 组织所适用的全局配置设置。

在邮箱服务器上的传输服务中进行分类期间，远程域设置将应用于邮件。当发生收件人解析时，收件人域将与配置的远程域进行匹配。如果远程域的配置阻止特定类型的邮件发送到该域中的收件人，则将删除该邮件。如果为远程域指定特定的邮件格式，则将修改邮件头和邮件内容。这些设置适用于由 Exchange 组织处理的所有邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果配置每个用户的邮件设置，则每个用户的设置将覆盖组织配置。</td>
</tr>
</tbody>
</table>


默认情况下，有一个单一的远程域条目。域地址空间配置为一个星号 (\*)。这表示所有远程域。如果未创建其他远程域条目，则发送到所有远程域中所有收件人的所有邮件都将应用相同的设置。

配置远程域后，可以防止某些类型的邮件发送到该域。这些邮件类型包括外出邮件、自动答复邮件、未送达报告 (NDR) 和会议转发通知。如果您有多林环境，则可能要允许这些类型的邮件发送到这些域。但是，如果识别出某个域发送垃圾邮件，则您可能要阻止这些类型的邮件发送到这些远程域。

**目录**

邮件格式

自动答复设置

控制 NDR 信息

## 邮件格式

可以为发送到远程域的电子邮件指定要使用的邮件格式和字符集。对于确保由域中发件人发送到远程域的电子邮件与接收电子邮件系统兼容，这些设置很有用。例如，如果知道远程域的邮件系统为 Exchange，则可以指定始终使用 Exchange RTF 格式。有关详细信息，请参阅[内容转换](content-conversion-exchange-2013-help.md)。

## 自动答复设置

在 Exchange 2013 中，用户可为内部收件人和外部收件人指定不同的自动答复。此外，在您的组织中可使用的自动答复类型还取决于正在使用的 Microsoft Outlook 版本。

在 Exchange 2013 中有两种自动答复类型：

  - **外部**Exchange 2013 和 Exchange 2010 支持该类型的自动答复。只能由 Outlook 2010 或 Office Outlook 2007 进行设置，或使用 Microsoft OfficeOutlook Web App 进行设置。

  - **内部**Exchange 2013 和 Exchange 2010 支持该类型的自动答复。只能由 Outlook 2010 或 Outlook 2007 进行设置，或使用 Outlook Web App 进行设置。

下表描述了各种客户端和服务器组合以及在每种方案下可以使用的自动答复类型。

**支持自动答复的客户端和服务器**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>客户端版本</th>
<th>Exchange 版本</th>
<th>支持的自动答复</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 或者 Outlook 2007</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>内部、外部</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>内部、外部</p></td>
</tr>
</tbody>
</table>


## 控制 NDR 信息

如本主题开头所述，可阻止将 NDR 发送到远程域。通过阻止 NDR 发送到远程域，可防止 NDR 邮件中包含的信息离开组织，从而限制恶意用户获得有关您的组织的信息。但是，这样也会阻止合法发件人接收 NDR，从而导致混淆和降低工作效率。

在 Exchange 2013 中，可精细地控制发往远程域的 NDR 的内容。在 Exchange 2013 中，可允许将 NDR 发往远程域，同时删除任何诊断信息。这样，在向外部发件人提供 NDR 通知的同时，仍可阻止有关 Exchange 部署的信息离开组织。

用 **Set-RemoteDomain** cmdlet 的新 *NDRDiagnosticInfoEnabled* 参数可控制此功能。由于对每个远程域都可配置此设置，因此可根据需要采用不同设置。例如，可选择删除默认远程域的 NDR 诊断信息，但允许将完整的 NDR 诊断信息发往代表合作伙伴的远程域。

有关这项新设置的详细信息，请参阅 [Set-RemoteDomain](https://technet.microsoft.com/zh-cn/library/aa997857\(v=exchg.150\))。

