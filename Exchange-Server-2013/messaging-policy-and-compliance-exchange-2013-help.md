---
title: '邮件策略和遵从性: Exchange 2013 Help'
TOCTitle: 邮件策略和遵从性
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50490731
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件策略和遵从性

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

电子邮件已成为各种规模组织中信息工作者的可靠且普遍的通信媒体。邮件存储和邮箱已成为宝贵数据的存储库。组织制定的邮件策略要求充分利用其邮件系统，为用户提供有关如何对策略进行操作以及何处需要策略的指导原则，并提供有关可能不允许的通信类型的详细信息，这十分重要。

组织还必须创建策略以管理电子邮件生命周期、在基于业务、法律和法规要求的时间长度内保留邮件、保留电子邮件记录以用于诉讼和调查目的以及准备好搜索并提供所需电子邮件记录来进行就地电子数据展示请求。

还必须防止泄露敏感信息，如知识产权、商业秘密、业务计划和组织收集或处理的个人身份信息 (PII)。

## Exchange 2013 中的邮件策略和合规性

下表提供 Microsoft Exchange Server 2013 中的邮件策略和合规性功能的概述，并包括可帮助了解和管理这些功能的主题的链接。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>描述</th>
<th>资源</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮件记录管理 (MRM)</p></td>
<td><p>为了遵守适用法规或满足法律或业务要求，组织在其邮件策略中包含电子邮件生命周期策略。这些策略应解决的常见问题包括：</p>
<ul>
<li><p>邮件应保留多长时间？</p></li>
<li><p>邮件应保留在何处？</p></li>
<li><p>所有邮件的保留期是否应相同？</p></li>
</ul>
<p>Exchange 2013 包含的 MRM 功能使您可以实现组织的电子邮件生命周期策略。可以使用 MRM 将统一保留设置应用于所有邮件、使用自定义保留策略为邮箱应用基线保留设置以及可以选择允许用户对邮件进行分类以便可以在指定持续时间内保留邮件。</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">邮件记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>就地存档</p></td>
<td><p>“就地存档”有助于您重新获得对组织的邮件数据的控制，而无需个人存储 (.pst) 文件，并且允许用户在可通过 Outlook 2010 及更高版本和 Outlook Web App 访问的“存档邮箱”中存储邮件。</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的就地存档</a></p></td>
</tr>
<tr class="odd">
<td><p>就地保留</p></td>
<td><p>当存在诉讼的合理预期时，需要组织保留与事实相关的以电子方式存储的信息 (ESI)，包括电子邮件。就地保留使您可以搜索并保留与查询参数匹配的邮件。可保护邮件不被删除、修改和篡改，并且可以无限期地保留邮件或保留一段指定时间。</p></td>
<td><p><a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留和诉讼保留</a></p></td>
</tr>
<tr class="even">
<td><p>就地电子数据展示</p></td>
<td><p>就地电子数据展示使您可以跨 Exchange 组织搜索邮箱数据、预览搜索结果并将结果复制到发现邮箱。</p></td>
<td><p><a href="in-place-ediscovery-exchange-2013-help.md">就地电子数据展示</a></p></td>
</tr>
<tr class="odd">
<td><p>日记</p></td>
<td><p>通过记录入站和出站电子邮件通信，日记功能可以帮助组织对法律、法规和组织遵从性要求做出响应。规划邮件保留和合规性时，了解日记功能及其如何适应组织的合规性策略，以及 Exchange 2013 如何帮助保护日志邮件的安全，这一点非常重要。</p></td>
<td><p><a href="journaling-exchange-2013-help.md">日记</a></p></td>
</tr>
<tr class="even">
<td><p>Transport Rules</p></td>
<td><p>使用传输规则可以查找针对通过组织传递的邮件的特定条件，然后对它们执行操作。传输规则可让您将邮件策略应用于电子邮件，以保护邮件安全，保护邮件系统安全，并防止信息泄露。</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">邮件流或传输规则</a></p></td>
</tr>
<tr class="odd">
<td><p>数据丢失预防 (DLP)</p></td>
<td><p>DLP 功能可帮助保护您的敏感数据，并向用户通知策略和法规。DLP 还可帮助防止用户错误地将敏感数据发送给未经授权的人。在配置 DLP 策略时，可以通过分析邮件系统的内容（其中包括大量关联文件类型）来标识和保护敏感数据。Exchange 2013 中提供的 DLP 策略模板基于法规标准，如 PII 和支付卡行业数据安全标准 (PCI-DSS)。DLP 可进行扩展，这样便使您可以包含对组织十分重要的其他策略。此外，新的策略提示功能还使您可以在发送敏感数据之前，通知用户有关的策略违反情况。</p></td>
<td><p><a href="technical-overview-of-dlp-data-loss-prevention-in-exchange.md">数据丢失预防</a></p></td>
</tr>
<tr class="even">
<td><p>信息权限管理 (IRM)</p></td>
<td><p>信息权限管理 (IRM) 使用 Active Directory 权限管理服务 (AD RMS) 为电子邮件和附件提供持续性联机和脱机保护。</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">信息权限管理</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>安全/多用途 Internet 邮件扩展 (S/MIME) 可帮助具有 Office 365 邮箱、Exchange 2013 和 Exchange Online 的人员通过在组织内发送已签名和加密的电子邮件来保护敏感信息。管理人员可通过在 Office 365 和本地服务器之间同步用户证书，然后将 Outlook Online 配置为支持 S/MIME，来为 Office 365 邮箱启用 S/MIME。</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">邮件签名和加密的 S/MIME</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱审核日志记录</p></td>
<td><p>由于邮箱可能包含敏感、对业务影响很大 (HBI) 的信息和 PII，因此，跟踪登录到组织内邮箱的人员及其所执行的操作非常重要。跟踪邮箱所有者之外的其他用户（称为委派用户）对邮箱的访问情况尤其重要。使用邮箱审核日志记录可以记录邮箱所有者、委派用户（包含具有完全邮箱访问权限的管理员）和管理员对邮箱的访问。</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">邮箱审核日志记录</a></p>
<p><a href="exchange-auditing-reports-exchange-2013-help.md">Exchange 审核报告</a></p></td>
</tr>
<tr class="odd">
<td><p>管理员审核日志记录</p></td>
<td><p>管理员审核日志支持您将管理员所做的日志更改保存至 Exchange 服务器中，并将对组织配置所做的更改保存至 Exchange 收件人中。您可以将管理员审核日志记录用作变更控制进程的一部分，也可以出于合规性目的使用它来跟踪配置和收件人的更改内容和访问权限。</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">管理员审核日志记录</a></p></td>
</tr>
</tbody>
</table>

