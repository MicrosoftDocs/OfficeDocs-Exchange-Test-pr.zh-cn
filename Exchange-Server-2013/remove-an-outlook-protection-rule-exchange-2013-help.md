---
title: '删除 Outlook 保护规则: Exchange 2013 Help'
TOCTitle: 删除 Outlook 保护规则
ms:assetid: 569fc3be-b269-43f5-8797-73ab0691e685
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633467(v=EXCHG.150)
ms:contentKeyID: 50490617
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 Outlook 保护规则

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

使用 Microsoft Outlook保护规则，您可以通过发送邮件前请先应用在Outlook 2010中的[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)模板保护邮件信息权限管理 (IRM)。若要防止应用Outlook保护规则，您可以禁用该规则。从Active DirectoryOutlook保护规则中删除删除规则定义。

关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间︰ 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - 您无法使用 Exchange 管理中心 (EAC) 删除Outlook保护规则。您必须使用外壳程序。

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


## 您想执行什么操作？

## 使用命令行管理程序删除 Outlook 保护规则

此示例删除 Outlook 保护规则 OPR-DG-Finance。

    Remove-OutlookProtectionRule -Identity "OPR-DG-Finance"

有关语法和参数的详细信息，请参阅 [Remove-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd297961\(v=exchg.150\))。

## 使用命令行管理程序删除所有 Outlook 保护规则

此示例删除 Exchange 组织中的所有 Outlook 保护规则。

    Get-OutlookProtectionRule | Remove-OutlookProtectionRule

有关语法和参数的详细信息，请参阅 [Get-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd298004\(v=exchg.150\)) 和 [Remove-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd297961\(v=exchg.150\))。

## 您如何知道这有效？

要验证您已成功删除 Outlook 的保护规则，请使用[Get-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd298004\(v=exchg.150\)) cmdlet 检索 Outlook 保护规则。如何检索 Outlook 保护规则的示例，请参阅**Get-OutlookProtectionRule**中的[示例](https://technet.microsoft.com/zh-cn/dd298004\(exchg.150\)#examples)。

