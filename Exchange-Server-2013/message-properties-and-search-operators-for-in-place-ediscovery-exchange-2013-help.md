---
title: '就地电子数据展示的邮件属性和搜索运算符: Exchange 2013 Help'
TOCTitle: 就地电子数据展示的邮件属性和搜索运算符
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62618528
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 就地电子数据展示的邮件属性和搜索运算符

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

本主题介绍了您可以在 Exchange Server 2013 和 Exchange Online 中使用就地电子数据展示和保留来搜索的 Exchange 电子邮件的属性。此外，本主题还介绍了布尔搜索运算符以及可以用于优化电子数据展示搜索结果的其他搜索查询技术。

就地电子数据展示使用关键字查询语言 (KQL)。有关详细信息，请参阅[关键字查询语言语法参考](https://go.microsoft.com/fwlink/?linkid=269603)。

## Exchange 中的可搜索属性

下表列出了电子邮件属性。这些属性可通过就地电子数据展示搜索或使用 **New-MailboxSearch** 或 **Set-MailboxSearch** cmdlet 进行搜索。该表包含了每个属性的 *property:value* 语法的示例，并介绍了这些示例返回的搜索结果。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>属性描述</th>
<th>示例</th>
<th>示例返回的搜索结果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>附加到电子邮件的文件名称。</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>含有名称为 annualreport.ppt 的附件的邮件。</p>
<p>在第二个示例中，使用通配符返回附件名中带有单词“annual”的邮件。</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>电子邮件的“密件抄送”字段。1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>所有示例都返回“密件抄送”字段中包含“Pilar Pinilla”的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>搜索类别。用户可以使用 Outlook 或 Outlook Web App 定义类别。可能的值是：</p>
<ul>
<li><p>蓝色</p></li>
<li><p>绿色</p></li>
<li><p>橙色</p></li>
<li><p>紫色</p></li>
<li><p>红色</p></li>
<li><p>黄色</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>在源邮箱中已指定红色类别的邮件。</p></td>
</tr>
<tr class="even">
<td><p>抄送</p></td>
<td><p>电子邮件的“抄送”字段。1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>在以上两个示例中，在“抄送”字段中指定了含有“Pilar Pinilla”的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>发件人</p></td>
<td><p>电子邮件的发件人。1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>由指定用户或指定域发送的邮件。</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>发件人在发送邮件时可以指定电子邮件的重要性。除非发件人将重要性设置为“高”或“低”，否则在发送邮件时将重要性默认为“普通”。</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>将重要性标记为高、中等或低的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>要搜索的邮件类型。可能的值：</p>
<ul>
<li><p>联系人</p></li>
<li><p>文档</p></li>
<li><p>电子邮件</p></li>
<li><p>传真</p></li>
<li><p>即时消息</p></li>
<li><p>日志</p></li>
<li><p>会议</p></li>
<li><p>注释</p></li>
<li><p>公告</p></li>
<li><p>RSS 源</p></li>
<li><p>任务</p></li>
<li><p>语音邮件</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>满足搜索条件的电子邮件。第二个示例返回满足搜索条件的电子邮件、即时消息对话以及语音邮件。</p></td>
</tr>
<tr class="even">
<td><p>参与者</p></td>
<td><p>电子邮件中的所有人员字段；这些字段分别为：发件人、收件人、抄送和密件抄送。1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>garthf@contoso.com 发送的邮件或发送至 garthf@contoso.com 的邮件。</p>
<p>第二个示例返回 contoso.com 域中的用户发送的所有邮件或发送至 contoso.com 域中的用户的所有邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>收件人接收电子邮件的日期。</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>2014 年 4 月 15 日接收的邮件。第二个示例返回 2014 年 1 月 1 日和 2014 年 3 月 31 日之间接收的所有邮件。</p></td>
</tr>
<tr class="even">
<td><p>收件人</p></td>
<td><p>电子邮件中的所有收件人字段；这些字段分别为：收件人、抄送和密件抄送。1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>发送至 garthf@contoso.com 的邮件。</p>
<p>第二个示例返回发送至 contoso.com 域中的任何收件人的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>发件人发送电子邮件的日期。</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>在指定日期或指定日期范围内发送的邮件。</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>邮件的大小（以字节为单位）。</p></td>
<td><p>大小&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>邮件超过 25 MB。</p>
<p>第二个示例返回大小介于 1 到 1,048,576 字节 (1 MB) 之间的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>电子邮件主题行中的文本。</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>主题行的文本中包含精确短语“Quarterly Financials”的邮件。</p>
<p>第二个示例返回主题行中包含单词“northwind”的所有邮件。</p></td>
</tr>
<tr class="even">
<td><p>收件人</p></td>
<td><p>电子邮件的“收件人”字段。1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>所有示例返回在“收件人:”行中指定为 Ann Beebe 的邮件。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1   对于收件人属性的值，你可以使用 SMTP 地址、显示名称或别名来指定用户。例如，你可以使用 annb@contoso.com、annb 或“Ann Beebe”指定用户 Ann Beebe。</td>
</tr>
</tbody>
</table>


## 支持的搜索运算符

使用布尔搜索运算符（如 **AND**、**OR**）可以在搜索查询中包括或排除特定单词，有助于定义更精确的邮箱搜索。使用其他技术（如属性运算符（如 \>= 或 ..）、问号、括号和通配符）有助于优化电子数据展示搜索查询。下表列出了可用于缩小或扩大搜索结果范围的运算符。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>必须在搜索查询中使用大写的布尔运算符。例如，请使用 <strong>AND</strong>，而不是 <strong>and</strong>。在搜索查询中使用小写的运算符会返回错误。</td>
</tr>
</tbody>
</table>



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>运算符</th>
<th>用法</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>返回包含所有指定关键字或 <code>property:value</code> 表达式的邮件。</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 +keyword2 +keyword3</p></td>
<td><p>包含 <code>keyword2 </code> <em>或</em> <code>keyword3</code> <em>且</em>包含 <code>keyword1</code> 的返回项。因此，此示例等同于查询 <code>(keyword2 OR keyword3) AND keyword1</code>。</p>
<p>注意，查询 <code>keyword1 + keyword2</code>（<strong>+</strong> 号后有一个空格）与使用 <strong>AND</strong> 运算符时作用不一样。此查询等同于 <code>&quot;keyword1 + keyword2&quot;</code>，并返回正好带有 <code>&quot;keyword1 + keyword2&quot;</code> 部分的项。</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>返回包含一个或多个指定关键字或 <code>property:value</code> 表达式的邮件。</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>排除按关键字或 <code>property:value</code> 表达式指定的邮件。例如，<code>NOT from:&quot;Ann Beebe&quot;</code> 排除 Ann Beebe 发送的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>与 <strong>NOT</strong> 运算符作用相同。此查询返回包含 <code>keyword1</code> 的项，并排除包含 <code>keyword2</code> 的项。</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>返回包含邻近字词的邮件，其中 n 表示间隔的字词数量。例如，<code>best NEAR(5) worst</code> 返回单词“worst”与“best”之间的距离不超过五个单词的邮件。如果您没有指定数目，则默认距离是 8 个字词。</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p><code>property:value</code> 语法中的冒号 (:) 指定要搜索的属性值等于指定值。例如，<code>recipients:garthf@contoso.com</code> 返回发送至 garthf@contoso.com 的所有邮件。</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>表示正在搜索的属性小于指定的值。1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>表示正在搜索的属性大于指定的值。1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>表示正在搜索的属性小于等于指定的值。1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>表示正在搜索的属性大于等于指定的值。1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>表示正在搜索的属性大于等于 value1，小于等于 value2。1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>使用双引号 (&quot; &quot;) 搜索关键字和 <code>property:value</code> 搜索查询中的确切短语或单词。</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>前缀通配符（其中星号放在单词的末尾）用于在关键字或 <code>property:value</code> 查询中搜索零个或多个匹配字符。例如，<code>subject:set*</code> 返回主题行中包含单词 set、setup、setting（以及其他以“set”开头的单词）的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(fair OR free) AND from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>括号将布尔短语、<code>property:value</code> 项目和关键字结合到一起。例如，<code>(quarterly financials)</code> 返回包含单词“quarterly”和“financials”的项目。</p></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1   为含有日期或数值的属性使用此运算符。</td>
</tr>
</tbody>
</table>


## 搜索查询不支持的字符

搜索查询不支持的字符通常会导致搜索错误或返回意外结果。不受支持的字符通常是隐藏的。当你将查询或部分查询从其他应用程序（如 Microsoft Word 或 Microsoft Excel）复制到就地电子数据展示搜索查询页上的关键字框中时，不受支持的字符通常会被添加到查询中。

下面列出了就地电子数据展示搜索查询不支持的字符。

  - **智能引号**   不支持智能单引号和智能双引号（亦称为“*弯引号*”）。只能在搜索查询中使用直双引号。

  - **非打印字符和控制字符**   非打印字符和控制字符并不表示书写符号，如字母数字字符。非打印字符和控制字符示例包括设置文本格式的字符或文本换行字符。

  - **从左到右和从右到左标记**   这些标记是用于指明从左到右语言（如英语和西班牙语）和从右到左语言（如阿拉伯语和希伯来语）的文字方向的控制字符。

  - **小写的布尔运算符**   如前所述，必须在搜索查询中使用大写的布尔运算符，如 **AND** 和 **OR**。请注意，查询语法通常会指明使用了布尔运算符，即使使用的是小写运算符，也会予以指明。例如，`(WordA or WordB) and (WordC or WordD)`。

**如何防止搜索查询中出现不受支持的字符？**防止出现不受支持的字符的最佳方式是，在关键字框中仅键入查询。或者，也可以从 Word 或 Excel 复制查询，然后将其粘贴到纯文本编辑器（如 Microsoft 记事本）文件中。接下来，保存文本文件，并选择“**编码**”下拉列表中的“**ANSI**”。这会删除所有格式和不受支持的字符。然后，便可将文本文件中的查询复制并粘贴到关键字查询框中。

## 搜索提示和技巧

  - 关键字搜索不区分大小写。例如，**cat** 和 **CAT** 将返回相同的结果。

  - 两个关键字或两个 `property:value` 表达式之间的空格与使用 **AND** 相同。例如，`from:"Sara Davis" subject:reorganization` 返回 Sara Davis 发送的所有邮件，其中的主题行包含单词 **reorganization**。

  - 使用与 `property:value` 格式相匹配的语法。值不区分大小写，并且它们不可以在运算符后留有空格。如果有空格，您的预期值将只会全文搜索。例如，**to:pilarp** 搜索“pilarp”作为关键字，而非发送至 pilarp 的邮件。

  - 在搜索收件人属性（如 To、From、Cc 或 Recipients）时，您可以使用 SMTP 地址、别名或显示名来表示收件人。例如，您可以使用 pilarp@contoso.com、pilarp 或“Pilar Pinilla”。

  - 您可以仅使用前缀通配符搜索，如 **cat\*** 或 **set\***。不支持后缀通配符搜索 (\*cat) 或子字符串通配符搜索 (\*cat\*)。

  - 在搜索属性时，如果搜索值包含多个单词，则使用双引号 (" ")。例如，**subject:budget Q1** 返回主题行中包含 **budget** 以及邮件中任意位置或任意邮件属性中包含 **Q1** 的邮件。使用 **subject:"budget Q1"** 返回主题行中任意位置包含 **budget Q1** 的所有邮件。

