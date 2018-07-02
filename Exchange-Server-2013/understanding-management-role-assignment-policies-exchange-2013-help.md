---
title: '了解管理角色分配策略: Exchange 2013 Help'
TOCTitle: 了解管理角色分配策略
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50490085
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解管理角色分配策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

*“管理角色分配策略”*是一个或多个最终用户管理角色的集合，使最终用户能够管理其自己的 Microsoft Exchange Server 2013 邮箱和通讯组配置。角色分配策略是 Exchange 2013 中基于角色的访问控制 (RBAC) 权限模型的一部分，使您能够控制最终用户可以修改的特定邮箱和通讯组配置设置。不同的用户组可以拥有对其专用的角色分配策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>本主题重点讲述高级 RBAC 功能。如果要管理基本的 Exchange 2013 权限（例如，使用 Exchange 管理中心 (EAC) 向角色组中添加成员或从角色组中删除成员，创建和修改角色组，或创建和修改角色分配策略），请参阅<a href="permissions-exchange-2013-help.md">权限</a>。</td>
</tr>
</tbody>
</table>


有关 RBAC 的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

**目录**

角色分配策略层

默认角色分配策略和显式角色分配策略

使用角色分配策略

角色分配策略管理

## 角色分配策略层

以下列表描述组成角色分配策略模型的各个层：

  - **邮箱：** 对邮箱分配一个角色分配策略。对某个邮箱分配角色分配策略时，将对该邮箱应用管理角色和角色分配策略之间的分配。此操作将向邮箱授予管理角色所提供的所有权限。

  - **管理角色分配策略：**  *“管理角色分配策略”*是 Exchange 2013 中的特殊对象。创建用户邮箱或更改邮箱上的角色分配策略时，用户将与角色分配策略关联。这也是您将最终用户管理角色分配到的对象。角色分配策略上的所有角色的组合定义用户可在其邮箱或通讯组上管理的所有事情。

  - **管理角色分配：**  *“管理角色分配”*是管理角色和角色分配策略之间的链接。将管理角色分配到角色分配策略，将允许使用在管理角色中定义的 cmdlet 和参数。在角色分配策略和管理角色之间创建角色分配时，无法指定任何作用域。由分配应用的作用域基于管理角色，该作用域是 `Self` 或 `MyGAL`。有关详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

  - **管理角色：**  *“管理角色”*是一组管理角色条目的容器。这些角色用于定义用户可使用其邮箱或通讯组来执行的特定任务。*“管理角色条目”*是允许执行管理角色中的每个特定任务的 cmdlet、脚本或特殊权限。您只能使用拥有角色分配策略的最终用户管理角色。有关详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

  - **管理角色条目：** 管理角色条目是管理角色上的单个条目，可确定哪些 cmdlet 和参数对管理角色和角色组可用。每个角色条目均由可通过管理角色访问的单个 cmdlet 和一些参数组成。

下图显示了前面列表中的每个角色分配策略层以及每个层如何与其他层相关。

**管理角色分配策略模型**

![角色分配模型关系](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "角色分配模型关系")

有关管理角色、角色分配和作用域的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

## 默认角色分配策略和显式角色分配策略

以下各节介绍了 Exchange 2013 中的这两种类型的角色分配策略。

## 默认角色分配策略

默认角色分配策略是在创建某个邮箱或将其移到运行 Exchange 2013 的服务器时分配到该邮箱的角色分配策略，它不使用 **New-Mailbox** 或 **Enable-Mailbox** cmdlet 上的 *RoleAssignmentPolicy* 参数提供。

Exchange 2013 包括向最终用户提供最常用权限的默认角色分配策略。可通过在默认角色分配策略上添加或删除管理角色，更改默认角色分配策略的默认权限。

如果要将内置默认角色分配策略替换为您自己的默认角色分配策略，则可以使用 **Set-RoleAssignmentPolicy** cmdlet 来选择新的默认设置。执行此操作时，如果不明确指定角色分配策略，则默认情况下将对任何新邮箱分配指定的角色分配策略。

更改默认角色分配策略时，不会自动对分配了默认角色分配策略的邮箱分配新的默认角色分配策略。如果要更新以前创建的邮箱，以使用已设置为默认设置的角色分配策略，则必须使用 **Set-Mailbox** cmdlet 来进行此操作。

## 显式角色分配策略

显式角色分配策略是使用 **New-Mailbox**、**Set-Mailbox** 或 **Enable-Mailbox** cmdlet 上的 *RoleAssignmentPolicy* 参数手动分配到邮箱的策略。分配显式角色分配策略时，新策略将立即生效，并替换以前分配的显式角色分配策略。

## 使用角色分配策略

角色分配策略使您能够根据用户需要能够配置的业务需求来定制权限。如果默认角色分配策略满足您的需要，则不必进行任何自定义设置。但是，如果拥有许多具有特殊需求的不同用户组，则可针对每个用户组创建角色分配策略。

使用的默认角色分配策略应当包含适用于广大用户的权限。然后，为每个特殊用户组创建角色分配策略并定制这些角色分配策略，以对其授予更多或更少的限制性权限。按此方式组织角色分配策略时，通过仅将角色分配策略显式分配到特殊用户，而大多数用户接收由默认角色分配策略提供的更常用权限，从而减少操作的复杂性。

一个邮箱只能拥有一个角色分配策略。所有用户（包括管理员和专家用户）均分配一个角色分配策略。如果希望用户拥有不同的权限集，则必须对该用户的邮箱分配另一个拥有所需权限的角色分配策略。

## 角色分配策略管理

若要添加新的角色分配策略，请首先创建一个角色分配策略，然后确定其是否应为默认的角色分配策略。创建角色分配策略之后，将管理角色分配到角色分配策略，然后将角色分配策略分配到邮箱。之后便可选择添加或删除管理角色，或者选择不同的角色分配策略作为默认设置。

下表列出了角色分配策略层以及可用于管理每个层的过程主题。

### 角色分配策略管理主题

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>角色分配策略模型层</th>
<th>管理主题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮箱</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">管理用户邮箱</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">更改邮箱的分配策略</a></p></td>
</tr>
<tr class="even">
<td><p>角色分配策略</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色分配策略</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>管理角色和分配</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">管理角色分配策略</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>管理角色条目</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">向角色添加角色</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">更改角色条目</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">从角色中删除一个角色条目</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>更改角色分配策略中管理角色的管理角色条目是一项高级任务，大多数情况下通常不需要执行此操作。您可以使用符合要求的预先存在的管理角色。有关详细信息，请参阅<a href="built-in-role-groups-exchange-2013-help.md">内置的角色组</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>

