---
title: '传输规则条件（谓词）: Exchange 2013 Help'
TOCTitle: 邮件流规则条件和异常（谓词）
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50491689
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 传输规则条件（谓词）

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2017-12-20_

邮件流规则（也称为传输规则）中的条件和例外可识别应用或不应用规则的邮件。例如，如果规则将免责声明添加到邮件，则可以配置规则只应用于包含特定词语的邮件、由特定用户发送的邮件，或由特定组中的成员发送的邮件之外的所有邮件。邮件流规则中的条件和例外也统称为*谓词*，因为针对每个条件，都存在使用完全相同的设置和语法的相应例外。唯一的区别是：条件指定要包含的邮件，而例外指定要排除的邮件。

大多数的条件及例外有一个需要一个或多个值的属性。例如，\&quot;**发件人是**\&quot;条件需要指定邮件的发件人。一些条件有两个属性。例如，\&quot;**邮件头包含以下任何词语**\&quot;条件需要一个属性来指定邮件头字段，需要第二个属性来指定要在头字段中查找的文本。某些条件或例外没有任何属性。例如，\&quot;**任何附件都具有可执行内容**\&quot;条件只是在邮件中查找包含可执行内容的附件。

在Exchange Server 2013中的邮件流规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

有关条件及在Exchange Online Protection或Exchange Online中的邮件流规则中的例外情况的详细信息，请参阅[在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\))或[邮件流规则条件和例外 （谓语） 在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj919234\(v=exchg.150\))。

## 邮箱服务器上的邮件流规则的条件和例外

以下各节中的表介绍条件和所提供的邮箱服务器上的邮件流规则的例外。属性类型属性类型部分中所述。

发件人

收件人

邮件主题或正文

附件

任意收件人

邮件敏感信息类型，"收件人"和"抄送"值、大小和字符集

发件人和收件人

邮件属性

邮件标头

**注意：** 

  - 在 Exchange 管理中心 (EAC) 中选择条件或例外后，在\&quot;**在以下情况应用此规则**\&quot;或\&quot;**下列情况除外**\&quot;字段中最终显示的值通常不同（短于）所选的单击路径值。此外，根据模板（已筛选的方案列表）创建新规则时，通常可以选择短条件名称而不是遵循完整单击路径。短名称和完整单击路径值显示在表的 EAC 列中。

  - 如果在 EAC 中选择\&quot;**\[应用于所有邮件\]**\&quot;，则无法指定任何其他条件。Exchange 命令行管理程序中的等效方法是在不指定任何条件参数的情况下创建规则。

  - 此设置和属性与条件和例外中的设置和属性一致，因此，**Get-TransportRulePredicate** cmdlet 的输出结果并不会单独列出例外。此外，此 cmdlet 返回的谓词的一些名称不同于相应的参数名，并且一个谓词可能需要多个参数。

## 发件人

对于检查发件人地址的条件和例外，可以指定规则查找发件人地址的位置。

在 EAC 的\&quot;**此规则的属性**\&quot;部分，单击\&quot;**匹配邮件中的发件人地址**\&quot;。注意，可能需要单击\&quot;**更多选项**\&quot;来查看此设置。在 Exchange 命令行管理程序中，该参数是 *SenderAddressLocation*。可用值有：

  - **标头**   只检查邮件头中的发件人（例如，\&quot;**From**\&quot;、\&quot;**Sender**\&quot;或\&quot;**Reply-To**\&quot;字段)。这是默认值，也是在 Exchange 2013 累积更新 1 (CU1) 之前邮件流规则的工作方式。

  - **信封**  只检查发件人邮件信封 （SMTP 传输，通常存储在**Return-Path**字段中使用的**MAIL FROM**值）。请注意，邮件信封搜索功能仅适用于以下情况 （和相应的例外）：
    
      - **发件人为** (*From*)
    
      - **发件人为以下组的成员** (*FromMemberOf*)
    
      - **在发件人地址中包含** (*FromAddressContainsWords*)
    
      - **发件人地址匹配** (*FromAddressMatchesPatterns*)
    
      - **发件人域为** (*SenderDomainIs*)

  - **标头或信封** (`HeaderOrEnvelope`)   检查邮件头和邮件信封中的发件人。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>发件人为</strong></p>
<p><strong>发件人</strong> &gt; <strong>是此人</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 组织中由指定邮箱、邮件用户、邮件联系人发送的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>找到发件人</strong></p>
<p><strong>发件人</strong> &gt; <strong>在外部/内部</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>由内部发件人或外部发件人发送的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>发件人为以下组的成员</strong></p>
<p><strong>发件人</strong> &gt; <strong>是此组的成员</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>由指定组成员发送的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>在发件人地址中包含</strong></p>
<p><strong>发件人</strong> &gt; <strong>地址包含这些词语中的任意词语</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>发件人电子邮件地址中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>发件人地址匹配</strong></p>
<p><strong>发件人</strong> &gt; <strong>地址与这些文本模式中的任意模式匹配</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>发件人的电子邮件地址包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>发件人的指定属性包括以下任何词语</strong></p>
<p><strong>发件人</strong> &gt; <strong>具有包括以下任何词语的特定属性</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>首要属性：<code>ADAttribute</code></p>
<p>次要属性：<code>Words</code></p></td>
<td><p>发件人的指定的 Active Directory 属性包含任意的指定词语的邮件。</p>
<p>注意，<strong>Country</strong> 属性要求两个字母的国家/地区代码值（例如，DE 代表德国）。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>发件人的指定属性匹配这些文本模式</strong></p>
<p><strong>发件人</strong> &gt; <strong>具有与以下文本模式匹配的特定属性</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>首要属性：<code>ADAttribute</code></p>
<p>次要属性：<code>Patterns</code></p></td>
<td><p>发件人的指定的 Active Directory 属性包含与指定正则表达式匹配的文本模式的邮件</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>发件人已覆盖策略提示</strong></p>
<p><strong>发件人</strong> &gt; <strong>已覆盖策略提示</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>无</p></td>
<td><p>发件人已选择覆盖数据丢失防护 (DLP) 策略的邮件。有关 DLP 策略的详细信息，请参阅 <a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">数据丢失预防</a>。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>发件人的 IP 地址在范围内</strong></p>
<p><strong>发件人</strong> &gt; <strong>IP 地址处于这些范围中的任何范围或完全匹配</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>发件人的 IP 地址匹配指定的 IP 地址或位于指定的 IP 地址范围内的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>发件人域为</strong></p>
<p><strong>发件人</strong> &gt; <strong>域为</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>发件人的电子邮件地址域与指定值匹配的邮件。</p>
<p>如果想要查找<em>包含</em>指定域（例如，域的任何子域）的发件人域，请使用&amp;quot;<strong>发件人地址匹配</strong>&amp;quot;(<em>FromAddressMatchesPatterns</em>) 条件并使用语法 <code>'@domain\.com$'</code> 指定域。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 收件人


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>收件人为</strong></p>
<p><strong>收件人</strong> &gt; <strong>是此人</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>邮件收件人所在的指定的邮箱、 邮件用户或邮件联系Exchange的组织中。收件人可以在邮件的<strong>To</strong>、 <strong>Cc</strong>或<strong>Bcc</strong>字段中。</p>
<p><strong>注意：</strong> 您不能指定通讯组或已启用邮件的安全组。如果您需要发送给某个组的邮件上执行操作，改用<strong>框包含</strong>(<em>AnyOfToHeader</em>) 条件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>找到收件人</strong></p>
<p><strong>收件人</strong> &gt; <strong>在内部/外部</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>发送给内部收件人、外部收件人、合作伙伴组织中的外部收件人或非合作伙伴组织中的外部收件人的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件人为以下组的成员</strong></p>
<p><strong>收件人</strong> &gt; <strong>是此组的成员</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>包含指定组成员的收件人的邮件。组可以位于邮件的&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段中。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件人地址包括</strong></p>
<p><strong>收件人</strong> &gt; <strong>地址包含这些词语中的任意词语</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>收件人电子邮件地址中包含指定词语的邮件。</p>
<p><strong>注意：</strong>此条件不考虑发送到收件人代理地址的邮件。它只匹配发送到收件人主电子邮件地址的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件人地址匹配</strong></p>
<p><strong>收件人</strong> &gt; <strong>地址与这些文本模式中的任意模式匹配</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>收件人的电子邮件地址包含匹配指定正则表达式的文本模式的邮件。</p>
<p><strong>注意：</strong>此条件不考虑发送到收件人代理地址的邮件。它只匹配发送到收件人主电子邮件地址的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件人的指定属性包括以下任何词语</strong></p>
<p><strong>收件人</strong> &gt; <strong>具有包括以下任何词语的特定属性</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>首要属性：<code>ADAttribute</code></p>
<p>次要属性：<code>Words</code></p></td>
<td><p>收件人的指定的 Active Directory 属性包含任意的指定词语的邮件。</p>
<p>注意，<strong>Country</strong> 属性要求两个字母的国家/地区代码值（例如，DE 代表德国）。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>收件人的指定属性匹配这些文本模式</strong></p>
<p><strong>收件人</strong> &gt; <strong>具有与以下文本模式匹配的特定属性</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>首要属性：<code>ADAttribute</code></p>
<p>次要属性：<code>Patterns</code></p></td>
<td><p>收件人的指定的 Active Directory 属性包含与指定正则表达式匹配的文本模式的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>收件人的域为</strong></p>
<p><strong>收件人</strong> &gt; <strong>域为</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>收件人的电子邮件地址域与指定的值匹配的邮件。</p>
<p>如果想要查找<em>包含</em>指定域（例如，域的任何子域）的收件人域，请使用&amp;quot;<strong>收件人地址匹配</strong>&amp;quot;(<em>RecipientAddressMatchesPatterns</em>) 条件并使用语法 <code>'@domain\.com$'</code> 指定域。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件主题或正文

> [!NOTE]
> 在邮件已通过 MIME 内容传输编码方法（用于以 ACSII 文本方式在 SMTP 服务器之间传输二进制消息）解码<em>后</em>，搜索邮件中主题或其他头字段中的字词或文本模式。不能使用条件或例外来搜索邮件中主题或其他头字段的原始（通常为 Base64）编码值。



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>在主题或正文中包含</strong></p>
<p><strong>主题或正文</strong> &gt; <strong>主题或正文包含以下任何词语</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在&amp;quot;<strong>Subject</strong>&amp;quot;字段或邮件正文中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>主题或正文匹配</strong></p>
<p><strong>主题或正文</strong> &gt; <strong>主题或正文与这些文本模式匹配</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>Subject</strong>&amp;quot;字段或邮件正文包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>主题包括</strong></p>
<p><strong>主题或正文</strong> &gt; <strong>主题包含以下任何词语</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在&amp;quot;<strong>Subject</strong>&amp;quot;字段中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>主题匹配</strong></p>
<p><strong>主题或正文</strong> &gt; <strong>主题与这些文本模式匹配</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>Subject</strong>&amp;quot;字段包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 附件

有关邮件流规则检查邮件附件的方式的详细信息，请参阅[使用传输规则检查邮件附件](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何附件的内容都包含</strong></p>
<p><strong>任何附件</strong> &gt; <strong>内容包含这些词语中任何词语</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>附件包含指定词语的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件内容都匹配</strong></p>
<p><strong>任何附件</strong> &gt; <strong>内容与这些文本模式匹配</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>附件包含匹配指定正则表达式的文本模式的邮件。</p>
<p><strong>注意：</strong> 只有第一个 150 千字节 (KB) 的附件进行扫描。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件的内容无法检查</strong></p>
<p><strong>任何附件</strong> &gt; <strong>无法检查内容</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>无</p></td>
<td><p>邮件附件本身不Exchange，通过识别，并在邮箱服务器上未安装所需的 IFilter。有关详细信息，请参阅<a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">向 Exchange 2013 注册 Filter Pack IFilter</a>。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件的文件名匹配</strong></p>
<p><strong>任何附件</strong> &gt; <strong>文件名匹配这些文本模式</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>附件的文件名包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件的文件扩展名匹配</strong></p>
<p><strong>任何附件</strong> &gt; <strong>文件扩展名包含这些词语</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>附件的文件扩展名匹配任意指定词语的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件都大于或等于</strong></p>
<p><strong>任何附件 &gt; 大小大于或等于</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>任何附件大于或等于指定值的邮件。</p>
<p>在 EAC 中，只能以千字节 (KB) 为单位指定大小。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>邮件未完成扫描</strong></p>
<p><strong>任何附件</strong> &gt; <strong>未完成扫描</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>无</p></td>
<td><p>规则引擎无法完成附件扫描的邮件。可以使用此条件创建规则，以协同工作来标识并处理无法完全扫描内容的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何附件具有可执行内容</strong></p>
<p><strong>任何附件</strong> &gt; <strong>具有可执行内容</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>无</p></td>
<td><p>附件是可执行文件的邮件。系统将检查该文件的属性，而不是依赖文件的扩展名。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>任何附件采用密码保护</strong></p>
<p><strong>任何附件</strong> &gt; <strong>采用密码保护</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>无</p></td>
<td><p>附件受密码保护的邮件（因而无法扫描）。密码检测仅适用于 Office 文档和 .zip 文件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 任意收件人

邮件包含至少一个指定收件人时，本部分中的条件和例外会提供可影响*全部*收件人的独特功能。例如，假设你有一个拒绝邮件的规则。如果使用收件人部分的收件人条件，则邮件仅被那些指定的收件人拒绝。例如，如果规则在在邮件中找到指定的收件人，但该邮件包含五个其他收件人。邮件将被其中一个收件人拒绝，但会发送给其他五个收件人。

如果添加此部分的收件人条件，则同一邮件将被检测到的收件人和其他五个收件人拒绝。

与此相反，此部分的收件人例外可*防止*该规则操作应用于邮件的*所有*收件人，而不仅是检测到的收件人。

**注意：** 此条件不考虑发送到收件人代理地址的邮件。它只匹配发送到收件人主电子邮件地址的邮件。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>任何收件人地址包括</strong></p>
<p><strong>任何收件人</strong> &gt; <strong>地址包含这些词语中的任意词语</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在邮件的&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段中包含指定词语的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>任何收件人地址匹配</strong></p>
<p><strong>任何收件人</strong> &gt; <strong>地址与这些文本模式中的任意模式匹配</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件敏感信息类型，\&quot;收件人\&quot;和\&quot;抄送\&quot;值、大小和字符集

在这样的条件对**To**和**Cc**字段中的值类似于任何收件人部分中的条件部分看起来 （邮件的*所有*收件人都受该规则，而不仅仅是检测到收件人）。

**注意：** 此条件不考虑发送到收件人代理地址的邮件。它只匹配发送到收件人主电子邮件地址的邮件。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>邮件包含敏感信息</strong></p>
<p><strong>邮件</strong> &gt; <strong>包含以下任意敏感信息类型</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>包含由数据丢失防护 (DLP) 策略定义的敏感信息的邮件。</p>
<p>使用&amp;quot;<strong>使用策略提示通知发件人</strong>&amp;quot;(<em>NotifySender</em>) 操作的规则需要此条件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>&amp;quot;收件人&amp;quot;框包含</strong></p>
<p><strong>邮件</strong> &gt; <strong>&amp;quot;收件人&amp;quot;框包含此人</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;字段包含任意指定收件人的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>&amp;quot;收件人&amp;quot;框包含以下组的成员</strong></p>
<p><strong>邮件</strong> &gt; <strong>&amp;quot;收件人&amp;quot;框包含此组的一个成员</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;字段包含的某个收件人为指定组的成员的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>&amp;quot;抄送&amp;quot;框包含</strong></p>
<p><strong>邮件</strong> &gt; <strong>&amp;quot;抄送&amp;quot;框包含此人</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>Cc</strong>&amp;quot;字段包含任意指定收件人的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>&amp;quot;抄送&amp;quot;框中包含以下组的成员</strong></p>
<p><strong>邮件</strong> &gt; <strong>包含此组的一个成员</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>Cc</strong>&amp;quot;字段包含的某个收件人为指定组的成员的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>&amp;quot;收件人&amp;quot;或&amp;quot;抄送&amp;quot;框中包含</strong></p>
<p><strong>邮件</strong> &gt; <strong>&amp;quot;收件人&amp;quot;或&amp;quot;抄送&amp;quot;框包含此人</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;或&amp;quot;<strong>Cc</strong>&amp;quot;字段包含任意指定收件人的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>&amp;quot;收件人&amp;quot;或&amp;quot;抄送&amp;quot;框包含以下组的成员</strong></p>
<p><strong>邮件</strong> &gt; <strong>&amp;quot;收件人&amp;quot;或&amp;quot;抄送&amp;quot;框包含此组的一个成员</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;或&amp;quot;<strong>Cc</strong>&amp;quot;字段包含的某个收件人为指定组的成员的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>邮件大小大于或等于</strong></p>
<p><strong>邮件</strong> &gt; <strong>大小大于或等于</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>总大小（邮件和附件）大于或等于指定值的邮件。</p>
<p>在 EAC 中，只能以千字节 (KB) 为单位指定大小。</p>
<p><strong>注意：</strong>在确定邮件流规则之前将对邮箱的邮件大小限制进行评估。对于邮箱而言过大的邮件将被拒绝，然后此条件的规则才能对该邮件采取措施。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>邮件的字符集名称包括以下任何词语</strong></p>
<p><strong>邮件</strong> &gt; <strong>字符集名称包括以下任何词语</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>具有任意指定字符集名称的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 发件人和收件人


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>发件人是收件人之一</strong></p>
<p><strong>发件人和收件人</strong> &gt; <strong>发件人与收件人的关系是</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>任一发件人是收件人的经理，或发件人由收件人管理的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>该邮件是在这些组的成员之间发送/接收的</strong></p>
<p><strong>发件人和收件人</strong> &gt; <strong>该邮件是在这些组的成员之间发送/接收的</strong></p></td>
<td><p><em>BetweenMemberOf1</em> 和 <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> 和 <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>在指定组成员之间发送的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>发件人或收件人的经理是</strong></p>
<p><strong>发件人和收件人</strong> &gt; <strong>发件人或收件人的经理为此人</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> 和 <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> 和 <em>ExceptIfManagerAddress</em></p></td>
<td><p>首要属性：<code>EvaluatedUser</code></p>
<p>次要属性：<code>Addresses</code></p></td>
<td><p>指定用户是发件人的经理，或者指定用户是收件人的经理的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>发件人和任何收件人的属性比较形式为</strong></p>
<p><strong>发件人和收件人</strong> &gt; <strong>发件人和收件人的属性比较结果为</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> 和 <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> 和 <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>首要属性：<code>ADAttribute</code></p>
<p>次要属性：<code>Evaluation</code></p></td>
<td><p>发件人和收件人的指定 Active Directory 属性匹配或不匹配的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件属性


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>邮件类型为</strong></p>
<p><strong>邮件属性</strong> &gt; <strong>包含邮件类型</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>指定类型的邮件。</p>

> [!NOTE]
> 当Outlook或Outlook Web App配置为转发邮件时， <strong>ForwardingSmtpAddress</strong>属性将添加到邮件中。消息类型不会更改为<code>AutoForward</code>。

</td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>邮件分类为</strong></p>
<p><strong>邮件属性</strong> &gt; <strong>包含此分类</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>包含指定邮件分类的邮件。这是一种自定义邮件分类，可以使用 <strong>New-MessageClassification</strong> cmdlet 在组织内进行创建。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>邮件没有用任何分类标记</strong></p>
<p><strong>邮件属性</strong> &gt; <strong>不包括任何分类</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>无</p></td>
<td><p>不包含邮件分类的邮件。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>邮件的 SCL 大于或等于</strong></p>
<p><strong>邮件属性</strong> &gt; <strong>包含大于或等于以下值的 SCL</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>分配了大于或等于指定值的垃圾邮件可信度 (SCL) 的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>消息的重要性设置为</strong></p>
<p><strong>邮件属性</strong> &gt; <strong>包含重要性级别</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>标记为指定重要性级别的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 邮件头

> [!NOTE]
> 在邮件已通过 MIME 内容传输编码方法（用于以 ACSII 文本方式在 SMTP 服务器之间传输二进制消息）解码<em>后</em>，搜索邮件中主题或其他头字段中的字词或文本模式。不能使用条件或例外来搜索邮件中主题或其他头字段的原始（通常为 Base64）编码值。



<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC 中的条件或例外</th>
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>邮件头中包含</strong></p>
<p><strong>邮件头</strong> &gt; <strong>包含以下任何词语</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> 和 <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> 和 <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>Words</code></p></td>
<td><p>包含指定标头字段，并且该标头字段的值的邮件包含指定的单词。</p>
<p>标头字段的名称和标头字段的值始终在一起使用。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>邮件头匹配</strong></p>
<p><strong>邮件头</strong> &gt; <strong>与这些文本模式匹配</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> 和 <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> 和 <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>Patterns</code></p></td>
<td><p>包含指定标头字段，并且该标头字段的值的邮件包含指定的正则表达式。</p>
<p>标头字段的名称和标头字段的值始终在一起使用。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 边缘传输服务器上的邮件流规则的条件和例外

边缘传输服务器上的邮件流规则中可用的条件和例外是可在邮箱服务器上使用的邮件流规则的一个小子集。边缘传输服务器上并没有 EAC，因此只能在本地边缘传输服务器的 Exchange 命令行管理程序 中管理邮件流规则。下表介绍了条件和例外。属性类型在属性类型部分进行介绍。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 命令行管理程序中的条件和例外参数</th>
<th>属性类型</th>
<th>说明</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段中包含指定词语的邮件。</p>
<p>邮件包含指定收件人时，此规则操作将应用（或不应用）于邮件的<em>全部</em>收件人。例如，邮件会被邮件的全部收件人拒绝，而不仅是指定收件人。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段包含匹配指定正则表达式的文本模式的邮件。</p>
<p>邮件包含指定收件人时，此规则操作将应用（或不应用）于邮件的<em>全部</em>收件人。例如，邮件会被邮件的全部收件人拒绝，而不仅是指定收件人。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>包含的任何附件大于或等于指定值的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>发件人电子邮件地址中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>发件人的电子邮件地址包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>由内部发件人或外部发件人发送的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> 和 <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> 和 <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>Words</code></p></td>
<td><p>包含指定标头字段，并且该标头字段的值的邮件包含指定的单词。</p>
<p>标头字段的名称和标头字段的值始终在一起使用。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> 和 <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> 和 <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>Patterns</code></p></td>
<td><p>包含指定标头字段，并且该标头字段的值的邮件包含指定的正则表达式。</p>
<p>标头字段的名称和标头字段的值始终在一起使用。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>总大小（邮件和附件）大于或等于指定值的邮件。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>分配了大于或等于指定值的 SCL 的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在&amp;quot;<strong>Subject</strong>&amp;quot;字段中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>Subject</strong>&amp;quot;字段包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>在&amp;quot;<strong>Subject</strong>&amp;quot;字段或邮件正文中包含指定词语的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>&amp;quot;<strong>Subject</strong>&amp;quot;字段或邮件正文包含匹配指定正则表达式的文本模式的邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 属性类型

下表介绍了条件和例外中使用的属性类型。

> [!NOTE]
> 如果该属性是一个字符串，不允许有尾随空格。



<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性类型</th>
<th>有效值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>从 Active Directory 属性的预定义列表中选择</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>在 EAC 中，要为同一属性指定多个词语或文本模式，请使用逗号分隔这些值。例如，<strong>City</strong> 属性的 <strong>San Francisco,Palo Alto</strong> 值会查找&amp;quot;City equals San Francisco&amp;quot;或&amp;quot;City equals Palo Alto&amp;quot;。</p>
<p>在 Exchange 命令行管理程序中，使用语法 <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>，其中 <code>Value</code> 是要匹配的词语或文本模式。</p>
<p>例如，<code>&quot;City:San Francisco,Palo Alto&quot;</code> 或 <code>&quot;City:San Francisco,Palo Alto&quot;</code>、<code>&quot;Department:Sales,Finance&quot;</code>。</p>
<p>为同一属性指定多个属性或多个值时，使用 <strong>or</strong> 运算符。请勿使用具有前导或尾随空格的值。</p>
<p>注意，<strong>Country</strong> 属性要求使用两个字母的 ISO 3166-1 国家/地区代码值（例如，DE 代表德国）。要搜索值，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 收件人</p></td>
<td><p>根据条件或例外的特性，或许能够在组织中指定任何启用邮件的对象（例如，收件人相关条件），或也可能限制为特定的对象类型（例如，组成员资格条件的组）。而且，条件或例外可能需要一个值，或允许多个值。</p>
<p>在 Exchange 命令行管理程序中，使用逗号分隔多个值。</p>
<p><strong>注意：</strong>此条件不考虑发送到收件人代理地址的邮件。它只匹配发送到收件人主电子邮件地址的邮件。</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>字符集名称数组</p></td>
<td><p>邮件中存在的一个或多个内容字符集。例如：</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>SMTP 域数组</p></td>
<td><p>例如，<code>contoso.com</code> 或 <code>eu.contoso.com</code>。</p>
<p>在 Exchange 命令行管理程序中，可以指定多个域，中间用逗号隔开。</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p>&amp;quot;<strong>发件人</strong>&amp;quot;或&amp;quot;<strong>收件人</strong>&amp;quot;的单个值</p></td>
<td><p>指定规则是否查找发件人的经理或收件人的经理。</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p>&amp;quot;<strong>等于</strong>&amp;quot;或&amp;quot;<strong>不等于</strong>&amp;quot;(<code>NotEqual</code>) 的单个值</p></td>
<td><p>比较发件人和收件人的 Active Directory 属性时，该属性将指定值应该匹配还是不应该匹配。</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p>&amp;quot;<strong>低</strong>&amp;quot;、&amp;quot;<strong>标准</strong>&amp;quot;或&amp;quot;<strong>高</strong>&amp;quot;的单个值</p></td>
<td><p>由Outlook或Outlook Web App中的发件人分配到该邮件的重要性级别。</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>IP 地址或地址范围数组</p></td>
<td><p>使用下面的语法输入 IPv4 地址：</p>
<ul>
<li><p><strong>单个 IP 地址</strong>   例如，<code>192.168.1.1</code>。</p></li>
<li><p><strong>IP 地址范围</strong>   例如，<code>192.168.0.1-192.168.0.254</code>。</p></li>
<li><p><strong>无类别域际路由选择 (CIDR) IP 地址范围</strong>   例如，<code>192.168.0.1/25</code>。</p></li>
</ul>
<p>在 Exchange 命令行管理程序中，你可以指定由逗号分隔的多个 IP 地址或范围。</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p>&amp;quot;<strong>经理</strong>&amp;quot;或&amp;quot;<strong>直接下属</strong>&amp;quot;(<code>DirectReport</code>) 的单个值</p></td>
<td><p>指定发件人和任意收件人之间的关系。此规则检查 Active Directory 中的 <strong>Manager</strong> 属性，以查看发件人是否是收件人的经理，或发件人是否由收件人管理。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>单个邮件分类</p></td>
<td><p>在 EAC 中，可以从所创建的邮件分类列表进行选择。</p>
<p>在 Exchange 命令行管理程序中，可以使用 <strong>Get-MessageClassification</strong> cmdlet 来标识邮件分类。例如，使用以下命令搜索带有 <code>Company Internal</code> 分类的邮件，并使用值 <code>CompanyInternal</code> 预挂起邮件主题。</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>单个字符串</p></td>
<td><p>指定标头字段的名称。标头字段的名称 （单词或文本模式匹配） 的标头字段中的值总是成对出现。</p>
<p><em>邮件头</em>是邮件中必需和可选的标头字段的集合。标头字段的示例有&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>From</strong>&amp;quot;、&amp;quot;<strong>Received</strong>&amp;quot;和&amp;quot;<strong>Content-Type</strong>&amp;quot;。正式标头字段用 RFC 5322 定义。非正式头字段以 <strong>X-</strong> 开头，称为 <em>X-headers</em>。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>单个邮件类型值</p></td>
<td><p>指定以下邮件类型之一：</p>
<ul>
<li><p><strong>自动答复</strong> (<code>OOF</code>)</p></li>
<li><p><strong>自动转发</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>已加密</strong></p></li>
<li><p><strong>日历</strong></p></li>
<li><p><strong>受权限控制</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>语音邮件</strong></p></li>
<li><p><strong>已签名</strong></p></li>
<li><p><strong>审批请求</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>已读回执</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!NOTE]
> 当Outlook或Outlook Web App配置为转发邮件时， <strong>ForwardingSmtpAddress</strong>属性将添加到邮件中。消息类型不会更改为<code>AutoForward</code>。

</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>正则表达式数组</p></td>
<td><p>指定用于识别值中的文本模式的一个或多个正则表达式。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=180327">正则表达式语法</a>。</p>
<p>在 Exchange 命令行管理程序中，指定多个用逗号分隔的正则表达式，并将每个正则表达式括在双引号 (&quot;) 中。</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p><strong>不使用垃圾邮件筛选</strong> (<code>-1</code>)</p></li>
<li><p>整数 0 到 9</p></li>
</ul></td>
<td><p>指定分配到邮件的垃圾邮件可信度 (SCL)。SCL 值越高，表示邮件是垃圾邮件的可能性越大。</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>敏感信息类型数组</p></td>
<td><p>指定一个或多个定义您的组织中的敏感信息类型。内置的敏感信息类型的列表，请参阅<a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">使用 Exchange 中的敏感信息类型查找什么</a>。</p>
<p>在 Exchange 命令行管理程序中，使用语法 <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>。例如，要查找包含至少两个信用卡号码和至少一个 ABA 银行代号的内容，请使用值 <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>单个大小值</p></td>
<td><p>指定附件或整个邮件的大小。</p>
<p>在 EAC 中，只能以千字节 (KB) 为单位指定大小。</p>
<p>在 Exchange 命令行管理程序中，输入值时，请用下列单位之一限定该值：</p>
<ul>
<li><p><code>B</code>（字节）</p></li>
<li><p><code>KB</code>（千字节）</p></li>
<li><p><code>MB</code>（兆字节）</p></li>
<li><p><code>GB</code>（千兆字节）</p></li>
</ul>
<p>例如，<code>20MB</code></p>
<p>未限定的值通常被视为以字节为单位，但较小的值可能会向上舍入为最接近的千字节。</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p>&amp;quot;<strong>组织内部</strong>&amp;quot;(<code>InOrganization</code>) 或&amp;quot;<strong>组织外部</strong>&amp;quot;(<code>NotInOrganization</code>) 的单个值</p></td>
<td><p>如果满足下列任一条件，则认为发件人位于组织内部：</p>
<ul>
<li><p>发件人是存在于组织的 Active Directory 内的邮箱、邮件用户、组或启用邮件功能的公用文件夹。</p></li>
<li><p>发件人的电子邮件地址是在接受域被配置为权威域或内部中继域，<strong>以及</strong>消息的发送或接收通过已经过身份验证的连接。接受域的详细信息，请参阅<a href="accepted-domains-exchange-2013-help.md">接受域</a>。</p></li>
</ul>
<p>如果满足下列任一条件，则认为发件人位于组织外部：</p>
<ul>
<li><p>发件人的电子邮件地址不位于接受域中。</p></li>
<li><p>发件人的电子邮件地址位于配置为外部中继域的接受域中。</p></li>
</ul>

> [!NOTE]
> 要确定邮件联系人在组织内部还是外部，可将发件人地址与组织的接受域进行比较。

</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p><strong>组织内部</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>组织外部</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>在外部合作伙伴组织中</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>在外部非合作伙伴组织中</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>如果满足下列任一条件，则认为收件人位于组织内部：</p>
<ul>
<li><p>收件人是存在于组织的 Active Directory 内的邮箱、邮件用户、组或启用邮件功能的公用文件夹。</p></li>
<li><p>收件人的电子邮件地址位于配置为权威域或内部中继域的接受的域中， <strong>并且</strong>通过经验证的连接发送或接收邮件。</p></li>
</ul>
<p>如果满足下列任一条件，则认为收件人位于组织外部：</p>
<ul>
<li><p>收件人的电子邮件地址不位于接受域中。</p></li>
<li><p>收件人的电子邮件地址位于配置为外部中继域的接受域中。</p></li>
</ul>
<p>外部合作伙伴组织是已在其中配置域安全（相互 TLS 身份验证）以发送邮件的外部域。</p>
<p>外部非合作伙伴组织是不被视为合作伙伴域的全部其他外部域。</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>字符串数组</p></td>
<td><p>指定一个或多个要查找的词语。词语不区分大小写，且可以由空格和标点围绕。不支持通配符和部分匹配。</p>
<p>例如，&amp;quot;contoso&amp;quot;匹配&amp;quot; Contoso&amp;quot;。但是，如果文本由其他字符围绕，则不会被视作匹配项。 例如，&amp;quot;contoso&amp;quot;并不匹配以下值：</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>星号 (*) 将被视为是文字字符，而不用作通配符。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 详细信息

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[传输规则操作](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[邮件流或传输规则过程](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

适用于 Exchange Online 的[在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\))

对于Exchange Online Protection[邮件流规则条件和例外 （谓语） 在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj919234\(v=exchg.150\))

