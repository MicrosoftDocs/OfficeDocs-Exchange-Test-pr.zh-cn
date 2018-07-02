﻿---
title: '边缘传输服务器上的附件筛选: Exchange 2013 Help'
TOCTitle: 边缘传输服务器上的附件筛选
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60829996
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘传输服务器上的附件筛选

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-02-10_

在 Microsoft Exchange Server 2013 中，您可以使用边缘传输服务器上的附件筛选控制用户在电子邮件中收到的附件。附件筛选代理执行附件筛选，而且仅在边缘传输服务器上可用。

## 附件筛选的类型

可以使用下列类型的附件筛选来控制通过边缘传输服务器传入或传出组织的附件：

  - **基于文件名或文件扩展名的筛选**   可以指定要筛选的准确文件名或文件扩展名。`BadFileName.exe` 是文件名筛选器的一个示例。`*.exe` 是文件扩展名筛选器的一个示例。

  - **基于文件 MIME 内容类型的筛选**   可以指定要筛选的 MIME 内容类型值。MIME 内容类型值指明附件的类型，例如，JPEG 图像、可执行文件或 Microsoft Excel 文件。内容类型以 `type/subtype` 形式表示。例如，JPEG 图像文件表示为 `image/jpeg`。
    
    若要查看附件筛选可以检测的文件扩展名和内容类型的完整列表，请在边缘传输服务器上运行以下命令：
    
        Get-AttachmentFilterEntry | Format-List

定义要查找的文件后，您可以配置要对包含这些附件的邮件采取的操作。无法为不同类型的附件指定不同的操作。为匹配任意附件筛选器的所有邮件配置下列操作之一：

  - **拒绝（阻止）邮件**   阻止邮件。发件人收到一份未送达报告 (NDR)，该报告表明邮件因包含不可接受的附件而导致未送达。可以在 NDR 中自定义该文本。默认文本为：`Message rejected due to unacceptable attachments`.

  - **剥除附件但允许邮件通过**   将附件从邮件中删除。但是，允许通过邮件本身以及与筛选器不匹配的其他任何附件。如果附件被剥离，则会将其替换为文本文件，解释删除该附件的原因。此为默认操作。

  - **自动删除邮件**   删除邮件。发件人和收件人都不会收到通知。

有关详细信息，请参阅[管理边缘传输服务器上的附件筛选](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>无法检索已阻止的邮件或已剥除的附件。在配置附件筛选器时，请认真检查所有可能的文件名匹配项，并验证筛选器不会影响合法的附件。<br />
此外，不要从已经过数字签名、已加密或权利受到保护的电子邮件中删除附件。如果从此类邮件中删除附件，则可能会使已数字签名的邮件失效，并导致无法读取已加密和权利受到保护的邮件。</td>
</tr>
</tbody>
</table>

