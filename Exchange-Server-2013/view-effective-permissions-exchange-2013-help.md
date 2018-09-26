---
title: '查看有效权限: Exchange 2013 Help'
TOCTitle: 查看有效权限
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50491374
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看有效权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-09_

使用分配给管理角色组、管理角色分配策略、通用安全组 (USG) 和直接分配给用户的管理角色授予 Microsoft Exchange Server 2013 中的权限。如果用户是角色组或 USG 的成员，或者已分配角色分配策略，则为这些用户授予权限。

根据角色组成员身份或分配策略的分配向最终用户授予大多数权限。虽然使用角色组和分配策略可以轻松向大量用户授予权限，但可能无法了解谁是角色组的成员或者已向谁分配了分配策略。这就是 **Get-ManagementRoleAssignment** cmdlet 上的 *GetEffectiveUsers* 开关发挥作用的地方。它显示通过分配给用户的角色组、分配策略和 USG 向哪些用户授予管理角色提供的权限。

使用 *Role* 参数时，*GetEffectiveUsers* 开关与 **Get-ManagementRoleAssignment** cmdlet 一起使用。通过使用特定的角色指定此开关，**Get-ManagementRoleAssignment** cmdlet 会检查分配给该角色的所有角色代理人，例如角色组、分配策略和 USG，并列出每种角色代理人的成员。

> [!NOTE]  
> <em>GetEffectiveUser</em> 开关不会列出作为链接的外部角色组成员的用户。如果找到链接角色组，会显示“所有链接组成员”，而不是用户列表。有关多个林中的权限的详细信息，请参阅<a href="understanding-multiple-forest-permissions-exchange-2013-help.md">了解多林权限</a>。


有关管理角色、角色组和分配策略的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。有关管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

是否正在寻找与管理权限相关的其他管理任务？请查看[权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色组”或“角色分配策略”条目。

  - 本主题中的此过程只能在命令行管理程序中执行。不能使用 Exchange 管理中心 (EAC) 查看有效权限。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序列出所有有效用户

若要列出授予管理角色提供的权限的所有用户，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers
```

此示例列出了授予由“邮件收件人”角色提供的权限的所有用户。

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers
```

如果要更改列表中返回的属性或将列表导出到逗号分隔值 (.csv) 文件，请参阅本主题后面的使用命令行管理程序自定义输出并显示该输出。

有关语法和参数的详细信息，请参阅[Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 使用命令行管理程序查找角色中的特定用户

若要查找管理角色授予其权限的特定用户，必须使用 **Get-ManagementRoleAssignment** cmdlet 检索所有有效用户的列表，然后通过管道将 cmdlet 的输出传递给 **Where** cmdlet。**Where** cmdlet 筛选输出并只返回指定的用户。请使用以下语法：

```powershell
    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }
```

此示例查找日记角色中的用户 David Strome。

```powershell
    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }
```

如果要更改列表中返回的属性或将列表导出到 .csv 文件，请参阅本主题后面的使用命令行管理程序自定义输出并显示该输出。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 使用命令行管理程序查找所有角色中的特定用户

若要了解用户可以从其接收权限的每个角色，必须使用 **Get-ManagementRoleAssignment** cmdlet 检索所有管理角色中的所有有效用户，然后通过管道将 cmdlet 的输出传递给 **Where** cmdlet。**Where** cmdlet 筛选输出并且只返回授予用户权限的角色分配。

```powershell
    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }
```

此示例查找向用户 Kim Akers 授予权限的所有角色分配。

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where {     Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }.EffectiveUserName -Eq "Kim Akers" }
```

如果要更改列表中返回的属性或将列表导出为 CSV 文件，请参阅本主题后面的使用命令行管理程序自定义输出并显示该输出。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 使用命令行管理程序自定义输出并显示该输出

**Get-ManagementRoleAssignment** cmdlet 的默认输出可能不包含您所需的信息。cmdlet 的输出包含其他许多您可以访问的属性。下面是一些可能有用的属性：

  - **EffectiveUserName**   用户名。

  - **角色**   授予权限的角色。

  - **RoleAssigneeName**   角色组、分配策略或分配给角色的 USG，而且包含 `EffectiveUserName` 属性中的用户。

  - **RoleAssigneeType**   表示是将角色分配给角色组、分配策略、USG 还是分配给用户。

  - **AssignmentMethod**   表示角色和角色代理人之间的分配是直接的还是间接的。

  - **CustomRecipientWriteScope**   表示创建自定义收件人写入作用域（如果有）时是否曾将其应用于角色分配。此属性中指定的作用域会覆盖 `RecipientWriteScope` 属性中指定的隐式收件人写入作用域。

  - **CustomConfigWriteScope**   表示创建自定义配置写入作用域（如果有）时是否曾将其应用于角色分配。此属性中指定的作用域会覆盖 `ConfigWriteScope` 属性中指定的隐式配置写入作用域。

  - **RecipientReadScope**   表示应用于角色的隐式收件人读取作用域。

  - **RecipientWriteScope**   表示应用于角色的隐式收件人写入作用域。

  - **ConfigReadScope**   表示应用于角色的隐式配置读取作用域。

  - **ConfigWriteScope**   表示应用于角色的隐式配置写入作用域。

若要选择希望在列表中显示的属性，使用的命令与使用命令行管理程序列出所有有效用户、使用命令行管理程序查找角色中的特定用户和使用命令行管理程序查找所有角色中的特定用户部分中的命令相似。区别是通过管道将这些命令的结果传递到 **Format-Table** 还是 **Select-Object** cmdlet。**Format-Table** cmdlet 对于将结果列表输出到屏幕上很有用。**Select-Object** cmdlet 对于将结果列表输出到 .csv 文件很有用。

这两个 cmdlet 都可以指定要查看的属性和查看属性的顺序。**Format-Table** cmdlet 可以让您以多种方式将结果显示在屏幕上，而 **Select-Object** 不会以任何方式修改输出，这在将列表通过管道传递到 .csv 文件时很有用。

有关 **Format-Table** 和 **Select-Object** cmdlet 的详细信息，请参阅[使用命令输出](working-with-command-output-exchange-2013-help.md)。

## 将自定义列表输出到屏幕上

1.  选择要查看的信息并从以下某个步骤中查找相关的命令：
    
      - 使用命令行管理程序列出所有有效用户
    
      - 使用命令行管理程序查找角色中的特定用户
    
      - 使用命令行管理程序查找所有角色中的特定用户

2.  选择要在列表中看到的属性。

3.  使用以下语法查看列表：
    
    ```powershell
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>
    ```

本示例在所有角色中查找用户 David Strome，并显示 `EffectiveUserName`、`Role`、`CustomRecipientWriteScope` 和 `CustomConfigWriteScope` 属性。

```powershell
    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 将自定义列表输出到 .csv 文件

若要将列表导出到 .csv 文件，您需要通过管道将先前列出的相应步骤中的 **Get-ManagementRoleAssignment** 命令的结果传递给 **Select-Object** cmdlet。然后，**Select-Object** cmdlet 的输出会通过管道传递给 **Export-CSV** cmdlet，这会将 .csv 输出保存到您指定的文件名中。

1.  选择要查看的信息并从以下某个步骤中查找相关的命令：
    
      - 使用命令行管理程序列出所有有效用户
    
      - 使用命令行管理程序查找角色中的特定用户
    
      - 使用命令行管理程序查找所有角色中的特定用户

2.  选择要在列表中看到的属性。

3.  使用以下语法将列表导出到 .csv 文件：
    
    ```powershell
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>
    ```

本示例在所有角色中查找用户 David Strome，并显示 `EffectiveUserName`、`Role`、`CustomRecipientWriteScope` 和 `CustomConfigWriteScope` 属性。

```powershell
    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv
```

现在，您可以在所选查看器中查看 .csv 文件。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

