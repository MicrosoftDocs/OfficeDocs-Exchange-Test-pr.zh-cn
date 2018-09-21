---
title: '查看角色分配: Exchange 2013 Help'
TOCTitle: 查看角色分配
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 50489899
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看角色分配

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色分配向角色受理人分配一个管理角色。有关 Microsoft Exchange Server 2013 中管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色分配\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 本主题使用了管道传输和 **Format-List** cmdlet。有关这些概念的详细信息，请参阅下列主题：
    
      - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))
    
      - [使用命令输出](working-with-command-output-exchange-2013-help.md)

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 查看所有角色分配的列表

通过运行 **Get-ManagementRoleAssignment** cmdlet，可以在组织中查看配置的所有角色分配的列表。如果要检索与指定的部分字符串匹配的角色分配列表，请使用通配符 (\*)。此示例将检索以字符串 "Tier 1" 开头的所有角色分配的列表。

    Get-ManagementRoleAssignment "Tier 1*"

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看特定角色分配的详细信息

可以查看某个角色分配的详细信息，方法是通过管道将 **Get-ManagementRoleAssignment** cmdlet 的结果传递给 **Format-List** cmdlet。请使用以下语法：

```powershell
Get-ManagementRoleAssignment <assignment name> | Format-List
```

此示例将检索 Help Desk Assignment 角色分配的详细信息。

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看分配给特定角色受理人的角色分配列表

若要查看与管理角色组、角色或角色分配策略相关联的角色分配列表，或与用户或通用安全组 (USG) 相关联的角色分配列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -RoleAssignee <role assignee name>
```

此示例将检索与\&quot;服务器管理\&quot;角色组相关联的所有角色分配。

```powershell
Get-ManagementRoleAssignment -RoleAssignee "Server Management"
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看与特定角色相关联的角色分配

每个角色都可以具有多个角色分配。可以使用 **Get-ManagementRoleAssigment** cmdlet 查看与指定的角色相关联的角色分配列表。

若要查看与指定的角色相关联的角色分配列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -Role <role name>
```

此示例将检索与\&quot;邮件收件人\&quot;角色相关联的所有角色分配。

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients"
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看使用特定预定义作用域的角色分配列表

若要查看使用特定预定义作用域的角色分配列表，请使用以下语法。

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

此示例将检索使用\&quot;组织\&quot;预定义作用域的所有角色分配。

```powershell
Get-ManagementRoleAssignment -RecipientWriteScope Organization
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看已将作用域限制为特定 OU 的角色分配列表

若要查看已将作用域限制为特定组织单位 (OU) 的角色分配列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>
```

此示例将检索已在 contoso.com 域中将作用域限制为 North America\\Engineering\\Users OU 的所有角色分配。

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看使用特定自定义作用域的分配列表

若要查看使用特定自定义作用域的角色分配列表，需要先确定作用域是收件人作用域、配置作用域、独占收件人作用域，还是独占配置作用域。每个类型的作用域会在 **Get-ManagementRoleAssignment** cmdlet 上使用不同的参数。下面列出了每个作用域及其关联的参数：

  - **收件人作用域：**  *CustomRecipientWriteScope*

  - **配置作用域：**  *CustomConfigWriteScope*

  - **独占收件人作用域：**  *ExclusiveRecipientWriteScope*

  - **独占配置作用域：**  *ExclusiveConfigWriteScope*

每个参数的语法都是相同的。使用与作用域类型匹配的参数指定此作用域的名称。

此示例将检索使用 Vancouver Recipients 收件人作用域的所有角色分配。

```powershell
Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"
```

此示例将检索使用 Seattle AD Site 独占配置作用域的所有角色分配。

```powershell
Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看独占作用域或常规作用域的列表

若要查看独占角色分配或常规角色分配的列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -Exclusive < $True | $False >
```

例如，要查看独占作用域的列表，请运行以下命令：

```powershell
Get-ManagementRoleAssignment -Exclusive $True
```

此示例将检索不具有任何独占作用域的常规作用域列表。

```powershell
Get-ManagementRoleAssignment -Exclusive $False
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看可以修改特定收件人或服务器的角色分配

若要查看可以修改特定收件人或服务器的角色分配列表，请使用 *WritableRecipient* 和 *WritableServer* 参数。使用 *WritableRecipient* 参数指定收件人的名称，并使用 *WritableServer* 参数指定服务器的名称。

此示例将检索可以修改收件人 Brian 的角色分配列表。

```powershell
Get-ManagementRoleAssignment -WritableRecipient "Brian"
```

可以将 *WritableRecipient* 和 *WritableServer* 参数与其他参数（如 *RoleAssignee* 参数和 *GetEffectiveUsers* 开关）组合，以优化查询，并展开任何角色组或 USG。此示例将检索可以修改服务器 EX02 的所有用户，以及分配了\&quot;服务器管理\&quot;角色组的所有用户。

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看通过角色组或 USG 从分配接收权限的用户

若要查看从角色分配接收权限的用户列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers
```

此示例将检索 Help Desk Assignment 角色分配中的用户列表。

```powershell
Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers
```

还可以将 *GetEffectiveUsers* 开关与 **Get-ManagementRoleAssignment** cmdlet 上的某些其他参数组合，以展开角色分配所分配到的角色组和 USG。有关如何将 *GetEffectiveUsers* 开关与其他参数配合使用的示例，请参阅本主题前面的\&quot;查看可以修改特定收件人或服务器的角色分配\&quot;。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

## 查看已启用或已禁用角色分配的列表

若要查看已启用或已禁用角色分配的列表，请使用以下语法。

```powershell
Get-ManagementRoleAssignment -Enabled < $True | $False >
```

此示例将检索已禁用的角色分配列表。

```powershell
Get-ManagementRoleAssignment -Enabled $False
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))。

