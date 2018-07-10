---
title: '权限: Exchange 2013 Help'
TOCTitle: 权限
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 50491760
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 权限

 

_**适用于：** Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2013 包括一个大型的根据基于角色的访问控制 (RBAC) 权限模型预定义的权限集，使用它可轻松便捷地向管理员和用户授予权限。你可以使用 Exchange 2013 中的权限功能，以便快速设置并运行新组织。

> [!NOTE]
> 一些 RBAC 功能和概念为高级功能，因此本主题将不对其进行讨论。如果本主题中讨论的功能无法满足您的需求，并且您希望进一步自定义权限模型，请参阅<a href="understanding-role-based-access-control-exchange-2013-help.md">了解基于角色的访问控制</a>。


需要所有权限主题的列表？请参阅权限文档。

**目录**

基于角色的权限

角色组和角色分配策略

使用角色组

使用角色分配策略

## 基于角色的权限

在 Exchange 2013 中，授予给管理员和用户的权限基于管理角色。角色定义了管理员或用户可以执行的任务集。例如，名为 `Mail Recipients` 的管理角色定义了某人可以对一组邮箱、联系人和通讯组执行的任务。为管理员或用户分配角色的同时，也会授予此人该角色所提供的权限。

角色分为两种类型，即管理角色和最终用户角色：

  - **管理角色** 可以使用管理 Exchange 组织的一部分（如收件人、服务器或数据库）的角色组，将这些角色包含的权限分配给管理员或专家用户。

  - **最终用户角色** 通过使用角色分配策略分配这些角色，使用户可以管理其自己的邮箱及其拥有的通讯组的各个方面。最终用户角色以前缀 `My` 开头。

角色通过向已分配角色的用户提供 cmdlet 来授予管理员和用户执行任务的权限。由于 Exchange 管理中心 (EAC) 和 Exchange 命令行管理程序使用 cmdlet 管理 Exchange，因此授予对 cmdlet 的访问权限将给予管理员或用户在每个 Exchange 管理界面中执行任务的权限。

Exchange 2013 包括大约 86 个可用于授予权限的角色。有关 Exchange 2013 中包含的角色的列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

基于角色的权限

## 角色组和角色分配策略

虽然角色授予在 Exchange 2013 中执行任务的权限，但需要简便的方式将这些权限分配给管理员和用户。Exchange 2013 为您提供以下方式帮助实现此目标：

  - **角色组** 使用角色组可以向管理员和专家用户授予权限。

  - **角色分配策略** 使用角色分配策略可以授予最终用户在其自己的邮箱或拥有的通讯组中更改设置的权限。

有关角色组和角色分配策略的详细信息，请参阅以下各部分。

## 角色组

必须为每个管理 Exchange 2013 的管理员分配至少一个或多个角色。由于管理员可能在 Exchange 中跨多个区域执行工作职能，因此他们可能会有多个角色。例如，一个管理员可能同时管理收件人和 Exchange 服务器。在这种情况下，可能同时为该管理员分配 `Mail Recipients` 角色和 `Exchange Servers` 角色。

为了能够更轻松地为管理员分配多个角色，Exchange 2013 包含了角色组。角色组是 Exchange 2013 使用的特殊通用安全组 (USG)，可以包含 Active Directory 用户、USG 及其他角色组。将一个角色分配给角色组时，会将该角色授予的权限授予该角色组的所有成员。这使你可以一次将许多角色分配给许多角色组成员。角色组通常覆盖更广泛的管理区域，如收件人管理。角色组只能与管理角色一起使用，而不能与最终用户角色一起使用。

> [!NOTE]
> 可以在不使用角色组的情况下将角色直接分配给用户或 USG。但是，这种角色分配方法是一个高级过程，本主题将不做介绍。建议你使用角色组来管理权限。


下图显示了用户、角色组和角色之间的关系。

**角色、角色组和角色组成员**

![角色、角色组和成员关系](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "角色、角色组和成员关系")

Exchange 2013 包括若干内置角色组，每个角色组都提供管理 Exchange 2013 中特定区域的权限。某些角色组可能与其他角色组重叠。下表列出了每个角色组及其使用说明。如果要查看分配给每个角色组的角色，请单击“角色组”列的角色组名称，然后打开“分配给此角色组的管理角色”部分。

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
<td><p>组织管理 角色组成员的管理员具有对整个 Exchange 2013 组织的管理访问权限，并且几乎可以对任意 Exchange 2013 对象执行任何任务，某些情况除外，例如 <code>Discovery Management</code> 角色。</p>

> [!important]
> 由于 组织管理 角色组是一个强大的角色，因此只有执行可能影响整个 Exchange 组织的组织级别管理任务的用户或 USG 才可以是此角色组的成员。

</td>
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
<td><p>如果管理员是“UM 管理”角色组中的成员，则他可以管理 Exchange 组织中的功能，例如统一消息 (UM) 服务配置、邮箱上的 UM 属性、UM 提示和 UM 自动助理配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
<td><p>默认情况下，技术支持角色组允许成员查看和修改组织中任何用户的 Microsoft OfficeOutlook Web App 选项。这些选项可能包括修改用户的显示名称、地址和电话号码。它们不包括 Outlook Web App 选项中不可用的选项，例如，修改邮箱大小或配置邮箱所在的邮箱数据库。</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
<td><p>作为清洁管理角色组成员的管理员可以配置 Exchange 2013 的防病毒和反垃圾邮件功能。与 Exchange 2013 集成的第三方程序可以将服务帐户添加到此角色组中，这样这些程序就可以访问检索和配置 Exchange 配置所需的 cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
<td><p>属于 记录管理 角色组成员的用户可以配置遵从性功能（如保留策略标记、邮件分类和传输规则）。</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">发现管理</a></p></td>
<td><p>作为 发现管理 角色组成员的管理员或用户可以在 Exchange 组织中的邮箱中搜索满足特定条件的数据，还可以在邮箱上配置合法保留。</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">公用文件夹管理</a></p></td>
<td><p>属于公用文件夹管理角色组成员的管理员可以管理运行 Exchange 2013 的服务器上的公用文件夹。</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
<td><p>属于“服务器管理”角色组成员的管理员可以配置诸如数据库副本、证书、传输队列和发送连接器、虚拟目录和客户端访问协议这样的传输、统一消息、客户端访问和邮箱功能的特定于服务器的配置。</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">委派安装</a></p></td>
<td><p>作为“委派安装”角色组成员的管理员可以部署正在运行 Exchange 2013 且以前由 组织管理 角色组成员设置的服务器。</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p></td>
<td><p>属于合规管理角色组的用户可根据其组织策略配置和管理 Exchange 合规性设置。</p></td>
</tr>
</tbody>
</table>


如果你在只有少数几个管理员的小型组织工作，那么可能只需要将这些管理员添加到 组织管理 角色组，并且可能永远不需要使用其他角色组。如果你在较大型的组织工作，可能会由执行特定任务的管理员管理 Exchange，如收件人或服务器管理。在这些情况下，可能要将某个管理员添加到 收件人管理 角色组，并将另一个管理员添加到“服务器管理”角色组。然后，这些管理员可以管理特定的 Exchange 2013 区域，但没有权限管理他们职责外的区域。

如果 Exchange 2013 中的内置角色组与管理员的工作职能不匹配，可以创建角色组并向其中添加角色。有关详细信息，请参阅本主题后面的使用角色组。

基于角色的权限

## 角色分配策略

Exchange 2013 提供了角色分配策略，以便控制用户可以在其自己的邮箱及其拥有的通讯组上配置哪些设置。这些设置包括其显示名称、联系人信息、语音邮件设置和通讯组成员身份。

Exchange 2013 组织可以有多个角色分配策略，以便为组织中不同类型的用户提供不同级别的权限。根据与其邮箱相关联的角色分配策略的不同，某些用户有权更改其地址或创建通讯组，另一些用户则不能。角色分配策略直接添加到邮箱，且每个邮箱一次只能与一个角色分配策略相关联。

对于组织中的角色分配策略，其中一个将被标记为默认策略。默认角色分配策略将与创建时未明确分配特定角色分配策略的新邮箱相关联。默认角色分配策略应包含适用于大多数邮箱的权限。

使用最终用户角色将权限添加到角色分配策略。最终用户角色以 `My` 开头，且仅向用户授予管理其邮箱或拥有的通讯组的权限。不能使用其管理其他任何邮箱。只有最终用户角色可以分配给角色分配策略。

将最终用户角色分配给角色分配策略后，与该角色分配策略相关联的所有邮箱都将获得该角色授予的权限。这使您可以在不配置各个邮箱的情况下添加或删除用户组的权限。下图显示了：

  - 将最终用户角色分配给角色分配策略。角色分配策略可以共享相同的最终用户角色。

  - 角色分配策略与邮箱相关联。每个邮箱只能与一个角色分配策略相关联。

  - 邮箱与角色分配策略相关联之后，最终用户角色会应用于该邮箱。将向该邮箱的用户授予此类角色授予的权限。

**角色、角色分配策略和邮箱**

![角色、角色分配策略、邮箱关系](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "角色、角色分配策略、邮箱关系")

默认角色分配策略角色分配策略包括在 Exchange 2013 中。顾名思义，它是默认角色分配策略。如果要更改该角色分配策略提供的权限或创建角色分配策略，请参阅本主题后面的使用角色分配策略。

## 使用角色组

要使用 Exchange 2013 中的角色组管理你的权限，我们建议使用 Exchange 管理中心。使用 EAC 管理角色组时，可以通过单击几次鼠标添加和删除角色和成员、创建角色组以及复制角色组。EAC 提供了简单的对话框来执行这些任务，如下图所示的“**新建角色组**”对话框。

**EAC 中的“新建角色组”对话框**

![EAC 中的“新建角色组”对话框](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "EAC 中的“新建角色组”对话框")

Exchange 2013 包括数个角色组，将权限分离为特定管理区域。如果这些现有角色组提供了管理员管理 Exchange 2013 组织所需的权限，则只需将管理员添加为相应角色组的成员。将管理员添加到角色组后，管理员就可以管理与该角色组相关的功能。若要向角色组中添加成员或删除其中的成员，请在 EAC 中打开该角色组，然后向成员列表中添加成员或从中删除成员。有关内置角色组的列表，请参阅[内置的角色组](built-in-role-groups-exchange-2013-help.md)。

> [!important]
> 如果某个管理员为多个角色组的成员，则 Exchange 2013 授予该管理员其所属的角色组提供的所有权限。


如果 Exchange 2013 中提供的角色组没有你所需的权限，则可以使用 EAC 创建角色组并添加具有你所需权限的角色。对于新建的角色组，需执行以下操作：

1.  为角色组选择名称。

2.  选择要添加到角色组的角色。

3.  向角色组中添加成员。

4.  保存角色组。

创建角色组后，可以像管理其他任何角色组一样对其进行管理。

如果某个现有角色组具有部分您需要的权限但并非全部，则可以复制该角色组，然后对其进行更改以创建一个角色组。您可以复制现有角色组并对其进行更改，而不影响原始角色组。复制角色组过程中，可以添加新的名称和说明，向新角色组中添加角色和删除新角色组中的角色，以及添加新成员。创建或复制角色组时，使用上图所示的同一对话框。

也可以修改现有角色组。使用与上图类似的 EAC 对话框，可以同时向现有角色组中添加角色和成员，以及从其中删除角色和成员。通过向角色组中添加角色和从其中删除角色，可以为该角色组的成员启用和禁用管理功能。有关可以添加到角色组的角色列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

> [!NOTE]
> 尽管可以更改分配给内置角色组的角色，但建议您复制内置角色组、修改角色组副本，然后将成员添加到角色组副本。


基于角色的权限

## 使用角色分配策略

若要管理授予最终用户在 Exchange 2013 中管理其自己的邮箱的权限，建议使用 EAC。使用 EAC 管理最终用户权限时，可以通过单击几次鼠标添加角色、删除角色和创建角色分配策略。EAC 提供了简单的对话框来执行这些任务，如下图所示的“角色分配策略”对话框。

**EAC 中的“角色分配策略”对话框**

![EAC 中的“角色分配策略”对话框](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "EAC 中的“角色分配策略”对话框")

Exchange 2013 包括名为“默认角色分配策略”的角色分配策略。通过该角色分配策略，与其关联的邮箱用户可以执行下列操作：

  - 加入或退出允许成员管理其自己的成员身份的通讯组。

  - 查看并修改自己邮箱中的基本邮箱设置，如收件箱规则、拼写检查行为、垃圾邮件设置和 Microsoft ActiveSync 设备。

  - 修改他们的联系信息，例如工作地址和电话号码、手机号码和寻呼机号码。

  - 创建、修改或查看文本邮件设置。

  - 查看或修改语音邮件设置。

  - 查看和修改其市场应用程序。

  - 创建团队邮箱，并且将它们连接到 Microsoft SharePoint 列表。

如果要向“默认角色分配策略”或其他任何角色分配策略中添加权限或删除其中的权限，可以使用 EAC。使用的对话框与上图中的对话框类似。在 EAC 中打开角色分配策略后，选中要为其分配的角色旁边的复选框或清除要删除的角色旁边的复选框。对角色分配策略所做的更改将应用到与其关联的每个邮箱。

如果要为组织中各种类型的用户分配不同的最终用户权限，可以创建角色分配策略。创建角色分配策略时，会看到与上图中类似的对话框。可以为角色分配策略指定新的名称，然后选择要分配给该角色分配策略的角色。创建角色分配策略后，可以使用 EAC 将其与邮箱相关联。

如果要更改默认的角色分配策略，必须使用命令行管理程序。在更改默认角色分配策略时，任何创建时未明确指定角色分配策略的新建邮箱都将与新的默认角色分配策略相关联。选择新的默认角色分配策略时，与现有邮箱关联的角色分配策略不会发生变化。

> [!NOTE]
> 如果选中具有子角色的角色对应的复选框，则同时还会选中其子角色对应的复选框。如果清除具有子角色的角色对应的复选框，则同时还会清除其子角色对应的复选框。<br />
> 有关如何创建角色分配策略或更改现有角色分配策略的详细步骤，请参阅下列主题：
> <ul>
> <li><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色分配策略</a></p></li>
> <li><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">更改邮箱的分配策略</a></p></li>
> </ul>


基于角色的权限

## 权限文档

下表包含指向某些主题的链接，这些主题将帮助您了解和管理 Exchange 2013 中的权限。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">了解基于角色的访问控制</a></p></td>
<td><p>了解构成 RBAC 的每个组件，以及如果角色组和管理角色不能满足需要，该如何创建高级权限模型。</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">了解多林权限</a></p></td>
<td><p>了解有关在组织中使用帐户和资源林实施 RBAC 权限的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">了解拆分权限</a></p></td>
<td><p>了解有关使用 RBAC 和 Active Directory 拆分权限拆分 Exchange 和安全主要管理的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">了解与 Exchange 2007 和 Exchange 2010 共存的权限</a></p></td>
<td><p>配置权限以启用在现有 Exchange 2007 和 Exchange 2010 组织中的 Exchange 2013 的管理。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">管理角色组</a></p></td>
<td><p>配置使用角色组的 Exchange 管理员和专家用户的权限。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">管理角色组成员</a></p></td>
<td><p>向角色组中添加或从中删除成员。通过向角色组中添加或从中删除成员，可配置谁将能够管理 Exchange 功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">管理链接的角色组</a></p></td>
<td><p>以多林 Exchange 部署配置 Exchange 管理员和专家用户的权限。</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色分配策略</a></p></td>
<td><p>使用角色分配策略配置用户在其邮箱上对哪些功能有访问权限。</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">更改邮箱的分配策略</a></p></td>
<td><p>配置将哪些角色分配策略应用到一个或多个邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">创建链接的角色组的镜像内置角色组</a></p></td>
<td><p>以多林 Exchange 部署将内置角色组重新创建为链接的角色组。</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">查看有效权限</a></p></td>
<td><p>查看谁有权限管理 Exchange 功能。</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">功能权限</a></p></td>
<td><p>了解更多有关管理 Exchange 功能和服务所需权限的信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">高级权限</a></p></td>
<td><p>使用高级的 RBAC 功能创建高度自定义的权限模型来满足任何组织的需求。</p></td>
</tr>
</tbody>
</table>

