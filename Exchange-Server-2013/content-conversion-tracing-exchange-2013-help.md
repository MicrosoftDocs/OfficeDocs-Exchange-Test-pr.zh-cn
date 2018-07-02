---
title: '内容转换跟踪: Exchange 2013 Help'
TOCTitle: 内容转换跟踪
ms:assetid: eb9c7df2-9093-49f9-aa4f-044909bd2225
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb397226(v=EXCHG.150)
ms:contentKeyID: 50491909
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 内容转换跟踪

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-09-25_

内容转换跟踪将捕获发生在 Microsoft Exchange Server 2013 邮箱服务器上入站和出站邮件上邮箱传输服务执行的 MAPI 内容转换中的失败。

邮箱服务器上的邮箱传输服务负责对邮箱收件人收发的所有邮件进行内容转换。 具体来说，邮箱传输提交服务将来自邮箱用户的出站邮件从 MAPI 转换为 MIME， 邮箱传输传递服务将邮箱用户的入站邮件从 MIME 转换为 MAPI。 内容转换跟踪负责捕获这些 MAPI 转换失败。

邮箱服务器上传输服务中的分类程序负责对发送给外部收件人的所有邮件进行内容转换。 但是，内容转换跟踪不会捕获传输服务中分类程序转换发送到外部收件人的邮件时遇到的任何内容转换失败。

**目录**

配置内容转换跟踪

内容转换跟踪工作原理

内容转换跟踪的注意事项

## 配置内容转换跟踪

内容转换跟踪由 Exchange 命令行管理程序中 **Set-TransportService** 和 **Set-MailboxTransportService** cmdlet 中的以下参数控制：

  - *ContentConversionTracingEnabled*   该参数启用或禁用邮箱服务器上传输服务中或邮箱服务器上邮箱传输服务中的内容转换跟踪。此参数的有效值是 `$true` 和 `$false`。默认值为 `$false`。 如果您的 Exchange 组织包含多个邮箱服务器，则必须在每个邮箱服务器上启用内容转换跟踪。

  - *PipelineTracingPath*   虽然此参数与管道跟踪相关联，但是它也可以指定内容转换跟踪文件的根位置。传输服务中的默认位置是 `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`。 邮箱传输服务中的默认位置为 `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`。路径必须在 Exchange 计算机本机上。

内容转换在 *PipelineTracingPath* 参数指定的路径中创建名为 `ContentConversionTracing` 的文件夹。 在 `ContentConversionTracing` 文件夹中，内容转换创建两个子文件夹：`InboundFailures` 和 `OutboundFailures`。 `InboundFailures` 文件夹包含入站邮件内容转换失败的信息。 `OutboundFailures` 文件夹包含出站邮件内容转换失败的信息。

`InboundFailures` 文件夹或 `OutboundFailures` 文件夹中所有文件的最大大小为 128 MB。 内容转换跟踪目录不会根据文件的期限或大小使用循环日志记录来删除旧文件。 一旦某个文件夹达到了最大大小，内容转换跟踪就会停止向该文件夹写入信息。 如果要确保文件夹不超出最大大小限制，您可以创建一个计划任务定期将内容转换跟踪文件移动到其他位置。

在内容转换跟踪中需要对文件夹和子文件夹具有以下权限：

  - 管理员： 完全控制

  - 网络服务： 完全控制

  - 系统：完全控制

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>内容转换跟踪将复制电子邮件的完整内容。 为了避免不利地披露机密信息，需要对内容转换跟踪文件的位置设置适当的安全权限。</td>
</tr>
</tbody>
</table>


返回顶部

## 内容转换跟踪工作原理

入站邮件的内容转换失败时，会向邮件发件人发送一封状态代码为 5.6.0 的传递状态通知 (DSN)。 如果已启用内容转换跟踪，则在生成 5.6.0 DSN 邮件时会记录该失败信息。 每个内容转换错误生成两个单独的文件。

将入站邮件从 MIME 转换为 MAPI 时发生的内容转换错误会在 InboundFailures 文件夹中生成以下两个文件：

  - **\<GUID\>.eml**   此文件包含以文本格式显示的失败邮件。

  - **\<GUID\>.txt**   此文件包含异常说明、转换结果、转换选项以及邮箱传输服务对所有邮件施加的邮件大小限制。

将出站邮件从 MAPI 转换为 MIME 时发生的内容转换错误会在 OutboundFailures 文件夹中生成以下两个文件：

  - **\<GUID\>.msg**   此文件包含以 Microsoft Outlook 邮件格式显示的失败邮件。

  - **\<GUID\>.txt**   此文件包含异常说明、转换结果、转换选项以及存储驱动程序对所有邮件施加的邮件大小限制。

两个文件名称中的占位符 \<*GUID*\> 是相同的。 每个内容转换错误都会生成不同的 GUID，用在对应的邮件和文本文件的文件名中。 `038b930e-61fd-4bfd-b9b4-0374c18b73f7` 就是一个用在文件名中的 GUID 示例。

返回顶部

## 内容转换跟踪的注意事项

可以使内容转换跟踪处于启用状态以便进行主动监视。 或者，还可以启用内容转换跟踪以解决特定失败事件问题。 通常，通过要求 5.6.0 DSN 邮件的收件人重新发送原始邮件可以重现入站内容转换失败。

入站内容转换失败最为常见。 出现入站内容转换错误的一些原因如下：

  - **违反邮件大小限制**   这些邮件大小限制由邮箱传输服务施加，以免受到拒绝服务 (DoS) 攻击。 \<*GUID*\>.txt 文件中列出了这些邮件限制。 这些邮件限制包括：
    
      - **MaxMimeTextHeaderLength**   此限制指定可在 MIME 头中使用的最大文本字符数。 该值为 2000。
    
      - **MaxMimeSubjectLength**   此限制指定可在主题行中使用最大文本字符数。 该值为 255。
    
      - **MSize**   此限制指定最大邮件大小。 该值为 2147483647 字节。
    
      - **MaxMimeRecipients**   此限制指定“收件人”、“抄送”和“密件抄送”。 该值为 12288。
    
      - **MaxRecipientPropertyLength**   此限制指定可在收件人描述中使用的最大文本字符数。 该值为 1000。
    
      - **MaxBodyPartsTotal**   此限制指定可在 MIME 多部分邮件中使用的最大邮件部分数。 该值为 250。
    
      - **MaxEmbeddedMessageDepth**   此限制指定邮件中可以存在的最大转发邮件数。 该值为 30。
    
    有关在邮件服务器或边缘传输服务器上传输服务中使用的可配置邮件大小限制的详细信息，请参阅[邮件大小限制](message-size-limits-exchange-2013-help.md)。

  - **将入站 iCalendar 邮件转换为会议请求失败**   RFC 2445 将 iCalendar 定义为日历数据交换的标准。 转换失败的特定原因包括：
    
      - 发送代理未正确使用 iCalendar。
    
      - Outlook 或 Exchange 日历架构不支持 iCalendar 结构。
    
    iCalendar 转换失败并不会导致发件人收到 5.6.0 DSN 邮件。 但是，该邮件将与包含 iCalendar 邮件正文的附加 .ics 文件一起发送。

  - **MIME 邮件格式不正确导致的失败**   商业垃圾邮件或垃圾邮件的邮件头可能存在格式错误，如收件人描述中的引号不匹配。 由 MIME 邮件格式不正确导致的失败（这种失败的次数要少得多）被视为缺陷。

相对于入站失败，出站内容转换失败较为少见。 如果发生出站失败，它们通常是由 Exchange 代码错误或已损坏的邮件内容导致的。

返回顶部

