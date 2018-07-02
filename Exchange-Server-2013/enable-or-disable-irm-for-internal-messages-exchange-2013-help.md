---
title: '对内部邮件启用或禁用 IRM: Exchange 2013 Help'
TOCTitle: 对内部邮件启用或禁用 IRM
ms:assetid: a6a17f57-5304-41f1-954d-7301857d54a1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124077(v=EXCHG.150)
ms:contentKeyID: 50491259
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 对内部邮件启用或禁用 IRM

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-12_

在 Microsoft Exchange Server 2013，信息权限管理 (IRM) 是默认启用的内部消息。这允许您创建传输保护规则和 Microsoft Outlook保护规则，以 IRM 保护的邮件在传输过程中和 Microsoft Outlook 2010和更高版本的客户端上。有关内部消息启用 IRM 的Exchange Server 2013，如传输解密、 日记规则解密，可使用 Microsoft OfficeOutlook Web App和 IRM 中 Microsoft Exchange ActiveSync中的所有其他 IRM 功能的先决条件。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange的组织中的所有 IRM 功能中都禁用禁用 IRM 的内部消息。Outlook （例如，能够读取、 答复、 转发、 和创建受 IRM 保护的邮件，使用Active Directory权限管理服务 (AD RMS) 服务器） 中的客户端的 IRM 功能不受影响。</td>
</tr>
</tbody>
</table>


关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - 不能使用 Exchange 管理中心 (EAC) 来启用或禁用 IRM 的内部消息。您必须使用外壳程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序为内部邮件启用 IRM

本示例为 Exchange 组织启用内部邮件的 IRM。

    Set-IRMConfiguration -InternalLicensingEnabled $true

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 使用命令行管理程序为内部邮件禁用 IRM

本示例为 Exchange 组织禁用内部邮件的 IRM。

    Set-IRMConfiguration -InternalLicensingEnabled $false

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已为内部邮件启用或禁用 IRM，请使用 [Get-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd776120\(v=exchg.150\)) cmdlet 检查配置。

