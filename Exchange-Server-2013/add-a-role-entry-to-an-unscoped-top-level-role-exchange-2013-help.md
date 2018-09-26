---
title: '向未区分范围的顶级角色添加角色: Exchange 2013 Help'
TOCTitle: 向未区分范围的顶级角色添加角色
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50490551
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 向未区分范围的顶级角色添加角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

如果要使新的脚本或非Exchange cmdlet 供现有未区分范围角色，可以给未区分范围顶级管理角色添加脚本和非Exchange cmdlet。这些脚本和非Exchange cmdlet 未区分范围顶级管理角色添加为管理角色的项。然后可以通过那些未区分范围顶级角色条目使用它们或顶级角色中派生的任何未区分范围的角色。有关未区分范围的角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

> [!NOTE]  
> 如果要更改包含 Exchange cmdlet 的管理角色的角色条目，请参阅<a href="change-a-role-entry-exchange-2013-help.md">更改角色条目</a>。


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 默认情况下不包含任何管理角色组中角色将项添加到未区分范围的顶级角色的能力。您必须首先将未区分范围角色管理角色的用户或角色组或通用安全组 (USG) 的用户是成员，用户才可以添加未区分范围顶级角色条目。有关为角色组、 用户或 USG 添加角色的详细信息，请参阅下列主题 ︰
    
      - [管理角色组](manage-role-groups-exchange-2013-help.md)
    
      - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 向无作用域的顶级角色添加脚本角色条目

如果您想要添加到现有未区分范围角色的脚本，请使用此过程。如果您想要添加到现有未区分范围角色非Exchange cmdlet，请参阅"添加非 Exchange cmdlet 角色条目未区分范围的顶级角色"本主题后面部分中。

若要向无作用域的顶级角色添加 Windows PowerShell 脚本，必须向该角色添加管理角色条目。角色条目包含脚本的名称以及脚本中要供角色使用的参数。

该脚本必须驻留在运行Exchange 2013的用户可能会连接运行脚本的每台服务器上的 Microsoft Exchange Server 2013安装路径中的脚本目录。如果用户具有访问权限才能运行一个脚本，但该脚本不位于用户连接到Exchange 2013服务器上，则会导致出错。默认情况下，脚本目录的路径是 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts。

将脚本复制到相应的 Exchange 2013 服务器并决定应使用脚本的哪些参数之后，使用以下语法创建角色条目。

```powershell
Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel
```

本示例用 *Name* 和 *Location* 参数将 BulkProvisionUsers.ps1 脚本添加到 IT Scripts 角色。

```powershell
Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel
```

> [!NOTE]  
> <strong>Add-ManagementRoleEntry</strong> cmdlet 执行基本验证，以确保仅添加该脚本中存在的参数。但是，添加角色条目之后就不再进行其他验证。如果以后要添加或删除参数，则必须手动更新包含该脚本的角色条目。


## 向无作用域的顶级角色添加非 Exchange cmdlet 角色条目

如果您想要添加到现有未区分范围角色非Exchange cmdlet，使用此过程。如果您想要添加到现有未区分范围角色的脚本，请参见本主题前面的"添加脚本角色进入未区分范围的顶级角色"。

若要向无作用域的顶级角色添加非 Exchange cmdlet，必须向该角色添加管理角色条目。角色条目包含 cmdlet 管理单元、cmdlet 名称以及 cmdlet 中要供角色使用的参数。

如果向新角色添加非 Exchange cmdlet，则必须在用户为运行这些 cmdlet 而可能连接的每台 Exchange 2013 服务器上都安装这些 cmdlet。若要了解如何正确安装和注册包含您要使用的 cmdlet 的 Windows PowerShell 管理单元，请参考产品的相关文档。

将包含 cmdlet 的 Windows PowerShell 管理单元安装在相应的 Exchange 2013 服务器上并决定应使用哪些 cmdlet 参数之后，请使用以下语法创建角色条目。

```powershell
Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel
```

本示例用 *Database* 和 *Size* 参数将 Contoso.Admin.Cmdlets 管理单元中的 **Set-WidgetConfiguration** cmdlet 添加到 Widget Cmdlets 角色。

```powershell
Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel
```

> [!NOTE]  
> <strong>Add-ManagementRoleEntry</strong> cmdlet 执行基本验证，以确保仅添加该 cmdlet 中存在的参数。但是，添加角色条目之后就不再进行其他验证。如果以后要更改 cmdlet 或者添加或删除参数，则必须手动更新包含该 cmdlet 的角色条目。


## 其他任务

在添加角色条目或无作用域的顶级角色之后，您可能还需要：

[向角色添加角色](add-a-role-entry-to-a-role-exchange-2013-help.md)

[管理角色组](manage-role-groups-exchange-2013-help.md)

[管理角色组成员](manage-role-group-members-exchange-2013-help.md)

[向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

