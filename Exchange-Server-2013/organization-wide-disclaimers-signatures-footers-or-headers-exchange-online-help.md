---
title: '组织范围内的免责声明、签名、脚注或标头: Exchange 2013 Help'
TOCTitle: 组织范围内的免责声明、签名、脚注或标头
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060568
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 组织范围内的免责声明、签名、脚注或标头

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

您可以将电子邮件免责声明、法律免责声明、披露声明、签名，或其他信息添加到进入或离开您的组织的电子邮件的顶部或底部。这对法律、业务或法规要求确定潜在的不安全电子邮件，或对您的组织中特有的其他原因而言，或许是必要的。

要设置一个免责声明，您需要创建一个传输规则，其中包括一些条件，比如发件人在某个特定的组中时，或者邮件中包含特定的文本模式以及要添加的文本时。要对单个电子邮件应用多个免责声明，您需要使用多个传输规则。

> [!IMPORTANT]  
> <ul>
> <li><p>如果只想将信息添加到传出邮件，您必须添加一个条件，例如收件人位于组织之外。默认情况下，传输规则同时应用于传入邮件和传出邮件。</p></li>
> </ul>


**目录**

示例

划定免责声明的作用域

规定免责声明的格式

不能添加免责声明时的回退选项

详细信息

寻找过程吗？请参阅[组织范围的邮件免责声明、 签名、 页脚或 Office 365 中的邮件头](https://technet.microsoft.com/zh-cn/library/dn600323\(v=exchg.150\))。

## 示例

以下是有关如何使用免责声明的几个建议。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>添加的示例文本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>法律 – 传出邮件</p></td>
<td><p>此电子邮件和随之传送的任何文件都是保密的，仅供收件的个人或实体使用。如果您错误地收到此电子邮件，请通知系统管理员。</p></td>
</tr>
<tr class="even">
<td><p>法律 – 传入邮件</p></td>
<td><p>明确要求员工不要制造诽谤性言论，不要侵犯或授权侵犯任何版权以及任何涉及到电子邮件通信的其他法律权利。收到这类电子邮件的员工必须立即通知主管。</p></td>
</tr>
<tr class="odd">
<td><p>请注意邮件的发送对象使用的是别名</p></td>
<td><p>此邮件的发送对象是销售讨论组。</p></td>
</tr>
<tr class="even">
<td><p>签名 - 获得每个员工的数据</p></td>
<td><p>Kathleen Mayer<br />
销售部门<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
电话：111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>广告</p></td>
<td><p>单击此处可查看 3 月的详细信息</p></td>
</tr>
</tbody>
</table>


本文中的示例不应按原样使用。针对您的需要，可以对其进行修改。

## 划定免责声明的作用域

您在制定免责声明时，应考虑它们适用于哪些邮件。例如，您可以为内部邮件和外部邮件或者特定部门中的用户发送的邮件指定不同的免责声明。为了确保只让对话中的第一封邮件收到免责声明，需要添加一个例外，查找免责声明中特有的文本。

以下是您可以使用的一些条件和例外的示例。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>说明</th>
<th>EAC 中的条件和例外</th>
<th>Shell 中的条件和例外</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织外部，如果原始邮件中不包含免责声明中的文本，如“CONTOSO 法律声明”</p></td>
<td><p>条件：“收件人位于”&gt;“组织外部”</p>
<p>例外：“主题或正文”&gt;“主题或正文与这些文本模式匹配”&gt; <strong>CONTOSO LEGAL NOTICE</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>带有可执行性附件的传入邮件</p></td>
<td><p>条件 1：“发件人位于”&gt;“组织外部”</p>
<p>条件 2：“任何附件”&gt;“具有可执行内容”</p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>发件人是市场营销部</p></td>
<td><p>条件：“发件人”&gt;“是此组的成员”&gt; <strong>group name</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>从外部发件人发送到销售讨论组的每封邮件</p></td>
<td><p>条件 1：“发件人位于”&gt;“组织外部”</p>
<p>条件 2：“邮件”&gt;“‘收件人’或‘抄送’框包含此人”&gt; <strong>group name</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>在长达一个月的时间内将广告预加在传出邮件上</p></td>
<td><p>条件 1：“收件人位于”&gt;“组织外部”</p>
<p>在“新建规则”对话框的底部指定日期。</p></td>
<td><p>-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' –ActivationDate ‘03/1/2014’ –ExpiryDate ‘03/31/2014’</p></td>
</tr>
</tbody>
</table>


有关您可以应用于免责声明的传输规则条件的完整列表，请参阅下列项之一：

  - [在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [在联机 Exchange 邮件流规则条件和例外 （谓语）](https://technet.microsoft.com/zh-cn/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## 规定免责声明的格式

根据需要，您可以规定您的免责声明的格式。以下是您可以包含在免责声明文本中的内容。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>信息类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>文本</p></td>
<td><p>最大长度为 5000 个字符，包括任何 HTML 标记和内联级联样式表 (CSS)。</p></td>
</tr>
<tr class="even">
<td><p>HTML 和内联 CSS</p></td>
<td><p>您可以使用 HTML 和内联 CSS 样式设置文本的格式。例如，使用 <code>&lt;HR&gt;</code> 标记可以在免责声明之前添加一行。</p>
<p>如果将免责声明添加到纯文本邮件中，则免责声明中的 HTML 将被忽略。</p></td>
</tr>
<tr class="odd">
<td><p>添加图像</p></td>
<td><p>使用 <code>&lt;IMG&gt;</code> 标记可以指向 Internet 上可用的图像。例如，<code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>请记住，在默认情况下，Outlook Web App 和 Outlook 会阻止外部网站的内容，包括图像。用户如果想查看被阻止的外部内容，可能需要执行特定操作。这意味着，默认情况下，通过使用 <code>IMG</code> 标记添加的图像可能是不可见的。我们建议您在您的收件人很可能在电子邮件客户端中使用的 <code>IMG</code> 标记来测试免责声明，以确认是否可以正常显示。</p></td>
</tr>
<tr class="even">
<td><p>添加个性化签名信息</p></td>
<td><p>如果您希望每个人的签名都使用相同格式并附有相同的信息，您可以为每一位员工添加独特的信息，如 <code>DisplayName</code>、<code>FirstName</code>、<code>LastName</code>、<code>PhoneNumber</code>、<code>Email</code>、<code>FaxNumber</code> 和 <code>Department</code>。必须在信息的两端都使用两个百分号 (%%)，将该信息封闭起来。例如，如果使用 <code>DisplayName</code>，就必须在免责声明中使用“%%DisplayName%%”。</p>
<p>当免责声明被触发，即插入该用户所对应的值。该数据来自发件人的 Active Directory 用户帐户（用于本地 Exchange 服务器），或来自发件人用于 Exchange Online 的 Office 365 帐户。</p>
<p>有关可以用在免责声明和个性化签名中的完整属性列表，请参阅<a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">传输规则条件（谓词）</a> (Exchange Server)、<a href="https://technet.microsoft.com/zh-cn/library/jj919235(v=exchg.150)">在联机 Exchange 邮件流规则条件和例外 （谓语）</a> (Exchange Online) 或 <a href="https://technet.microsoft.com/zh-cn/library/jj919234(v=exchg.150)">邮件流规则条件和例外 （谓语） 在 Exchange 在线保护</a> (Exchange Online Protection) 中的 <code>ADAttribute</code> 属性说明。</p></td>
</tr>
</tbody>
</table>


例如，下面是一个 HTML 免责声明示例，其中包括签名、 `IMG` 标记和嵌入的 CSS。

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## 不能添加免责声明时的回退选项

有一些邮件（如加密的邮件）会阻止 Exchange 修改原始邮件的内容。您可以控制​​您的组织处理这些邮件的方式。您可以对包含免责声明的邮件信封中无法修改的邮件指定是否进行封装，如果无法添加免责声明，是否要拒绝该邮件，或忽略免责声明的操作并传递该不包含免责声明的邮件。

下面以列表形式对每个回退操作进行了说明：

  - **封装**   如果不能将免责声明插入到原始邮件中，则 Exchange 会将原始邮件封装在新的邮件信封中。然后将免责声明插入新邮件中。如果无法将原始邮件封装在新邮件信封中，则不会传递原始邮件。邮件的发件人将收到说明邮件未送达原因的未送达报告 (NDR)。
    
    > [!IMPORTANT]  
    > 如果将原始邮件封装在新邮件信封中，则后续传输规则将应用于新邮件信封，而不是原始邮件。因此，在配置其他传输规则之后，必须配置包含免责声明操作的传输规则，将原始邮件封装在新的邮件正文中。


  - **拒绝**   如果无法将免责声明插入原始邮件，则 Exchange 不传递该邮件。邮件的发件人将收到说明邮件未送达原因的 NDR。

  - **忽略**   如果无法将免责声明插入原始邮件，则 Exchange 将在未经修改的情况下继续传递原始邮件。这种情况下，不添加免责声明。

## 详细信息

[组织范围的邮件免责声明、 签名、 页脚或 Office 365 中的邮件头](https://technet.microsoft.com/zh-cn/library/dn600323\(v=exchg.150\))

[邮件流或传输规则](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Exchange Online Protection 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

