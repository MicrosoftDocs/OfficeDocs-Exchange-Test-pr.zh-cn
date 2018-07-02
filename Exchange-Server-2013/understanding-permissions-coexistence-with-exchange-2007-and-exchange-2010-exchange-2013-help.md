---
title: '了解与 Exchange 2007 和 Exchange 2010 共存的权限: Exchange 2013 Help'
TOCTitle: 了解与 Exchange 2007 和 Exchange 2010 共存的权限
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54913692
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 了解与 Exchange 2007 和 Exchange 2010 共存的权限

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

将 Microsoft Exchange Server 2013 安装到现有的 Microsoft Exchange Server 2010 或 Microsoft Exchange Server 2007 组织中时，您需要了解新组织中的权限工作原理。阅读以下适用于您的组织的部分。

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## 将 Exchange 2013 安装到现有 Exchange 2010 组织中

Exchange 2013 使用 Exchange 2010 中所用的基于角色的访问控制 (RBAC) 权限模型。当您将 Exchange 2013 安装到现有的 Exchange 2010 组织中时，相同的管理角色组、管理角色和管理作用域适用于 Exchange 2013 和 Exchange 2010 服务器及收件人。角色组的成员或分配到角色的用户可以管理角色组或角色作用域中包括的任何 Exchange 2013 或 Exchange 2013 服务器或收件人。如果您在组织中不使用作用域，并希望现有角色组的成员能够管理 Exchange 2010 和 Exchange 2013 服务器及收件人，则您不需要做任何事情。这些管理员将能够管理添加到组织的 Exchange 2013 服务器和收件人。如果您需要有关 Exchange 2010 和 Exchange 2013 中的权限工作原理的提醒，请参阅[权限](permissions-exchange-2013-help.md)。

在新组织中，您可能希望分开单独管理 Exchange 2010 和 Exchange 2013 服务器及收件人。负责管理 Exchange 2010 服务器和收件人的管理员组不能管理 Exchange 2013 服务器和收件人，反之亦然。在这种情况下，您可以使用管理作用域来定义每个管理员组可以管理的服务器和收件人。创建需要的作用域之后，您可以复制现有的角色组，添加作为各组成员的管理员，然后将作用域添加到角色组。完成后，每个角色组的成员都将只能管理与各自作用域相匹配的服务器和收件人。

有关角色组、作用域、复制角色组以及向角色组添加作用域的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

## 将 Exchange 2013 安装到现有 Exchange 2007 组织中

Exchange 2013 包含基于角色的访问控制 (RBAC) 权限，这些权限会替换 Microsoft Exchange Server 2007 中使用的基于 Active Directory 访问控制条目 (ACE) 的授权模型。RBAC 是用于大多数 Exchange 2013 管理的授权机制。此机制包括以下管理区域：

  - Exchange 命令行管理程序

  - Exchange 管理中心 (EAC)

  - Exchange Web 服务

有关如何在 Exchange 2013 与 Exchange 2007 之间规划共存的详细信息，请参阅[从 Exchange 2007 升级到 Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)。

要查找与权限相关的管理任务吗？请查看[权限](permissions-exchange-2013-help.md)。

## Exchange 2013 权限

Exchange 2013 RBAC 权限模型由分配了若干管理角色之一的管理角色组构成。管理角色包含使管理员能够在 Exchange 组织中执行任务的权限。已将管理员添加为角色组成员，并且授予了角色提供的所有权限。下表提供了角色组、分配给角色组的一些角色以及可能是角色组成员的用户类型的说明的示例。

### Exchange 2013 中的角色组和角色的示例

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色组</th>
<th>管理角色</th>
<th>此角色组的成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>组织管理</p></td>
<td><p>以下角色是分配给此角色组的一些角色：</p>
<ul>
<li><p>地址列表</p></li>
<li><p>Exchange 服务器</p></li>
<li><p>日记</p></li>
<li><p>邮件收件人</p></li>
<li><p>公用文件夹</p></li>
</ul></td>
<td><p>管理整个 Exchange 2013 组织的用户应是此角色组的成员。除一些例外之外，此角色组的成员几乎可以管理 Exchange 2013 组织的任何方面。</p>
<p>默认情况下，用于为 Exchange 2013 准备 Active Directory 的用户帐户是此角色组的成员。</p>
<p>有关此角色组的详细信息和分配给此角色组的角色的完整列表，请参阅<a href="organization-management-exchange-2013-help.md">组织管理</a>。</p></td>
</tr>
<tr class="even">
<td><p>仅查看组织管理</p></td>
<td><p>以下是分配给此角色组的角色：</p>
<ul>
<li><p>监视</p></li>
<li><p>仅查看配置</p></li>
<li><p>仅查看收件人</p></li>
</ul></td>
<td><p>查看整个 Exchange 2013 组织的配置的用户应是此角色组的成员。这些用户必须能够查看服务器配置和收件人信息，并且能够执行监视功能，但不能更改组织或收件人配置。</p>
<p>有关此角色组的详细信息，请参阅<a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a>。</p></td>
</tr>
<tr class="odd">
<td><p>收件人管理</p></td>
<td><p>以下是分配给此角色组的角色：</p>
<ul>
<li><p>通讯组</p></li>
<li><p>启用了邮件的公用文件夹</p></li>
<li><p>邮件收件人创建</p></li>
<li><p>邮件收件人</p></li>
<li><p>邮件跟踪</p></li>
<li><p>迁移</p></li>
<li><p>移动邮箱</p></li>
<li><p>收件人策略</p></li>
</ul></td>
<td><p>管理收件人（如 Exchange 2013 组织中的邮箱、联系人和通讯组）的用户应是此角色组的成员。这些用户可以创建收件人、修改或删除现有收件人或移动邮箱。</p>
<p>有关此角色组的详细信息和分配给此角色组的角色的完整列表，请参阅<a href="recipient-management-exchange-2013-help.md">收件人管理</a>。</p></td>
</tr>
<tr class="even">
<td><p>服务器管理</p></td>
<td><p>以下角色是分配给此角色组的一些角色：</p>
<ul>
<li><p>数据库</p></li>
<li><p>Exchange 连接器</p></li>
<li><p>Exchange 服务器</p></li>
<li><p>接收连接器</p></li>
<li><p>传输队列</p></li>
</ul></td>
<td><p>管理 Exchange 服务器配置（如接收连接器、证书、数据库和虚拟目录）的用户应是此角色组的成员。这些用户可以修改 Exchange 服务器配置、创建数据库以及重新启动和处理传输队列。</p>
<p>有关此角色组的详细信息和分配给此角色组的角色的完整列表，请参阅<a href="server-management-exchange-2013-help.md">服务器管理</a>。</p></td>
</tr>
<tr class="odd">
<td><p>发现管理</p></td>
<td><p>以下是分配给此角色组的角色：</p>
<ul>
<li><p>合法保留</p></li>
<li><p>邮箱搜索</p></li>
</ul></td>
<td><p>执行邮箱搜索以支持法律程序或配置合法保留的用户应是此角色组的成员。</p>
<p>此角色组的成员可以包含非 Exchange 管理员，如法律部门的人员。法律部门的人员可以在 Exchange 管理员不进行干预的情况下执行其任务。</p>
<p>有关此角色组的详细信息和分配给此角色组的角色的完整列表，请参阅<a href="discovery-management-exchange-2013-help.md">发现管理</a>。</p></td>
</tr>
</tbody>
</table>


此表显示 Exchange 2013 提供了对授予管理员的权限的精细级别的控制。可以从 Exchange 2013 的 12 个角色组中进行选择。有关角色组及其提供的权限的完整列表，请参阅[内置的角色组](built-in-role-groups-exchange-2013-help.md)。

由于 Exchange 2013 提供了许多角色组，以及由于可通过创建具有不同角色组合的角色组来进行进一步的自定义，因此不再需要处理 Active Directory 对象的访问控制列表 (ACL)，处理将没有任何效果。ACL 不再用于对 Exchange 2013 中的各个管理员或组应用权限。诸如管理员创建邮箱或用户访问邮箱的所有任务将由 RBAC 管理。RBAC 对任务进行授权，如果允许，则 Exchange 代表用户执行任务。Exchange 执行 Exchange 受信任子系统通用安全组 (USG) 中的任务。除一些例外之外，Exchange 2010 必须访问的 Active Directory 中对象的所有 ACL 都已授予 Exchange 受信任子系统 USG。这是 Exchange 2007 中处理权限的方式的一项根本更改。

为 Active Directory 中的用户授予的权限与此用户使用 Exchange 2013 管理工具时，RBAC 为用户授予的权限不同。

有关 RBAC 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## Exchange 2007 权限

Exchange 2007 管理模型利用 Active Directory 林定义安全边界。特定林中的安全权限不会进行隔离。林所有者和企业管理员可以始终获取对任何域中所有资源的访问权限。在 Exchange 2007 中，可能必须只是临时授予企业管理员权限和顶级域管理员权限。

Exchange 2007 提供以下预定义的管理员角色：

  - **Exchange 组织管理员角色**   此角色授予控制 Exchange 2007 组织的所有方面的权限。此外，具有此角色的管理员可以向其他 Exchange 管理员授予权限。此角色授予用于安装 Exchange 2007 的帐户。

  - **Exchange 仅查看管理员角色**   此角色授予查看 Exchange 配置的权限。但是，具有此角色的管理员不能修改 Exchange 2007 组织中的对象。

  - **Exchange 收件人管理员角色**   此角色授予管理电子邮件收件人的权限。具有此角色的管理员可以为用户、组、联系人和通讯组修改与 Exchange 相关的项目。

  - **Exchange Server 管理员角色**   此角色授予管理特定服务器的权限。但是，此角色不授予执行对 Exchange 2007 组织具有全局影响的操作的权限。

  - **Exchange 公用文件夹管理员角色**   此角色是在 Exchange 2007 Service Pack 1 中添加的**。**此角色授予管理 Exchange 2007 组织中的公用文件夹的权限。

此权限模型将 USG 用于所有角色，除了 Exchange Server 管理员角色以外。在运行 Exchange 2007**Setup /PrepareAD** 命令时，安装程序会在根域中创建 USG，并向 USG 指定林范围内的作用域。会向 USG 分配 ACL，以管理整个 Active Directory 中的 Exchange 对象。

在 Exchange 2007 中，可以通过向管理员分配各种角色来分隔管理员。直接将权限分配给用户或分配给用户是其成员的 USG。用户执行的任何操作都会在此用户的 Active Directory 帐户上下文中执行。下表列出了 Exchange 2007 管理员角色以及其与 Exchange 相关的权限。

### Exchange 2007 管理员角色

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>管理员角色</th>
<th>成员</th>
<th>隶属于</th>
<th>Exchange 权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 组织管理员</p></td>
<td><p>管理员帐户或用于安装第一个 Exchange 2007 服务器的帐户</p></td>
<td><p>Exchange 收件人管理员</p>
<p><em>&lt;服务器名称&gt;</em> 的管理员本地组</p></td>
<td><p>对 Active Directory 中的 Microsoft Exchange 容器拥有完全控制权</p></td>
</tr>
<tr class="even">
<td><p>Exchange 仅查看管理员</p></td>
<td><p>Exchange 收件人管理员</p>
<p>Exchange Server 管理员（<em>&lt;服务器名称</em>&gt;）</p></td>
<td><p>Exchange 收件人管理员</p>
<p>Exchange Server 管理员</p></td>
<td><p>对 Active Directory 中的 Microsoft Exchange 容器拥有读取访问权限</p>
<p>对包含 Exchange 收件人的所有 Windows 域拥有读取访问权限</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 收件人管理员</p></td>
<td><p>Exchange 组织管理员</p></td>
<td><p>Exchange 仅查看管理员</p></td>
<td><p>对 Active Directory 用户对象的 Exchange 属性拥有完全控制权</p></td>
</tr>
<tr class="even">
<td><p>Exchange Server 管理员</p></td>
<td><p>Exchange 组织管理员</p></td>
<td><p>Exchange 仅查看管理员</p>
<p><em>&lt;服务器名称</em>&gt; 的管理员本地组</p></td>
<td><p>对 Exchange<em>&lt;服务器名称</em>&gt; 拥有完全控制权</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>每个 Exchange 2007 计算机帐户</p></td>
<td><p>Exchange 仅查看管理员</p></td>
<td><p>特殊</p></td>
</tr>
<tr class="even">
<td><p>Exchange 公用文件夹管理员</p></td>
<td><p>Exchange 组织管理员</p></td>
<td><p>Exchange 仅查看管理员</p></td>
<td><p>拥有管理所有公用文件夹的完全控制权（授予了&amp;quot;创建顶级公用文件夹&amp;quot;扩展权限）</p></td>
</tr>
</tbody>
</table>


如果需要更加精细地分配权限，可以修改各个 Exchange 2007 对象（如地址列表或数据库）上的 ACL。您必须将用户或用户是其成员的安全组直接添加到 ACL。然后，在特定用户的上下文中执行操作。

有关如何在 Exchange 2007 中管理权限的详细信息，请参阅[在 Exchange Server 2007 中配置权限](http://go.microsoft.com/fwlink/p/?linkid=90671)。

## Exchange 2013 和 Exchange 2007 共存权限

因为 Exchange 2013 的权限模型与 Exchange 2007 的权限模型不同，所以 Exchange 2013 权限分配独立于 Exchange 2007 权限分配。即使在同一林中同时安装了这两个版本的 Exchange，情况也是如此。如果不进行额外配置，则 Exchange 2013 管理员没有管理基于 Exchange 2007 的服务器的所需权限，Exchange 2007 管理员也没有管理基于 Exchange 2013 的服务器的所需权限。应考虑以下问题：

  - 是否要授予 Exchange 2013 管理员管理 Exchange 2007 服务器的访问权限？

  - 是否要授予 Exchange 2007 管理员管理 Exchange 2013 服务器的访问权限？

  - 是否要自定义 Exchange 2013 权限，以便这些权限匹配对 Exchange 2007 ACL 所进行的任何自定义？

## 授予 Exchange 2007 管理员 Exchange 2013 权限

如果您希望 Exchange 2007 管理员管理 Exchange 2013 服务器，则必须将 Exchange 2007 管理员添加为一个或多个 Exchange 2013 角色组的成员。可以将用户或 USG 添加到角色组中。然后，为角色组授予的权限会应用于作为成员添加的用户或 USG。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用域本地或全局 Active Directory 安全组，则在需要将其添加为 Exchange 2013 角色组的成员时，必须将其更改为 USG。Exchange 2013 只支持 USG。</td>
</tr>
</tbody>
</table>


下表说明了 Exchange 2007 管理员角色和 Exchange 2013 角色组之间的映射。

### Exchange 2007 管理员角色和 Exchange 2010 角色组

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007 管理员角色</th>
<th>Exchange 2013 角色组</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 组织管理员</p></td>
<td><p>组织管理</p></td>
</tr>
<tr class="even">
<td><p>Exchange 收件人管理员</p></td>
<td><p>收件人管理</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server 管理员</p></td>
<td><p>服务器管理</p></td>
</tr>
<tr class="even">
<td><p>Exchange 仅查看管理员</p></td>
<td><p>仅查看组织管理</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Exchange 2013 中没有等效角色组</p>
<p>（有关如何创建自定义角色组的详细信息，请参阅<a href="manage-role-groups-exchange-2013-help.md">管理角色组</a>。）</p></td>
</tr>
<tr class="even">
<td><p>Exchange 公用文件夹管理员</p></td>
<td><p>公用文件夹管理</p></td>
</tr>
</tbody>
</table>


如果所有 Exchange 2007 管理员都是 Exchange 2007 管理角色之一的成员，则可以将每个管理组的成员添加到其等效的 Exchange 2013 角色组。例如，如果要授予所有 Exchange 2007 组织管理员对 Exchange 2013 对象的完全访问权限，请将 Exchange 组织管理员 USG 添加到 组织管理 角色组。

有关如何向角色组添加用户和 USG 的详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

如果您修改 Exchange 2007 对象上的 ACL 以便向 Exchange 2007 管理员授予更精细的权限，并且如果要为这些管理员分配 Exchange 2013 服务器的类似权限，请按照以下步骤执行：

1.  查看对 Exchange 2007 对象进行的 ACL 自定义，并查找被授予了针对每个对象的权限的管理员。

2.  对每个 Exchange 2007 对象进行分类。例如，确定对象是数据库、服务器还是收件人对象。

3.  将对象映射到相应的 Exchange 2013 角色组。有关内置角色组的列表，请参阅[内置的角色组](built-in-role-groups-exchange-2013-help.md)。

4.  将每种对象类型的 USG 或用户添加到相应的 Exchange 2013 角色组。有关如何向角色组添加用户和 USG 的详细信息，请参阅[管理角色组成员](manage-role-group-members-exchange-2013-help.md)。

完成这些步骤之后，Exchange 2007 管理员将成为映射到相应 Exchange 2013 对象的特定角色组的成员。Exchange 2007 管理员可以使用 Exchange 2013 管理工具来管理 Exchange 2013 服务器和收件人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>通常，Exchange 2007 服务器和收件人必须使用 Exchange 2007 管理工具进行管理，Exchange 2013 服务器和收件人必须使用 Exchange 2013 管理工具进行管理。</td>
</tr>
</tbody>
</table>


如果内置角色组没有提供要授予某些管理员的一组特定权限，则可以创建自定义角色组。创建自定义角色组时，可以选择要向其添加的角色。可以定义希望角色组的成员进行管理的特定功能。例如，如果希望管理员只管理通讯组，则可以创建一个自定义角色组，然后只选择通讯组角色。执行此操作之后，该自定义角色组的成员只能管理通讯组。有关如何创建自定义角色组的详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)。

如果您分配针对特定 Exchange 2007 对象的选择性权限（例如，只允许管理员管理特定数据库），并且要将同一配置应用于 Exchange 2013 服务器，请参阅本主题后面的\&quot;使用 Exchange 2007 中的管理作用域重新创建 Exchange 2013 ACL 自定义\&quot;。

## 授予 Exchange 2013 管理员 Exchange 2007 权限

如果您希望 Exchange 2013 管理员管理 Exchange 2007 服务器，请将 Exchange 2013 管理员添加到 USG 或与特定 Exchange 2007 管理员角色对应的安全组。或者，如果自定义了 ACL 设置，请将管理员添加到相应的 ACL。角色组是 USG，因此可以将角色组直接添加到 Exchange 2007 管理员角色 USG。

完成后，Exchange 2013 管理员将成为相应 Exchange 2007 管理员角色的成员。Exchange 2013 管理员可以使用 Exchange 2007 管理工具来管理 Exchange 2007 服务器和收件人。

## 使用 Exchange 2013 中的管理作用域重新创建 Exchange 2007 ACL 自定义

在 Exchange 2007 中，如果您希望限制哪些人可以管理特定邮箱存储、管理特定用户或控制在其上创建邮箱的邮箱存储，则必须修改要限制的对象的 ACL。通过 Exchange 2013，您不必修改任何 ACL，即可实现此操作。它通过使用管理作用域来达到此目的，管理作用域是 RBAC 的组件。

管理作用域提供了内置作用域和自定义作用域来定义管理员可以管理的对象。通过应用管理作用域，能够定义可以管理哪些收件人、可以在哪些邮箱数据库上创建邮箱，以及哪些收件人或服务器应由小型管理员组管理，而不是由其他人管理。

您可以创建以下类型的管理作用域：

  - **预定义相对**   预定义相对作用域包括在 Exchange 2013 中。可以控制用户看到的内容以及用户修改的内容。例如，预定义相对作用域可以控制用户是只能看到有关自己的信息还是能看到有关整个组织的信息。

  - **收件人**   收件人作用域控制管理员可以创建、修改或删除哪些收件人。这些选择可以基于组织单元 (OU)、收件人筛选器或者基于这两者。收件人筛选器指定的条件收件人必须匹配才能包括在作用域中。例如，可以创建包括特定位置或特定部门中所有用户的收件人筛选器作用域。甚至可以将 OU 和收件人筛选器组合，以便匹配位于特定 OU 中且向特定经理报告的用户。

  - **服务器**   服务器作用域控制管理员可以管理哪些服务器。可以指定服务器列表或服务器筛选器。对于服务器列表，可定义可以管理的服务器的静态列表。服务器筛选器的工作方式与收件人筛选器相同，也可以指定必须匹配的条件。例如，可以创建匹配特定 Active Directory 站点中的所有服务器的服务器作用域。

  - **数据库**   数据库作用域控制管理员可以管理哪些数据库。它们也可控制可以在哪些数据库上创建邮箱，或者可以将邮箱移到哪些数据库。与服务器作用域一样，可以将其定义为列表或筛选器。例如，可以创建一个列表或筛选器，以便允许管理员在特定子公司管理的特定邮箱数据库上创建邮箱或将邮箱移动到该数据库。

  - **独占**   收件人、服务器和数据库作用域还可以创建为独占作用域。独占作用域的工作方式与 ACL 中的拒绝访问 ACE 相同。如果有任何对象匹配独占作用域，则只有分配了独占作用域的管理员才能管理该对象。即使另一个非独占的作用域匹配同一个对象，情况也是如此。当您只希望几个高度信任的个人可以管理高级管理人员的邮箱时，这尤其有用。即使另一个常规收件人作用域范围更广并且在其作用域中包括高级管理人员的邮箱，分配了范围更广的常规收件人作用域的管理员也无法管理该高级管理人员的邮箱，除非他们也分配了独占作用域。

管理作用域与管理角色、管理角色分配和管理角色组一起使用，以控制谁可以管理哪些对象以及可以采用何种方式管理这些对象。有关详细信息，请参阅下列主题：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解独占作用域](understanding-exclusive-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

  - [了解管理角色组](understanding-management-role-groups-exchange-2013-help.md)

  - [了解管理角色](understanding-management-roles-exchange-2013-help.md)

若要使用管理作用域（可能已经使用自定义 ACL 进行了定义）在 Exchange 2013 中创建相同的权限模型，必须对已经自定义的 ACL 进行编录并创建与其匹配的管理作用域。可以使用收件人、服务器和数据库对象上可用的可筛选属性创建管理作用域，这些作用域包括希望每个管理作用域控制其访问权限的对象。有关可以与管理作用域筛选器一起使用的属性的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

有关如何创建管理作用域的详细信息，请参阅[创建常规或独占作用域](create-a-regular-or-exclusive-scope-exchange-2013-help.md)。

