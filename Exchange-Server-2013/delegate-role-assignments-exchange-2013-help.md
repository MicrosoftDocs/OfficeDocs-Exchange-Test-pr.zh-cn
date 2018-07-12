---
title: '委派角色分配: Exchange 2013 Help'
TOCTitle: 委派角色分配
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 50491895
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 委派角色分配

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-02_

通过管理角色委派，角色受理人可以将指定的管理角色分配给其他管理角色组、管理角色分配策略、用户或通用安全组 (USG)。 默认情况下，只有“组织管理”管理角色组的成员才能委派角色分配。部署新安装的 Microsoft Exchange Server 2013 时，只有安装了 Exchange 2013 的用户帐户才是“组织管理”角色组的成员。

如果要向某个角色组分配委派角色分配，则该角色组中的任何成员都可以将相关联的管理角色委派给其他角色受理人。

> [!IMPORTANT]  
> 委派角色分配并不会向角色受理人提供角色所授予的权限，而只是使角色受理人具有将角色分配给其他人的能力。 如果要同时向角色受理人提供角色所授予的权限，还必须创建常规角色分配。 若要创建常规角色分配，请参阅下列主题：
> <a href="manage-role-groups-exchange-2013-help.md">管理角色组</a>
> <a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色分配策略</a>
> <a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">向用户或 USG 添加角色</a>


> [!NOTE]  
> 本主题讨论管理角色分配委派。如果要委派可以在角色组中添加或删除成员的用户（这是建议的委派方法），请参阅<a href="manage-role-groups-exchange-2013-help.md">管理角色组</a>。


有关常规角色分配和委派管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

是否正在寻找与管理权限相关的其他管理任务？ 请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色分配”条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序委派管理角色

您可以使用创建常规或独占作用域时所使用的预定义作用域、基于收件人筛选器或服务器筛选器的作用域、基于服务器列表的作用域以及组织单位 (OU) 作用域来创建委派角色分配。 创建常规角色分配与委派角色分配的唯一区别在于是否将 *Delegating* 开关添加到命令中。 有关如何创建角色分配的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

> [!NOTE]  
> 您不能对管理角色分配策略创建委派角色分配。


此示例将创建一个委派角色分配，以便 Senior Admins 角色组的成员将 Mail Recipients 角色分配给 Exchange 组织中的任何角色受理人。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

此示例将创建一个委派角色分配，以便 Senior Admins 角色组的成员将 Mail Recipients 角色只分配给 contoso.com 域的 Sales/Users OU 中的用户。

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

有关详细的语法和参数信息，请参阅[New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))。

