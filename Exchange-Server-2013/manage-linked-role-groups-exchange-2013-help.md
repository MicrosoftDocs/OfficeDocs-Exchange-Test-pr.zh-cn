---
title: '管理链接的角色组: Exchange 2013 Help'
TOCTitle: 管理链接的角色组
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50491825
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理链接的角色组

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-09_

可以使用链接的管理角色组，使外Active Directory目录林中的通用安全组 (USG) 管理中资源Active Directory林的 Microsoft Exchange Server 2013组织的成员。通过将外部林中 USG 关联与链接的角色组，成员的 USG 被授予由分配给链接的角色组的管理角色的权限。有关链接的角色组的详细信息，请参阅[了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)。

若要创建并配置链接的角色组，您需要使用**New-RoleGroup**和**Set-RoleGroup** cmdlet。有关详细的语法和参数的信息，请参阅下列主题 ︰

  - [New-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/zh-cn/library/dd638182\(v=exchg.150\))

有关角色组相关的其他管理任务，请参阅 [权限](permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个过程的时间 ︰ 5 至 10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;角色组\&quot;条目。

  - 您不能使用 Exchange 管理中心 (EAC) 创建或配置链接的角色组。您必须使用 Exchange 管理外壳程序。

  - 至少，配置链接的角色组要求，链接的角色组将驻留在其中的资源Active Directory林和用户或 USGs 所驻留的外Active Directory林之间建立单向信任。资源林必须信任外部林。

  - 您必须具有关于外部 Active Directory 林的以下信息：
    
      - **凭据**  您必须具有用户名和密码，才能访问外Active Directory林。此信息用于**New-RoleGroup**和**Set-RoleGroup** cmdlet 的*LinkedCredential*参数。
    
      - **域控制器**  林中外Active DirectoryActive Directory域控制器必须完全限定的域名称 (FQDN)。此信息用于**New-RoleGroup**和**Set-RoleGroup** cmdlet 的*LinkedDomainController*参数。
    
      - **外 USG**  在外Active Directory目录林中包含您想要与链接的角色组关联的成员必须 USG 的完整名称。此信息用于在**New-RoleGroup**和**Set-RoleGroup** cmdlet 的*LinkedForeignGroup*参数。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建链接的角色组

## 使用命令行管理程序创建没有作用域的链接角色组

若要创建链接角色组并为其分配管理角色，请执行以下操作：

1.  将外部 Active Directory 林的凭据存储在一个变量中。
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  使用下面的语法创建链接的角色组。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  在外部 Active Directory 林中的计算机上使用 Active Directory 用户和计算机向外部 USG 添加成员或从中删除成员。

本示例执行以下操作：

  - 检索 users.contoso.com 外Active Directory林的凭据。这些凭据用于连接到外部目录林中的 DC01.users.contoso.com 域控制器。

  - 在安装了 Exchange 2013 的资源林中创建名为 Compliance Role Group 的链接角色组。

  - 将新角色组链接到 users.contoso.com 外部 Active Directory 林中的 Compliance Administrators USG。

  - 将传输规则和日记管理角色分配到新链接角色组。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## 使用命令行管理程序创建具有自定义管理作用域的链接角色组

您可以与自定义收件人管理范围和 / 或自定义配置管理范围，创建链接的角色组。若要创建链接的角色组并为其分配管理角色具有自定义的作用域，请执行以下操作 ︰

1.  将外部 Active Directory 林的凭据存储在一个变量中。
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  使用下面的语法创建链接的角色组。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  在外部 Active Directory 林中的计算机上使用 Active Directory 用户和计算机向外部 USG 添加成员或从中删除成员。

本示例执行以下操作：

  - 检索 users.contoso.com 外Active Directory林的凭据。这些凭据用于连接到外部目录林中的 DC01.users.contoso.com 域控制器。

  - 在安装了 Exchange 2013 的资源林中创建名为 Seattle Compliance Role Group 的链接角色组。

  - 将新角色组链接到 users.contoso.com 外部 Active Directory 林中的 Seattle Compliance Administrators USG。

  - 将传输规则和日记管理角色分配到具有 Seattle Recipients 自定义收件人作用域的新链接角色组。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

## 使用命令行管理程序创建具有 OU 作用域的链接角色组

您可以创建使用 OU 收件人范围的链接的角色组。要创建链接的角色组并与 OU 范围为其分配管理角色，请执行以下操作 ︰

1.  将外部 Active Directory 林的凭据存储在一个变量中。
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  使用下面的语法创建链接的角色组。
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  在外部 Active Directory 林中的计算机上使用 Active Directory 用户和计算机向外部 USG 添加成员或从中删除成员。

本示例执行以下操作：

  - 检索 users.contoso.com 外Active Directory林的凭据。这些凭据用于连接到外部目录林中的 DC01.users.contoso.com 域控制器。

  - 在安装了 Exchange 2013 的资源林中创建名为 Executives Compliance Role Group 的链接角色组。

  - 将新角色组链接到 users.contoso.com 外部 Active Directory 林中的 Executives Compliance Administrators USG。

  - 将传输规则和日记管理角色分配到具有 OU 收件人作用域 Executives OU 的新链接角色组。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

## 更改链接的角色组上的外部 USG

## 使用命令行管理程序更改链接角色组中的外部 USG

若要更改与链接角色组相关的外部 USG，请执行以下操作：

1.  将外部 Active Directory 林的凭据存储在一个变量中。
    
    ```powershell
$ForeignCredential = Get-Credential
```

2.  使用以下语法更改现有的链接的角色组上的外部 USG。
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

本示例执行以下操作：

  - 检索 users.contoso.com 外Active Directory林的凭据。这些凭据用于连接到外部目录林中的 DC01.users.contoso.com 域控制器。

  - 将 Compliance Role Group 角色组上的外部 USG 更改为 Regulatory Compliance Officers。

<!-- end list -->

```powershell
$ForeignCredential = Get-Credential
```
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential

