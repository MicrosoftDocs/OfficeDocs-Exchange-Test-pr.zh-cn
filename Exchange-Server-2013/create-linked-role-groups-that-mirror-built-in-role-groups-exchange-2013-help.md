---
title: '创建链接的角色组的镜像内置角色组: Exchange 2013 Help'
TOCTitle: 创建链接的角色组的镜像内置角色组
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50491124
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建链接的角色组的镜像内置角色组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

在 Microsoft Exchange Server 2013中使用链接的管理角色组，可以在外部用户目录林中链接与通用安全组 (USG) Exchange 2013资源目录林中的角色组。当您希望用户目录林中的帐户管理员管理服务器资源目录林中运行Exchange时，这非常有用。有关链接的角色组的详细信息，请参阅[了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)。

默认情况下， Exchange 2013包括大量的内置角色组的权限来管理不同的功能和工作职能为您提供。每个角色组定制提供功能和作业的每个函数的特定权限。但是，这些角色组无法链接到 USGs 外的树林中。他们只能包含用户和从本地资源的林 USGs。幸运的是，就可以复制这些内置角色组使用链接的角色组。

作为一个链接的角色组，您可以重新创建每个内置角色组。所有管理角色和管理作用域分配给每个角色组添加到新组中链接的角色。关于管理角色和作用域的详细信息，请参阅下列主题 ︰

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

寻找与角色组相关的其他管理任务？检出[权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色组\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 配置链接的角色组，需要将驻留在其中的链接的角色组，资源Active Directory林和用户或 USGs 驻留外Active Directory林之间的单向信任。资源林必须信任外部林。

  - 您必须具有关于外部 Active Directory 林的以下信息：
    
      - **凭据**  您必须具有用户名和密码，才能访问外Active Directory林。此信息用于**New-RoleGroup** cmdlet 的*LinkedCredential*参数。通过运行**Get-Credential** cmdlet 来获得此信息。用户名称的格式是*domain*\\*username*。
    
      - **域控制器**  林中外Active DirectoryActive Directory域控制器必须完全限定的域名称 (FQDN)。此信息用于**New-RoleGroup** cmdlet 的*LinkedDomainController*参数。
    
      - **外 USG**  在外Active Directory目录林中包含您想要与链接的角色组关联的成员必须 USG 的完整名称。此信息用于**New-RoleGroup** cmdlet 的*LinkedForeignGroup*参数。

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


## 使用命令行管理程序创建复制内置角色组的链接角色组

以下各部分将演示如何重新创建链接的角色组的每个角色组。完成重新创建所有内置角色组的链接的角色组的每个节中的过程。

## 创建组织管理链接角色组

要重新创建链接的角色组的组织管理角色组，您需要执行的过程，是不同于用于重新创建其他内置角色组的过程。这是因为组织管理角色组委派它之间的所有管理角色的角色分配。重新创建委托的角色分配需要额外的步骤。

1.  在外部林中创建将链接到 组织管理 角色组的 USG。

2.  将外部 Active Directory 林的凭据存储在一个变量中。
    
        $ForeignCredential = Get-Credential

3.  将分配到 组织管理 角色组的所有角色存储在一个变量中。
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  创建 组织管理 链接角色组并添加分配到内置 组织管理 角色组的角色。
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  删除新 组织管理 链接角色组与 My\* 最终用户角色之间的所有常规分配。
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  在新 组织管理 链接角色组和所有管理角色之间添加委派角色分配。
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

本示例假定以下值分别用于每个参数：

  - **LinkedForeignGroup：**  `Organization Management Administrators`

  - **LinkedDomainController：**  `DC01.users.contoso.com`

通过使用前面的值，本示例可将 组织管理 角色组重新创建为链接角色组。

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## 创建其他所有链接角色组

若要将内置角色组（组织管理 角色组除外）重新创建为链接角色组，请使用以下用于每个组的步骤。

1.  在各个角色组的外部林中创建将链接到各个新角色组的 USG。

2.  外Active Directory林凭据存储在一个变量中。您只需执行一次。
    
        $ForeignCredential = Get-Credential

3.  使用以下 cmdlet 检索角色组列表。
    
        Get-RoleGroup

4.  对于每个角色组（组织管理 角色组除外），执行以下操作：
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  对于每个您要将其重新创建为链接角色组的内置角色组，可重复前面的步骤。

本示例假定以下值分别用于每个参数：

  - **LinkedDomainController：**  `DC01.users.contoso.com`

  - **要重新创建为链接角色组的内置角色组：**  `Recipient Management, Server Management`

  - **Recipient Management 链接角色组的外部组：**  `Recipient Management Administrators`

  - **Server Management 链接角色组的外部组：**  `Server Management Administrators`

通过使用前面的值，本示例可将 收件人管理 和 Server Management 角色组重新创建为链接角色组。

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## 其他任务

创建链接角色组之后，您可能还需要：

使用外部林中的 Active Directory 用户和计算机向外部 USG 中添加成员。

删除内置角色组的成员。有关详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

添加、 删除或更改对新链接的角色组的角色的范围。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

创建附加链接的角色组。有关详细信息，请参阅[管理链接的角色组](manage-linked-role-groups-exchange-2013-help.md)。

