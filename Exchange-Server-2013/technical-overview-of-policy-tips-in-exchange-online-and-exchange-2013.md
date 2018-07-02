---
title: Exchange Online 和 Exchange 2013 中策略提示的技术概述
TOCTitle: 策略提示
ms:assetid: 4266b83c-dd8a-4b3d-99ff-402e68fc810c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150512(v=EXCHG.150)
ms:contentKeyID: 50489654
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 策略提示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-07-22_

您可以创建包含*策略提示*通知消息的数据丢失防护 (DLP) 策略来帮助组织的 Microsoft Outlook、Outlook Web App (OWA) 和 OWA for Devices 电子邮件用户避免以不当方式发送敏感信息。与 Microsoft Exchange Server 2010 中引入的邮件提示类似，策略提示通知消息会在用户撰写电子邮件时显示在 Outlook 中。只有当发件人的电子邮件的某些信息可能违反现有某项 DLP 策略，并且策略的规则会在满足设定条件时通知发件人时，才会显示策略提示通知消息。有关数据丢失防护的更多常规信息，请参阅[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)。

为便于向电子邮件发件人显示策略提示，规则中必须包含“使用策略提示通知发件人”这项操作。您可以从 Exchange 管理中心向规则编辑器中添加此操作。有关详细信息，请参阅[管理策略提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)。

强制执行 DLP 策略的传输规则代理在评估邮件和策略中的条件时，不会区分邮件附件、正文文本或主题行。例如，如果用户创建了一封邮件正文包含信用卡号的电子邮件，然后尝试将该邮件发送给组织外部的收件人，Outlook 或 Outlook Web App 中会向该用户显示策略提示通知消息，提醒他们企业对于此类信息的要求。但是，此类通知仅在已配置了 DLP 策略来限制上例所述操作时才会显示；在本例中，要在含有信用卡数据的邮件的标头添加一个外部电子邮件别名。在创建 DLP 策略时，有各种条件、操作和例外可供选择。这种多样化的选择让您可以根据特定的组织需求来灵活调整数据丢失防护工作。

当您使用规则内的通知发件人操作或覆盖操作时，我们建议您同时包括从组织内部发送邮件的条件。可以通过使用策略规则编辑器添加以下条件来做到这一点：“发件人位于…”\>“组织内部”。有关更改现有 DLP 策略的详细信息，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。这是一个最佳实践建议，因为通知发件人操作已作为公司邮件创建体验的一部分进行应用。该操作中涉及的发件人即为公司内的邮件撰写者。对于传入邮件，您的用户无法对由策略提示呈现的用户交互执行操作，并且当发件人位于组织外部时，将忽略该用户交互。您可以应用 DLP 策略来扫描传入邮件并执行各种操作，但当您这样做时，不要添加通知发件人操作。

如果策略提示通知让组织中正在撰写邮件的发件人实时了解到组织的相关要求和标准，将可以降低他们违反组织强制执行的各种标准的可能。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Exchange Online：DLP 是一项高级功能，要求使用 Exchange Online 计划 2 订阅。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=286154">Exchange Online Licensing</a>（Exchange Online 授权）。</p></li>
<li><p>Exchange 2013：DLP 是一项高级功能，要求使用 Exchange 企业客户端访问许可证 (CAL)。有关 CAL 和服务器授权的详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server Licensing</a>（Exchange Server 授权）。</p></li>
<li><p>如果组织使用的是 Exchange 2013 SP1 或 Exchange Online，则人们可使用策略提示从 Outlook 2013、Outlook Web App 或 适用于设备的 OWA 发送邮件。但是，如果组织目前使用的是 Exchange 2013，则人们仅可以使用策略提示从 Outlook 2013 发送电子邮件。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 策略提示的默认文本和规则选项

在向 DLP 策略添加发件人通知规则时，可以选择各种各样的选项。在 DLP 策略中添加规则指定通过“使用策略提示通知发件人”操作通知发件人时，可以选择限制程度。下表列出了可用的通知选项。有关编辑策略的常规信息，请参阅[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)。有关创建策略提示的具体信息，请参阅[管理策略提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>通知规则</th>
<th>含义</th>
<th>Outlook 用户将会看到的默认策略提示通知消息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>仅通知</strong></p></td>
<td><p>类似于邮件提示，这将导致出现有关策略违反的信息性策略提示通知消息。发件人可以使用“策略提示”选项对话框（可以在 Outlook 中进行访问）来阻止显示此类型的提示。</p></td>
<td><p>此邮件可能包含敏感内容。必须对所有收件人进行授权才能接收此内容。</p></td>
</tr>
<tr class="even">
<td><p><strong>拒绝邮件</strong></p></td>
<td><p>在条件不再存在之前，不会传递邮件。发件人要通过选项指明其电子邮件不包含敏感内容。这也称为误报替代。如果发件人指示为这种情况，则 Outlook 会允许邮件离开发件箱，以便可以审核用户报告，但是 Exchange 会阻止发送邮件。</p></td>
<td><p>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p></td>
</tr>
<tr class="odd">
<td><p><strong>除非为误报替代，否则拒绝</strong></p></td>
<td><p>此通知规则的结果类似于“拒绝邮件”通知规则。但是，如果选择此选项，则 Exchange 会允许将邮件发送给目标收件人，而不是阻止邮件。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>在发送邮件时会将反馈提交给管理员。</p></td>
</tr>
<tr class="even">
<td><p><strong>除非为无提示替代，否则拒绝</strong></p></td>
<td><p>在条件不再存在或发件人指示为替代之前，不会传递邮件。会向发件人提供一个选项，用于指示他们希望替代此策略。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>针对邮件中的敏感内容替代了组织策略。组织会审核您的操作。</p></td>
</tr>
<tr class="odd">
<td><p><strong>除非为显式替代，否则拒绝</strong></p></td>
<td><p>此通知规则的结果类似于“除非为无提示替代，否则拒绝”通知规则，只不过当发件人尝试替代此策略时，需要提供替代策略的理由。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>针对邮件中的敏感内容替代了组织策略。组织会审核您的操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>仅通知</strong></p></td>
<td><p>类似于邮件提示，这将导致出现有关策略违反的信息性策略提示通知消息。发件人可以使用“策略提示”选项对话框（可以在 Outlook 中进行访问）来阻止显示此类型的提示。</p></td>
<td><p>此邮件可能包含敏感内容。必须对所有收件人进行授权才能接收此内容。</p></td>
</tr>
<tr class="odd">
<td><p><strong>拒绝邮件</strong></p></td>
<td><p>在条件不再存在之前，不会传递邮件。发件人要通过选项指明其电子邮件不包含敏感内容。这也称为误报替代。如果发件人指示为这种情况，则 Outlook 会允许邮件离开发件箱，以便可以审核用户报告，但是 Exchange 会阻止发送邮件。</p></td>
<td><p>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p></td>
</tr>
<tr class="even">
<td><p><strong>除非为误报替代，否则拒绝</strong></p></td>
<td><p>此通知规则的结果类似于“拒绝邮件”通知规则。但是，如果选择此选项，则 Exchange 会允许将邮件发送给目标收件人，而不是阻止邮件。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>在发送邮件时会将反馈提交给管理员。</p></td>
</tr>
<tr class="odd">
<td><p><strong>除非为无提示替代，否则拒绝</strong></p></td>
<td><p>在条件不再存在或发件人指示为替代之前，不会传递邮件。会向发件人提供一个选项，用于指示他们希望替代此策略。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>针对邮件中的敏感内容替代了组织策略。组织会审核您的操作。</p></td>
</tr>
<tr class="even">
<td><p><strong>除非为显式替代，否则拒绝</strong></p></td>
<td><p>此通知规则的结果类似于“除非为无提示替代，否则拒绝”通知规则，只不过当发件人尝试替代此策略时，需要提供替代策略的理由。</p></td>
<td><p><strong>在发件人选择选项进行替代之前：</strong>此邮件可能包含敏感内容。在删除该内容之前，组织不允许发送此邮件。</p>
<p><strong>在发件人选择选项进行替代之后：</strong>针对邮件中的敏感内容替代了组织策略。组织会审核您的操作。</p></td>
</tr>
</tbody>
</table>


## 自定义“策略提示”通知邮件

要自定义发件人在其电子邮件程序中看到的“策略提示”通知的文本，请选择“数据丢失防护”页面上的“管理策略提示”。为显示任何自定义文本，DLP 策略规则必须包括“使用策略提示通知发件人”操作。请使用 DLP 规则编辑器向规则中添加这项操作。

有关说明如何创建自己的策略提示的步骤，请参阅[管理策略提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)。您创建的自定义文本可以替换以前表格中显示的默认文本。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>策略提示通知操作和设置</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>通知发件人</strong></p></td>
<td><p>仅当启动了“通知发件人，但是允许他们发送”操作时才会出现您的文本。</p></td>
</tr>
<tr class="even">
<td><p><strong>允许发件人进行覆盖</strong></p></td>
<td><p>仅在启动了以下操作时，才会出现您的文本：“除非邮件为错误判断否则进行拦截”，“拦截邮件，但是允许发件人进行覆盖和发送”。</p></td>
</tr>
<tr class="odd">
<td><p><strong>阻止邮件</strong></p></td>
<td><p>仅在启动了“拦截邮件”操作时，才会出现您的文本。</p></td>
</tr>
<tr class="even">
<td><p><strong>指向遵从性 URL 的链接</strong></p></td>
<td><p>合规性 URL 是指向您可以在其中阐释您的合规性和覆盖策略的网页的链接。当用户单击“更多详细信息”链接时，策略提示中会显示此链接。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通知发件人</strong></p></td>
<td><p>仅当启动了“通知发件人，但是允许他们发送”操作时才会出现您的文本。</p></td>
</tr>
<tr class="even">
<td><p><strong>允许发件人进行覆盖</strong></p></td>
<td><p>仅在启动了以下操作时，才会出现您的文本：“除非邮件为错误判断否则进行拦截”，“拦截邮件，但是允许发件人进行覆盖和发送”。</p></td>
</tr>
<tr class="odd">
<td><p><strong>阻止邮件</strong></p></td>
<td><p>仅在启动了“拦截邮件”操作时，才会出现您的文本。</p></td>
</tr>
<tr class="even">
<td><p><strong>指向遵从性 URL 的链接</strong></p></td>
<td><p>合规性 URL 是指向您可以在其中阐释您的合规性和覆盖策略的网页的链接。当用户单击“更多详细信息”链接时，策略提示中会显示此链接。</p></td>
</tr>
</tbody>
</table>


## 详细信息

[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

[管理 DLP 策略](manage-dlp-policies-exchange-2013-help.md)

[管理策略提示](how-to-configure-and-manage-policy-tips-a-dlp-feature-exchange.md)

