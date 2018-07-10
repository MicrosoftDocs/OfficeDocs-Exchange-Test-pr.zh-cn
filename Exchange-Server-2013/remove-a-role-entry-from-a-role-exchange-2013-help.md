---
title: '从角色中删除一个角色条目: Exchange 2013 Help'
TOCTitle: 从角色中删除一个角色条目
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50490463
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从角色中删除一个角色条目

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色项目管理角色确定 cmdlet 和参数上的管理角色。通过删除角色条目或角色输入参数，您可以限制哪些用户分配管理角色可以执行。有关 Microsoft Exchange Server 2013中的管理角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 从角色中删除一个完整的角色项

从角色中删除角色项时，分配了该角色的用户将失去访问关联 cmdlet 或脚本的能力。

使用以下语法从角色中删除整个管理角色条目。

    Remove-ManagementRoleEntry <management role>\<management role entry>

此示例从 Seattle Server Administrators 角色中删除 **Enable-MailUser** cmdlet。

    Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"

有关语法和参数的详细信息，请参阅[Remove-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351187\(v=exchg.150\))。

## 从角色中删除多个完整的角色项

从角色中删除多个角色项时，分配了该角色的用户将失去访问关联 cmdlet 或脚本的能力。

若要从角色中删除多个角色条目，您需要检索的角色去使用**Get-ManagementRoleEntry** cmdlet 的项的列表。然后，您需要将输出传输到**Remove-ManagementRoleEntry** cmdlet。可以使用**Get-ManagementRoleEntry** cmdlet 使用通配符来匹配多个角色条目。它是一个好主意，使用*WhatIf*开关来确认您要删除的正确角色条目。使用以下语法。

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

此示例从 Seattle Server Administrators 角色中删除包含文字\&quot;journal\&quot;的所有角色项。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

使用*WhatIf*开关运行该命令时，该 cmdlet 返回列表中的角色的所有条目都将被删除。如果列表看起来正确，运行再次不使用*WhatIf*开关命令，以删除角色条目。

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

有关语法和参数的详细信息，请参阅[Get-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd335210\(v=exchg.150\))和[Remove-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351187\(v=exchg.150\))。

## 删除角色中一个角色项上的参数

删除角色中一个角色项上的参数时，这些参数对于分配该角色的用户将不再可用。

使用以下语法从角色项中删除参数。

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

此示例从 Seattle Server Administrators 角色上的 **Set-Mailbox** 角色项中删除 *MaxSafeSenders*、*MaxSendSize*、*SecondaryAddress* 和 *UseDatabaseQuotaDefaults* 参数。

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

有关语法和参数的详细信息，请参阅[Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

