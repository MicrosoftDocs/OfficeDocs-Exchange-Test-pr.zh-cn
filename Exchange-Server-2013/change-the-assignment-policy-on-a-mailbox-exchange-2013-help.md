---
title: '更改邮箱的分配策略: Exchange 2013 Help'
TOCTitle: 更改邮箱的分配策略
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50489829
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改邮箱的分配策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-08_

您可以更改已分配给邮箱的管理角色分配策略。在更改邮箱的分配策略时，所做更改会在用户刷新连接（如用户下次登录到其邮箱或打开邮箱选项页）之后立即生效。有关 Microsoft Exchange Server 2013 中的分配策略的详细信息，请参阅[了解管理角色分配策略](understanding-management-role-assignment-policies-exchange-2013-help.md)。

若要了解与权限相关的其他管理任务，请查看[权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“角色组”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 EAC 更改邮箱的分配策略

1.  在 Exchange 管理中心 (EAC) 中，导航到“收件人”\>“邮箱”。

2.  选择要更改其分配策略的用户或资源邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  选择“邮箱功能”。

4.  在“角色分配策略”列表中，选择要分配给邮箱的分配策略，然后单击“保存”。

## 使用命令行管理程序更改邮箱的分配策略

若要更改已分配到邮箱的分配策略，请使用以下语法。

```powershell
Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>
```

此示例将邮箱 Brian 上的分配策略设置为“统一消息用户”。

```powershell
Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"
```

## 使用命令行管理程序可在分配了特定分配策略的一组邮箱上更改分配策略

> [!NOTE]  
> 不能使用 EAC 一次更改一组邮箱的分配策略。


此过程使用了管道传输、**Where** cmdlet 和 *WhatIf* 参数。有关这些概念的详细信息，请参阅下列主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

  - [WhatIf、Confirm 和 ValidateOnly 开关](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

如果要为分配了特定策略的一组邮箱更改分配策略，则使用以下语法。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>

此示例将查找所有已分配了“Redmond 用户 - 无语音邮件”分配策略的邮箱，并更改对“Redmond 用户 - 已启用语音邮件”的分配策略。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"

此示例包括 *WhatIf* 参数，以便可以查看所有在不提交任何更改的情况下进行更改的邮箱。

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

