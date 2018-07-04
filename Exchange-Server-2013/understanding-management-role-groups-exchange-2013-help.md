---
title: '了解管理角色组: Exchange 2013 Help'
TOCTitle: 了解管理角色组
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50490121
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解管理角色组

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

*管理角色组*是在 Microsoft Exchange Server 2013 的基于角色的访问控制 (RBAC) 权限模型中使用的通用安全组 (USG)。管理角色组可简化向用户组分配管理角色。角色组的所有成员都被授予相同的角色集。为角色组分配的角色有管理员和专家角色，这类角色用于在 Exchange 2013 中定义主要管理任务（如组织管理、收件人管理和其他任务）。角色组使您能够更容易地将范围更广的权限集分配到管理员组或专家用户组。

> [!NOTE]
> 本主题重点讲述高级 RBAC 功能。如果要管理基本的 Exchange 2013 权限（例如，使用 Exchange 管理中心 (EAC) 向角色组中添加成员或从角色组中删除成员，创建和修改角色组，或创建和修改角色分配策略），请参阅<a href="permissions-exchange-2013-help.md">权限</a>。


**目录**

角色组层

角色组管理

内置的角色组

链接的角色组

角色组委派

角色组成员身份

角色组创建工作流

> [!NOTE]
> 如果要将权限分配到用户以管理其拥有的邮箱或通讯组，请参阅<a href="understanding-management-role-assignment-policies-exchange-2013-help.md">了解管理角色分配策略</a>。


## 角色组层

以下是组成角色组模型的各层：

  - **角色组成员** *角色组成员*是可添加为角色组成员的邮箱、通用安全组 (USG) 或其他角色组。作为一个角色组的成员添加邮箱、USG 或另一个角色组时，已在管理角色和角色组之间所做的分配会应用于新成员。此操作将向新成员授予管理角色所提供的所有权限。

  - **管理角色组** *管理角色组*是一个特殊的 USG，它包含属于角色组成员的邮箱、USG 以及其他角色组。可以在此处添加和删除成员，并且它还是向其分配管理角色的对象。角色组中所有角色的组合定义添加到角色组的成员可以在 Exchange 组织中管理的所有事情。

  - **管理角色分配：**  *“管理角色分配”*链接管理角色和角色组。将管理角色分配到角色组，将使角色组的成员能够使用此管理角色中定义的 cmdlet 和参数。角色分配可以使用管理作用域来控制何处能够使用此分配。有关详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

  - **管理角色作用域：**  *“管理角色作用域”*是对角色分配产生影响的作用域。将角色与作用域分配到角色组时，管理作用域会专门指定允许该分配进行管理的对象。然后会将此分配及其作用域指定给角色组的成员，从而限制这些成员可以管理的内容。作用域可以由服务器或数据库、组织单位或是服务器、数据库或收件人对象上的筛选器的列表组成。有关详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

  - **管理角色：**  *“管理角色”*是一组管理角色条目的容器。角色用于定义特定任务，这些任务可以由分配该角色的角色组成员执行。有关详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

  - **管理角色条目：**  *“管理角色条目”*是管理角色上的单个条目，这些条目可提供对 cmdlet、脚本和其他特殊权限（允许执行特定任务）的访问。通常，角色条目由管理角色以及分配了该角色的角色组可以访问的一个 cmdlet 或脚本及若干参数构成。

下图显示了前面列表中的每个角色组层以及每个层如何与其他层相关。

**管理角色组层**

![管理角色组层](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "管理角色组层")

有关 RBAC 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

返回顶部

## 角色组管理

创建某个角色组时，将创建包含此角色组成员的 USG，并在指定的角色组和管理角色之间创建分配。（可选）还可以指定要应用于此角色分配的管理作用域，并可添加任何您希望其成为新角色组成员的邮箱。

创建角色组后，每个层都成为独立的对象。角色组仍是所有互连层的中心点，但是，每个层都单独进行管理。例如，要修改在角色组创建时应用于该角色组的管理作用域，需要在创建此角色组之后，在每个单独角色分配上更改作用域。对角色组模型的管理是通过使用管理此角色组模型的单个层的 cmdlet 来执行的。

下表列出了角色组层以及可用于管理每个层的过程主题。

### 角色组管理主题

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色组模型层</th>
<th>管理主题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>角色组成员</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">管理角色组成员</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>角色组</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色组</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>管理角色和分配</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色组</a></p></td>
</tr>
<tr class="even">
<td><p>管理角色条目</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">向角色添加角色</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">更改角色条目</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">从角色中删除一个角色条目</a></p>

> [!NOTE]
> 更改角色组中管理角色的管理角色条目是一项高级任务，大多数情况下不需要执行此操作。相反，您可以使用符合要求的预先存在的管理角色。有关详细信息，请参阅<a href="built-in-role-groups-exchange-2013-help.md">内置的角色组</a>。

</td>
</tr>
</tbody>
</table>


返回顶部

## 内置的角色组

内置角色组是 Exchange 2013 附带的角色。它们提供一组角色组，可用于为用户组提供各种级别的管理权限。可以向任何内置角色组添加或从中删除用户。还可以向大多数角色组添加或从中删除角色分配。仅有的例外如下所示：

  - 不能从 组织管理 角色组中删除任何委派角色分配。

  - 不能从 组织管理 角色组中删除“角色管理”角色。

下表列出了 Exchange 2013 中包含的所有内置角色组。有关内置角色组的详细信息，请参阅[内置的角色组](built-in-role-groups-exchange-2013-help.md)。

### 内置的角色组

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色组</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
<td><p>属于 组织管理 角色组成员的管理员具有对整个 Exchange 2013 组织的管理访问权限，并且几乎可以对任意 Exchange 2013 对象执行任何任务（某些情况除外）。默认情况下，此角色组的成员无法执行邮箱搜索以及对无作用域的顶级管理角色的管理。</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
<td><p>属于 仅查看组织管理 角色组成员的管理员可以查看 Exchange 组织中任何对象的属性。</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
<td><p>属于 收件人管理 角色组成员的管理员拥有在 Exchange 2013 组织中创建或修改 Exchange 2013 收件人的管理访问权限。</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
<td><p>属于 UM 管理 角色组成员的管理员可以管理 Exchange 组织中的功能，例如统一消息 (UM) 服务配置、邮箱上的 UM 属性、UM 提示和 UM 自动助理配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">发现管理</a></p></td>
<td><p>属于 发现管理 角色组成员的管理员或用户可以在 Exchange 组织中的邮箱中搜索满足特定条件的数据，还可以在邮箱上配置诉讼保留。</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
<td><p>属于 记录管理 角色组成员的用户可以配置遵从性功能，如保留策略标记、邮件分类、传输规则等。</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
<td><p>属于此角色组成员的管理员可以配置诸如数据库副本、证书、传输队列和发送连接器、虚拟目录和客户端访问协议这样的传输、客户端访问和邮箱功能的特定于服务器的配置。</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
<td><p>属于 Help Desk 角色组成员的用户可以对 Exchange 2013 收件人执行受限制的收件人管理。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
<td><p>属于清洁管理角色组成员的用户可以配置 Exchange 2013 的防病毒和反垃圾邮件功能。与 Exchange 2013 集成的第三方程序可以将服务帐户添加到此角色组中，这样这些程序就可以访问检索和配置 Exchange 配置所需的 cmdlet。</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p></td>
<td><p>属于合规性管理角色组成员的用户可以根据其策略配置和管理 Exchange 合规性配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">公用文件夹管理</a></p></td>
<td><p>属于公用文件夹管理角色组成员的管理员可以管理运行 Exchange 2013 的服务器上的公用文件夹。</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">委派安装</a></p></td>
<td><p>作为“委派安装”角色组成员的管理员可以部署正在运行 Exchange 2013 且以前由 组织管理 角色组成员设置的服务器。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 链接的角色组

链接的角色组用于在专用资源林中安装 Exchange 2013 并将用户放置在其他受信任的外部林的组织。顾名思义，链接角色组在 Exchange 林中的角色组和外部林中的 USG 之间创建链接。如果您要用于管理 Exchange 的管理员 Active Directory 域服务 (AD DS) 用户帐户所驻留的资源林与 Exchange 驻留的资源林不相同，这将很有用。链接角色组只能与一个外部 USG 相关联。另外，无需在 Exchange 林和外部林之间创建双向信任。Exchange 林需要信任外部林，但外部林无需信任 Exchange 林。

有关在多林拓扑中的权限的详细信息，请参阅[了解多林权限](understanding-multiple-forest-permissions-exchange-2013-help.md)。

链接角色组由两部分组成：

  - **链接角色组：** 链接角色组是将外部 USG 与分配到角色组的管理角色分配相关联的容器对象。

  - **外部 USG：** 外部 USG 包含应当授予由链接角色组提供权限的成员。

创建链接角色组时，您需要在外部林（包含您需要依靠其来管理 Exchange 林的用户）和 USG（包含那些成员用户、外部 USG 名称和访问外部林所需的凭据）中提供域控制器。Exchange 会将外部 USG 的安全标识符 (SID) 添加到链接角色组。因为 USG SID 是外部 USG 的唯一标识，所以当具有多个外部林时，我们强烈建议您在角色组的名称中指定外部林。

链接角色组不包含任何成员。该角色组的所有成员都使用外部 USG 进行管理。这意味着您无法使用 **Update-RoleGroupMember**、**Add-RoleGroupMember** 或 **Remove-RoleGroupMember** cmdlet 添加或删除角色组成员。将成员添加到外部 USG 时，系统会授予这些成员由链接角色组提供的权限。

无法将标准角色组（包含其自身的成员）更改为链接角色组，反之亦然。如果要将角色组从标准角色组更改为链接角色组，则必须创建新链接角色组，并将存在于标准角色组上的管理角色分配复制到链接角色组上。这也适用于内置角色组，因为内置角色组是标准角色组。如果要从外部林执行 Exchange 林的所有管理，则需要新建链接角色组，并将存在于内置角色组上的管理角色添加到新链接角色组。有关如何完成此过程的详细信息，请参阅[创建链接的角色组的镜像内置角色组](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)。

返回顶部

## 角色组委派

默认情况下，组织管理 角色组的成员可以向角色组添加和从中删除成员。但是，可能要允许不属于 组织管理 角色组成员的用户添加和删除角色组成员。如果是这样，则您可以使用角色组委派。

角色组委派由每个角色组上的 **ManagedBy** 属性控制。**ManagedBy** 属性包含可以向角色组添加和从中删除成员的用户的列表，或可以更改角色组配置的用户的列表。用户不会分配由角色组给予的任何权限，除非它们也是角色组的成员。

如果在角色组上设置了 **ManagedBy** 属性，则默认情况下，只有在该属性上作为角色组管理者列出的那些用户可以修改角色组或角色组的成员身份。但是，cmdlet 上用于修改角色组或角色组成员身份的可选参数可以覆盖该限制。*BypassSecurityGroupManagerCheck* 开关可以由属于 组织管理 角色的成员的用户或者直接或间接分配了“角色管理”管理角色的用户使用。使用此开关时，会忽略 **ManagedBy** 属性，并且用户可以修改角色组或角色组成员身份。

如果没有在角色组上设置 **ManagedBy** 属性，则只有属于 组织管理 角色成员的用户或直接/间接分配了“角色管理”管理角色的用户可以修改角色组或角色组成员身份。

> [!NOTE]
> 分配给某个角色组的角色可能会使用委派角色分配来进行分配。使用委派角色分配，分配了委派角色的角色组成员可以将该角色分配给另一个角色组、分配策略、用户或 USG。角色组的成员只能分配该角色，并且无法委派角色组，除非它们也被添加到了 <strong>ManagedBy</strong> 属性。有关委派角色分配的详细信息，请参阅<a href="understanding-management-role-assignments-exchange-2013-help.md">了解管理角色分配</a>。


有关如何管理角色组委派的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

返回顶部

## 角色组成员身份

如果用户是某个角色组的成员，则分配给此角色组的管理角色也会分配给该用户。如果用户是多个角色组的成员，则会聚合每个角色组的管理角色并将其分配给该用户。用户、USG 和其他角色组都可以是角色组的成员。

只有属于 组织管理 或“角色管理”角色组成员的用户，以及授予了向角色组添加或从中删除用户权限的用户可以管理角色组成员身份。

有关如何管理角色组成员身份的详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

## 角色组创建工作流

如前所述，角色组由若干层组成。为了帮助您了解创建角色组时的操作，请参阅以下示例，此示例将创建新角色组。

    New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"

运行上述命令时，会发生下列情况：

1.  创建一个名为 Seattle Recipient Management 的新角色组对象，该对象是一种特殊的 USG。

2.  Ray、Jenn、Maria、Chris、Maija、Carter、Jenny、Sam、Lukas、Isabel 和 Katie 的邮箱添加为角色组的成员。这些用户接收由此角色组提供的权限。

3.  用户 Brian 和 David 被添加到角色组的 **ManagedBy** 属性中。这些用户可以添加和删除角色组成员，但不会授予任何由此角色组提供的权限，因为它们不是成员。Katie 也被添加到此角色组的 **ManagedBy** 属性中。因为她已被添加到 **ManagedBy** 属性，并且她是此角色组的成员，所以她可以添加和删除角色组成员，而且还可以接收由此角色组提供的权限。

4.  创建了下列管理角色分配。角色分配会将命令中指定的每个管理角色分配给角色组。将管理作用域 Seattle Users 添加到每个角色分配。每个角色分配的名称是分配的管理角色和角色组名称的组合。
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

如果将此命令的结果与本主题前面介绍的管理角色组层图进行比较，则可以看到对应于角色组层的每个步骤。然后，可以参考本主题前面的“角色组管理”中显示的管理角色组管理主题，管理每个角色组层。

返回顶部

