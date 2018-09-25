---
title: '创建常规或独占作用域: Exchange 2013 Help'
TOCTitle: 创建常规或独占作用域
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 50491500
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建常规或独占作用域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

管理角色作用域确定向用户提供哪些对象，以便可以使用 cmdlet 以及为其分配的参数更改这些对象。通过添加管理作用域，您可以配置管理角色分配，以便用户可以管理组织中的特定服务器、数据库、收件人和其他对象，同时限制更改其他对象。

> [!IMPORTANT]  
> 创建常规或独占作用域时，将覆盖在分配的管理角色上定义的写入作用域。不能覆盖在管理角色上配置的读取作用域。


可以创建自定义管理作用域以及添加或更改管理角色分配。如果要使用预制的管理作用域或组织单位 (OU) 管理作用域创建管理角色分配，请参阅[向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

有关 Microsoft Exchange Server 2013 中管理角色作用域和分配的详细信息，请参阅下列主题：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

要查找与作用域相关的其他管理任务吗？请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“管理作用域”条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：创建自定义作用域

若要创建自定义作用域，请选择下列作用域类型之一：

## 收件人筛选器作用域

使用 **New-ManagementScope** cmdlet 的 *RecipientRestrictionFilter* 参数创建基于收件人筛选器的作用域。创建收件人筛选器时，除了要筛选的收件人属性外，您还可以指定在其中运行筛选器查询的 OU。指定基础 OU 时，可以进一步限制该角色的写入作用域。

有关管理作用域筛选器的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用以下语法创建具有基础 OU 的域限制筛选器作用域。

```powershell
New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]
```

此示例创建一个包含 contoso.com/Sales OU 中所有邮箱的作用域。

```powershell
New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"
```

> [!NOTE]  
> 如果希望将筛选器应用到管理角色的整个隐式读取作用域而不只是特定 OU 内的读取作用域，则可以省略 <em>RecipientRoot</em> 参数。


有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 服务器筛选器配置作用域

使用 **New-ManagementScope** cmdlet 上的 *ServerRestrictionFilter* 参数创建基于服务器筛选器的配置作用域。使用服务器筛选器可以创建一个作用域，该作用域仅适用于与您指定的筛选器匹配的服务器。

有关管理作用域筛选器的详细信息和可筛选服务器属性的列表，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用以下语法创建服务器筛选器作用域。

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

此示例创建了一个包括 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' AD (Active Directory) 站点中所有服务器的作用域。

```powershell
New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }
```

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 服务器列表配置作用域

使用 **New-ManagementScope** cmdlet 的 *ServerList* 参数创建基于服务器列表的配置作用域。使用服务器列表作用域可以创建一个作用域，该作用域仅适用于您在列表中指定的服务器。

使用以下语法创建服务器列表作用域。

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

此示例创建一个仅适用于 MBX1、MBX3 和 MBX5 的作用域。

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 数据库筛选器配置作用域

基于数据库筛选器的配置作用域是使用 **New-ManagementScope** cmdlet 上的 *DatabaseRestrictionFilter* 参数创建的。使用数据库筛选器可以创建一个作用域，该作用域仅适用于与您指定的筛选器匹配的数据库。

> [!IMPORTANT]  
> 与数据库作用域关联的角色分配仅应用到连接到运行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本或者 Exchange 2013 的服务器的用户。如果分配了与数据库作用域相关联的角色分配的用户连接到之前的 Exchange 2010 SP1 服务器，则角色分配不会应用于此用户，并且也不会向此用户授予角色分配提供的任何权限。


有关管理作用域筛选器的详细信息和可筛选数据库属性的列表，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

使用以下语法创建数据库限制筛选器。

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

本示例将创建一个作用域，该作用域包括数据库的 **Name** 属性中含有字符串“Executive”的所有数据库。

```powershell
New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }
```

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 数据库列表配置作用域

基于数据库列表的配置作用域是使用 **New-ManagementScope** cmdlet 上的 *DatabaseList* 参数创建的。使用数据库列表作用域可以创建一个作用域，该作用域仅适用于您在列表中指定的数据库。

> [!IMPORTANT]  
> 与数据库作用域关联的角色分配仅应用于连接到运行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本或者 Exchange 2013 的服务器的用户。如果分配了与数据库作用域相关联的角色分配的用户连接到之前的 Exchange 2010 SP1 服务器，则角色分配不会应用于此用户，并且也不会向此用户授予角色分配提供的任何权限。


使用以下语法创建数据库列表作用域。

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

本示例将创建仅适用于数据库 Database 1、Database 2 和 Database 3 的作用域。

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 独占作用域

可将使用 **New-ManagementScope** cmdlet 创建的任何作用域指定为独占作用域。若要创建独占作用域，请在上述某一节中使用相同命令创建基于收件人筛选器的作用域、基于服务器筛选器的作用域、基于服务器列表的作用域、基于数据库筛选器的作用域或基于数据库列表的作用域，然后向该命令中添加 *Exclusive* 开关。

> [!CAUTION]  
> 在创建独占管理作用域时，仅分配有包含要修改对象的独占作用域的角色接受者才可以访问这些对象。只有分配了具有独占作用域角色的管理员才可以访问这些独占或受保护的对象。


此示例创建基于收件人筛选器的独占作用域，该作用域与 Executives 部门中的任何用户匹配。

```powershell
New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive
```

默认情况下，创建独占作用域时，将要求您确认已创建独占作用域且了解独占作用域对现有非独占角色分配造成的影响。如果您希望取消此警告，则可以使用 *Force* 开关。此示例创建一个与上一示例相同的作用域，但没有警告。

```powershell
New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force
```

有关语法和参数的详细信息，请参阅 [New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))。

## 步骤 2：添加或更改管理角色分配

创建作用域后，必须将其添加到新建或现有的管理角色分配。

如果创建了一个管理作用域并要将其添加到即将创建的新管理角色分配，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

如果创建了一个管理角色作用域并要将其添加到现有的管理角色分配，请参阅下列主题：

  - [管理角色分配策略](manage-role-assignment-policies-exchange-2013-help.md)

  - [更改角色分配](change-a-role-assignment-exchange-2013-help.md)

