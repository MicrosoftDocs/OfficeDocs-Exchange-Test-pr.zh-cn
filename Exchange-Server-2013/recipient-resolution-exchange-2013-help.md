---
title: '收件人解析: Exchange 2013 Help'
TOCTitle: 收件人解析
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52061477
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 收件人解析

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-03-17_

“收件人解析”是展开并解析邮件中的所有收件人的过程。解析收件人的操作是将收件人与 Microsoft Exchange 组织中对应的 Active Directory 对象进行匹配。展开收件人的操作是将所有通讯组展开成各个收件人的列表。通过收件人解析，可以正确地将邮件限制和备选收件人应用于每个收件人。

在 Microsoft Exchange Server 2013 组织中，通过邮箱服务器上传输服务的分类程序执行收件人解析。在将新到达的邮件放入提交队列之后，对每封邮件进行分类。在将邮件放入传递队列之前，除了对邮件执行内容转换和路由之外，还将对邮件执行收件人解析。分类程序在路由之前执行收件人解析。分类程序中负责解析收件人的组件通常称为“解析程序”。

**目录**

顶级解析

展开

拆分和控制收件人展开

收件人解析诊断

## 顶级解析

“顶级解析”是收件人解析的第一个阶段。顶级解析将传入邮件中的每个收件人与 Active Directory 中相匹配的收件人对象进行关联。在顶级解析期间，分类程序会创建一个列表，列表中包含邮件中存在的发件人电子邮件地址以及初始的未展开收件人的电子邮件地址。然后，分类程序使用该电子邮件地址列表查询 Active Directory，以查找任何具有相匹配的电子邮件地址属性并且已启用邮件的对象。找到匹配项之后，将缓存相匹配的 Active Directory 对象的属性，以便以后使用。同时，还会强制执行任何发件人邮件限制。

## 收件人电子邮件地址

顶级解析从某封邮件并从“邮件信封”的初始的、未展开的收件人列表开始。“邮件信封”包含用于在 SMTP 邮件服务器之间传输邮件的命令。发件人的电子邮件地址包含在 **MAIL FROM:**  命令中。每个收件人的电子邮件地址分别包含在各自的 **RCPT TO:**  命令中。信封发件人和信封收件人通常通过邮件头中的 `To:`、`From:`、`Cc:` 和 `Bcc:` 头字段的发件人和收件人创建。但是，并非始终如此。邮件中的 `To:`、`From:`、`Cc:` 和 `Bcc:` 头字段很容易伪造，可能与用于传输邮件的实际发件人电子邮件地址和收件人电子邮件地址不匹配。

## 封装电子邮件地址

标准的 SMTP 电子邮件地址遵循 RFC 2821 和 RFC 2822 的规范，例如 chris@contoso.com。但是，电子邮件地址也可以是封装在有效 SMTP 地址内的非 SMTP 电子邮件地址。Exchange 支持使用 Internet Mail 连接器封装地址 (IMCEA) 封装方法封装的地址。

此封装方法要求对任何在 SMTP 电子邮件地址中无效的字符进行编码。字母数字字符、等号 (=) 和连字符 (-) 不需要进行编码。其他字符使用以下编码语法：

  - 正斜杠 (/) 替换为下划线 (\_)。

  - 其他 US-ASCII 字符替换为加号 (+)，而它的两位 ASCII 值以十六进制表示。例如，空格字符的编码值为 `+20`。

IMCEA 封装方法使用以下语法：`IMCEA<Type>-<address>@<domain>`

占位符 \<*Type*\> 标识非 SMTP 地址的类型，例如 `EX`、`X400` 或 `FAX`。

> [!NOTE]
> 尽管 <code>SMTP</code> 和 <code>X500</code> 在理论上是 &lt;<em>Type</em>&gt; 的有效值，但是，Exchange 收件人解析拒绝任何使用其中任一类型的 IMCEA 编码地址。


占位符 \<*address*\> 是编码的原始地址。占位符 \<*domain*\> 代表用于封装非 SMTP 地址的 SMTP 域，例如 contoso.com。

使用 IMCEA 封装方法，仅当域与 Exchange 组织中的默认权威域相匹配时，才会解除地址的封装。有关接受域的详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

Exchange 中的 SMTP 电子邮件地址的最大长度为 571 个字符。此限制包括：

  - 代表地址的名称部分的 315 个字符

  - 代表域名的 255 个字符

  - 用于分隔地址的名称部分和域名的 at 符号 (@)

请注意，如果地址的名称部分超过 315 个字符，即使完整的电子邮件地址少于 571 个字符，Exchange 也不支持使用 IMCEA 封装方法进行编码的邮件。

## 地址解析

每封邮件的发件人电子邮件地址和所有收件人电子邮件地址将添加到用于查询 Active Directory 的列表中。任何封装的地址将先解除封装，然后再添加到电子邮件地址列表中。Active Directory 一次最多可以对 20 个电子邮件地址执行查询。如果 Active Directory 查询遇到任何暂时性错误，邮件将返回到提交队列，并延迟与 Microsoft Exchange 传输服务相关联的 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 应用程序配置文件中 *ResolverRetryInterval* 项指定的时间。默认值为 30 分钟。

下表介绍 Active Directory 中存在的收件人对象。有关 Exchange 收件人类型的详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

### Active Directory 中的收件人对象

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 收件人类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>任何已启用邮件的组对象。通讯组对象类型如下所述：</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   通用通讯组对象</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   具有电子邮件地址的通用安全组 (USG) 对象</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   具有电子邮件地址的本地安全组对象或全局安全组对象</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>具有 Active Directory 类 <strong>msExchDynamicDistributionList</strong> 的对象。有关详细信息，请参阅<a href="manage-dynamic-distribution-groups-exchange-2013-help.md">管理动态通讯组</a>。</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>具有电子邮件地址以及已定义的 <em>Database</em> 参数的用户对象</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>具有电子邮件地址以及已定义的 <em>Database</em> 参数的用户对象有关详细信息，请参阅<a href="manage-mail-users-exchange-2013-help.md">管理邮件用户</a>。</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>具有电子邮件地址的联系人对象。通常，邮件联系人用于 Exchange 组织外部的收件人。在跨林的 Exchange 环境中也会使用邮件联系人。有关详细信息，请参阅<a href="manage-mail-contacts-exchange-2013-help.md">管理邮件联系人</a>。</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>具有电子邮件地址的公用文件夹对象。</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>具有 Active Directory 类 <strong>msExchExchangeServerRecipient</strong> 的对象。有关 Microsoft Exchange 收件人对象的详细信息，请参阅<a href="recipients-exchange-2013-help.md">收件人</a>。</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>具有 Active Directory 类 <strong>exchangeAdminService</strong> 的对象。Exchange 组织中只应有一个系统助理邮箱。</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>具有电子邮件地址并且位于 Microsoft Exchange 系统对象容器中的用户对象。Exchange 组织中的每个邮箱数据库应有一个系统邮箱。</p></td>
</tr>
</tbody>
</table>


Active Directory 查询将缺少关键属性或关键属性格式不正确的对象视为无效对象。例如，将没有电子邮件地址的动态通讯组对象视为无效对象。发送给被视为无效对象的收件人的邮件将导致生成未送达报告 (NDR)。

对每个电子邮件地址，将针对所有可能的收件人属性（例如收件人标识符、收件人类型、邮件限制、电子邮件地址和备选收件人）执行一次初始查询。将缓存适用的收件人属性，供以后使用。收件人解析将根据解析收件人的方式的相似之处以及适用的收件人属性的相似之处来对收件人进行分类。

用于地址解析的 LDAP 筛选器如下所述：

  - 对于 **EX** 电子邮件地址类型，LDAP 筛选器基于收件人的 **legacyExchangeDN** Active Directory 属性或收件人的 **proxyAddresses** Active Directory 属性。**legacyExchangeDN** Active Directory 属性优先。

  - 对于所有其他电子邮件地址类型，使用收件人的 **proxyAddresses** Active Directory 属性作为 LDAP 筛选器。

如果邮件中使用的电子邮件地址与对应的 Active Directory 对象的主 SMTP 地址不匹配，分类程序将在邮件中重写电子邮件地址，以匹配主 SMTP 地址。原始电子邮件地址保存在邮件信封中 **RCPT TO:**  命令的 `ORCPT=` 条目中。

## 发件人邮件限制

用于发件人邮件大小限制的大小是邮件头中“X-MS-Exchange-Organization-OriginalSize:”头字段的值。Exchange 使用此头字段来记录该邮件进入 Exchange 组织时的原始邮件大小。只要检查邮件的指定邮件大小限制，就会使用当前邮件大小或原始邮件大小头字段的较低值。邮件的大小可能会由于内容转换、编码和代理处理等原因而有所变化。如果此头字段不存在，将使用当前邮件大小值进行创建。如果邮件过大，将生成 NDR 并停止其他邮件处理。

只在处理邮件的第一台邮箱服务器上强制执行发件人的收件人限制。将比较原始的未展开邮件信封的收件人数与发件人的收件人限制。嵌套的通讯组列表使用远程展开服务器时，使用原始的未展开邮件信封收件人数可以避免在 Microsoft Exchange Server 2003 中发生部分邮件传递问题。

通过在邮件中标记某个扩展属性，将邮件发件人和所有收件人标记为已解析。如果必须再次对邮件进行收件人解析，此扩展属性使邮件可以绕过顶级解析。邮件可能由于 Microsoft Exchange 传输服务重新启动，而必须再次进行收件人解析。

返回顶部

## 展开

展开在顶级解析之后进行。展开将嵌套的收件人级别完全展开为各个收件人。展开可能需要多次进行展开过程，才能展开所有收件人。并非所有收件人都必须展开。但是，所有收件人必须都要进行展开过程。展开过程还强制执行所有收件人类型的收件人邮件限制。

下表介绍需要展开的收件人类型：

  - **通讯组和动态通讯组**   通讯组基于 **memberOf** Active Directory 属性展开。动态通讯组使用 Active Directory 查询定义展开。如果对组设置了 *ExpansionServer* 参数，则不是由当前服务器展开该组。通讯组将被路由到指定的服务器进行展开。
    
    > [!NOTE]
    > 如果选择组织中的特定传输服务器作为展开服务器，通讯组的使用将取决于展开服务器的可用性。如果展开服务器不可用，任何发送给该通讯组的邮件均将无法送达。如果计划对通讯组使用特定的展开服务器，为了降低服务中断的风险，应考虑对这些服务器实现高可用性解决方案。


  - **备选收件人**   邮箱和已启用邮件的公用文件夹可能会设置 *ForwardingAddress* 参数。*ForwardingAddress* 参数将所有邮件重定向到指定的备选收件人。这称为“转发收件人”。如果在 *ForwardingAddress* 参数中指定了备用传递地址，并将 *DeliverToMailboxAndForward* 参数设置为 `$true`，邮件将传递给原始收件人和备选收件人。这称为“送达并转发收件人”。

  - **联系人链**   “联系人链”是将 *ExternalEmailAddress* 参数设置为 Exchange 组织中另一个收件人的电子邮件地址的邮件用户或邮件联系人。

## 收件人循环的检测

在展开通讯组、备选收件人和联系人链时，分类程序将检查“收件人循环”。收件人循环属于收件人配置问题，使邮件无休止地循环传递给相同的收件人。下表介绍不同类型的收件人循环：

  - **无害收件人循环**   无害收件人循环可以使邮件成功地送达。下表介绍发生无害收件人循环的两种情况：
    
      - 两个通讯组互为成员时。
    
      - 将邮箱或已启用邮件的公用文件夹设置为送达并转发到另一个收件人时。当两个收件人的 *DeliverToMailboxAndForward* 参数都设置为 `$true`，并且 *ForwardingAddress* 参数设置为另一个收件人时，才会发生这种情况。
    
    检测到无害收件人循环时，邮件将传递给收件人，但是不会再尝试将邮件传递给同一个收件人。

  - **中断收件人循环**   中断收件人循环将无法使邮件成功地送达。例如，如果邮箱或已启用邮件的公用文件夹相互将 *ForwardingAddress* 参数设置为另一个收件人，则会出现中断收件人循环。分类程序检测到中断收件人循环时，展开当前收件人的活动将停止，并为该收件人生成 NDR。

检测收件人循环不会阻止重复邮件的传递。例如，如果满足下列条件，通讯组 C 将遇到传递重复邮件的情况：

  - 通讯组 B 和通讯组 C 是通讯组 A 的成员。

  - 通讯组 C 也是通讯组 B 的成员。

## 通讯组的送达报告重定向

展开通讯组后，将检查邮件类型，以确定是否是送达报告邮件。如果邮件是送达报告，将检查通讯组的重定向设置，以确定是否要求重定向送达报告。由于送达报告可能会错误地披露有关通讯组及其成员身份的信息，所以，您可能希望禁止送达报告。

下表介绍通讯组和动态通讯组可用的送达报告重定向设置：

  - **ReportToManagerEnabled**   此参数使送达报告发送给通讯组主管。有效值为 `$true` 或 `$false`。默认值为 `$false`。通讯组的主管由 **Set-Group** cmdlet 中的 *ManagedBy* 参数控制。动态通讯组的主管由 **Set-DynamicDistributionGroup** cmdlet 中的 *ManagedBy* 参数控制。

  - **ReportToOriginatorEnabled**   此参数使送达报告发送给向此通讯组发送的电子邮件的发件人。有效值为 `$true` 或 `$false`。默认值为 `$true`。
    
    > [!NOTE]
    > <em>ReportToManagerEnabled</em> 参数和 <em>ReportToOriginatorEnabled</em> 参数的值不能同时为 <code>$true</code>。如果一个参数设置为 <code>$true</code>，另一个参数必须设置为 <code>$false</code>。两个参数的值可以同时为 <code>$false</code>。这样将抑制所有送达报告邮件的所有重定向。


下表介绍可用的送达报告邮件：

  - **送达回执 (DR)**   此报告确认邮件已成功传递给所需的收件人。

  - **传递状态通知 (DSN)**   此报告介绍尝试传递邮件的结果。有关 DSN 邮件的详细信息，请参阅 [Exchange 2013 中的 DSN 和 NDR](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)。

  - **邮件处理通知 (MDN)**   此报告介绍邮件在成功地传递给收件人之后的状态。已读通知 (RN) 和未读通知 (NRN) 均是 MDN 邮件的示例。MDN 邮件在 RFC 2298 中定义，由邮件头中的 **Disposition-Notification-To:**  头字段控制。使用 `Disposition-Notification-To:` 头字段的 MDN 设置与许多不同的邮件服务器兼容。MDN 设置还可以使用 Microsoft Outlook 和 Exchange 中的 MAPI 属性进行定义。

  - **未送达报告 (NDR)**   此报告向邮件发件人指示邮件无法传递给指定的收件人。

  - **未读通知 (NRN)**   此报告指示邮件尚未阅读即被删除。

  - **外出 (OOF)**   此报告指示收件人将无法答复电子邮件。首字母缩写 OOF 来源于原来的 Microsoft 邮件系统，其中对应的通知名为“out of facility”。

  - **已读通知 (RN)**   此报告指示邮件已读。

  - **重新调用报告**   此报告指示特定收件人的重新调用请求的状态。发件人尝试使用 Outlook 重新调用已发送的邮件时，将发出重新调用请求。

将送达报告邮件发送给通讯组时，下列设置将删除该报告邮件：

  - 未设置报告重定向。此外，报告重定向设置为邮件发件人。

  - 报告重定向设置为通讯组主管，并且送达报告邮件不是 NDR。

将送达报告邮件发送给通讯组时，送达报告邮件可能会传递给通讯组主管：当报告重定向设置为通讯组主管，并且报告邮件是 NDR 时会发生这种情况。

将不是送达报告邮件的邮件发送给通讯组时，邮件将传递给通讯组成员。下表汇总了报告请求设置：

  - 如果报告重定向设置为邮件发件人，则不会修改报告请求设置。

  - 如果未设置报告重定向，则将抑制所有报告请求设置。`NOTIFY=NEVER` 条目将添加到邮件信封中每个收件人的 **RCPT TO:**  中。

  - 如果报告重定向设置为通讯组主管，将抑制所有报告请求设置，发送给通讯组主管的 NDR 邮件除外。

## 收件人的邮件限制

展开过程还强制执行任何为收件人配置的邮件限制。可以为每个收件人分别配置这些限制，也可以以组织级别为 Exchange 组织中的所有集线器传输服务器配置这些限制。下表介绍为收件人配置的邮件限制。

### 收件人的邮件限制

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>来源</th>
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p><em>MaxReceiveSize</em> 参数指定用于为收件人配置的邮件限制的大小，该大小是邮件头中 <strong>X-MS-Exchange-Organization-OriginalSize:</strong> 头字段的值。Exchange 使用此头字段来记录该邮件进入 Exchange 组织时的原始邮件大小。只要检查邮件的指定邮件大小限制，就会使用当前邮件大小或原始邮件大小头字段的较低值。邮件的大小可能会由于内容转换、编码和代理处理等原因而有所变化。如果此头字段不存在，将使用当前邮件大小值进行创建。如果邮件过大，将生成 NDR 并停止其他邮件处理。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em> 参数要求发送给收件人的所有邮件均来自经过身份验证的发件人。此参数的值设置为 <code>$true</code> 时，将拒绝来自未经过身份验证的发件人的邮件。所有向系统邮箱和系统助理邮箱发送邮件的发件人必须经过身份验证。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em> 参数指定允许其成员向此收件人发送邮件的发件人或通讯组。请注意，此参数结合了旧 <em>AcceptMessagesOnlyFrom</em> 和 <em>AcceptMessagesOnlyFromDLMembers</em> 参数的功能。</p>
<p><em>RejectMessagesFromSendersOrMembers</em> 参数指定不允许其成员向此收件人发送邮件的发件人或通讯组。请注意，此参数结合了旧 <em>RejectMessagesFrom</em> 和 <em>RejectMessagesFromDLMembers</em> 参数的功能。</p>
<p>分类程序通过两个阶段检查收件人权限。第一个阶段确定发件人在 <em>AcceptOnlyMessagesFromSendersOrMembers</em> 或 <em>RejectMessagesFromSendersOrMembers</em> 参数中是否存在。如果在两个参数中均未找到发件人，则将完全展开这些参数中的通讯组。完全展开通讯组可能需要一段时间。建议您最大程度地减少这些参数中嵌套通讯组的深度。</p></td>
</tr>
</tbody>
</table>


由经过身份验证的发件人发送的某些邮件类型不在限制范围内。下表介绍不在收件人限制范围内的邮件：

  - **由 Microsoft Exchange 收件人发送的所有邮件**   这些邮件包括 DSN 邮件、日记报告、配额邮件以及其他由系统生成的并发送给内部邮件发件人的邮件。有关 Microsoft 收件人的详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

  - **由外部邮局主管地址发送的所有邮件**   这些邮件包括 DSN 邮件以及其他由系统生成的并发送给外部邮件发件人的邮件。有关外部邮局主管地址的详细信息，请参阅[配置外部邮局主管地址](configure-the-external-postmaster-address-exchange-2013-help.md)。

某些类型的邮件将禁止从 Exchange 组织发送到外部域。相关设置由 **Set-RemoteDomain** cmdlet 中的下列参数控制：

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

有关详细信息，请参阅[远程域](remote-domains-exchange-2013-help.md)。

返回顶部

## 拆分和控制收件人展开

由于通过收件人解析展开并解析邮件收件人的完整列表，所以，有时必须为同一封邮件创建不同的副本。这些情况如下所述：

  - **邮件收件人要求使用不同的邮件设置时**   可能必须对某些收件人启用已读回执等邮件属性，并对其他收件人禁用。创建与原始邮件的属性略有不同的新邮件版本称为“拆分”。

  - **要限制单封邮件中的信封收件人数时**   在展开较大的通讯组时，收件人展开过程可能会生成数千个收件人。在 Exchange 中，将为具有数千个信封收件人的邮件创建具有有限信封收件人数的多个副本，而不是为该邮件创建单一副本。

## 拆分

如果满足下列条件，收件人解析将拆分邮件：

  - 更新邮件信封的 **MAIL FROM:**  中的邮件发件人时。例如，当通讯组的 *ReportToManagerEnabled* 参数的值为 `$true` 时。

  - 必须抑制自动答复邮件（例如 DSN、OOF 邮件和重新调用报告）时。

  - 展开备选收件人时。

  - 当 **Resent-From:**  头字段必须添加到邮件头时。Resent 头字段是信息性头字段，可用于确定邮件是否已由用户转发。使用 Resent 头字段，该邮件在收件人处看似是由原始发件人直接发来的邮件。收件人可以查看该邮件头来了解转发邮件的用户。Resent 头字段在 RFC 2822 的 3.6.6 节中定义。

  - 必须传输展开通讯组的历史记录时。

## 控制收件人展开

如果展开的收件人数过多，分类程序会将邮件拆分为多个副本。通过进行拆分，可以减少展开邮件期间使用的系统资源。邮件中的最大信封收件人数由 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` 应用程序配置文件中的 *ExpansionSizeLimit* 项控制。默认值为 1000。

> [!CAUTION]
> 建议您不要在生产环境中的 Exchange 传输服务器上修改 <em>ExpansionSizeLimit</em> 项的值。


返回顶部

## 收件人解析诊断

收件人解析的报告和诊断信息由性能计数器和邮件跟踪日志项提供。这些信息源可以帮助您确定并诊断收件人解析出现的问题。

## 收件人解析性能计数器

下表介绍收件人解析可用的性能计数器。

### 收件人解析性能计数器

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>计数器名称</th>
<th>显示名</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Ambiguous Recipients</p></td>
<td><p>此计数器是在解析收件人期间检测到的不明确的收件人总数。不明确的收件人是具有相匹配的 <strong>legacyExchangeDN</strong> Active Directory 属性或相匹配的 <strong>proxyAddresses</strong> Active Directory 属性的不同收件人。</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Ambiguous Senders</p></td>
<td><p>此计数器是在解析收件人期间检测到的不明确的发件人数。不明确的发件人是具有相匹配的 <strong>legacyExchangeDN</strong> Active Directory 属性或相匹配的 <strong>proxyAddresses</strong> Active Directory 属性的不同发件人。</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Failed Recipients</p></td>
<td><p>此计数器是在解析收件人期间检测到的失败的收件人数。</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Loop Recipients</p></td>
<td><p>此计数器是由于收件人循环导致收件人解析失败的收件人数。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Messages Chipped</p></td>
<td><p>此计数器是在解析收件人期间为了控制单封邮件中的信封收件人数，为同一封邮件创建的副本总数。在 Exchange 中，此过程称为“分片”。</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Messages Created</p></td>
<td><p>此计数器是在解析收件人期间创建的邮件数。</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Messages Retried</p></td>
<td><p>此计数器是在解析收件人期间计划重试的邮件数。</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Unresolved Org Recipients</p></td>
<td><p>此计数器是在解析收件人期间检测到的来自权威域的未解析收件人数。</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Unresolved Org Senders</p></td>
<td><p>此计数器是在解析收件人期间检测到的来自权威域的未解析发件人数。</p></td>
</tr>
</tbody>
</table>


## 邮件跟踪日志中的收件人解析事件

下表介绍邮件跟踪日志中记录的收件人解析事件。

### 邮件跟踪日志中的收件人解析事件

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>邮件跟踪事件</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPAND</p></td>
<td><p>此事件指示通讯组已展开。</p></td>
</tr>
<tr class="even">
<td><p>REDIRECT</p></td>
<td><p>此事件指示发送给邮箱收件人或已启用邮件的公用文件夹收件人的邮件已重定向到 <em>ForwardingAddress</em> 参数指定的备选收件人。</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVE</p></td>
<td><p>此事件指示收件人电子邮件地址已更改为对应的 Active Directory 收件人对象的主 SMTP 电子邮件地址。</p></td>
</tr>
<tr class="even">
<td><p>TRANSFER</p></td>
<td><p>此事件指示已进行邮件拆分或分片。</p></td>
</tr>
</tbody>
</table>


有关邮件跟踪的详细信息，请参阅[邮件跟踪](message-tracking-exchange-2013-help.md)。

