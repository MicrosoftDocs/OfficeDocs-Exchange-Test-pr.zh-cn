---
title: '为 Exchange 2013 配置拆分权限: Exchange 2013 Help'
TOCTitle: 为 Exchange 2013 配置拆分权限
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50491004
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 Exchange 2013 配置拆分权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

拆分权限使两个不同的组（如 Active Directory 管理员和 Microsoft Exchange Server 2013 管理员）能够管理各自的服务、对象和属性。Active Directory 管理员管理安全主体（如用户），这种安全主体可提供访问 Active Directory 林的权限。Exchange 管理员管理 Active Directory 对象上与 Exchange 相关的属性以及 Exchange 特定的对象创建和管理。

Microsoft Exchange Server 2013 提供下列类型的拆分权限模型：

  - **RBAC 拆分权限**   在 Active Directory 域分区中创建安全主体的权限由基于角色的访问控制 (RBAC) 控制。只有相应角色组的成员才能创建安全主体。

  - **Active Directory 拆分权限**   从任何 Active Directory 用户、服务或服务器完全删除了用于在 Exchange 域分区中创建安全主体的权限。RBAC 中未提供用于创建安全主体的任何选项。必须使用 Active Directory 管理工具在 Active Directory 中创建安全主体。
    
    > [!NOTE]  
    > Active Directory 拆分权限在运行 Microsoft Exchange Server 2010 Service Pack 1 (SP1) 或更高版本、Exchange 2013 或同时运行这两种 Exchange 版本的组织中可用。


您选择的模型取决于您组织的结构和需求。请根据想要配置的模型从下面选择适用的过程。我们建议您使用 RBAC 拆分权限模型。RBAC 拆分权限模型提供极大的灵活性，同时还提供与 Active Directory 拆分权限相同的管理分离。

有关共享和拆分权限的详细信息，请参阅[了解拆分权限](understanding-split-permissions-exchange-2013-help.md)。

有关管理角色组、管理角色以及常规和委派管理角色分配的详细信息，请参阅下列主题：

  - [了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)

  - [了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

若要了解与权限相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的“Active Directory 拆分权限”条目。

  - 您必须使用 Windows PowerShell 和/或 Windows 命令行管理程序执行这些过程。有关详细信息，请参阅每个过程。

  - 如果您组织中有 Exchange 2010 服务器，则所选择的权限模型也会应用于这些服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 切换到 RBAC 拆分权限

您可以为您的 Exchange 2013 组织配置 RBAC 拆分权限。配置拆分权限后，将只有 Active Directory 管理员能够创建 Active Directory 安全主体。这意味着 Exchange 管理员不能使用以下 cmdlet：

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Exchange 管理员将只能管理现有 Active Directory 安全主体上的 Exchange 属性。但是，这些管理员能够创建和管理 Exchange 特定的对象，如传输规则和通讯组。有关详细信息，请参阅[了解拆分权限](understanding-split-permissions-exchange-2013-help.md)中的“RBAC 拆分权限”一节。

若要配置 Exchange 2013 的拆分权限，必须将 Mail Recipient Creation 角色和 Security Group Creation and Membership 角色分配给包含 Active Directory 管理员成员的角色组。然后，必须删除这些角色与任何包含 Exchange 管理员的角色组或通用安全组 (USG) 之间的分配。

要配置 RBAC 拆分权限，请执行以下操作：

1.  如果组织目前已经配置了 Active Directory 拆分权限，请从 Windows 命令行管理程序提示符执行下列操作：
    
    1.  从 Exchange 2013 安装介质运行下列命令禁用 Active Directory 拆分权限。
        
        ```powershell
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
        ```
    
    2.  在组织中重新启动 Exchange 2013 服务器或等待 Active Directory 访问令牌复制到所有 Exchange 2013 服务器。
        
        > [!NOTE]  
        > 如果您组织中有 Exchange 2010 服务器，则还需要重启这些服务器。


2.  从 Exchange 命令行管理程序中执行以下操作：
    
    1.  为 Active Directory 管理员创建角色组。除了创建角色组之外，该命令还可以在新角色组与 Mail Recipient Creation 角色和 Security Group Creation and Membership 角色之间创建常规角色分配。
        ```powershell
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        ```
        > [!NOTE]  
        > 如果想要使此角色组的成员能够创建角色分配，请添加“角色管理”角色。现在不必添加此角色。但是，如果要将“邮件收件人创建”角色或“安全组创建和成员身份”角色分配给其他角色接受者，则必须将“角色管理”角色分配到此新角色组。以下步骤将“Active Directory Administrators”角色组作为可以委派这些角色的唯一角色组进行配置。
    
    2.  使用以下命令在新角色组和“邮件收件人创建”角色以及“安全组创建和成员身份”角色之间创建委派角色分配。
        ```powershell
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
        ```
    3.  使用以下命令将成员添加到新角色组。
        
        ```powershell
        Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
        ```
    
    4.  替换新角色组上的委派列表，以使只有该角色组的成员可以添加或删除成员。
        
        ```powershell
        Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        ```
        
        > [!IMPORTANT]  
        > 组织管理 角色组的成员，或者直接或通过另一角色组或 USG 获得 Role Management 角色的成员可以绕过这一委派安全检查。如果想要阻止所有 Exchange 管理员将其自身添加到该新角色组，则必须删除“角色管理”角色和所有 Exchange 管理员之间的角色分配，并将其分配给另一个角色组。
    
    5.  使用以下命令查找所有分配给 Mail Recipient Creation 角色的常规和委派角色分配。该命令只显示 **Name**、**Role** 和 **RoleAssigneeName** 属性。
        ```powershell
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
        ```
    6.  使用以下命令删除所有分配给 Mail Recipient Creation 角色，且与该新角色组或您想要保留的任何其他角色组、USG 或直接分配不相关联的常规和委派角色分配。
        
        ```powershell
        Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        ```
        
        > [!NOTE]  
        > 如果想要删除所有分配给任何角色接受者（“Active Directory Administrators”角色组除外）的“邮件收件人创建”角色的常规和委派角色分配，请使用以下命令。<em>WhatIf</em> 开关使您能够看到将删除哪些角色分配。删除 <em>WhatIf</em> 开关，然后重新运行该命令以删除角色分配。

        ```powershell
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```
    7.  使用以下命令查找所有分配给“安全组创建和成员身份”角色的常规和委派角色分配。该命令只显示 **Name**、**Role** 和 **RoleAssigneeName** 属性。
        ```powershell
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
        ```
    8.  使用以下命令删除所有分配给“安全组创建和成员身份”角色，且与该新角色组或您想要保留的任何其他角色组、USG 或直接分配不相关联的常规和委派角色分配。
        ```powershell
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        ```
        > [!NOTE]  
        > 您可以使用以上注意中的命令，删除所有分配给任何角色分配（“Active Directory Administrators”角色组除外）的“安全组创建和成员身份”角色的常规和委派角色分配，如此示例中所示。
        ```powershell
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```
有关语法和参数的详细信息，请参阅下列主题：

  - [New-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/zh-cn/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd351205\(v=exchg.150\))

## 切换到 Active Directory 拆分权限

您可以为您的 Exchange 2013 组织配置 Active Directory 拆分权限。Active Directory 拆分权限完全删除以下权限：允许 Exchange 管理员和服务器在 Active Directory 中创建安全主体或在这些对象上修改非 Exchange 属性的权限。配置拆分权限后，将只有 Active Directory 管理员能够创建 Active Directory 安全主体。这意味着 Exchange 管理员不能使用以下 cmdlet：

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Exchange 管理员和服务器将只能管理现有 Active Directory 安全主体上的 Exchange 属性。但是，这些管理员和服务器将能够创建和管理特定于 Exchange 的对象，如传输规则和统一消息拨号计划。

> [!CAUTION]  
> 启用 Active Directory 拆分权限后，Exchange 管理员和服务器将不能再在 Active Directory 中创建安全主体，并且他们将不能管理通讯组成员身份。必须使用具有所需 Active Directory 权限的 Active Directory 管理工具执行这些任务。进行此更改之前，应该了解此更改将对与 Exchange 2013 相集成的管理流程和第三方应用程序以及 RBAC 权限模型产生的影响。
> 有关详细信息，请参阅<a href="understanding-split-permissions-exchange-2013-help.md">了解拆分权限</a>中的“Active Directory 拆分权限”一节。


要从共享或 RBAC 拆分权限切换到 Active Directory 拆分权限，请执行以下操作：

1.  在 Windows 命令行管理程序中，从 Exchange 2013 安装介质运行下列命令启用 Active Directory 拆分权限。
    
    ```powershell
    setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true
    ```

2.  如果组织中有多个 Active Directory 域，必须在每个包含 Exchange 服务器或对象的子域中运行 `setup.exe /PrepareDomain`，或者从每个域中均有一台 Active Directory 服务器的站点运行 `setup.exe /PrepareAllDomains`。

3.  在组织中重新启动 Exchange 2013 服务器或等待 Active Directory 访问令牌复制到所有 Exchange 2013 服务器。
    
    > [!NOTE]  
    > 如果您组织中有 Exchange 2010 服务器，则还需要重启这些服务器。

