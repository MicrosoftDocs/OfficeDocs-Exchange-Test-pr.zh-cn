---
title: '配置内容传输编码: Exchange 2013 Help'
TOCTitle: 配置内容传输编码
ms:assetid: c4922362-18d4-42f7-9189-9076720eb1d8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg144562(v=EXCHG.150)
ms:contentKeyID: 50491490
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置内容传输编码

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

“内容传输编码”定义将二进制电子邮件数据转变为 US-ASCII 纯文本格式的方法。此转换允许邮件通过仅支持 US-ASCII 文本邮件的旧版 SMTP 邮件服务器。内容传输编码在 RFC 2045 中定义。传输编码方法存储在邮件中的“内容传输编码”标题字段中。在 Microsoft Exchange Server 2013 中，有以下内容传输编码方法可用：

  - **7 位**   该值表示邮件正文已采用 US ASCII 纯文本格式，并且尚未对邮件进行邮件编码。

  - **Quoted-printable (QP)**   此编码方法使用可打印 US-ASCII 字符对邮件正文数据进行编码。如果原始邮件文本大部分都是 US-ASCII 文本，则 QP 编码可提供便于阅读的紧凑的显示结果。默认情况下，Exchange 2013 使用 QP 对二进制消息数据编码。

  - **Base64**   此编码方法在很大程度上基于 RFC 1421 中定义的增强隐私邮件 (PEM) 标准。Base64 编码使用 64 个字符字母编码方法和 PEM 定义的输出填充字符对邮件正文数据进行编码。经 Base64 编码而增加的邮件大小是可预测的，对于二进制数据和非 US-ASCII 文本来说它是最佳选择。

您使用“Set-OrganizationConfig”上的 *ByteEncoderTypeFor7BitCharsets* 参数和 **Set-RemoteDomain** cmdlet 配置传输编码方法。您使用 **Set-OrganizationConfig** 配置的内容传输编码设置适用于 Exchange 组织中的所有邮件。您使用 **Set-RemoteDomain** 配置的内容传输编码设置仅适用于发送至远程域中外部收件人的邮件。

下表列出了可用于设置传输编码方法的值。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Set-OrganizationConfig</strong> 中的参数</th>
<th><strong>Set-RemoteDomain</strong> 中的参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p><code>Use7Bit</code></p></td>
<td><p>对于 HTML 和纯文本始终使用 7 位编码。此值为默认值。</p></td>
</tr>
<tr class="even">
<td><p>1</p></td>
<td><p><code>UseQP</code></p></td>
<td><p>对于 HTML 和纯文本始终使用 QP 编码。</p></td>
</tr>
<tr class="odd">
<td><p>2</p></td>
<td><p><code>UseBase64</code></p></td>
<td><p>对于 HTML 和纯文本始终使用 Base64 编码。</p></td>
</tr>
<tr class="even">
<td><p>5</p></td>
<td><p><code>UseQPHtmlDetectTextPlain</code></p></td>
<td><p>对于 HTML 和纯文本使用 QP 编码，除非纯文本中已启用换行。如果已启用换行，请对纯文本使用 7 位编码。</p></td>
</tr>
<tr class="odd">
<td><p>6</p></td>
<td><p><code>UseBase64HtmlDetectTextPlain</code></p></td>
<td><p>对于 HTML 和纯文本使用 Base64 编码，除非纯文本中已启用换行。如果纯文本中已启用换行，则对于 HTML 使用 Base64 编码，对于纯文本使用 7 位编码。</p></td>
</tr>
<tr class="even">
<td><p>13</p></td>
<td><p><code>UseQPHtml7BitTextPlain</code></p></td>
<td><p>对于 HTML 始终使用 QP 编码。对于纯文本始终使用 7 位编码。</p></td>
</tr>
<tr class="odd">
<td><p>14</p></td>
<td><p><code>UseBase64Html7BitTextPlain</code></p></td>
<td><p>对于 HTML 始终使用 Base64 编码。对于纯文本始终使用 7 位编码。</p></td>
</tr>
</tbody>
</table>


有关“内容传输编码”标题字段的详细信息，请参阅[内容转换](content-conversion-exchange-2013-help.md)中的“了解电子邮件的结构”部分。

有关远程域的详细信息，请参阅[远程域](remote-domains-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序来配置组织的内容传输编码方法

要配置组织的内容传输编码方法，可运行以下命令：

```powershell
Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets <Integer>
```

例如，要设置内容传输编码方法为 Base64，请运行以下命令：

```powershell
Set-OrganizationConfig -ByteEncoderTypeFor7BitCharsets 2
```

## 使用命令行管理程序来配置远程域的内容传输编码方法

要配置远程域中所有收件人的内容传输编码方法，可运行以下命令：

```powershell
Set-RemoteDomain -ByteEncoderTypeFor7BitCharsets <Value>
```

例如，要设置内容传输编码方法为 Base64，请运行以下命令：

```powershell
Set- RemoteDomain -ByteEncoderTypeFor7BitCharsets UseBase64
```

## 您如何知道这有效？

为了确认您已经成功配置了内容传输编码的方法，请执行下列操作：

1.  将包含 US-ASCII 文本和二进制数据或非 US-ASCII 文本混合格式的测试邮件发送至内部或外部测试帐户。使用内部帐户来测试组织设置，并使用远程域中的外部帐户来测试远程域设置。

2.  在电子邮件客户端中，查看邮件中的 **Content-Transfer-Encoding** 标题字段，并检查邮件上使用的内容传输编码方法是否与您所配置的匹配。

