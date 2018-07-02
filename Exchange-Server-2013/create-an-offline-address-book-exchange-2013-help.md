---
title: '创建脱机通讯簿: Exchange 2013 Help'
TOCTitle: 创建脱机通讯簿
ms:assetid: b57bb4ce-5b6e-4702-a2f8-04bf3898a861
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124339(v=EXCHG.150)
ms:contentKeyID: 50491387
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.Mailbox.NewOabWizardForm.OabIntroductionWizardPage
ms.translationtype: HT
---

# 创建脱机通讯簿

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-04-24_

Exchange Server 2013 中的脱机通讯簿 (OAB) 是已下载通讯簿副本，通过此通讯簿，Outlook 用户可以在与服务器断开连接的情况下访问信息。Exchange 管理员可以决定脱机工作的用户能够使用哪些通讯簿，还可以配置通讯簿的分发方法（基于 Web 分发或公用文件夹分发）。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“脱机通讯簿”条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的“向角色组添加角色”部分。

  - 不能使用 Exchange 管理中心 (EAC) 执行此过程。必须使用命令行管理程序。

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


## 使用命令行管理程序创建基于 Web 分发的 OAB

本示例通过使用默认虚拟目录为 Outlook 2007 或更高版本的客户端创建使用基于 Web 分发的名为 OAB\_Contoso 的 OAB。

    New-OfflineAddressBook -Name "OAB_Contoso" -AddressLists "\Default Global Address List" -VirtualDirectories $Null -GlobalWebDistributionEnabled $True

有关语法和参数的详细信息，请参阅[New-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/bb123692\(v=exchg.150\))。

