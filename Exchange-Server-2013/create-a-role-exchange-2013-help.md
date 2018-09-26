---
title: '创建角色: Exchange 2013 Help'
TOCTitle: 创建角色
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 50491834
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-17_

您可以创建一个管理角色，更改管理角色项、 添加一个作用域，如果需要然后将该角色分配给角色受托人。很少需要执行此过程。我们建议您检查而不是创建一个管理角色中是否可以使用内置的管理角色。内置管理角色的列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

有关 Microsoft Exchange Server 2013 中管理角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

> [!NOTE]  
> 本主题不讨论如何创建未区分范围的管理角色。有关如何创建未区分范围的管理角色的信息，请参阅<a href="create-an-unscoped-role-exchange-2013-help.md">创建一个未区分范围的角色</a>。


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1 ︰ 创建管理角色

新的管理角色基于现有的角色。当您创建一个角色时，现有角色和管理角色条目复制到新的角色。现有角色将成为新的子角色的父级。您必须始终选择角色包含所有的 cmdlet 和参数，您需要使用，然后删除您不想的要。孩子角色不能管理角色条目中父角色不存在。

使用以下语法创建新角色。

```powershell
New-ManagementRole -Parent <existing role to copy> -Name <name of new role>
```

此示例将 Mail Recipients 角色及其管理角色项复制到 Seattle Mail Recipients 角色。

```powershell
New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"
```

有关详细的语法和参数信息，请参阅[New-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd298073\(v=exchg.150\))。

## 步骤 2 ︰ 更改新的角色管理角色条目

创建您的角色后，您需要更改角色的条目。您可以删除整个角色条目，这将完全删除访问关联的 cmdlet。或者，您可以从一个角色条目，以删除对这些特定的参数相关联的 cmdlet 上访问删除参数。

不能添加新角色输入或参数对角色项除非它们存在父角色中。因为刚才从父角色在步骤 1 中创建角色，无法添加任何其他角色的条目或参数对角色项因为它们不存在于父角色。

更改角色的角色项时，可以执行以下操作之一：

  - 删除一个完整的角色项。

  - 删除多个完整的角色项。

  - 删除角色项中的参数。

若要删除新角色中的角色项，请参阅[从角色中删除一个角色条目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

## 步骤 3 ︰ 创建一个自定义的管理角色范围内，如果需要

管理角色的作用域确定可供用户查看或更改使用在第 2 步中配置的角色项的对象。新的管理角色继承读取和写入其父角色的角色作用域的管理。这些被称为*隐式的范围*。但是，可能想要更改写领域新的角色，以满足业务需求的情况。当您创建一个自定义的作用域时，则重写角色的隐写作用域。角色的隐式的阅读的范围不会改变。关于管理角色作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

可以创建自定义的作用域、 创建独占范围，使用预定义的作用域，或作用域分配给组织单位 (OU)。新建作用域必须在角色的隐式阅读的范围内。若要使用预定义的作用域或指定的组织单位，请跳至步骤 4。

若要将自定义作用域添加至新角色，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

## 步骤 4 ︰ 将新的管理角色分配

创建和配置角色时的最后一步是将其分配给角色接受者。

创建角色分配时，可以选择执行以下步骤之一：

  - 创建无作用域的角色分配。

  - 创建具有预定义作用域的角色分配。

  - 创建具有 OU（没有域限制筛选器）的角色分配。

  - 创建具有在步骤 3 中创建的自定义或独占作用域的角色分配。
    
    > [!NOTE]  
    > 在角色和管理角色分配策略之间创建分配时，不能指定作用域。


您可以分配新角色到角色组、 角色分配策略、 用户或通用安全组 (USG)。有关详细信息，请参阅下列主题 ︰

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [管理角色分配策略](manage-role-assignment-policies-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

