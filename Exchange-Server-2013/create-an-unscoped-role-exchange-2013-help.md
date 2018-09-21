---
title: '创建一个未区分范围的角色: Exchange 2013 Help'
TOCTitle: 创建一个未区分范围的角色
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50490621
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建一个未区分范围的角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-09_

无作用域的管理角色可用于向管理员和专家用户提供对 Windows PowerShell 脚本和非 Exchange cmdlet 的访问权限。可以创建无作用域的顶级角色并将脚本或非 Exchange cmdlet 添加到该角色，也可以基于现有的无作用域顶级角色来创建角色。创建并自定义无作用域角色之后，可以将该角色分配到管理角色组、用户和通用安全组 (USG)。不能将无作用域角色分配到管理角色分配策略。有关无作用域角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

> [!CAUTION]  
> 无作用域角色的功能非常强大，因为顾名思义，无作用域角色就是指未应用任何管理作用域。这意味着它们所包含的脚本和非 Exchange cmdlet 可以针对您的 Exchange 组织中的任何对象运行。在将脚本或非 Exchange cmdlet 添加到无作用域角色时，以及分配无作用域角色时，应考虑上述情况。


> [!NOTE]  
> 如果要创建包含 Exchange cmdlet 的角色，则必须创建基于现有管理角色的角色。有关创建包含 Exchange cmdlet 的角色的详细信息，请参阅<a href="create-a-role-exchange-2013-help.md">创建角色</a>。


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 默认情况下，任何管理角色组中都不包括创建无作用域角色的能力。必须首先将无作用域角色管理角色分配给用户或者用户所属的 USG 或角色组，用户才能创建角色组。有关向用户、USG 或角色组添加角色的详细信息，请参阅下列主题：
    
      - [管理角色组](manage-role-groups-exchange-2013-help.md)
    
      - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建无作用域的顶级管理角色

如果要使组织中的管理员或专家可以访问脚本或非 Exchange cmdlet，则需要创建无作用域的顶级角色。初始无作用域角色不可从其他角色继承，因此脚本和非 Exchange cmdlet 只能添加到作为顶级角色创建的无作用域角色。然后，可将新建的无作用域顶级角色作为其他无作用域角色的父级，这些无作用域角色也可以使用所添加的脚本和非 Exchange cmdlet。

下面是创建无作用域顶级角色的步骤：

## 步骤 1：创建无作用域的顶级角色

无作用域的顶级角色没有父角色。需要指定 *UnscopedTopLevel* 开关以创建没有父级的角色。使用以下语法创建新角色。

```powershell
New-ManagementRole <name of new role> -UnscopedTopLevel
```

本示例创建 IT Scripts 无作用域顶级角色。

```powershell
New-ManagementRole "IT Scripts" -UnscopedTopLevel
```

创建后，在您向角色中添加脚本或非 Exchange cmdlet 之前，该角色为空。

有关语法和参数的详细信息，请参阅 [New-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd298073\(v=exchg.150\))。

## 步骤 2a：添加脚本管理角色条目

如果要向新建的无作用域角色添加脚本，请使用此步骤。如果要向新建的无作用域角色添加非 Exchange cmdlet，请使用Step 2b。

若要向无作用域的顶级角色添加 Windows PowerShell 脚本，必须向该角色添加管理角色条目。角色条目包含脚本的名称以及脚本中要供角色使用的参数。

脚本必须位于每个运行 Exchange 2013（用户必须与之连接以运行脚本）的服务器上 Microsoft Exchange Server 2013 安装路径的 `RemoteScripts` 目录中。如果用户有权运行脚本，但脚本并非位于用户所连接的 Exchange 2013 服务器上，则会发生错误。默认情况下，`RemoteScripts` 目录的路径为 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts。

将脚本复制到相应的 Exchange 2013 服务器并决定应使用脚本的哪些参数之后，使用以下语法创建角色条目。

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

本示例用 *Name* 和 *Location* 参数将 BulkProvisionUsers.ps1 脚本添加到 IT Scripts 角色。

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel

> [!NOTE]  
> <strong>Add-ManagementRoleEntry</strong> cmdlet 执行基本验证，以确保仅添加该脚本中存在的参数。但是，添加角色条目之后就不再进行其他验证。如果以后要添加或删除参数，则必须手动更新包含该脚本的角色条目。


## 步骤 2b：添加非 Exchange cmdlet 角色条目

如果要向新建的无作用域角色添加非 Exchange cmdlet，请使用此步骤。如果要向新建的无作用域角色添加脚本，请使用Step 2a。

若要向无作用域的顶级角色添加非 Exchange cmdlet，必须向该角色添加管理角色条目。角色条目包含 cmdlet 管理单元、cmdlet 名称以及 cmdlet 中要供角色使用的参数。

如果向新角色添加非 Exchange cmdlet，则必须在用户为运行这些 cmdlet 而可能连接的每台 Exchange 2013 服务器上都安装这些 cmdlet。若要了解如何正确安装和注册包含您要使用的 cmdlet 的 Windows PowerShell 管理单元，请参考产品的相关文档。

将包含 cmdlet 的 Windows PowerShell 管理单元安装在相应的 Exchange 2013 服务器上，并确定要使用的 cmdlet 参数之后，请使用以下语法创建角色条目。

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

本示例用 *Database* 和 *Size* 参数将 Contoso.Admin.Cmdlets 管理单元中的 **Set-WidgetConfiguration** cmdlet 添加到 Widget Cmdlets 角色。

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel

> [!NOTE]  
> <strong>Add-ManagementRoleEntry</strong> cmdlet 执行基本验证，以确保仅添加该 cmdlet 中存在的参数。但是，添加角色条目之后就不再进行其他验证。如果以后要更改 cmdlet 或者添加或删除参数，则必须手动更新包含该 cmdlet 的角色条目。


## 步骤 3：分配管理角色

创建和配置角色时的最后一步是将其分配给角色受理人。

> [!IMPORTANT]  
> 不能对分配无作用域角色的角色分配配置管理作用域。无论选择为角色组、用户还是 USG 创建角色分配，都必须选择用于创建无管理作用域的角色分配的选项。


可以将新角色分配给角色组、用户或 USG。有关详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## 基于另一个无作用域角色创建无作用域角色

如果有现成的无作用域顶级角色或其他无作用域角色，并且希望基于这些角色创建新的无作用域角色，则可以创建子级无作用域角色。子级无作用域角色可以包含存在于父级无作用域角色上的脚本和 cmdlet 子集。这一点非常有用，例如，当您希望使经验不足的管理员只能访问父级无作用域角色上的脚本或 cmdlet 的某个子集时，就可以使用此功能。

下面是创建无作用域子角色的步骤：

## 步骤 1：创建无作用域的子角色

可以基于现有的无作用域角色创建新的无作用域子角色。创建角色时，将把现有角色及其管理角色条目复制到新角色。现有角色将成为新子角色的父级。如果要基于其他无作用域角色创建无作用域角色，则必须选择包含所有需要使用的 cmdlet 和参数的角色，然后将不需要的 cmdlet 和参数删除。子级无作用域角色不能拥有父角色中不存在的管理角色条目。

> [!NOTE]  
> 如果需要创建一个无作用域角色，使其包含其他任何无作用域角色中都不存在的脚本或非 Exchange cmdlet，应创建无作用域顶级角色。有关详细信息，请参阅本主题前面所述的Create an unscoped top-level management role。


使用以下语法创建新角色。

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

此示例将 IT Global Scripts 角色及其管理角色条目复制到 Diagnostic IT Scripts 角色。

```powershell
New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"
```

有关语法和参数的详细信息，请参阅 [New-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd298073\(v=exchg.150\))。

## 步骤 2：更改角色的管理角色条目

创建角色之后，需要更改角色的条目。可以删除整个角色条目，这将完全删除对关联的脚本或非 Exchange cmdlet 的访问权限。或者，也可以从角色条目中删除参数，从而删除对关联脚本或非 Exchange cmdlet 上的这些特定参数的访问权限。

无法在角色条目上添加角色条目或参数，除非它们存在于父角色中。由于刚刚在第 1 步中从父角色创建了一个角色，因此无法在角色条目上添加任何其他角色条目或参数，原因是它们不存在于父角色中。

更改角色的角色条目时，可以执行以下操作之一：

  - 删除一个完整的角色条目。

  - 删除多个完整的角色条目。

  - 删除角色条目中的参数。

若要删除新角色中的角色条目，请参阅[从角色中删除一个角色条目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

## 步骤 3：分配管理角色

创建和配置角色时的最后一步是将其分配给角色受理人。

> [!IMPORTANT]  
> 不能对分配无作用域角色的角色分配配置管理作用域。无论选择为角色组、用户还是 USG 创建角色分配，都必须选择用于创建无管理作用域的角色分配的选项。


可以将新角色分配给角色组、用户或 USG。有关详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

