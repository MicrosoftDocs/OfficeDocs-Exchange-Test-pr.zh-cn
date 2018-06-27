---
title: '内容转换: Exchange 2013 Help'
TOCTitle: 内容转换
ms:assetid: bc367eb3-0306-4da9-9a84-4341caef77af
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232174(v=EXCHG.150)
ms:contentKeyID: 50491436
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 内容转换

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

“内容转换”是针对每个收件人正确设置邮件格式的过程。是否对邮件执行内容转换取决于要处理的邮件的目标和格式。在 Microsoft Exchange Server 2013 中存在两种不同的内容转换：

  - **外部收件人的邮件转换**   此类型的内容转换包括传输中性封装格式 (TNEF) 转换选项和外部收件人的邮件编码选项。发送到 Exchange 组织内部的收件人的邮件不要求此类型的内容转换。此类型的内容转换由邮箱服务器上传输服务中的分类程序进行处理。在将新到达的邮件放入提交队列之后，对每封邮件进行分类。除了收件人解析和路由解析外，还要对邮件执行内容转换，然后再将该邮件放入传递队列。如果单个邮件包含多个收件人，则分类程序会针对每个邮件收件人确定相应的编码。但是，内容转换跟踪不会捕获分类程序转换发送到外部收件人的邮件时遇到的任何内容转换失败。

  - **内部收件人的 MAPI 转换**   此类型内容转换由邮箱传输服务处理。邮箱传输服务位于邮箱服务器上，用于在本地服务器上邮箱数据库和邮箱服务器上的传输服务之间传输邮件。具体来说，邮箱传输提交服务将邮件从发件人的发件箱传输到邮箱服务器上的传输服务。邮箱传输传递服务将邮件从邮箱服务器的传输服务传输到收件人的收件箱。邮箱传输提交服务转换 MAPI 的所有传出邮件，邮箱传输传递服务将所有传入邮件转换为 MAPI。内容转换跟踪捕获这些 MAPI 转换失败。有关详细信息，请参阅[内容转换跟踪](content-conversion-tracing-exchange-2013-help.md)。

本主题介绍外部收件人的邮件转换选项。

**目录**

Exchange 和 Outlook 邮件格式

外部收件人的内容转换选项

了解电子邮件消息的结构

## Exchange 和 Outlook 邮件格式

以下列表描述了 Exchange 和 Microsoft Outlook 中可采用的基本邮件格式：

  - **纯文本**   纯文本邮件仅使用 RFC 2822 中描述的 US-ASCII 文本。这种邮件不能包含其他的字体或其他文本格式。纯文本邮件可以使用以下两种格式：
    
      - 邮件头和邮件正文由 US-ASCII 文本组成。必须使用 *Uuencode* 对附件进行编码。Uuencode 指的是“Unix 到 Unix”的编码，它定义使用 US-ASCII 文本字符存储电子邮件正文中的二进制附件的编码算法。
    
      - 邮件是经过 MIME 编码的邮件，并且 Content-Type 的值为 text/plain（对于多部分邮件的文本部分，Content-Transfer-Encoding 的值为 7bit）。任何邮件附件都使用 Quoted-printable 或 Base64 编码进行编码。默认情况下，当您在 Outlook 中撰写和发送纯文本邮件时，该邮件是经过 MIME 编码的邮件，Content-Type 值为 text/plain。

  - **HTML**   HTML 邮件支持文本格式、背景图像、表、项目符号及其他图形元素。根据定义，必须对 HTML 格式的邮件进行 MIME 编码以保留这些格式元素。

  - **RTF 格式 (RTF)**   RTF 支持文本格式和其他图形元素。RTF 格式是 TNEF 的同义词。TNEF 与 RTF 可以互换使用。RTF 邮件格式完全不同于 Microsoft Word 中提供的 RTF 文档格式。
    
    仅 Outlook 和几个其他 MAPI 电子邮件客户端支持 RTF 邮件。

  - **TNEF**   传输中性封装格式是 Microsoft 特有的格式，用于封装 MAPI 邮件属性。TNEF 邮件包含纯文本形式的邮件以及打包原始格式形式的邮件的附件。通常，此附件名为 Winmail.dat，它包含以下信息：
    
      - 邮件的原始格式版本，如字体、文本大小和文字颜色
    
      - OLE 对象，如嵌入的图片或 Microsoft Office 文档
    
      - 特殊 Outlook 功能，如自定义表单、投票按钮或会议请求
    
      - 原始邮件中的常规邮件附件
    
    最终生成的纯文本邮件可以通过下列格式表示：
    
      - 符合 RFC 2822 的邮件，由仅采用 US-ASCII 编码的文本组成，所带的 Winmail.dat 附件采用 Uuencode 编码
    
      - 带有 Winmail.dat 附件的多节 MIME 编码的邮件
    
    完全识别 TNEF 的符合 MAPI 的电子邮件客户端（例如 Outlook）可处理 Winmail.dat 附件并显示原始邮件内容，而不会显示 Winmail.dat 附件。不支持 TNEF 的电子邮件客户端可以通过下列任一方式显示 TNEF 邮件：
    
      - 显示纯文本版本的邮件，并且该邮件包含名为 Winmail.dat、Win.dat 或一些其他中性名称（如 Att*nnnnn*.dat 或 Att*nnnnn*.eml，其中 *nnnnn* 占位符表示随机数字）的附件。
    
      - 显示纯文本版本的邮件。忽略或删除 TNEF 附件。结果是纯文本邮件。
    
      - 支持 TNEF 的邮件服务器可以配置为从传入邮件中删除 TNEF 附件。结果是纯文本邮件。另外，某些电子邮件客户端（如 Microsoft Outlook Express）可能无法支持 TNEF，但可识别和忽略 TNEF 附件。结果是纯文本邮件。
    
    有一些第三方实用程序可以帮助转换 Winmail.dat 附件。
    
    从 Exchange Server 版本 5.5 开始，所有 Exchange 版本均支持 TNEF。

  - **汇总传输中性封装格式 (STNEF)**   STNEF 等同于 TNEF。但是，STNEF 邮件的编码方式与 TNEF 邮件不同。具体来说，STNEF 邮件始终进行 MIME 编码并且 Content-Transfer-Encoding 的值始终为 Binary。所以，该邮件没有纯文本表示形式，并且该邮件的正文中没有确切的 Winmail.dat 附件。整个邮件只使用二进制数据表示。Content-Transfer-Encoding 值为 Binary 的邮件只能在支持和公布在 RFC 3030 中定义的 BINARYMIME 和 CHUNKING SMTP 扩展的 SMTP 邮件服务器之间传输。通过 BDAT 命令而不是标准 DATA 命令，该邮件始终可以在 SMTP 邮件服务器之间传输。
    
    从 Exchange 2000 开始，所有 Exchange 版本均支持 STNEF。从本机模式 Exchange Server 2003 开始，STNEF 自动用于组织中 Exchange 服务器之间传输的所有邮件。
    
    Exchange 从不将 STNEF 邮件发送到外部收件人。只有 TNEF 邮件可以发送到 Exchange 组织外的收件人。

返回顶部

## 外部收件人的内容转换选项

您可以在 Exchange 组织中为外部收件人设置的内容转换选项可以分为以下几类：

  - **TNEF 转换选项**   这些转换选项指定在从 Exchange 组织传出的邮件中应保留还是删除 TNEF。

  - **邮件编码选项**   这些选项指定邮件编码选项，如 MIME 字符集和非 MIME 字符集、邮件编码以及附件格式。

这些转换和编码选项相互独立。例如，TNEF 邮件是否可以从 Exchange 组织发出与这些邮件的 MIME 编码设置或纯文本编码设置无关。

您可以在各种 Exchange 组织级别指定内容转换，如下面列表所示：

  - **远程域设置**   远程域定义 Exchange 组织和外部域之间传输传出邮件的设置。即使没有为特定域创建远程域条目，也会存在一个名为 Default 的预定义远程域，它适用于所有远程地址空间 ( \* )。

  - **邮件用户和邮件联系人设置**   邮件用户与邮件联系人相似，因为二者都具有外部电子邮件地址，并包含有关 Exchange 组织外用户的信息。主要不同之处在于邮件用户具有可以登录 Active Directory 域并访问组织中资源的帐户。

  - **Outlook 设置**   在 Outlook 中，您可以设置以下列表中介绍的邮件格式和编码选项：
    
      - **邮件格式**   您可以为所有邮件设置默认邮件格式。撰写特定邮件时，您可以覆盖默认邮件格式。
    
      - **Internet 邮件格式**   您可以控制是否将 TNEF 邮件发送到远程收件人，或者是否先将这些邮件转换为更兼容的格式。您还可以为发送到远程收件人的邮件指定各种邮件编码选项。这些设置不适用于发送到 Exchange 组织中的邮件。
    
      - **Internet 收件人邮件格式**   您可以控制是否将 TNEF 邮件发送到特定收件人，或者是否先将这些邮件转换为更兼容的格式。您可以为联系人文件夹中的特定联系人设置转换选项，并且可以在撰写邮件时在“收件人:”、“抄送:”、“密件抄送:”字段中覆盖特定收件人的转换选项。这些转换选项不适用于 Exchange 组织中的收件人。
    
      - **Internet 收件人邮件编码选项**   您可以控制联系人文件夹中特定联系人的 MIME 或纯文本编码选项，并且可以在撰写邮件时在“收件人:”、“抄送:”、“密件抄送:”字段中覆盖特定收件人的转换选项。这些转换选项不适用于 Exchange 组织中的收件人。
    
      - **国际选项**   您可以控制在邮件中使用的字符集。

## TNEF 转换选项

您可以指定以下级别的 TNEF 转换选项：

  - 远程域设置

  - 邮件用户和邮件联系人设置

  - Outlook 设置包括：
    
      - 邮件格式
    
      - Internet 邮件格式
    
      - Internet 收件人邮件格式

## 邮件编码选项

您可以指定以下级别的邮件编码选项：

  - 远程域设置

  - 邮件用户和邮件联系人设置

  - Outlook 设置包括：
    
      - 邮件格式
    
      - Internet 邮件
    
      - Internet 收件人邮件格式
    
      - 邮件字符集编码选项

有关详细信息，请参阅[邮件编码选项](message-encoding-options-exchange-2013-help.md)。

返回顶部

## 了解电子邮件消息的结构

为了更好地了解外部收件人的内容转换选项，需要了解电子邮件的结构。SMTP 邮件基于 7 位 US-ASCII 纯文本来撰写和发送电子邮件。标准 SMTP 邮件由下列元素组成：

  - **邮件信封**   邮件信封在 RFC 2821 中进行定义。邮件信封包括传输和传递邮件所需的信息。收件人从不会看到邮件信封，因为它是由邮件传输进程生成的，实际上并不是邮件内容的一部分。

  - **邮件内容**   邮件内容在 RFC 2822 中定义。邮件内容由下列元素组成：
    
      - **邮件头**   邮件头是头字段的集合。头字段包括字段名称，后跟冒号 (:)、字段正文，最后是回车换行 (CR/LF) 字符组合。
        
        字段名称必须由可打印的 US-ASCII 文本字符（冒号 (:) 除外）组成。具体来说，允许使用值范围在 33 到 57 和 59 到 126 的 ASCII 字符。
        
        字段正文可由任何 US-ASCII 字符组成，但回车符 (CR) 和换行符 (LF) 除外。但是，在“头折叠”中使用时，字段正文可以包含 CR/LF 字符组合。头折叠是指将单个头字段正文分为多行，如 RFC 2822 的第 2.2.3 节中所述。RFC 2822 的第 3 节和第 4 节中介绍了其他字段正文语法要求。
    
      - **邮件正文**   邮件正文是继邮件头之后出现的 US-ASCII 文本字符行的集合。邮件头和邮件正文由一个以 CR/LF 字符组合结尾的空行分隔。邮件正文是可选的。在邮件正文中，任何文本行都不得超过 998 个字符。CR 和 LF 字符同时显示才能表示一行的结束。

当 SMTP 邮件包含非 US-ASCII 纯文本元素时，必须对其进行编码以保留这些元素。MIME 标准定义了一种对邮件中非文本内容进行编码的方法。MIME 允许存在使用其他字符集的文本、不带文本的附件、多部分邮件正文以及使用其他字符集的头字段。MIME 在 RFC 2045、RFC 2046、RFC 2047、RFC 2048 和 RFC 2077 中定义。MIME 定义了指定其他邮件属性的头字段集合。下表介绍了一些重要的 MIME 头字段。

### 重要的 MIME 头字段

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>头字段名称</th>
<th>默认值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MIME-Version</p></td>
<td><p>1.0</p></td>
<td><p>此头字段是 MIME 格式的邮件中出现的第一个 MIME 头字段。此头字段出现在其他标准 RFC 2822 头字段之后，任何其他非标准 RFC 2822 头字段之前。MIME 感知电子邮件客户端使用此头字段标识 MIME 编码的邮件。当缺少此头字段时，MIME 感知电子邮件客户端会将该邮件标识为纯文本。</p></td>
</tr>
<tr class="even">
<td><p>Content-Type</p></td>
<td><p>text/plain</p></td>
<td><p>此头字段标识 RFC 2046 中描述的邮件内容的媒体类型。媒体类型由类型、子类型以及一个或多个可选参数组成，如定义 MIME 字符编码的 <em>charset=</em> 参数。以“x-”开头的类型是非标准类型。以“vnd.”开头的子类型是供应商特定的类型。Internet 号码分配机构 (IANA) 维护已注册的媒体类型列表。有关详细信息，请参阅 <a href="https://www.iana.org/assignments/media-types/">MIME 媒体类型</a>。</p>
<p><em>多节</em>媒体类型通过使用由不同媒体类型定义的节允许在同一邮件中使用多个邮件部分。某些 Content-Type 字段值包含 text/plain、text/html、multipart/mixed 和 multipart/alternative。</p></td>
</tr>
<tr class="odd">
<td><p>Content-Transfer-Encoding</p></td>
<td><p>7bit</p></td>
<td><p>此头字段可以说明有关邮件的以下信息：</p>
<ul>
<li><p>用于转换邮件正文中的任何非 US-ASCII 文本或二进制数据的编码算法。</p></li>
<li><p>描述邮件正文当前情况的指示器。</p></li>
</ul>
<p>MIME 邮件中的 Content-Transfer-Encoding 头字段可以有多个值。Content-Transfer-Encoding 头字段出现在邮件头中时，将适用于整个邮件正文。Content-Transfer-Encoding 头字段出现在多部分邮件的一部分中时，将仅适用于该邮件部分。</p>
<p>如果对邮件正文数据应用编码算法，邮件正文数据将转换为 US-ASCII 纯文本。此转换允许邮件通过仅支持 US-ASCII 文本邮件的旧版 SMTP 邮件服务器。用于表示已在邮件正文中使用编码算法的 Content-Transfer-Encoding 头字段的值如下：</p>
<ul>
<li><p><strong>Quoted-printable</strong>   此编码算法使用可打印 US-ASCII 字符对邮件正文数据进行编码。如果原始邮件文本大部分都是 US-ASCII 文本，则 quoted-printable 编码可提供便于阅读的紧凑的显示结果。除了等号字符 (=) 之外，所有可打印 US-ASCII 文本字符都可不经过编码而呈现。</p></li>
<li><p><strong>Base64</strong>   此编码算法在很大程度上基于 RFC 1421 中定义的增强隐私邮件 (PEM) 标准。Base64 编码使用 64 个字符字母编码算法和 PEM 定义的输出填充字符对邮件正文数据进行编码。经过 Base64 编码的邮件通常比原始邮件大 33%。经 Base64 编码而增加的邮件大小是可预测的，对于二进制数据和非 US-ASCII 文本来说它是最佳选择。</p></li>
</ul>
<p>通常，您不会看到在同一个邮件中使用多个编码算法。</p>
<p>如果未对邮件正文使用编码算法，Content-Transfer-Encoding 头字段只标识邮件正文数据的当前情况。用于表示未在邮件正文中使用编码算法的 Content-Transfer-Encoding 头字段的值如下：</p>
<ul>
<li><p><strong>7bit</strong>   此值表示邮件正文数据已使用 RFC 2822 格式。具体来说，这表示必须满足下列条件：</p>
<ul>
<li><p>所有文本行的长度不得超过 998 个字符。</p></li>
<li><p>所有字符必须是字符值为 1 到 127（包括 1 和 127）的 US-ASCII 文本。</p></li>
<li><p>CR 和 LF 字符一起使用才能表示一个文本行的结束。</p></li>
</ul>
<p>整个邮件正文可能是 7bit，或者多部分邮件中的部分邮件正文可能是 7bit。如果多部分邮件包含具有任何二进制数据或非 US-ASCII 文本的其他部分，则必须使用 Quoted-printable 或 Base64 编码算法对邮件的该部分进行编码。</p>
<p>具有 7bit 正文的邮件可以使用标准 DATA 命令在 SMTP 邮件服务器之间传输。</p></li>
<li><p><strong>8bit</strong>   此值表示邮件正文数据包含非 US-ASCII 字符。具体来说，这表示必须满足下列条件：</p>
<ul>
<li><p>所有文本行的长度不得超过 998 个字符。</p></li>
<li><p>邮件正文中一个或多个字符的值大于 127。</p></li>
<li><p>CR 和 LF 字符一起使用才能表示一个文本行的结束。</p></li>
</ul>
<p>整个邮件正文可能是 8bit，或者多部分邮件中的部分邮件正文可能是 8bit。如果多部分邮件包含具有二进制数据的其他部分，则必须使用 Quoted-printable 或 Base64 编码算法对邮件的该部分进行编码。</p>
<p>具有 8bit 正文的邮件只能在支持 RFC 1652 中定义的 8BITMIME SMTP 扩展的 SMTP 邮件服务器（如运行 Exchange 2000 Server 或更高版本的服务器）之间传输。具体来说，这表示必须满足下列条件：</p>
<ul>
<li><p>必须在服务器的 EHLO 响应中公布 8BITMIME 关键字。</p></li>
<li><p>邮件仍然使用 SMTP 标准 DATA 命令传输。但是，必须将 BODY=8BITMIME 参数添加到 MAIL FROM 命令的末尾。</p></li>
</ul></li>
<li><p><strong>Binary</strong>   此值表示邮件正文包含非 US-ASCII 文本或二进制数据。具体来说，这表示必须满足下列条件：</p>
<ul>
<li><p>允许使用任何字符序列。</p></li>
<li><p>行没有长度限制。</p></li>
<li><p>二进制邮件元素不需要编码。</p></li>
</ul>
<p>具有二进制正文的邮件只能在支持 RFC 3030 中定义的 BINARYMIME SMTP 扩展的 SMTP 邮件服务器（如运行 Exchange 2000 Server 或更高版本的服务器）之间传输。具体来说，这表示必须满足下列条件：</p>
<ul>
<li><p>必须在服务器的 EHLO 响应中公布 BINARYMIME 关键字。</p></li>
<li><p>BINARYMIME SMTP 扩展只能与 CHUNKING SMTP 扩展一起使用。“分块”允许以多个较小块的形式发送大型邮件正文。分块也在 RFC 3030 中定义。CHUNKING 关键字也必须在服务器的 EHLO 响应中公布。</p></li>
<li><p>邮件使用 BDAT 命令而不是标准 DATA 命令进行传输。</p></li>
<li><p>如果邮件具有邮件正文，必须将 <em>BODY=BINARYMIME</em> 参数添加到 MAIL FROM 命令的末尾。</p></li>
</ul></li>
</ul>
<p>在同一个多部分邮件中不能同时存在 7bit、8bit 和 Binary。这些值相互排斥。Quoted-printable 或 Base64 值可以在 7bit 或 8bit 多部分邮件正文中出现，但永远不会在 Binary 邮件正文出现。如果多部分邮件正文包含由 7bit 和 8bit 内容组成的不同部分，则整个邮件被归类为 8bit。如果多部分邮件正文包含由 7bit、8bit 和 Binary 内容组成的不同部分，则整个邮件被归类为 Binary。</p></td>
</tr>
<tr class="even">
<td><p>Content-Disposition</p></td>
<td><p>Attachment</p></td>
<td><p>此头字段指示启用 MIME 的电子邮件客户端应如何显示附件，在 RFC 2183 中有相关说明。此字段的值可以是 Inline 或 Attachment。当此字段的值为 Inline 时，附件将显示在邮件正文中。当此字段的值为 Attachment 时，附件将显示为与邮件正文分开的常规附件。当值为 Attachment 时，可以使用其他参数，如 Filename、Creation-date 和 Size。</p></td>
</tr>
</tbody>
</table>


返回顶部

