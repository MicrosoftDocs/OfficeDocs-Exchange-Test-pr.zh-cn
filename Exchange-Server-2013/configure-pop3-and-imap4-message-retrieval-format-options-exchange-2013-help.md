---
title: '配置 POP3 和 IMAP4 邮件检索格式选项: Exchange 2013 Help'
TOCTitle: 配置 POP3 和 IMAP4 邮件检索格式选项
ms:assetid: 481096e0-4492-46c2-8ca8-bdf84a84531e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997869(v=EXCHG.150)
ms:contentKeyID: 50556572
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 POP3 和 IMAP4 邮件检索格式选项

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

您可以为使用 POP3 和 IMAP4 连接到其电子邮件的用户配置邮件检索格式。 可以使用 EAC 或命令行管理程序在服务器级别配置邮件检索选项，也可使用命令行管理程序在用户级别配置邮件检索选项。

有关与 POP3 和 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”和“IMAP4 设置”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 在服务器级别设置 POP3 邮件检索格式

## 使用 EAC 在服务器级别设置 POP3 邮件检索格式

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“POP3”。

4.  在“邮件 MIME 格式”下，从以下设置中进行选择：
    
      - 文本
    
      - HTML
    
      - HTML 和替代文本
    
      - 压缩文本
    
      - 压缩文本和替代文本
    
      - Best body format
    
      - TNEF

5.  单击“保存”。

为 POP3 设置邮件检索格式设置后，您必须重新启动 POP3 服务，设置才能生效。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令行管理程序在服务器级别设置 POP3 邮件检索格式

此示例针对服务器 CAS01 上的所有 POP3 用户将邮件检索格式选项设置为“仅文本”。

    Set-PopSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

可从以下设置中进行选择。 您可以通过使用数字值或文本字符串为 *MessageRetrievalMimeFormat* 参数指定值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>邮件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文本</p></td>
<td><p><code>0</code> 或者<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或者 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 和替代文本</p></td>
<td><p><code>2</code> 或者<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>压缩文本</p></td>
<td><p><code>3</code> 或者<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>压缩文本和替代文本</p></td>
<td><p><code>4</code> 或者<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> 或者<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或者 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


为 POP3 设置邮件检索格式设置后，您必须重新启动 POP3 服务，设置才能生效。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作，验证是否在服务器上成功设置了 POP3 邮件检索设置。

1.  在命令行管理程序中运行以下命令。
    
        Get-PopSettings | format-list

2.  验证 *MessageRetrievalMimeFormat* 设置是否正确。

## 在服务器级别设置 IMAP4 邮件检索格式

## 使用 EAC 在服务器级别设置 IMAP4 邮件检索格式

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“IMAP4”。

4.  在“邮件 MIME 格式”下，从以下设置中进行选择：
    
      - 文本
    
      - HTML
    
      - HTML 和替代文本
    
      - 压缩文本
    
      - 压缩文本和替代文本
    
      - Best body format
    
      - TNEF

5.  单击“保存”。

为 IMAP4 设置邮件检索格式设置后，您必须重新启动 IMAP4 服务，设置才能生效。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 使用命令行管理程序在服务器级别设置 IMAP4 邮件检索格式

此示例针对服务器 CAS01 上的所有 IMAP4 用户将邮件检索格式选项设置为“仅文本”。

    Set-ImapSettings -Identity CAS01 -MessageRetrievalMimeFormat TextOnly

可从以下设置中进行选择。 您可以通过使用数字值或文本字符串为 *MessageRetrievalMimeFormat* 参数指定值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>邮件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文本</p></td>
<td><p><code>0</code> 或者<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或者 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 和替代文本</p></td>
<td><p><code>2</code> 或者<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>压缩文本</p></td>
<td><p><code>3</code> 或者<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>压缩文本和替代文本</p></td>
<td><p><code>4</code> 或者<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> 或者<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或者 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


为 IMAP4 设置邮件检索格式设置后，您必须重新启动 IMAP4 服务，设置才能生效。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作，验证是否在服务器上成功设置了 IMAP4 邮件检索设置。

1.  在命令行管理程序中运行以下命令。
    
        Get-ImapSettings | format-list

2.  验证 *MessageRetrievalMimeFormat* 设置是否正确。

## 为用户设置 POP3 邮件检索格式

## 使用命令行管理程序为用户设置 POP3 邮件检索格式

此示例针对 `USER01` 的 POP3 访问权限将邮件检索格式设置为“仅文本”。

    Set-CASMailbox -Identity USER01 -PopMessagesRetrievalMimeFormat TextOnly

可从以下设置中进行选择。 您可以通过使用数字值或文本字符串为 *PopMessagesRetrievalMimeFormat* 参数指定值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>邮件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文本</p></td>
<td><p><code>0</code> 或者<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或者 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 和替代文本</p></td>
<td><p><code>2</code> 或者<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>压缩文本</p></td>
<td><p><code>3</code> 或者<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>压缩文本和替代文本</p></td>
<td><p><code>4</code> 或者<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> 或者<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或者 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


为 POP3 设置邮件检索格式设置后，您必须重新启动 POP3 服务，设置才能生效。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作，验证是否为用户成功设置了 POP3 邮件检索格式选项。

1.  在命令行管理程序中运行以下命令。
    
        Get-CAS Mailbox <identity> | format-list

2.  验证 *PopMessagesRetrievalMimeFormat* 的值是否正确。

## 为用户设置 IMAP4 邮件检索格式

## 使用命令行管理程序为用户设置 IMAP4 邮件检索格式

此示例针对 `USER01` 的 IMAP4 访问权限将邮件检索格式设置为“仅文本”。

    Set-CASMailbox -Identity USER01 -ImapMessagesRetrievalMimeFormat TextOnly

您可以通过使用数字值或文本字符串为 *ImapMessagesRetrievalMimeFormat* 参数指定值。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>邮件格式</strong></p></td>
<td><p><strong>值</strong></p></td>
</tr>
<tr class="even">
<td><p>文本</p></td>
<td><p><code>0</code> 或者<code>TextOnly</code></p></td>
</tr>
<tr class="odd">
<td><p>HTML</p></td>
<td><p><code>1</code> 或者 <code>HtmlOnly</code></p></td>
</tr>
<tr class="even">
<td><p>HTML 和替代文本</p></td>
<td><p><code>2</code> 或者<code>HtmlAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>压缩文本</p></td>
<td><p><code>3</code> 或者<code>TextEnriched</code></p></td>
</tr>
<tr class="even">
<td><p>压缩文本和替代文本</p></td>
<td><p><code>4</code> 或者<code>TextEnrichedAndTextAlternative</code></p></td>
</tr>
<tr class="odd">
<td><p>Best body format</p></td>
<td><p><code>5</code> 或者<code>BestBodyFormat</code></p></td>
</tr>
<tr class="even">
<td><p>TNEF</p></td>
<td><p><code>6</code> 或者 <code>Tnef</code></p></td>
</tr>
</tbody>
</table>


为 IMAP4 设置邮件检索格式设置后，您必须重新启动 IMAP4 服务，设置才能生效。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作，验证是否为用户成功设置了 IMAP4 邮件检索格式选项。

1.  在命令行管理程序中运行以下命令。
    
        Get-CAS Mailbox <identity> | format-list

2.  验证 *ImapMessagesRetrievalMimeFormat* 的值是否正确。

## 详细信息

在设置了 IMAP4 和 POP3 用户的邮件检索格式后，您可能还需要：

[对用户启用或禁用 POP3 访问](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[对用户启用或禁用 IMAP4 访问](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

[配置 IMAP4 的日历选项](configure-calendar-options-for-imap4-exchange-2013-help.md)

[配置 POP3 的日历选项](configure-calendar-options-for-pop3-exchange-2013-help.md)

