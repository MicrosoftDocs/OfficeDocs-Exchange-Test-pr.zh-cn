---
title: 'Outlook 保护规则: Exchange 2013 Help'
TOCTitle: Outlook 保护规则
ms:assetid: bd7d0ad7-1f8e-46da-a74b-58c58f3eff93
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638178(v=EXCHG.150)
ms:contentKeyID: 50491536
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 保护规则

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

每天，信息人员都通过电子邮件传递敏感信息，包括财务报表和数据、客户和员工信息、机密的产品信息和规格信息等。在 Microsoft Exchange Server 2013、Microsoft Outlook 和 Microsoft OfficeOutlook Web App 中，用户可以通过应用 Active Directory 权限管理服务 (AD RMS) 权限策略模板将信息权限管理 (IRM) 保护应用于邮件。这要求在组织中部署 AD RMS。有关 AD RMS 的详细信息，请参阅 [Active Directory 权限管理服务](https://go.microsoft.com/fwlink/p/?linkid=129823)。

但是，当由用户做出决定时，邮件可能会在没有 IRM 保护的情况下以明文形式发送。在使用电子邮件作为托管服务的组织中，存在信息泄漏的风险，因为邮件离开客户端后将经过路由并存储在组织边界以外。尽管电子邮件托管公司可能会有定义明确的手续和检查来帮助降低信息泄漏的风险，但在邮件离开组织的边界后，组织就会失去对信息的控制。Outlook 保护规则可以帮助防止这种类型的信息泄漏。

有关管理 IRM 的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## Outlook 中的自动 IRM 保护

在 Exchange 2013 中，Outlook 保护规则通过自动将 IRM 保护应用于 Exchange 2013 中的邮件来帮助你的组织防止出现信息泄漏的风险。邮件在离开 Outlook 客户端之前受 IRM 保护。这种保护也适用于任何使用受支持的文件格式的附件。

在 Outlook 服务器上创建 Exchange 2013 保护规则时，会使用 Exchange Web 服务将这些规则自动分发到 Outlook 2010。要对 Outlook 2010 应用规则，指定的 AD RMS 权限策略模板必须能够在用户的计算机上可用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果将权限策略模板从 AD RMS 服务器中删除，必须修改使用该删除模板的任何 Outlook 保护规则。如果 Outlook 保护规则继续使用已删除的权限策略模板，并在组织中启用传输解密，则解密代理将无法解密使用不再可用的模板保护的邮件。如果将传输解密配置为必要操作，那么传输服务将拒绝邮件并向发件人发送未送达报告 (NDR)。有关传输解密的详细信息，请参阅<a href="transport-decryption-exchange-2013-help.md">传输解密</a>。有关 AD RMS 权限策略模板的更多详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=179455">AD RMS 策略模板注意事项</a>。<br />
在 Windows Server 2008 和更高版本中，可以存档而不是删除权限策略模板。存档的模板仍然可以用于许可证内容，但是如果创建或修改 Outlook 保护规则，存档的模板则不会包含在模板列表中。</td>
</tr>
</tbody>
</table>


Outlook 保护规则类似于传输保护规则。两者均根据邮件条件进行应用，并且两者都通过应用 AD RMS 权限保护模板来保护邮件。但是，传输保护规则由传输规则代理应用到邮箱服务器上的传输服务。Outlook 保护规则在邮件从用户的计算机中发出之前应用到 Outlook 2010。由 Outlook 保护规则保护的邮件会在应用了 IRM 保护的情况下进入传输管道。此外，由 Outlook 保护规则保护的邮件也会以加密格式保存在发件人邮箱的“已发送邮件”文件夹中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在 Exchange 组织中启用了传输解密，则传输服务上的解密代理可以解密组织中使用 AD RMS 服务器由 Outlook 保护规则进行 IRM 保护的邮件。传输服务上安装的传输规则代理和其他传输代理可以检查邮件内容。有关传输解密的详细信息，请参阅<a href="transport-decryption-exchange-2013-help.md">传输解密</a>。</td>
</tr>
</tbody>
</table>


使用传输保护规则时，不会向用户显示邮件在传输服务上是否自动受到保护。将 Outlook 保护规则应用于 Outlook 2010 中的邮件时，用户就会知道邮件是否受到 IRM 保护。如果需要，用户还可以选择其他的权限策略模板。

## 创建 Outlook 保护规则

要创建 Outlook 保护规则，必须使用 Exchange 命令行管理程序中的 [New-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd298182\(v=exchg.150\)) cmdlet。有关详细说明，请参阅[创建 Outlook 保护规则](create-an-outlook-protection-rule-exchange-2013-help.md)。

创建规则时，可以通过删除 IRM 保护或应用该规则中指定的 AD RMS 权限策略模板以外的权限策略模板来指定用户是否覆盖它。如果用户覆盖 Outlook 保护规则应用的 IRM 保护，Outlook 2010 会将 `X-MS-Outlook-Client-Rule-Overridden` 头插入到邮件中，这样就可以确定用户已覆盖了此规则。

## Outlook 保护规则中的谓词

Outlook 保护规则允许您使用三个谓词以自动在 Outlook 2010 中应用 IRM 保护：

  - **FromDepartment**   *FromDepartment* 谓词在 Active Directory 中查找发件人的部门属性，并在发件人的部门与规则中指定的部门相匹配时自动使用 IRM 保护邮件。例如，可以创建 Outlook 保护规则以自动保护“研究”部门发送的所有邮件。

  - **SentTo**   组织可能需要保护发送给某些敏感收件人（例如“所有公司”或“财务”通讯组）的邮件。使用 *SentTo* 谓词，您可以创建 Outlook 保护规则，以自动使用 IRM 保护发送给指定收件人的邮件。

  - **SentToScope**   *SentToScope* 谓词允许创建 Outlook 保护规则，以自动使用 IRM 保护在组织内部或外部发送的邮件。例如，可以使用 *SentToScope* 谓词和 *FromDepartment* 谓词来使用 IRM 保护特定部门发送给内部用户的邮件。

