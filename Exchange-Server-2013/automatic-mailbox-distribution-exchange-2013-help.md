---
title: '自动邮箱分发: Exchange 2013 Help'
TOCTitle: 自动邮箱分发
ms:assetid: f4db4636-948c-466b-839c-300c1a3a9544
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff477621(v=EXCHG.150)
ms:contentKeyID: 59636433
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自动邮箱分发

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上一次修改主题：** 2013-08-13_

创建或移动邮箱，或者对现有用户启用邮件时，需要在邮箱数据库中存储此邮箱。在 Microsoft Exchange Server 2013 中，可以选择让 Exchange 使用自动邮箱分发为您选择数据库。

使用自动邮箱分发时，Exchange 会查看组织中的邮箱数据库，使用本主题后面讨论的条件排除不适合的数据库，然后随机选择一个将使邮箱位于其上的数据库。此过程会在组织中所有适合的邮箱数据库内随机分发邮箱。

未在 **New-Mailbox** 和 **Enable-Mailbox** cmdlet 上指定 *Database* 参数或者未在 **New-MoveRequest** cmdlet 上指定 *TargetDatabase* 参数时，将使用自动分发。

> [!NOTE]  
> 仅当在 Exchange 2013 服务器上创建邮箱、将邮箱移动到 Exchange 2013 服务器或者对用户启用邮件时，才会执行自动邮箱分发。必须从运行 Exchange 2013 的服务器运行 <strong>New-Mailbox</strong>、<strong>New-MoveRequest</strong> 和 <strong>Enable-Mailbox</strong> cmdlet。Exchange 不会重新分发邮箱以基于服务器负载自动在数据库之间分配负载。


以下过程用于查找适合的邮箱数据库，其中新邮箱或移动的邮箱将位于此数据库上：

1.  Exchange 检索 Exchange 2013 组织中所有邮箱数据库的列表。

2.  标记为从分发过程中排除的任何邮箱数据库将从可用数据库列表中删除。可以控制将排除哪些数据库。有关详细信息，请参阅本主题后面的从自动分发排除数据库。

3.  适用于执行操作的管理员的数据库管理作用域外的任何邮箱数据库都将从可用数据库列表中删除。有关详细信息，请参阅本主题后面的数据库作用域。

4.  位于在其中执行操作的本地 Active Directory 站点外部的任何邮箱数据库将从可用数据库列表中删除。

5.  在剩余邮箱数据库列表中，Exchange 会随机选择一个数据库。如果数据库处于联机状态且运行状况良好，则 Exchange 将使用此数据库。如果其处于脱机状态或运行状况不佳，则将会随机选择另一个数据库。如果找不到联机或运行状况良好的数据库，则操作将失败，并出现错误。

选择邮箱数据库的过程由邮箱资源管理代理 cmdlet 扩展代理执行。`Mailbox Resources Management Agent` 是多个 cmdlet 扩展代理之一，可扩展运行中的 cmdlet 的功能。有关 cmdlet 扩展代理的详细信息，请参阅 [cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

如果始终不希望自动分发邮箱，则可以禁用`Mailbox Resources Management Agent`。禁用代理时，更改将应用于整个 Exchange 组织。有关如何禁用 cmdlet 扩展代理的详细信息，请参阅[管理 cmdlet 扩展代理](manage-cmdlet-extension-agents-exchange-2013-help.md)。

## 从自动分发排除数据库

默认情况下，自动邮箱分发可以选择本地 Exchange 2013 站点的 Active Directory 服务器上的所有联机和运行状况良好的邮箱数据库，以存储新邮箱或移动的邮箱。但是，出于各种原因，可能要从分发过程中排除某些数据库。例如，可能要将邮箱数据库指定为日记数据库，只有手动指定的邮箱应位于此数据库上。或者，可能要从轮换中暂时删除数据库，以执行计划的维护。Exchange 2013 向您提供了选项，可以使用 *IsExcludedFromProvisioning* 参数（可使用 **Set-MailboxDatabase** cmdlet 来设置该参数）从排除过程中永久或暂时排除数据库。

> [!NOTE]  
> 其他两个参数（即 <em>IsSuspendedFromProvisioning</em> 和 <em>IsExcludedFromInitialProvisioning</em>）在 <strong>Set-MailboxDatabase</strong> cmdlet 上也可用。在 Exchange 将来的版本中将删除这些参数，并且不支持它们的使用。


*IsExcludedFromProvisioning* 参数具有两个有效值，即 `$True` 和 `$False`。将该属性设置为 `$True` 时，邮箱数据库将从自动分发过程中排除。将其设置为 `$False` 时，邮箱数据库将包括在自动分发过程中。默认值为 `$False`。

要将邮箱数据库从自动分发中排除，请使用以下命令：

    Set-MailboxDatabase <database name> -IsExcludedFromProvisioning $True

从自动分发中排除邮箱数据库时，在数据库中创建邮箱或者将邮箱移动到数据库的唯一方法是，在 **New-Mailbox** 和 **Enable-Mailbox** cmdlet 上使用 *Database* 参数或者在 **New-MoveRequest** cmdlet 上使用 *TargetDatabase* 参数。

## 数据库作用域

数据库管理作用域是对自动邮箱分发过程的其他级别的控制，在 Exchange 2013 中可用。如果邮箱数据库处于联机状态且运行状况良好，位于本地 Active Directory 站点中，并且未从自动分发过程中排除，则 Exchange 2013 将检查邮箱数据库是否包括在适用于运行 cmdlet 的管理员的数据库作用域中。如果包括在数据库作用域中，则会将其包括在此管理员可用的数据库列表中。

数据库作用域是基于角色的访问控制 (RBAC) 权限模型的组成部分。有关 RBAC 和数据库作用域的详细信息，请参阅下列主题：

  - [了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

如果在本地 Active Directory 站点中有多个可用于自动分发的邮箱数据库，但是要限制一组特定的管理员可以使用哪些数据库，数据库作用域将非常有用。例如，Exchange 2013 服务器可以为多个机构提供服务，但是您只希望允许每个机构创建邮箱或者将邮箱移动到分配给它们的邮箱数据库。

默认情况下，Exchange 2013 组织中的所有管理员可以查看组织中的所有邮箱数据库。若要限制他们可以查看的数据库，并因此限制他们可以在其中创建邮箱或者将邮箱移动到的数据库，必须执行以下操作：

1.  使用 **New-ManagementScope** cmdlet 创建只包括希望管理员使用的邮箱数据库的自定义数据库管理作用域。

2.  使用下列方法之一将新数据库作用域与管理角色分配关联：
    
      - 在 **Set-ManagementRoleAssignment** cmdlet 上使用 *CustomConfigWriteScope* 参数将新数据库作用域添加到现有管理角色分配。现在，数据库作用域即应用于分配了此角色分配的管理角色组、通用安全组 (USG) 或用户。
    
      - 使用 **New-ManagementRoleAssignment** cmdlet 创建管理角色分配并使用 *CustomConfigWriteScope* 参数指定新数据库作用域。可以在管理角色和角色组、USG 或用户之间创建角色分配。

3.  如果为角色组或 USG 创建了角色分配，则将用户添加到角色组或 USG，以便角色分配和数据库作用域应用于用户。

4.  如果适用，则从可能分配了包含您不希望它们访问的数据库的数据库作用域的任何其他角色组或 USG 中，删除分配了新角色分配的用户（或者在以前的步骤中创建的角色组或 USG 的成员的用户）。

5.  验证管理员是否只对其应该具有访问权限的数据库具有访问权限。

完成这些步骤之后，分配了创建的数据库作用域的角色分配的管理员将只能在指定的数据库中创建邮箱，或者将邮箱移动到指定的数据库。

有关如何使用数据库作用域限制哪些邮箱数据库可用于管理员的详细信息，请参阅[使用数据库作用域控制自动邮箱分发](control-automatic-mailbox-distribution-using-database-scopes-exchange-2013-help.md)。

