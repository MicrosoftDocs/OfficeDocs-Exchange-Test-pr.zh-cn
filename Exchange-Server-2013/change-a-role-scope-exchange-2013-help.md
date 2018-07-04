---
title: '更改角色范围: Exchange 2013 Help'
TOCTitle: 更改角色范围
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 50491028
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改角色范围

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色的作用域确定哪些对象进行对用户可用，以便可以更改使用的 cmdlet 和分配给它们的参数的对象。通过更改作用域，您可以更改哪些对象可供用户可以创建、 更改或删除。

您可以更改自定义的管理范围。您可以更改排斥或定期范围。如果您更改一个独占的范围，新的作用域将立即生效。如果您想要更改管理角色分配具有预定义的或组织单位 (OU) 管理作用域，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

有关 Microsoft Exchange Server 2013 中管理角色作用域和分配的详细信息，请参阅下列主题：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

要查找与角色作用域相关的其他管理任务吗？请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理作用域\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 更改作用域的名称

若要更改作用域的名称，请使用以下语法。

    Set-ManagementScope <current scope name> -Name <new scope name>

本示例将 Seattle Servers 作用域更改为 Seattle Exchange Servers。

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

有关语法和参数的详细信息，请参阅 [Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))。

## 更改作用域的收件人筛选器

若要更改作用域的收件人筛选器，请使用以下语法。

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

本示例将更改收件人筛选器，以使其与 **Company** 属性设置为 Contoso 的所有收件人对象相匹配。

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

有关语法和参数的详细信息，请参阅 [Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))。

有关收件人筛选器和可筛选收件人属性列表的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 更改作用域的组织单位根目录

若要更改作用域的组织单位根目录，请使用以下语法。

    Set-ManagementScope <scope name> -RecipientRoot <OU>

本示例将组织单位根目录更改为 contoso.com 域下的 North America/Sales 的 Sales Users OU。

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

有关语法和参数的详细信息，请参阅 [Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))。

## 更改作用域的服务器筛选器

要更改作用域的服务器筛选器，请使用以下语法。

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

本示例更改服务器筛选器，以匹配所有将 **ServerSite** 属性设置为 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' 的服务器对象。

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

有关语法和参数的详细信息，请参阅 [Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))。

有关服务器筛选器和可筛选服务器属性列表的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 更改作用域的服务器列表

您不能更改作用域上的服务器列表。如果您需要更改的服务器列表中，您需要执行下列操作 ︰

1.  如果需要，请使用[查看角色作用域](view-role-scopes-exchange-2013-help.md)主题中的\&quot;查看特定作用域\&quot;步骤来检索作用域上要替换的当前服务器列表。

2.  通过使用新的服务器列表创建一个作用域"步骤 1 ︰ 创建自定义的作用域" [创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)主题中的过程。

3.  使用[更改角色分配](change-a-role-assignment-exchange-2013-help.md)主题中的\&quot;使用命令行管理程序在角色分配上更改服务器筛选器或基于列表的作用域\&quot;步骤，将所有使用旧作用域的管理角色分配更改为使用新作用域。

4.  使用[删除角色的作用域](remove-a-role-scope-exchange-2013-help.md)主题中的步骤删除旧作用域。

## 更改作用域的数据库筛选器

要更改作用域的数据库筛选器，请使用以下语法。

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

本示例将更改数据库筛选器，以使其与 **Name** 属性包含字符串\&quot;Executive\&quot;的所有数据库对象相匹配。

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

有关语法和参数的详细信息，请参阅 [Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))。

有关数据库筛选器和可筛选数据库属性列表的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 更改作用域的数据库列表

您不能更改作用域上的数据库列表。如果您需要更改数据库列表中，您需要执行下列操作 ︰

1.  如果需要，请使用[查看角色作用域](view-role-scopes-exchange-2013-help.md)主题中的\&quot;查看特定作用域\&quot;步骤来检索作用域上要替换的当前数据库列表。

2.  通过使用新的数据库列表创建一个作用域"步骤 1 ︰ 创建自定义的作用域" [创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)主题中的过程。

3.  使用[更改角色分配](change-a-role-assignment-exchange-2013-help.md)主题中的\&quot;使用命令行管理程序在角色分配上更改数据库筛选器或基于列表的作用域\&quot;步骤，将所有使用旧作用域的管理角色分配更改为使用新作用域。

4.  使用[删除角色的作用域](remove-a-role-scope-exchange-2013-help.md)主题中的步骤删除旧作用域。

