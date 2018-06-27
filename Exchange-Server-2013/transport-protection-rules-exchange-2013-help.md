---
title: '传输保护规则: Exchange 2013 Help'
TOCTitle: 传输保护规则
ms:assetid: 9bd6d049-165e-4e51-a79f-3b8ff409da55
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298166(v=EXCHG.150)
ms:contentKeyID: 50491142
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 传输保护规则

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

越来越多的电子邮件和附件包含业务关键信息（例如产品规范、商务策略文档和财务数据）或个人可识别信息 (PII)（例如联系人详细信息、社会保险号、信用卡号和员工记录）。世界上很多地方都有许多特定于行业的法规和当地法规来控制对 PII 的收集、存放和公开。

为了帮助保护敏感信息，组织创建了可提供有关此类信息处理方法的准则的邮件策略。在 MicrosoftExchange Server 2013 中，可以使用传输保护规则来实现这些邮件策略，具体做法是检查邮件内容、加密敏感电子邮件内容以及使用权限管理来控制对内容的访问。

有关管理 IRM 的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 传输保护规则和 AD RMS

传输保护规则允许对 IRM 保护的邮件使用传输规则，具体做法是应用 [Active Directory 权限管理服务](https://go.microsoft.com/fwlink/p/?linkid=129823) (AD RMS) 权限策略模板。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>AD RMS 是一种信息保护技术，适用于启用了权限管理服务 (RMS) 的应用程序和客户端，以便以联机和脱机方式保护敏感信息。若要在内部部署的 Exchange 部署中使用 IRM 保护，Exchange 2013 要求在 Windows Server 2008 或更高版本上运行内部部署 AD RMS 部署。</td>
</tr>
</tbody>
</table>


AD RMS 使用基于 XML 的策略模板，从而使启用 IRM 的兼容应用程序可以应用一致的保护策略。在 Windows Server 2008 及更高版本中，AD RMS 服务器提供了可用于枚举和获取模板的 Web 服务。Exchange 2013 附带有“不要转发”模板。

将“不要转发”模板应用于邮件时，只有邮件的收件人可解密该邮件。收件人无法将邮件转发给其他任何人、复制邮件内容，或打印邮件。

可以在内部 AD RMS 部署中创建其他 RMS 模板，以满足组织中的权限保护要求。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果从 AD RMS 服务器中删除了权限策略模板，则必须修改任何使用已删除模板的传输保护规则。如果传输保护规则继续使用已删除的权限策略模板，则 AD RMS 服务器将无法对任何收件人认证内容，且会向发件人发送未送达报告 (NDR)。<br />
在 Windows Server 2008 和更高版本中，可以存档而不是删除权限策略模板。存档模板仍可以用于认证内容，但是创建或修改传输保护规则时，存档模板不会包含在模板列表中。</td>
</tr>
</tbody>
</table>


有关创建 AD RMS 模板的详细信息，请参阅 [AD RMS 权限策略模板部署分步指南](https://go.microsoft.com/fwlink/p/?linkid=136593)。

## 使用传输保护规则进行自动保护

通过使用传输规则条件的组合（包括标识诸如社会保险号之类的文本模式的正则表达式），可以标识包含业务关键信息或 PII 的邮件。组织要求对于敏感信息进行不同级别的保护。某些信息可能限于员工、承包商或合作伙伴使用，而另外一些信息可能仅限于全职员工使用。通过应用适当的权限策略模板，可将所需保护级别应用于邮件。例如，用户可以将邮件或电子邮件附件标记为“公司机密”。如下图所示，可以创建检查邮件内容是否包含“公司机密”一词并自动使用 IRM 保护邮件的传输保护规则。

有关创建传输规则以强制执行权限保护的详细信息，请参阅[创建传输保护规则](create-a-transport-protection-rule-exchange-2013-help.md)。

## 持续保护电子邮件附件

用户使用常见的 Microsoft Office 文件格式（例如 Microsoft OfficeWord、Excel 和 PowerPoint）以电子邮件附件形式发送业务关键信息和 PII。所有这些文件格式都通过 IRM 支持持久保护，并且可以确保这些文档中的业务关键信息和 PII 都已得到妥善保护。传输保护规则会对受支持文件格式的电子邮件和附件应用相同的保护。

## 传输规则代理和加密代理

使用传输保护规则根据规则条件对邮件进行 IRM 保护时，传输服务上的传输规则代理将对邮件进行检查。如果它们满足所有条件且无一例外，则会将邮件标记为受 IRM 保护。加密代理是触发 **OnRoutedMessage** 事件的内置传输代理，它实际上将 IRM 保护应用于邮件。仅当为内部邮件启用了 IRM 时，加密代理才对这些邮件进行操作。有关启用 IRM 的详细信息，请参阅[对内部邮件启用或禁用 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

重新启动传输服务后，它将处理需要 IRM 加密的第一封邮件，加密代理必须能够访问组织中的 AD RMS 服务器。对于后续邮件，代理无需与 AD RMS 服务器联系。由于暂时情况而导致加密邮件失败时，Exchange 将每隔 10 分钟重新尝试加密邮件 3 次。重试 3 次后，如果仍无法加密邮件，则不会将该邮件传递给收件人。此时，将向发件人发送 NDR。建议规划 AD RMS 部署以实现高可用性，从而确保邮件流不受影响。

计划使用传输保护规则时，必须相应地考虑要保护的信息的类型和有关创建规则的计划。在 Exchange 2013 中，传输规则包含大量谓词，可通过这些谓词检查邮件内容，包括受支持的附件、邮件头、发件人和收件人地址及其 Active Directory 属性（例如部门、通讯组成员以及发件人与收件人的管理关系）。有关 Exchange 2013 中可用传输规则谓词的详细信息，请参阅 [传输规则条件（谓词）](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)。

还必须考虑组织中的邮件通信以及将使用传输保护规则保护的邮件数。在邮箱服务器上将 IRM 保护应用于大量邮件需要更多资源。此外，保护大量邮件或所有邮件还会影响客户端体验，对于 Microsoft Outlook 用户尤其如此。

