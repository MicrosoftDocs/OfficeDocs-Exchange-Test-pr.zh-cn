---
title: '传输规则操作: Exchange 2013 Help'
TOCTitle: 邮件流规则操作
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50490671
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 传输规则操作

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2017-05-03_

邮件流规则（也称为传输规则）中的操作指定想要对匹配规则条件的邮件所执行的操作。例如，可以创建将来自特定发件人的邮件转发给审查方或者将免责声明或个性化签名添加到所有出站邮件的规则。

操作通常需要其他属性。例如，当该规则重定向邮件时，需要指定重定向邮件的位置。某些操作具有多个可用的或必需的属性。例如，在规则向邮件头添加头字段时，需要指定该邮件头的名称和值。当规则向邮件添加免责声明时，需要指定该免责声明文本，但还可以指定插入文本的位置或指定在无法将该免责声明添加到邮件的情况下所应执行的操作。通常，在一个规则中可以配置多个操作，但一些操作是独占的。例如，一个规则不能拒绝并重定向同一邮件。

在Exchange Server 2013中的邮件流规则的详细信息，请参阅[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)。

有关条件及邮件流规则中的例外情况的详细信息，请参阅[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

有关在Exchange Online或Exchange Online Protection的邮件流规则中的操作的详细信息，请参阅[联机在 Exchange 邮件流规则操作](https://technet.microsoft.com/zh-cn/library/jj919237\(v=exchg.150\))或[邮件流规则操作在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj920117\(v=exchg.150\))。

## 邮箱服务器上邮件流规则的操作

在邮箱服务器上的邮件流规则中可用的操作详见下表。对于每个属性的有效值属性值部分所述。

**注意：**

  - 选择 Exchange 管理中心 (EAC) 中的操作后，\&quot;**按以下内容操作**\&quot;字段中最终显示的值通常与所选的单击路径不同。此外，在创建新规则时，有时可以（取决于所做的选择）从模板（已筛选的操作列表）而不是以下完整的单击路径来选择一个短操作名称。短名称和完整单击路径值显示在表的 EAC 列中。

  - **Get-TransportRuleAction** cmdlet 返回的一些操作名称不同于相应的参数名，并且一个操作可能需要多个参数。


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
<th>EAC 中的操作</th>
<th>Exchange 命令行管理程序中的操作参数</th>
<th>属性</th>
<th>描述</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>将要审批的邮件转发给这些人</strong></p>
<p><strong>将要审批的邮件转发给</strong> &gt; <strong>这些人</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将邮件转发到指定审查方，作为包装在审批请求的附件。有关详细信息，请参阅<a href="common-message-approval-scenarios-exchange-2013-help.md">常见邮件审批方案</a>。不能使用的通讯组作为仲裁人。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>将要审批的邮件转发给发件人的经理</strong></p>
<p><strong>将要审批的邮件转发给</strong> &gt; <strong>发件人的经理</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>无</p></td>
<td><p>将邮件转发给发件人的经理以进行审批。</p>
<p>此操作仅在发件人的 <strong>Manager</strong> 属性于 Active Directory 中定义时适用。否则，邮件会在没有审阅的情况下传递给收件人。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>将邮件重定向给这些收件人。</strong></p>
<p><strong>将邮件重定向给</strong> &gt; <strong>这些收件人</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将电子邮件重定向到指定的收件人。邮件不会传递给原始收件人，也不会向发件人或原始收件人发送通知。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>拒绝邮件并提供说明</strong></p>
<p><strong>阻止邮件</strong> &gt; <strong>拒绝邮件并包括说明</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>在未送达报告（也称为 NDR 或退回邮件）中将邮件返回给发件人，并包含作为拒绝理由的指定文本。收件人不会收到原始邮件或通知。</p>
<p>使用的默认增强状态代码是 <code>5.7.1</code>。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，可以通过使用 <em>RejectMessageEnhancedStatusCode</em> 参数指定 DSN 代码。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>拒绝具有增强状态代码的邮件</strong></p>
<p><strong>阻止邮件</strong> &gt; <strong>拒绝具有以下增强状态代码的邮件</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>在具有指定增强传递状态通知 (DSN) 代码的 NDR 中将邮件返回给发件人。收件人不会收到原始邮件或通知。</p>
<p>有效的 DSN 代码是 <code>5.7.1</code> 或 <code>5.7.900</code> 到 <code>5.7.999</code>。</p>
<p>使用的默认原因文本是 <code>Delivery not authorized, message refused</code>。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，可以通过使用 <em>RejectMessageReasonText</em> 参数指定拒绝原因文本。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>在不通知任何人的情况下删除邮件</strong></p>
<p><strong>阻止邮件</strong> &gt; <strong>在不通知任何人的情况下删除邮件</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>无</p></td>
<td><p>默认删除电子邮件，而不向收件人或发件人发送通知。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>将收件人添加到&amp;quot;密件抄送&amp;quot;框</strong></p>
<p><strong>将收件人</strong> &gt; <strong>添加到&amp;quot;密件抄送&amp;quot;框</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>Bcc</strong>&amp;quot;字段中。原始收件人不会收到通知，也无法看到添加的地址。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>将收件人添加到&amp;quot;收件人&amp;quot;框</strong></p>
<p><strong>将收件人</strong> &gt; <strong>添加到&amp;quot;收件人&amp;quot;框</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>To</strong>&amp;quot;字段中。原始收件人可以看到添加的地址。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>将收件人添加到&amp;quot;抄送&amp;quot;框</strong></p>
<p><strong>将收件人</strong> &gt; <strong>添加到&amp;quot;抄送&amp;quot;框</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>Cc</strong>&amp;quot;字段中。原始收件人可以看到添加的地址。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>将发件人的经理添加为收件人</strong></p>
<p><strong>添加收件人</strong> &gt; <strong>将发件人的经理添加为收件人</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>将发件人的经理添加到邮件中作为指定收件人类型 (<strong>To</strong>、<strong>Cc</strong>、<strong>Bcc</strong>)，或在不通知发件人或收件人的情况下将邮件重定向到发件人的经理。</p>
<p>此操作仅在发件人的 <strong>Manager</strong> 属性于 Active Directory 中定义时适用。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>附加免责声明</strong></p>
<p><strong>对邮件应用免责声明</strong> &gt; <strong>附加免责声明</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>首要属性：<code>DisclaimerText</code></p>
<p>次要属性：<code>DisclaimerFallbackAction</code></p>
<p>第三个属性（仅 Exchange 命令行管理程序）：<code>DisclaimerTextLocation</code></p></td>
<td><p>将指定的 HTML 免责声明应用到邮件末尾。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，可以通过值 <code>Append</code> 使用 <em>ApplyHtmlDisclaimerTextLocation</em> 参数。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>在开头附加免责声明</strong></p>
<p><strong>对邮件应用免责声明</strong> &gt; <strong>在开头附加免责声明</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>首要属性：<code>DisclaimerText</code></p>
<p>次要属性：<code>DisclaimerFallbackAction</code></p>
<p>第三个属性（仅 Exchange 命令行管理程序）：<code>DisclaimerTextLocation</code></p></td>
<td><p>将指定的 HTML 免责声明应用到邮件开头。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，可以通过值 <code>Prepend</code> 使用 <em>ApplyHtmlDisclaimerTextLocation</em> 参数。</p>
<p></p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>删除此头</strong></p>
<p><strong>修改邮件属性</strong> &gt; <strong>删除邮件头</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>可以从邮件头中删除指定的头字段。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>将邮件头设置为此值</strong></p>
<p><strong>修改邮件属性</strong> &gt; <strong>设置邮件头</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>String</code></p></td>
<td><p>在邮件头中添加或修改指定的头字段，并将头字段设置为指定值。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>应用邮件分类</strong></p>
<p><strong>修改邮件属性</strong> &gt; <strong>应用邮件分类</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>将指定邮件分类应用到邮件。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>将垃圾邮件可信度 (SCL) 设置为</strong></p>
<p><strong>修改邮件属性</strong> &gt; <strong>设置垃圾邮件可信度 (SCL)</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>将此邮件的垃圾邮件可信度 (SCL) 设置为指定值。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>将权限保护应用于邮件</strong></p>
<p><strong>修改邮件安全性</strong> &gt; <strong>应用权限保护</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>将指定的权限管理服务 (RMS) 模板应用到邮件中。</p>
<p>针对每个邮箱，RMS 需要 Exchange 企业版客户端访问许可证 (CAL)。有关 CAL 的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 许可</a>。</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>需要 TLS 加密</strong></p>
<p><strong>修改邮件安全性</strong> &gt; <strong>要求 TLS 加密</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>强制出站邮件通过 TLS 加密连接进行路由。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>在邮件主题前面追加</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>将指定的文本添加到邮件&amp;quot;<strong>Subject</strong>&amp;quot;字段的开头。考虑使用空格或冒号 (:) 作为指定文本的最后一个字符以区别于原始的主题文本。</p>
<p>若要防止将相同的字符串添加到主题已包含文本的邮件中（例如，答复），可向规则添加&amp;quot;<strong>主题包括</strong>&amp;quot;(<em>ExceptIfSubjectContainsWords</em>) 例外。</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>使用策略提示通知发件人</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em>（仅 Exchange 命令行管理程序）</p></td>
<td><p>首要属性：<code>NotifySenderType</code></p>
<p>次要属性：<code>String</code></p>
<p>第三个属性（仅 Exchange 命令行管理程序）：<code>DSNEnhancedStatusCode</code></p></td>
<td><p>邮件匹配 DLP 策略时通知发件人或阻止邮件。</p>
<p>使用此操作时，需要使用&amp;quot;<strong>邮件包含敏感信息</strong>&amp;quot;(<em>MessageContainsDataClassification</em>) 条件。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，<em>RejectMessageReasonText</em> 参数为可选参数。如果不使用此参数，则将使用默认文本&amp;quot;<code>Delivery not authorized, message refused</code>&amp;quot;。</p>
<p>在 Exchange 命令行管理程序中，还可以使用 <em>RejectMessageEnhancedStatusCode</em> 参数指定增强状态代码。如果不使用此参数，则将使用默认的增强状态代码 <code>5.7.1</code>。</p>
<p>此操作将限制其他条件、例外以及可以在规则中配置的操作。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>生成事件报告并将它发送到</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>首要属性：<code>Addresses</code></p>
<p>次要属性：<code>IncidentReportContent</code></p></td>
<td><p>将包含指定内容的事件报告发送给指定收件人。</p>
<p>如果邮件与组织中的数据丢失防护 (DLP) 策略相匹配，则将为其生成一个事件报告。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>使用邮件通知收件人</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>指定文本、HTML 标记以及发送给邮件收件人的通知邮件中包含的邮件关键字。例如，可以通知收件人，邮件被规则拒绝，或标记为垃圾邮件并且传递到其&amp;quot;垃圾邮件&amp;quot;文件夹。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><strong>此规则的属性</strong>部分 &gt; <strong>使用以下严重性级别审核此规则</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>指定是否执行以下操作：</p>
<ul>
<li><p>防止在邮件跟踪日志中生成事件报告和相应的条目。</p></li>
<li><p>以指定的严重性级别（低、中或高）在邮件跟踪日志中生成一个事件报告和相应的条目。</p></li>
</ul></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
<tr class="even">
<td><p><strong>此规则的属性</strong> 部分 &gt; <strong>停止处理更多规则</strong></p>
<p><strong>更多选项</strong> &gt; <strong>此规则的属性</strong>部分 &gt; <strong>停止处理更多规则</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>无</p></td>
<td><p>在邮件受规则影响后进行指定，这样免于邮件被其他规则处理。</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


返回顶部

## 边缘传输服务器上邮件流规则的操作

邮箱服务器上可用的一小部分操作也可在边缘传输服务器上使用，但仍有一些操作只在边缘传输服务器上可用。边缘传输服务器上并没有 EAC，因此，只能在本地边缘传输服务器的 Exchange 命令行管理程序中管理邮件流规则。下表介绍了这些操作。属性类型在属性值部分进行介绍。


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
<th>Exchange 命令行管理程序中的操作参数</th>
<th>属性</th>
<th>说明</th>
<th>可用于</th>
<th>适用对象</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>To</strong>&amp;quot;字段中。原始收件人可以看到添加的地址。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>Bcc</strong>&amp;quot;字段中。原始收件人不会收到通知，也无法看到添加的地址。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将一个或多个收件人添加到邮件的&amp;quot;<strong>Cc</strong>&amp;quot;字段中。原始收件人可以看到添加的地址。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>无</p></td>
<td><p>默认删除电子邮件，而不向收件人或发件人发送通知。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>无</p></td>
<td><p>可以断开发送服务器与边缘传输服务器之间的 SMTP 连接，而不生成 NDR。</p></td>
<td><p>仅边缘传输服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>使用本地边缘传输服务器应用程序日志中指定的文本生成一个事件。条目包含以下信息：</p>
<ul>
<li><p><strong>级别</strong> <code>Information</code></p></li>
<li><p><strong>源</strong> <code>MSExchange Messaging Policies</code></p></li>
<li><p><strong>事件 ID</strong> <code>4000</code></p></li>
<li><p><strong>任务类别</strong> <code>Rules</code></p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>仅边缘传输服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>将指定的文本添加到邮件&amp;quot;<strong>Subject</strong>&amp;quot;字段的开头。考虑使用空格或冒号 (:) 作为指定文本的最后一个字符以区别于原始主题。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>无</p></td>
<td><p>将邮件传送到在边缘传输服务器的内容筛选配置中定义的隔离邮箱中。有关详细信息，请参阅<a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">配置垃圾邮件隔离邮箱</a>。</p>
<p>如果没有配置隔离邮箱，则会将邮件以 NDR 的形式退回给发件人。</p></td>
<td><p>仅边缘传输服务器</p></td>
<td><p>Exchange 2010 或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>将电子邮件重定向到指定的收件人。邮件不会传递给原始收件人，也不会向发件人或原始收件人发送通知。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>可以从邮件头中删除指定的头字段。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>首要属性：<code>MessageHeaderField</code></p>
<p>次要属性：<code>String</code></p></td>
<td><p>在邮件头中添加或修改指定的头字段，并将头字段设置为指定值。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>将此邮件的 SCL 设置为指定值。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>首要属性：<code>String</code></p>
<p>次要属性：<code>SMTPStatusCode</code></p></td>
<td><p>可以使用指定的 SMTP 状态和指定的拒绝文本断开发送服务器与边缘传输服务器之间的 SMTP 连接。收件人不会收到原始邮件或通知。</p>
<p>SMTP 状态代码的有效值是从 <code>400</code> 到 <code>500</code> 的整数，如用 RFC 3463 所定义。</p>
<p>如果在不指定 SMTP 状态代码的情况下指定拒绝文本，则会使用默认代码 <code>550</code>。</p>
<p>如果在不指定拒绝文本的情况下指定 SMTP 状态代码，则使用的文本是 <code>Delivery not authorized, message refused</code>。</p></td>
<td><p>仅边缘传输服务器</p></td>
<td><p>Exchange 2007或更高版本</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>无</p></td>
<td><p>在邮件受规则影响后进行指定，这样免于邮件被其他规则处理。</p></td>
<td><p>邮箱服务器和边缘服务器</p></td>
<td><p>Exchange 2013 或更高版本</p></td>
</tr>
</tbody>
</table>


## 属性值

用于邮件流规则中操作的属性值如下表所述。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>有效值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p><strong>收件人</strong></p></li>
<li><p><strong>抄送</strong></p></li>
<li><p><strong>密件抄送</strong></p></li>
<li><p><strong>重定向</strong></p></li>
</ul></td>
<td><p>指定如何在邮件中包含发件人的经理。</p>
<ul>
<li><p>如果选择&amp;quot;<strong>收件人</strong>&amp;quot;、&amp;quot;<strong>抄送</strong>&amp;quot;或&amp;quot;<strong>密件抄送</strong>&amp;quot;，则会将发件人的经理在指定字段中添加为收件人。</p></li>
<li><p>如果选择&amp;quot;<strong>重定向</strong>&amp;quot;，邮件仅会发送给发件人的经理，而不通知发件人或收件人。</p></li>
</ul>
<p>此操作仅在发件人的 <strong>Manager</strong> 属性于 Active Directory 中定义时适用。</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 收件人</p></td>
<td><p>取决于操作，可能能够在组织中指定任何启用邮件的对象，或可能限制为特定的对象类型。通常，可以选择多个收件人，但仅能向一个收件人发送事件报告。</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p>取消选中&amp;quot;<strong>使用以下严重性级别审核此规则</strong>&amp;quot;，或在值为&amp;quot;<strong>未指定</strong>&amp;quot;(<code>DoNotAudit</code>) 的情况下选择&amp;quot;<strong>使用以下严重性级别审核此规则</strong>&amp;quot;</p></li>
<li><p><strong>低</strong></p></li>
<li><p><strong>中</strong></p></li>
<li><p><strong>高</strong></p></li>
</ul></td>
<td><p>&amp;quot;<strong>低</strong>&amp;quot;、&amp;quot;<strong>中</strong>&amp;quot;或&amp;quot;<strong>高</strong>&amp;quot;值指定分配到事件报告和邮件跟踪日志中相应条目的严重性级别。</p>
<p>其他值防止生成事件报告，并防止相应条目被写入邮件跟踪日志中。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p><strong>封装</strong></p></li>
<li><p><strong>忽略</strong></p></li>
<li><p><strong>拒绝</strong></p></li>
</ul></td>
<td><p>指定免责声明无法应用到邮件时的操作。有时无法更改邮件内容（例如，邮件进行加密时）。可用的回退操作为：</p>
<ul>
<li><p><strong>封装</strong>   将原始邮件封装到新的邮件信封中，并将免责声明文本插入到新邮件中。这是默认值。</p>
<p><strong>注意：</strong></p>
<ul>
<li><p>后续邮件流规则将应用于新的邮件信封，而不是应用于原始邮件。因此，使用比其他规则更低的优先级配置这些规则。</p></li>
<li><p>如果无法将原始邮件封装在新邮件信封中，则不会传递原始邮件。邮件将以 NDR 形式退回给发件人。</p></li>
</ul></li>
<li><p><strong>忽略</strong>   忽略该规则，传递邮件时不带免责声明</p></li>
<li><p><strong>拒绝</strong>   邮件以 NDR 的形式退回给发件人。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>HTML 字符串</p></td>
<td><p>指定免责声明文本，该文本可以包含 HTML 标记、级联样式表 (CSS) 标记以及图像（通过使用 IMG 标记）。长度不得超过 5000 个字符，包括标记在内。</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>单值：<code>Append</code> 或 <code>Prepend</code></p></td>
<td><p>在 Exchange 命令行管理程序中，使用 <em>ApplyHtmlDisclaimerTextLocation</em> 指定邮件中免责声明文本的位置：</p>
<ul>
<li><p><code>Append</code>   将免责声明添加到邮件正文的末尾。这是默认值。</p></li>
<li><p><code>Prepend</code>   将免责声明添加到邮件正文的开头。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>单个 DSN 代码值：</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p><code>5.7.900</code> 到 <code>5.7.999</code></p></li>
</ul></td>
<td><p>指定使用的 DSN 代码。通过使用 <strong>New-SystemMessage</strong> cmdlet，可以创建自定义 DSN。</p>
<p>如果不指定拒绝原因文本和 DSN 代码，则使用的默认原因文本是&amp;quot;<code>Delivery not authorized, message refused</code>&amp;quot;。</p>
<p>在创建或修改 Exchange 命令行管理程序中的规则时，可以通过使用 <em>RejectMessageReasonText</em> 参数指定拒绝原因文本。</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>下列值中的一个或多个：</p>
<ul>
<li><p><strong>发件人</strong></p></li>
<li><p><strong>Recipients</strong></p></li>
<li><p><strong>主题</strong></p></li>
<li><p><strong>抄送收件人</strong> (<code>Cc</code>)</p></li>
<li><p><strong>密件抄送收件人</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>严重性</strong></p></li>
<li><p><strong>发件人重写信息</strong> (<code>Override</code>)</p></li>
<li><p><strong>匹配规则</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>误报报告</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>检测到的数据分类</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>匹配内容</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>原始邮件</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>指定事件报告中包含的原始邮件属性。可以选择包含这些属性的任意组合。除了指定的属性，邮件 ID 始终包含在内。这些可用属性为：</p>
<ul>
<li><p><strong>发件人</strong>   原始邮件的实际发件人。</p></li>
<li><p><strong>收件人</strong>、<strong>抄送收件人</strong>和<strong>密件抄送收件人</strong>   邮件所有的收件人或仅&amp;quot;<strong>Cc</strong>&amp;quot;或&amp;quot;<strong>Bcc</strong>&amp;quot;字段中的收件人。对于每个属性，事件报告中只包含前 10 个收件人。</p></li>
<li><p><strong>主题</strong>   原始邮件的&amp;quot;<strong>Subject</strong>&amp;quot;字段。</p></li>
<li><p><strong>严重性</strong>   触发规则的审核严重性。邮件跟踪日志包括所有审核严重性级别，并可以按审核严重性进行筛选。在 EAC 中，如果清除&amp;quot;<strong>使用以下严重性级别审核此规则</strong>&amp;quot;复选框（在 Exchange 命令行管理程序中，<em>SetAuditSeverity</em> 参数值 <code>DoNotAudit</code>），则规则匹配不会显示在规则报告中。如果邮件是由多个规则进行处理，则所有事件报告中均包含最高严重性。</p></li>
<li><p><strong>发件人重写信息</strong>   如果发件人选择覆盖策略提示，则指定覆盖。如果发件人已提供理由，还将包含理由的前 100 个字符。</p></li>
<li><p><strong>匹配规则</strong>   邮件触发的规则的列表。</p></li>
<li><p><strong>误报报告</strong>   如果发件人将邮件标记为策略提示误报，则指定误报。</p></li>
<li><p><strong>检测到的数据分类</strong>   在邮件中检测到的敏感信息类型列表。</p></li>
<li><p><strong>匹配内容</strong>   包含检测到的敏感信息类型、邮件中的准确匹配内容以及匹配敏感信息前后的 150 个字符。</p></li>
<li><p><strong>原始邮件</strong>   将触发规则的整个邮件附加到事件报告中。</p></li>
</ul>
<p>在 Exchange 命令行管理程序中，可以指定用逗号分隔的多个值。</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>单个邮件分类对象</p></td>
<td><p>在 EAC 中，可以从可用邮件分类列表进行选择。</p>
<p>在 Exchange 命令行管理程序中，使用 <strong>Get-MessageClassification</strong> cmdlet 以查看可用的邮件分类对象。</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>单个字符串</p></td>
<td><p>指定要添加、删除或修改的 SMTP 邮件头字段。</p>
<p><em>邮件头</em>是邮件中必需和可选的头字段的集合。头字段的示例有&amp;quot;<strong>To</strong>&amp;quot;、&amp;quot;<strong>From</strong>&amp;quot;、&amp;quot;<strong>Received</strong>&amp;quot;和&amp;quot;<strong>Content-Type</strong>&amp;quot;。正式头字段用 RFC 5322 定义。非正式头字段以 <strong>X-</strong> 开头，称为 <em>X-headers</em>。</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>纯文本、HTML 标记和关键字的任意组合</p></td>
<td><p>指定收件人通知邮件中要使用的文本。</p>
<p>除了纯文本和 HTML 标记外，可以指定使用原始邮件值的以下关键字：</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>下列值之一：</p>
<ul>
<li><p><strong>通知发件人，但允许其发送</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>阻止邮件</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>除非邮件为误报否则阻止邮件</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>阻止邮件，但是允许发件人进行覆盖和发送</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>阻止邮件，但是允许发件人用业务理由覆盖并发送</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>如果邮件违反了 DLP 策略，请指定发件人收到的策略提示类型。以下列表描述了这些设置：</p>
<ul>
<li><p><strong>通知发件人，但允许其发送</strong> 通知发件人，但邮件正常传送。</p></li>
<li><p><strong>阻止邮件</strong> 拒绝邮件并通知发件人。</p></li>
<li><p><strong>除非邮件为误报否则阻止邮件</strong> 除非发件人将邮件标记为误报，否则拒绝邮件。</p></li>
<li><p><strong>阻止邮件，但是允许发件人进行覆盖和发送</strong> 除非发件人选择覆盖策略限制，否则拒绝邮件。</p></li>
<li><p><strong>阻止邮件，但是允许发件人用业务理由覆盖并发送</strong> 这与&amp;quot;<strong>阻止邮件，但是允许发件人进行覆盖和发送</strong>&amp;quot;类型相似，但发件人还提供了覆盖策略限制的理由。</p></li>
</ul>
<p>使用此操作时，需要使用&amp;quot;<strong>邮件包含敏感信息</strong>&amp;quot;(<em>MessageContainsDataClassification</em>) 条件。</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>单个 RMS 模板对象</p></td>
<td><p>指定应用到邮件中的权限管理服务 (RMS) 模板。</p>
<p>在 EAC 中，从列表中选择 RMS 模板。</p>
<p>在 Exchange 命令行管理程序中，使用 <strong>Get-RMSTemplate</strong> cmdlet 来查看可用的 RMS 模板。</p>
<p>针对每个邮箱，RMS 需要 Exchange 企业版客户端访问许可证 (CAL)。有关 CAL 的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 许可</a>。</p></td>
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
<td><p><code>String</code></p></td>
<td><p>单个字符串</p></td>
<td><p>指定将应用于指定邮件头字段、NDR 或事件日志条目的文本。</p>
<p>在 Exchange 命令行管理程序中，如果值包含空格，请使用双引号 (&quot;) 将此值括起来。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 详细信息

[管理邮件流规则](manage-mail-flow-rules-exchange-2013-help.md)

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[联机在 Exchange 邮件流规则操作](https://technet.microsoft.com/zh-cn/library/jj919237\(v=exchg.150\)) 对于Exchange Online

适用于 Exchange Online Protection 的[邮件流规则操作在 Exchange 在线保护](https://technet.microsoft.com/zh-cn/library/jj920117\(v=exchg.150\))

[组织范围的邮件免责声明、 签名、 页脚或 Office 365 中的邮件头](https://technet.microsoft.com/zh-cn/library/dn600323\(v=exchg.150\))

