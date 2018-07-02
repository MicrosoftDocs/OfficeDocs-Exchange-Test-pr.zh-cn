---
title: '共享和协作权限: Exchange 2013 Help'
TOCTitle: 共享和协作权限
ms:assetid: b7fa4b7c-1266-45bd-a14b-f66be0459cc5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150556(v=EXCHG.150)
ms:contentKeyID: 50491412
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 共享和协作权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

配置共享和协作功能所需的权限取决于要执行的步骤或要运行的 cmdlet。有关共享和协作的详细信息，请参阅[协作](collaboration-exchange-2013-help.md)和[共享](sharing-exchange-2013-help.md)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。</td>
    </tr>
    </tbody>
    </table>


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

## 共享和协作功能权限

可以使用下表中的功能来配置共享和协作功能。其中列出了配置每个功能所需的角色组。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>合作伙伴应用程序 - 配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>公用文件夹, 已启用邮件</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="public-folder-management-exchange-2013-help.md">公用文件夹管理</a></p></td>
</tr>
<tr class="even">
<td><p>站点邮箱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>站点邮箱设置策略</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
</tbody>
</table>

