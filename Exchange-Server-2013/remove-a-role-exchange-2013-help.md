---
title: '删除角色: Exchange 2013 Help'
TOCTitle: 删除角色
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50490142
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

不再需要的管理角色可以从组织中删除。您只能删除您创建的管理角色。不能删除内置管理角色。有关 Microsoft Exchange Server 2013 中管理角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“管理角色”条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 在可以删除管理角色之前，必须删除其所有的管理角色分配。有关如何删除角色分配的详细信息，请参阅[从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 删除没有子角色的管理角色

要删除没有子角色的角色，请使用以下语法。

    Remove-ManagementRole <role name>

本示例删除 Seattle Server Administrators 角色。

    Remove-ManagementRole "Seattle Server Administrators"

有关语法和参数的详细信息，请参阅 [Remove-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351170\(v=exchg.150\))。

## 删除具有子角色的管理角色

如果要删除的角色有子角色，则还必须删除所有的子角色。尝试删除有子角色的角色时，必须使用 *Recurse* 开关，否则会收到错误消息。如果在删除角色时使用 *Recurse* 开关，则将删除指定的角色和其所有子角色。

> [!CAUTION]  
> 如果使用 <em>Recurse</em> 开关，则还将删除要删除的指定角色的所有子角色。在运行此命令之前，确保您了解将要删除的角色。


要确保仅删除希望删除的角色，请将 *WhatIf* 开关与您的命令配合使用以验证命令是否正确。请使用以下语法：

    Remove-ManagementRole <role name> -Recurse -WhatIf

*WhatIf* 开关将在不提交任何更改的情况下执行该命令并报告哪些角色已经删除。有关 *WhatIf* 开关的详细信息，请参阅[WhatIf、Confirm 和 ValidateOnly 开关](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)。

在确认将仅删除希望删除的角色之后，在不使用 *WhatIf* 开关的情况下运行相同的命令。本示例删除 London Administrators 角色和其所有子角色。

    Remove-ManagementRole "London Administrators" -Recurse

有关语法和参数的详细信息，请参阅 [Remove-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351170\(v=exchg.150\))。

## 删除无作用域的管理角色

要删除无作用域的角色，可以使用本主题中前面提供的 删除没有子角色的管理角色 和 删除具有子角色的管理角色 中的相同步骤。唯一的区别在于，如果要删除无作用域的角色，则必须在运行此命令时指定 *UnScopedTopLevel* 开关。本示例删除无作用域的角色和其所有子角色。

    Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel

与删除其他角色一样，应该使用 *WhatIf* 开关验证是否正在删除正确的角色。

有关语法和参数的详细信息，请参阅 [Remove-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351170\(v=exchg.150\))。

