---
title: '更改角色条目: Exchange 2013 Help'
TOCTitle: 更改角色条目
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50490629
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改角色条目

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色中的每个管理角色条目表示一个 cmdlet。通过添加参数或删除参数从角色项，然后添加到管理角色，您可以控制这些参数是否可在该 cmdlet。有关 Microsoft Exchange Server 2013中的管理角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

无法修改内置管理角色上的角色条目。

> [!NOTE]  
> 本主题不讨论如何修改未区分范围的管理角色条目未区分范围的管理角色。有关如何修改未区分范围的角色条目的详细信息，请参阅<a href="create-a-role-exchange-2013-help.md">创建角色</a>。


> [!CAUTION]  
> 若要添加或从角色中移除参数，必须使用<em>AddParameter</em>或<em>RemoveParameter</em>参数。如果您运行<strong>Set-ManagementRoleEntry</strong> cmdlet 时省略了使用<em>AddParameter</em>或<em>RemoveParameter</em>参数，仅使用<em>Parameters</em>参数指定的参数将包括角色条目中。该角色条目中的所有其他参数都将被删除。


若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 如果您想要将参数添加到角色条目，您添加的参数必须位于父角色中的角色条目。参数必须也存在于您指定 cmdlet。

  - 如果您想要从角色中移除参数，删除的参数不能存在任何子角色的角色条目中。您必须从孩子角色的角色项移除参数。本主题后面部分中使用"使用外壳程序从角色中移除一个或多个参数"过程，若要从所有子角色的角色项中移除参数。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序向角色条目添加一个或多个参数

若要将参数添加到角色条目，您需要指定您想要使用*Parameters*参数添加的参数。然后，您需要指定*AddParameter*参数，以指示您要执行添加操作。

若要向角色条目添加参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter

此示例将 *EmailAddresses* 和 *Type* 参数添加到收件人管理员角色上的 **Set-Mailbox** cmdlet。

    Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序删除角色条目中的一个或多个参数

若要从角色中移除参数，您需要指定您想要使用*Parameters*参数中移除的参数。然后，您需要指定*RemoveParameter*参数来指示要执行的删除操作。

若要删除角色条目中的参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter

此示例将 *Port*、*ProtocolLoggingLevel* 及 *SmartHostAuthMechanism* 参数从 Tier 1 Server Administrators 角色上的 **Set-SendConnector** cmdlet 中删除。

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序删除角色条目中的所有参数

若要从角色中删除所有参数，您需要在*Parameters*参数中指定值`$Null` 。您不需要使用*RemoveParameters*参数。

当您想要使几个参数只能出现在 cmdlet 并排除所有其他参数，从角色中删除所有参数是最有用。如果您不想要有权 cmdlet 的角色，而只删除参数不是完全在角色中删除关联的角色条目。有关如何从角色中删除一个角色条目的详细信息，请参阅[从角色中删除一个角色条目](remove-a-role-entry-from-a-role-exchange-2013-help.md)。

> [!CAUTION]  
> 您不能撤消删除操作。如果错误地从角色条目中删除所有参数，您必须再次手动添加它们。


若要删除角色条目中的所有参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 

此示例对 Recipient Administrators 角色删除 **Set-CASMailbox** cmdlet 中的所有参数。

    Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

## 使用命令行管理程序应用特定的一组参数

如果您希望仅一组特定的参数将被包括在一个角色条目，指定*Parameters*参数只。不要包含*AddParameter*或*RemoveParameter*参数。指定只有*Parameters*参数时，只在命令中指定的参数包含在角色条目。所有其它参数将被移除。

若要指定一组特定的参数，请使用以下语法。

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

此示例使 Seattle Mail Recipients 角色上的 **Set-UMMailbox** cmdlet 中仅包括 *Identity*、*DisplayName*、*MissedCallNotificationEnabled* 和 *PersonalAuthAttendantEnabled* 参数。

    Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled

有关语法和参数的详细信息，请参阅 [Set-ManagementRoleEntry](https://technet.microsoft.com/zh-cn/library/dd351162\(v=exchg.150\))。

