---
title: '向用户或 USG 添加角色: Exchange 2013 Help'
TOCTitle: 向用户或 USG 添加角色
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50491297
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 向用户或 USG 添加角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色分配可以将管理角色分配给用户或通用安全性组 (USG)。通过将角色分配给用户或 USG，您可以使这些用户根据 cmdlet 或脚本以及其在管理角色上定义的参数来执行任务。

如果要将角色分配给管理角色组或管理角色分配策略，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [管理角色分配策略](manage-role-assignment-policies-exchange-2013-help.md)

如果要将成员添加到角色组或将角色分配策略分配给最终用户，请参阅下列主题：

  - [管理角色组成员](manage-role-group-members-exchange-2013-help.md)

  - [更改邮箱的分配策略](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

有关详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色分配”条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 虽然可以直接将角色分配给用户和 USG，但向管理员和最终用户授予权限的建议方法是使用管理角色组和管理角色分配策略。使用角色组和分配策略时，可以简化权限模型。

  - 角色分配是累加的。这意味着对所有角色进行评估时将一起添加这些角色。如果向某个用户分配了两个角色，但其中只有一个角色包含 cmdlet，该用户将仍然可以使用此 cmdlet。
    
    默认情况下，角色分配不能将角色分配给其他用户。若要使用户能够将角色分配给其他用户或 USG，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

  - 如果创建具有作用域的分配，则该作用域将覆盖角色的隐式写入作用域。但是，角色的隐式读取作用域仍然适用。新作用域无法返回角色的隐式读取作用域之外的对象。有关详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

  - 本主题中的所有步骤都使用 *SecurityGroup* 参数将角色分配给 USG。如果要将角色分配给特定用户，请使用 *User* 参数，而不是 *SecurityGroup* 参数。每个命令的所有其他语法都相同。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建没有作用域的角色分配

可以创建没有作用域的角色分配。这样做时，角色的隐式读取和隐式写入作用域都适用。

使用以下语法将角色分配给没有任何作用域的 USG。

    
```PowerShell
New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>
```

本示例将 Exchange Servers 角色分配给 SeattleAdmins USG。

    
```PowerShell
New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"
```

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 创建具有预定义相对作用域的角色分配

如果预定义相对作用域满足您的业务要求，则可以将该作用域应用于角色分配，而无需创建自定义作用域。有关预定义作用域及其说明的列表，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

使用以下语法将角色分配给具有预定义作用域的 USG。

    
```PowerShell
New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >
```

本示例将 Exchange Servers 角色分配给 SeattleAdmins USG 并应用 Organization 预定义作用域。

    
```PowerShell
New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization
```

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 创建具有基于收件人筛选器的作用域的角色分配

如果创建了基于收件人筛选器的作用域且要将其与角色分配一起使用，需要使用 *CustomRecipientWriteScope* 参数将该作用域包含在用于将该角色分配给 USG 的命令中。如果使用 *CustomRecipientWriteScope* 参数，则无法使用 *RecipientOrganizationalUnitScope* 参数。

需要先创建一个角色分配，然后才能向其添加作用域。有关详细信息，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

使用以下语法将角色分配给具有基于收件人筛选器的作用域的 USG。

    
```PowerShell
New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>
```

本示例将 Mail Recipients 角色分配给 Seattle Recipient Admins USG 并应用 Seattle Recipients 作用域。

    
```PowerShell
New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"
```

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 创建具有基于服务器筛选器、基于数据库筛选器或基于列表的配置作用域的角色分配

如果创建了基于服务器筛选器、基于数据库筛选器或基于列表的配置作用域，且要将其与角色分配一起使用，则需要使用 *CustomConfigWriteScope* 参数将该作用域包含在用于将角色分配给 USG 的命令中。

需要先创建一个角色分配，然后才能向其添加作用域。有关详细信息，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

使用以下语法将角色分配给具有配置作用域的 USG。

    
```PowerShell
New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>
```

本示例将 Exchange Servers 角色分配给 MailboxAdmins USG 并应用 Mailbox Servers 作用域。

    
```PowerShell
New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"
```

前面的示例显示了如何添加具有服务器配置作用域的角色分配。添加数据库配置作用域的语法是相同的。不过，需要指定的是数据库作用域的名称，而不是服务器作用域的名称。

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 创建具有 OU 作用域的角色分配

如果要将角色的写入作用域扩展到组织单位 (OU)，可以在 *RecipientOrganizationalUnitScope* 参数中直接指定 OU。如果使用 *RecipientOrganizationalUnitScope* 参数，则无法使用 *CustomRecipientWriteScope* 参数。

使用以下语法将角色分配给 USG 并将角色的写入作用域限制为特定 OU。

    
```PowerShell
New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>
```

本示例将 Mail Recipients 角色分配给 SalesRecipientAdmins USG 并将该分配的作用域限定为 contoso.com 域中的 sales/users OU。

    
```PowerShell
New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users
```

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

## 创建具有独占收件人或配置作用域的角色分配

若要创建具有独占收件人或配置作用域的独占角色分配，可以使用创建具有基于收件人筛选器的作用域的角色分配和创建具有基于服务器筛选器、基于数据库筛选器或基于列表的配置作用域的角色分配部分中提供的相同过程。唯一的区别是，创建具有独占作用域的角色分配时，您必须根据使用的是独占收件人作用域还是独占配置作用域指定下列独占参数：

  - **独占收件人作用域**   使用 *ExclusiveRecipientWriteScope* 参数代替 *CustomRecipientWriteScope* 参数。

  - **独占配置作用域**   使用 *ExclusiveConfigWriteScope* 参数代替 *CustomConfigWriteScope* 参数。

执行此过程时，分配有角色的角色接受者可以对独占作用域中包含的对象执行操作。有关独占作用域的详细信息，请参阅[了解独占作用域](understanding-exclusive-scopes-exchange-2013-help.md)。

不能创建同时具有互斥作用域和常规作用域的角色分配。

本示例将 Mail Recipients 角色分配给 Protected User Admins USG 并应用 Protected Users 独占作用域。

    
```PowerShell
New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"
```

有关语法和参数的详细信息，请参阅 [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

