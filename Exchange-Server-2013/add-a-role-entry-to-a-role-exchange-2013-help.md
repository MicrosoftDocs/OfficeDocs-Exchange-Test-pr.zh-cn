---
title: '向角色添加角色: Exchange 2013 Help'
TOCTitle: 向角色添加角色
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50490269
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 向角色添加角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-04_

如果您想要授予访问权限的 cmdlet，您需要将相关的管理角色条目添加到一个管理角色。向角色添加角色条目后，指派角色的用户将能够访问该 cmdlet。有关 Microsoft Exchange Server 2013中的管理角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

您不能将角色项添加到内置角色。如果您希望自定义角色，您必须创建新的角色。有关如何创建新的角色的详细信息，请参阅[创建角色](create-a-role-exchange-2013-help.md)。

> [!NOTE]
> 本主题不讨论如何将未区分范围的管理角色条目添加到未区分范围的管理角色。有关如何添加未区分范围的角色条目的详细信息，请参阅<a href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">向未区分范围的顶级角色添加角色</a>。


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 要添加到管理角色的角色条目必须存在于该角色的直接父管理角色中。

  - 本主题使用的管道。流水线操作的详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 从父角色中添加单个角色条目

通过使用以下语法，可以完全按照角色条目在父角色上的显示原样将其添加到角色。

    Add-ManagementRoleEntry <child role name>\<cmdlet>

本示例将 **Set-Mailbox** cmdlet 添加到 Recipient Administrators 角色。

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

此命令检查父角色，如果角色的项存在，则将其添加到子角色。如果角色输入已经存在于子角色中，可以包括要改写现有的角色词条的*Overwrite*参数。

有关语法和参数的详细信息，请参阅 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351236\(v=exchg.150\))。

## 从父角色添加单个角色条目，并且仅包括特定参数

如果要从父角色添加角色条目，但要在子角色上的角色条目中仅包括特定参数，请使用以下语法。

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

此示例将 **Set-Mailbox** cmdlet 添加到 Help Desk 角色，但在子角色上的条目中仅包括 *DisplayName* 和 *EmailAddresses* 参数。

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

此命令检查父角色，如果角色的项存在，则将其添加到子角色。如果角色输入已经存在于子角色中，可以包括要改写现有的角色词条的*Overwrite*参数。

有关语法和参数的详细信息，请参阅 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351236\(v=exchg.150\))。

## 从父角色中添加多个角色条目

如果您想要添加到角色的角色的多个条目，您需要检索的角色存在的项，您想要添加到子角色，并将它们添加到子角色的父角色的列表。若要执行此操作，请使用**Get-ManagementRoleEntry** cmdlet 检索父角色的角色序列。然后您管**Get-ManagementRoleEntry**到**Add-ManagementRoleEntry** cmdlet cmdlet 的输出。若要检索多个角色条目，您需要使用通配符 （\*）。

要将多个条目从父角色添加到子角色，请使用以下语法。

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

本示例将包含\&quot;邮件收件人\&quot;父角色上 cmdlet 名称中的字符串 `Mailbox` 的所有角色条目添加到\&quot;Seattle 邮件收件人\&quot;子角色。

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

如果子角色上已存在角色条目，则可以包括 *Overwrite* 参数以覆盖现有的角色条目。

有关检索管理角色条目列表的详细信息，请参阅[查看角色条目](view-role-entries-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\)) 和 [Add-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351236\(v=exchg.150\))。

