---
title: '启用或禁用客户端访问服务器上的信息权限管理: Exchange 2013 Help'
TOCTitle: 启用或禁用客户端访问服务器上的信息权限管理
ms:assetid: c7ce069b-a572-4755-90a3-7105472e4c83
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876938(v=EXCHG.150)
ms:contentKeyID: 50491508
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用客户端访问服务器上的信息权限管理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

客户端访问服务器上启用信息权限管理 (IRM) 启用下列功能︰

  - Microsoft Office Outlook Web App

  - 可使用 Microsoft Exchange ActiveSync

当客户端访问服务器上启用了 IRM 时， Outlook Web App用户将可以通过应用在 AD RMS 群集上创建一个[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)模板的 IRM 保护的邮件。Outlook Web App用户可以查看受 IRM 保护的邮件并支持附件。在启用 IRM 客户端访问服务器上之前，必须将联盟邮箱添加 AD RMS 群集上的超级用户组。

> [!important]
> 当他们从 AD RMS 群集申请许可证，超级用户组被授予了所有者的成员使用许可证。这允许他们解密该群集的 RMS 保护的所有内容。


关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间︰ 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的"信息权限管理 (IRM) 配置"条目。

  - 必须在 Active Directory 林中安装一个 AD RMS 群集。

  - 联合身份验证邮箱已添加到 AD RMS 超级用户组。有关详细说明，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 必须为组织启用 IRM 功能。有关详细说明，请参阅[对内部邮件启用或禁用 IRM](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md)。

  - 可以使用**Set-IRMConfiguration** cmdlet 来启用或禁用在Outlook Web App和 IRM IRM，在Exchange ActiveSyncExchange的整个组织或特定级别。
    
    您可以控制 IRM 中Outlook Web App以下级别︰
    
      - **每个 Outlook Web App 虚拟目录：** 若要为 Outlook Web App 虚拟目录启用或禁用 Outlook Web App 中的 IRM，请使用 **Set-OWAVirtualDirectory** cmdlet 并将 *IRMEnabled* 参数设置为 `$false` 或 `$true`（默认）。此操作可以为 Exchange 2013 客户端访问服务器上的一个虚拟目录禁用 Outlook Web App 中的 IRM，同时保持其他客户端访问服务器上的另一个虚拟目录上的 IRM 为启用状态。
    
      - **每个 Outlook Web App 邮箱策略：** 若要为 Outlook Web App 邮箱策略启用或禁用 Outlook Web App 中的 IRM，请使用 **Set-OWAMailboxPolicy** cmdlet 并将 *IRMEnabled* 参数设置为 `$false` 或 `$true`（默认）。此操作通过为用户组分配不同的 Outlook Web App 邮箱策略，可以对一组用户启用 Outlook Web App 中的 IRM，而同时对另一组用户禁用 IRM。
    
    您可以控制每个Exchange ActiveSync邮箱策略Exchange ActiveSync IRM。若要禁用或启用 IRM 中Exchange ActiveSyncExchange ActiveSync邮箱策略，使用**Set-ActiveSyncMailboxPolicy** cmdlet 并将*IRMEnabled*参数设置为`$false`或`$true` （默认值）。这允许您在Exchange ActiveSync为一组用户启用 IRM 和禁用它的另一组用户通过将他们分配到不同的Exchange ActiveSync邮箱策略。

  - 您不能使用 Exchange 管理中心 (EAC) 来启用或禁用 IRM 客户端访问服务器上。您必须使用外壳程序。

## 您想执行什么操作？

## 使用外壳程序启用 IRM 客户端访问服务器上

本示例在Exchange公司的客户端访问服务器上启用 IRM。

    Set-IRMConfiguration -ClientAccessServerEnabled $true

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 使用外壳程序禁用 IRM 客户端访问服务器上

本示例在Exchange公司的客户端访问服务器上禁用 IRM。

    Set-IRMConfiguration -ClientAccessServerEnabled $false

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 您如何知道这有效？

若要验证已成功启用或禁用 IRM 客户端访问服务器上，请执行以下操作︰

  - 运行**Get-IRMConfiguration** cmdlet 并检查*ClientAccessServerEnabled*属性的值。
    
    有关如何获取 IRM 配置的示例，请参阅**Get-IRMConfiguration**中的[示例](https://technet.microsoft.com/zh-cn/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

  - 使用Outlook Web App来创建或读取受 IRM 保护的邮件。

