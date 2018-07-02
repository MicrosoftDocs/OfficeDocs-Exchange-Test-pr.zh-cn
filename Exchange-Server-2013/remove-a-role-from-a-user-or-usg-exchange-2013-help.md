---
title: '从用户或 USG 删除角色: Exchange 2013 Help'
TOCTitle: 从用户或 USG 删除角色
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50491773
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从用户或 USG 删除角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-02_

管理角色分配给用户或通用安全组 (USG) 分配管理角色。如果您删除角色分配，分配该角色的用户将不再有权使用的 cmdlet 上该角色。有关 Microsoft Exchange Server 2013中的管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成这一过程的时间 ︰ 5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色分配\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 删除管理角色分配

如果您知道要删除的角色分配的名称，请使用以下语法。

    Remove-ManagementRoleAssignment <assignment name>

例如，若要删除\&quot;Tier 2 Help Desk Assignment\&quot;角色分配，请使用以下命令。

    Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"

如果您不知道角色分配的名称，可以使用以下语法。

    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 

例如，如果要从用户 Davids 删除邮件收件人常规角色分配，请使用以下命令。

    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment

