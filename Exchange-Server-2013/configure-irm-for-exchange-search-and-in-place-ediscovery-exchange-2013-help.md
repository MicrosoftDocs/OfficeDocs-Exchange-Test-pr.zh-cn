---
title: '为 Exchange 搜索和就地 eDiscovery 配置 IRM: Exchange 2013 Help'
TOCTitle: 为 Exchange 搜索和就地 eDiscovery 配置 IRM
ms:assetid: d96790e9-93ad-4a56-b90f-2dbfa2f2073c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg588319(v=EXCHG.150)
ms:contentKeyID: 50491761
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为 Exchange 搜索和就地 eDiscovery 配置 IRM

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-16_

在 Microsoft Exchange Server 2013，您可以配置信息权限管理 (IRM)，以便Exchange搜索可以索引受 IRM 保护的邮件。

当发现管理角色组的成员执行一个[就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)搜索时，搜索结果中返回并复制到指定的搜索发现邮箱受 IRM 保护的消息。此外，发现管理角色组的成员可以使用Outlook Web App来访问已复制到发现邮箱发现搜索的结果受 IRM 保护的邮件。

> [!NOTE]  
> 搜索管理角色组的成员无法访问到另一个邮箱或.pst 文件从发现邮箱导出受 IRM 保护的邮件。只能通过使用Outlook Web App，可以访问受 IRM 保护发现邮箱中的邮件。


关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间 ︰ 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - Exchange 2013组织中必须配置 IRM。若要了解详细信息，请参阅[对内部邮件启用或禁用 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 联合身份验证邮箱必须添加到Active Directory权限管理服务 (AD RMS) 超级用户组。若要了解详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 不能使用 Exchange 管理中心 (EAC) 为Exchange搜索和就地 eDiscovery 配置 IRM。您必须使用外壳程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 Shell 配置 IRM Exchange 搜索

本示例配置 IRM 允许Exchange搜索索引受 IRM 保护的邮件。

> [!NOTE]  
> 默认情况下，将<em>SearchEnabled</em>参数设置为<code>$true</code>。若要禁用索引的受 IRM 保护的邮件，请将其设置为<code>$false</code>。禁用索引的受 IRM 保护的邮件，会使他们当用户搜索他们的邮箱时，或当发现经理使用就地 eDiscovery 搜索结果中返回。


    Set-IRMConfiguration -SearchEnabled $true

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 使用外壳配置 IRM 就地 eDiscovery

本示例允许访问受 IRM 保护的邮件驻留在发现邮箱发现管理角色组的成员。

> [!NOTE]  
> 默认情况下，将<em>EDiscoverySuperUserEnabled</em>参数设置为<code>$true</code>。若要禁用访问受 IRM 保护的电子邮件，发现管理角色组的成员，请将其设置为<code>$false</code>。


    Set-IRMConfiguration -EDiscoverySuperUserEnabled $true

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 您如何知道这有效？

要验证已成功地配置 IRM Exchange 搜索和就地 eDiscovery，使用**Get-IRMConfigurtaion** cmdlet 检索 IRM 配置信息。有关如何获取 IRM 配置的示例，请参阅**Get-IRMConfiguration**中的[示例](https://technet.microsoft.com/zh-cn/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

