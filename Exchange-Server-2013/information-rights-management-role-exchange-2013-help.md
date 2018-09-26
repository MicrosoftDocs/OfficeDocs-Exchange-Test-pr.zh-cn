---
title: '信息权限管理角色: Exchange 2013 Help'
TOCTitle: 信息权限管理角色
ms:assetid: bb40c2ec-1eb8-43d4-af7c-4fa74c7c3ce2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876934(v=EXCHG.150)
ms:contentKeyID: 50491521
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 信息权限管理角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

`Information Rights Management` 管理角色使管理员能够管理组织中 Exchange 的信息权限管理 (IRM) 功能。

此管理角色是 Microsoft Exchange Server 2013 中基于角色的访问控制 (RBAC) 权限模型中的多个内置角色之一。管理角色分配到一个或多个管理角色组、管理角色分配策略、用户或通用安全组 (USG)，充当 cmdlet 或脚本的逻辑分组，这些 cmdlet 或脚本的组合可用于查看或修改 Exchange 2013 组件的配置，如邮箱数据库、传输规则和收件人。如果 cmdlet 或脚本及其参数（统称为管理角色条目）包含在某个角色上，则该 cmdlet 或脚本及其参数可由该角色的分配人运行。有关管理角色和管理角色条目的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

有关管理角色、管理角色组和其他 RBAC 组件的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 管理角色分配

为了给此角色授予权限，必须将其分配给角色受理人，这里的角色受理人可以是角色组、用户或通用安全组 (USG)。此分配通过使用管理角色分配完成。角色分配将角色受理人和角色链接在一起。如果一个角色受理人分配了多个角色，则该角色受理人将获得所有已分配角色所授予的所有权限组合。

除了将角色受理人链接到角色之外，角色分配还可以应用自定义或内置管理作用域。管理作用域控制可以由角色受理人修改的收件人、服务器和数据库对象。如果该角色分配到某个角色受理人，但管理作用域仅允许该角色受理人基于已定义的作用域管理特定对象，则该角色受理人仅可以对这些特定对象使用该角色所授予的权限。该角色所提供的权限无法应用于角色分配所定义的作用域以外的对象。有关角色分配和作用域的详细信息，请参阅下列主题：

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

默认情况下，此角色分配给一个或多个角色组。有关详细信息，请参阅本主题后面的\&quot;默认管理角色分配\&quot;一节。

如果要查看分配给此角色的角色组、用户或 USG 的列表，请使用以下命令。

```powershell
Get-ManagementRoleAssignment -Role "<role name>"
```

## 常规和委派角色分配

可以使用常规角色分配或委派角色分配，将此角色分配给角色受理人。常规角色分配会将此角色提供的权限授予角色受理人。委派角色分配会授予角色受理人，将此角色分配给其他角色受理人的权限。有关常规角色分配和委派角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

## 添加或删除角色分配

可以更改获得此角色的角色受理人。通过更改获得此角色的角色受理人，可以更改获得该角色权限的受理人。可将此角色分配到其他内置角色组，也可以创建角色组并向他们分配此角色。还可以向用户或 USG 分配此角色。但是，建议您限制对用户和 USG 的角色分配，因为这些分配可能大大增加权限模型的复杂性。

要将此角色分配给角色受理人，则必须使用委派角色分配将此角色分配到您所在的角色组、直接分配给您或分配到您所在的 USG。有关委派角色分配的详细信息，请参阅\&quot;常规和委派角色分配\&quot;一节。

另外，还可以从内置角色组、创建的角色组、用户和 USG 中删除此角色。但是，在该角色与角色组或 USG 之间必须始终至少有一个委派角色分配。不能删除最后一个委派角色分配。此限制有助于避免您将自己锁定在系统之外。

> [!IMPORTANT]  
> 在该角色与角色组或 USG 之间必须至少有一个委派角色分配。如果最后一个分配面向用户，则不能删除与此角色相关联的最后一个委派角色分配。


有关如何在此角色与角色组、用户和 USG 之间添加或删除分配的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## 更改角色分配的管理作用域

也可以更改此角色和角色受理人之间的现有角色分配上的管理作用域。通过更改角色分配上的作用域，可以控制能够使用该角色所提供的权限进行管理的对象。有多种方法可以更改角色分配上的作用域。可以执行下列操作之一：

  - 使用 **Set-ManagementRoleAssignment** cmdlet 添加新的自定义作用域。有关详细信息，请参阅下列主题：
    
      - [创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [更改角色分配](change-a-role-assignment-exchange-2013-help.md)

  - 使用 **Set-ManagementRoleAssignment** cmdlet 添加或更改组织单位作用域。有关详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

  - 使用 **Set-ManagementRoleAssignment** cmdlet 添加或更改预定义作用域。有关详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

  - 使用 **Set-ManagementScope** cmdlet 可以更改与角色分配相关的自定义作用域上的收件人、服务器或数据库作用域。有关详细信息，请参阅[更改角色范围](change-a-role-scope-exchange-2013-help.md)。

## 启用或禁用角色分配

通过启用或禁用角色分配，您可以控制角色分配是否生效。如果您禁用角色分配，则相关角色所授予的权限不会应用于角色受理人。这在需要暂时删除权限而不删除角色分配时会很方便。有关详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

## 默认管理角色分配

此角色可向一个或多个角色受理人分配角色。下表指明了该角色分配是常规角色分配还是委派角色分配，同时还指明了应用于每个分配的管理作用域。下面以列表形式对各个列进行了说明：

  - **常规分配：** 常规角色分配使角色受理人能够访问由此角色上管理角色条目所提供的权限。

  - **委派分配：** 委派角色分配使角色受理人能够将此角色分配给角色组、用户或 USG。

  - **收件人读取作用域：** 收件人读取作用域确定角色受理人可从 Active Directory 读取的收件人对象。

  - **收件人写入作用域：** 收件人写入作用域确定角色受理人可在 Active Directory 中修改的收件人对象。

  - **配置读取作用域：** 配置读取作用域确定角色受理人可从 Active Directory 读取的配置和服务器对象。

  - **配置写入作用域：** 配置写入作用域确定角色受理人可在 Active Directory 中修改的组织对象和服务器对象。

### 此角色的默认管理角色分配

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>角色组</th>
<th>常规分配</th>
<th>委派分配</th>
<th>收件人读取作用域</th>
<th>收件人写入作用域</th>
<th>配置读取作用域</th>
<th>配置写入作用域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 管理角色自定义

此角色已配置为向角色受理人提供管理本主题开头所列出的功能和组件所需的 cmdlet 及其参数。也提供了其他角色以便能够管理其他功能。通过对角色组添加和删除角色，无需自定义各个管理角色即可创建自定义权限模型。有关角色的完整列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。有关自定义角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

如果决定需要创建此角色的自定义版本，则必须创建此角色的子角色并自定义新角色。

> [!CAUTION]  
> 通过以下信息可以执行高级权限管理。自定义管理角色可能大大增加权限模型的复杂性。如果用未正确配置的自定义角色替换内置管理角色，则可能导致某些功能无法正常运行。


以下是创建自定义角色并将其分配给角色受理人的最常见步骤：

1.  创建该角色的副本。有关详细信息，请参阅[创建角色](create-a-role-exchange-2013-help.md)。

2.  使用 **Set-ManagementRoleEntry** cmdlet 和 **Remove-ManagementRoleEntry** cmdlet 更改或删除新角色的角色条目。无法将其他角色条目添加到新角色中，因为新角色仅包含父级内置角色的角色条目。有关详细信息，请参阅下列主题：
    
      - [更改角色条目](change-a-role-entry-exchange-2013-help.md)
    
      - [从角色中删除一个角色条目](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  如果要用这一新的自定义角色替换内置角色，请删除与内置角色相关联的任何角色分配。有关详细信息，请参阅下列主题：
    
      - [管理角色组](manage-role-groups-exchange-2013-help.md)中的\&quot;在角色组中添加或删除角色\&quot;部分
    
      - [从用户或 USG 删除角色](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  将新的自定义角色添加到所需的角色受理人。有关详细信息，请参阅下列主题：
    
      - [管理角色组](manage-role-groups-exchange-2013-help.md)中的\&quot;在角色组中添加或删除角色\&quot;部分
    
      - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        
        > [!IMPORTANT]  
        > 如果希望除角色创建用户以外的其他用户也能够分配新的自定义角色，请确保向至少一个角色受理人添加委派角色分配。有关详细信息，请参阅<a href="delegate-role-assignments-exchange-2013-help.md">委派角色分配</a>。

