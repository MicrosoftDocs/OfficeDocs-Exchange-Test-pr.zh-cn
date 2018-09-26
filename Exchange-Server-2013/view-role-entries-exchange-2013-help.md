---
title: '查看角色条目: Exchange 2013 Help'
TOCTitle: 查看角色条目
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 50491659
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看角色条目

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色的每个条目表示一个 cmdlet 或脚本。在角色条目中包含的参数确定在用户可以访问哪些 cmdlet 或脚本的参数。

角色条目标识包含角色条目相关联，管理角色名称的 cmdlet 或角色条目所引用的脚本。有关 Microsoft Exchange Server 2013中的角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

寻找与角色条目相关的其他管理任务？检出[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 本主题将使用流水线、 **Format-List** cmdlet、 对象和属性。有关这些概念的详细信息，请参阅下列主题 ︰
    
      - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))
    
      - [使用命令输出](working-with-command-output-exchange-2013-help.md)
    
      - [结构化数据](https://technet.microsoft.com/zh-cn/library/aa996386\(v=exchg.150\))

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 查看角色项列表

您可以使用**Get-ManagementRoleEntry** cmdlet 检索角色条目的列表。当您使用**Get-ManagementRoleEntry** cmdlet 时，必须指定一个包含两个角色名称包含到列表所需的角色条目和也要列出该角色条目的 cmdlet 名称的值。通过结合使用通配符 （\*） 的角色名称和 cmdlet 名称，您可以返回特定或广泛个角色条目列表。

有关详细的语法和参数信息，请参阅[Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

## 查看角色的所有角色项列表

若要查看特定角色的角色项列表，请使用以下语法。

```powershell
Get-ManagementRoleEntry <role name>\*
```

此示例检索 `Recipient Administrators` 角色的所有角色项。

```powershell
Get-ManagementRole "Recipient Administrators\*"
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

## 查看包含特定角色项的角色的列表

若要查看包含特定角色项的所有角色的列表，请使用以下语法。

```powershell
Get-ManagementRoleEntry *\<cmdlet name>
```

此示例检索包含 **Set-Mailbox** 角色项的所有角色。

```powershell
Get-ManagementRoleEntry *\Set-Mailbox
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

## 查看包含相似角色项的角色的目标列表

若要查看包含具有相似名称的 cmdlet 的角色的目标列表，请使用以下语法。

```powershell
Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*
```

此示例返回包含字符串 `Mailbox` 的角色项的列表，这些角色项又是名称中包含字符串 `Tier 1` 的角色的角色项。

```powershell
Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"
```

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

## 查看单个角色项

若要查看单个角色项的详细信息，请使用以下语法。

```powershell
Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List
```

此示例检索 `Recipient Administrators` 角色的 **Set-Mailbox** 角色项的详细信息。

```powershell
Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List
```

如果所查看的角色项的参数太多，以至于无法使用 **Format-List** cmdlet 列出，请参阅本主题后面的\&quot;查看单个角色项的参数\&quot;。

有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

## 查看单个角色项的参数

角色中的某些条目具有多个参数不是可以通过管道向**Format-List** cmdlet **Get-ManagementRoleEntry** cmdlet 的结果。如果您需要查看在角色条目中的所有参数，您需要直接访问角色输入对象的**Parameters**属性。

若要查看角色项对象的 **Parameters** 属性中存储的参数，请使用以下语法。

```powershell
(Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters
```

此示例检索 Mail Recipients 角色的 **Set-Mailbox** 角色项的参数。

```powershell
(Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters
```
有关语法和参数的详细信息，请参阅 [Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))。

