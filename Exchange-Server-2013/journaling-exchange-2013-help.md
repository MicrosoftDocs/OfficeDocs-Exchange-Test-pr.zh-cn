---
title: '日记: Exchange 2013 Help'
TOCTitle: 日记
ms:assetid: 6a20f207-4485-44ef-b010-ec760eb5165b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998649(v=EXCHG.150)
ms:contentKeyID: 50490876
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 日记

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

通过记录入站和出站电子邮件通信，日记功能可以帮助组织对法律、法规和组织遵从性要求做出响应。规划邮件保留和遵从性时，了解日记功能及其如何适应组织的遵从性策略，以及 Microsoft Exchange Server 2013 如何帮助保护日记邮件的安全，这一点非常重要。

**目录**

Why journaling is important

Journaling agent

Journal rules

Journal rule replication

Journal reports

Interoperability with Exchange 2010 and Exchange 2007

Troubleshooting

## 日记功能为什么很重要

首先，请务必注意区分日记功能和数据存档策略：

  - *日记*可以记录组织中的所有通信（包括电子邮件通信），以便在组织的电子邮件保留或存档策略中使用。为了满足日益增长的法规和遵从性要求，许多组织都必须保留雇员执行日常的公司任务时发生的通信记录。

  - *数据存档*是指通过备份数据，将数据从本机环境中删除，然后将数据存储在其他位置，从而缓解数据存储空间紧张的情况。可以将 Exchange 日记功能用作电子邮件保留或存档策略中的一种工具。

虽然日记可能并非某个特定法规所要求的，但是遵从性可以通过按特定法规进行记录而得到实现。例如，某些金融企业的公司主管可能要负责处理员工对客户做出的理赔。为了检查理赔是否准确无误，公司官员可能会建立一套系统，让管理人员定期查看雇员与客户的部分通信。管理人员会在每个季度检查遵守法规的情况并审查雇员的行为。在全部管理人员的报告提交公司官员批准之后，公司官员便会代表公司向法律机关报告公司遵守法规的情况。在此示例中，电子邮件可能是管理人员必须查看的雇员与客户之间通信类型中的一种；因此，可以使用日记来收集直接面向客户的雇员所发送的所有电子邮件。其他客户通信机制可能包括传真和电话会议，这些内容也必须进行管理。记录企业中各类数据的功能是 IT 体系结构的一项很有价值的功能。

下表列出了一些比较著名的美国和国际法规，这些法规中日记功能可能会帮助构建部分遵从性策略：

  - 2002 年萨班尼斯-奥克斯莱法案 (Sarbanes-Oxley Act of 2002, SOX)

  - 证券交易委员会法规 17a-4 (Security Exchange Commission Rule 17a-4, SEC Rule 17 A-4)

  - 全国证券交易商协会 3010 & 3110 (National Association of Securities Dealers 3010 & 3110, NASD 3010 & 3110)

  - 格雷姆-里奇-比利雷法案（金融现代化法案） (Gramm-Leach-Bliley Act \[Financial Modernization Act\])

  - 2001 年金融机构隐私权保护法案 (Financial Institution Privacy Protection Act of 2001)

  - 2003 年金融机构隐私权保护法案 (Financial Institution Privacy Protection Act of 2003)

  - 1996 年的健康保险便利和义务法案 (HIPAA)

  - 2001 年的提供打击与防止恐怖主义所需的适当工具以团结并强化美国法案（爱国法案）

  - 欧盟数据保护指导 (European Union Data Protection Directive, EUDPD)

  - 日本的个人信息保护法案 (Japan's Personal Information Protection Act)

返回顶部

## 日记代理

在 Exchange 2013 组织中，所有电子邮件流量都由邮箱服务器进行路由。所有邮件在其生存期内都将至少遍历一个运行传输服务的服务器。*日记代理*是着重处理合规性的传输代理，用于处理邮箱服务器上的邮件。它可以触发 **OnSubmittedMessage** 和 **OnRoutedMessage** 传输事件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，日记代理是内置代理。内置代理不包含在 <strong>Get-TransportAgent</strong> cmdlet 所返回的代理列表中。有关更多详细信息，请参阅<a href="transport-agents-exchange-2013-help.md">传输代理</a>。</td>
</tr>
</tbody>
</table>


Exchange 2013 提供了下列日记选项：

  - **标准日记**   标准日记是在邮箱数据库上配置的。通过使用标准日记，日记代理能够记录特定邮箱数据库中的邮箱所接收和发送的所有邮件。如果要记录所有收件人和发件人接收和发送的所有邮件，则必须为组织中所有邮箱服务器上的所有邮箱数据库配置日记功能。

  - **高级日记**   通过高级日记，日记代理能够使用日记规则执行更详细的日记记录。可以通过记录单个收件人或通讯组成员来配置日记规则，以满足组织的需要，而不是记录邮箱数据库上驻留的所有邮箱。您必须拥有 Exchange Enterprise 客户端访问许可证 (CAL) 才能使用高级日记。

在邮箱数据库上启用标准日记时，此信息将保存在 Active Directory 中并由日记代理读取。同样，使用高级日记功能配置的日记规则也保存在 Active Directory 中并由日记代理应用。有关如何配置标准日记和高级日记的详细信息，请参阅[管理日记](manage-journaling-exchange-2013-help.md)。

返回顶部

## 日记规则

以下是日记规则的主要方面：

  - **日记规则作用域**   定义了由日记代理进行记录的邮件。

  - **日记收件人**   指定了要记录的收件人的 SMTP 地址。

  - **日记邮箱**   指定了用于收集日记报告的一个或多个邮箱。

## 日记规则作用域

可以使用日记规则仅记录内部邮件、仅记录外部邮件或同时记录这两者。以下列表介绍了这些作用域：

  - **仅内部邮件**   作用域设置为记录在 Exchange 组织内的收件人之间发送的内部邮件的日记规则。

  - **仅外部邮件**   作用域设置为记录在 Exchange 组织外部发送给收件人的外部邮件和接收自发件人的外部邮件的日记规则。

  - **所有邮件**   作用域设置为记录通过组织的所有邮件（无论来源或目标是哪里）的日记规则。这些邮件包括可能已由内部作用域和外部作用域中的日记规则进行了处理的邮件。

## 日记收件人

可以通过指定要记录的收件人的 SMTP 地址来实施目标日记规则。这些收件人可以是 Exchange 邮箱、通讯组、邮件用户或联系人。这些收件人可能需要遵守法规要求，也可能参与到将电子邮件或其他通信内容作为证据进行收集的法律程序中。通过确定特定的收件人或收件人组，您可以轻松地配置符合组织的过程并满足法规和法律要求的日记环境。仅确定需要记录的特定收件人还可最大程度减少与大量数据保留关联的存储和其他成本。

在日记规则中指定的日记收件人接收或发送的所有邮件都将得到记录。如果指定通讯组作为日记收件人，则会记录通讯组成员接收或发送的所有邮件。如果不指定日记收件人，则将记录与日记规则作用域相匹配的收件人接收或发送的所有邮件。

**已启用统一消息的日记收件人**

许多实现日记功能的组织可能还会使用统一消息 (UM) 来合并其电子邮件、语音邮件和传真基础结构。但是，您可能不希望日记进程为由统一消息生成的邮件生成日记报告。在这些情况下，可以决定是记录由运行统一消息服务的 Exchange 服务器处理的语音邮件和未接来电通知邮件，还是跳过此类邮件。如果您的组织不需要记录此类邮件，可以通过跳过此类邮件来减少存储日记报告所需的硬盘存储空间量。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将始终记录包含由统一消息服务生成的传真的邮件，即使您禁用统一消息语音邮件和未接来电通知邮件的日记功能也是如此。</td>
</tr>
</tbody>
</table>


有关如何启用或禁用语音邮件和未接来电通知邮件的详细信息，请参阅[禁用或启用语音邮件和未接来电通知的日记功能](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)。

## 日记邮箱

日记邮箱用于收集日记报告。如何配置日记邮箱取决于组织策略以及法规和法律要求。可以针对组织中配置的所有日记规则指定一个用于收集邮件的日记邮箱，或者可以针对不同的日记规则或日记规则集使用不同的日记邮箱。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能将 Office 365 邮箱指定为日记邮箱。不能将日记报告传递给内部部署存档系统或第三方存档服务。如果运行将邮箱在内部部署服务器与 Office 365 之间进行拆分的混合部署，则可以将内部部署邮箱指定为 Office 365 和内部部署邮箱的日记邮箱。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>日记邮箱包含非常敏感的信息。必须确保日记邮箱的安全，因为它们会收集发送到组织中的收件人或从组织中的发件人发出的邮件。这些邮件可能属于法律程序的一部分，或者可能需要遵守法规要求。多项法律均规定在将邮件提交给调查机构之前不能对其进行篡改。建议您制定相应的策略来确定何人有权访问组织中的日记邮箱，仅允许有直接需要的人员对邮箱进行访问。请与您的法律代理人联系，以确保日记解决方案符合适用于您所在组织的所有法律和法规的要求。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>日记邮箱应接受最大大小等于或大于你在组织中设置的最大邮件大小的邮件。如果已在个别用户的邮箱中配置大于 TransportConfig 中的常规设置的 MaxSendSize 和 MaxReceiveSize 例外，应相应地设置日记邮箱的 MaxSendSize 和 MaxReceiveSize，确保发送到日记邮箱的邮件被接受，而不是排队等候或被拒绝。日记邮箱拒绝的邮件将定期重试，从而导致不必要的数据库增长和资源浪费。此外，建议你设置备用日记邮箱，防止发生其他无法送达的情况。</td>
</tr>
</tbody>
</table>


## 备用日记邮箱

日记邮箱不可用时，可能不希望在邮箱服务器上的邮件队列中收集无法送达的日记报告。您可以改为配置备用日记邮箱，来存储这些日记报告。备用日记邮箱可接收未送达报告 (NDR) 中作为附件的日记报告；当日记邮箱或其所在服务器拒绝传递日记报告或不可用时，就会生成未送达报告。

当日记邮箱重新变为可用时，您可以使用 OfficeOutlook 的\&quot;重新发送\&quot;功能，来提交日记报告以便传递到日记邮箱。

配置备用日记邮箱后，整个 Exchange 组织中被拒绝或无法传递的所有日记报告都将传递到备用日记邮箱。因此，请务必确保备用日记邮箱及其所在邮箱服务器可以支持很多日记报告。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果配置了备用日记邮箱，必须监视此邮箱以确保它不会与日记邮箱同时处于不可用状态。如果备用日记邮箱也不可用或同时拒绝日记报告，则被拒绝的日记报告会丢失并且无法检索。</td>
</tr>
</tbody>
</table>


因为备用日记邮箱收集整个 Exchange 组织的所有被拒绝日记报告，所以，必须确保这不违反任何适用于组织的法律或法规。如果法律或法规禁止组织将日记报告发送到不同的日记邮箱或存储在同一个备用日记邮箱中，则可能无法配置备用日记邮箱。请与您的法定代表人联系，以确定是否可以使用备用日记邮箱。

配置备用日记邮箱时，使用的标准与配置日记邮箱时使用的标准相同。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>应将备用日记邮箱当做特殊的专用邮箱。任何直接发送到备用日记邮箱的邮件都不会记入日记。</td>
</tr>
</tbody>
</table>


返回顶部

## 日记规则复制

日记规则存储在 Active Directory 中，并由 Exchange 2013 组织中的所有邮箱服务器进行应用。创建、修改或删除日记规则时，此更改会复制到组织中的所有 Active Directory 服务器上。随后，组织中所有的邮箱服务器将从 Active Directory 服务器中检索更新的日记规则配置，并应用新的或修改过的日记规则。

通过在整个组织中复制所有日记规则，Exchange 2013 可以为整个组织提供一致的日记规则组。所有通过 Exchange 2013 组织传递的邮件都遵守相同的日记规则。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>整个组织的日记规则的复制是取决于Active Directory复制。Active Directory域控制器之间的复制时间各不相同，具体取决于组织中的站点的数量和速度的链接和Microsoft Exchange的控制之外的其他因素。当您在您的组织中实现日记规则时，请考虑复制延迟。有关Active Directory复制的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=274904">活动目录复制和拓扑管理使用 Windows PowerShell 简介</a>。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>每个邮箱服务器都会缓存通讯组成员身份，以避免重复往返 Active Directory。扩展组缓存可以减少每个邮箱服务器必须向 Active Directory 域控制器发出的请求数。默认情况下，展开组缓存中的条目将在四个小时后过期。因此，如果指定通讯组作为日记收件人，则对通讯组成员身份的更改在展开组缓存更新之前，可能不会应用于日记规则。若要强制立即更新收件人缓存，必须停止后再启动 Microsoft Exchange 传输服务。必须对希望强制更新其收件人缓存的每个邮箱服务器执行此操作。</td>
</tr>
</tbody>
</table>


返回顶部

## 日记报告

*日记报告*是指当某封邮件符合日记规则并要被提交到日记邮箱时，由日记代理生成的邮件。符合日记规则的原始邮件将按原样作为日记报告的附件包含在其中。日记报告的正文包含原始邮件的信息，例如发件人电子邮件地址、邮件主题、邮件 ID 以及收件人电子邮件地址。这也称为信封日记，是 Exchange 2013 支持的唯一日记方法。

## 日记报告和受 IRM 保护的邮件

在 Exchange 2013 环境中实施日记功能时，必须考虑日记报告和受 IRM 保护的邮件。受 IRM 保护的邮件将影响未内置 RMS 支持的第三方存档系统的搜索和发现功能。在 Exchange 2013 中，可以配置日记报告解密，以便在日记报告中保存邮件的明文副本。

返回顶部

## 与 Exchange 2007 的互操作性

Exchange 2013、Exchange 2010 与 Exchange 2007 中的日记功能之间几乎没什么差异。但是，Exchange 2010 及更高版本安装程序会在 Active Directory 中创建单独的容器来存储日记规则。在 Exchange 2007 组织中安装第一个 Exchange 2010 或更高版本服务器时，安装程序会在 Exchange 2007 中创建现有日记规则的副本并将其存储在新的容器中。安装程序完成后，Exchange 两个版本的日记规则将一致。

安装程序完成后，如果更改了 Exchange 2010 或更高版本上的日记规则配置，则必须在 Exchange 2007 服务器上进行相同更改，以确保它们一致。同样，对 Exchange 2007 上日记规则的更改也必须应用到 Exchange 2010 或更高版本中。也可以从 Exchange 2007 中导出日记规则并将其导入到 Exchange 2013 中。

返回顶部

## 故障排除

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。。如果您在使用 **JournalingReportDNRTo** 邮箱时遇到困难，请参阅 [Exchange Online 中的传输和邮箱规则不按预期运行](https://go.microsoft.com/fwlink/p/?linkid=331674)。

