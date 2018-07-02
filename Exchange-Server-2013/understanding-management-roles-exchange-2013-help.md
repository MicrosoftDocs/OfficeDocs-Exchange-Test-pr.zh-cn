---
title: '了解管理角色: Exchange 2013 Help'
TOCTitle: 了解管理角色
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50491123
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解管理角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

管理角色是 Microsoft Exchange Server 2013 中所使用的基于角色的访问控制 (RBAC) 权限模型的组成部分。角色充当 cmdlet 的逻辑分组，这些 cmdlet 组合在一起提供查看或修改 Exchange 2013 组件配置（如邮箱、传输规则和收件人）的访问权限。管理角色可以进一步组合到称为管理角色组和管理角色分配策略的更大分组，从而实现管理功能区域和收件人配置。角色组和角色分配策略分别为管理员和最终用户分配权限。有关管理角色组和管理角色分配策略的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

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


**目录**

内置管理角色

未区分范围的顶级管理角色

自定义管理角色

管理角色层次结构

管理角色条目

未区分范围的顶级角色条目

管理角色类型

详细信息

管理角色作用域和管理角色分配是管理角色操作的重要组件。有关这些组件的详细信息，请参阅下列主题：

  - [了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)

  - [了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)

若要了解与管理角色相关的管理任务，请参阅[权限](permissions-exchange-2013-help.md)。

## 内置管理角色

Exchange 2013 提供了多种内置管理角色，您可以使用这些角色来管理您的组织。每个角色都包括用户管理特定 Exchange 组件所必需的 cmdlet 和参数。以下是一些内置管理角色的示例：

  - **邮件收件人**   使管理员可以管理邮箱、联系人和邮件用户。

  - **传输规则：** 使获得该角色的管理员或专家用户能够管理传输规则功能。

  - **通讯组：** 使获得该角色的管理员或专家用户能够管理通讯组和通讯组成员。

  - **MyPersonalInformation**   使最终用户可以修改其家庭电话号码和网站地址。

有关 Exchange 2013 中附带的管理角色的完整列表，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

可以使用 Exchange 2013 中附带的内置角色，并以任意方式对其进行组合，以创建适合您业务的权限模型。例如，如果要让某个角色组的成员管理收件人和公用文件夹，则将 Mail Recipients 和 Public Folders 角色都分配给该角色组。通常，角色将分配给角色组或角色分配策略。如果要更细致地控制权限，还可以将管理角色直接分配给用户。建议使用角色组和角色分配策略而不是直接使用用户角色分配，以简化权限模型。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您只能将最终用户管理角色分配到角色分配策略。</td>
</tr>
</tbody>
</table>


内置管理角色无法更改。但是，可以基于内置管理角色创建管理角色，然后将这些新角色分配到角色组或角色分配策略。然后，可以更改新的管理角色以满足您的需要。这是高级任务，一般极少需要执行此过程。

有关基于内置 Exchange 角色创建自定义角色的详细信息，请参阅本主题后面的自定义管理角色一节。

您需要为其分配管理角色，以使其生效。通常，管理角色将分配给角色组和角色分配策略。在某些情况下，还可以将角色直接分配给用户，但这是高级任务，一般极少需要执行此过程。

有关分配管理角色的详细信息，请参阅下列主题：

  - [管理角色组](manage-role-groups-exchange-2013-help.md)

  - [管理角色分配策略](manage-role-assignment-policies-exchange-2013-help.md)

  - [向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

有关管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

返回顶部

## 未区分范围的顶级管理角色

未区分范围的顶级管理角色是一种特殊类型的管理角色，使您能够通过使用 RBAC 为用户授予访问自定义脚本和非 Exchange cmdlet 的权限。常规管理角色仅提供对 Exchange cmdlet 的访问。如果需要提供对运行于 Exchange 服务器上的非 Exchange cmdlet 的访问，或者需要发布用户可运行的脚本，则需要将这些 cmdlet 和脚本添加到无作用域角色。它们称为顶级角色，因为如果创建一个未区分范围的角色，而没有从父角色派生时，则该角色没有父级，而且是 Exchange 2013 中附带的内置管理角色的对等方。若要表明要创建未区分范围的顶级角色条目，需要使用 *UnscopedTopLevel* 开关和 **New-ManagementRole** cmdlet。

无作用域角色也是使用相同方法进行命名的，因为与常规管理角色不同，其作用域不能限定在某个特定范围内。无作用域角色始终覆盖整个组织范围。这意味分配了未区分范围角色的人员可以修改 Exchange 2013 组织中的任何对象。因此，必须特别小心，确保对无作用域角色可使用的脚本和 cmdlet 进行全面的测试，以便了解它们将要修改的内容，并确保慎重分配无作用域角色。

未区分范围角色可以分配给诸如角色组、管理角色、用户和通用安全组 (USG) 等角色接受者。但不能将它们分配给管理角色分配策略。

尽管不能将 Exchange cmdlet 作为管理角色条目添加到无作用域角色上，但可以将它们包含在脚本中，然后将这些脚本作为角色条目添加。通过此操作，您可以创建自定义脚本，由这些脚本来执行本可分配给用户的 Exchange 任务。当用户必须执行通常属于其管理级别之外的高权限任务，以及草拟新管理角色或角色组出现问题时，这种方案非常有用。可以创建可执行此特定功能的脚本，将其添加到某个无作用域角色，然后将该无作用域角色分配给用户。此时，该用户则只能执行由该脚本提供的特定功能。

添加到未区分范围角色的角色条目必须也指定为未区分范围的顶级角色条目。有关未区分范围的顶级角色条目的详细信息，请参阅本主题后面的未区分范围的顶级角色条目。

默认情况下，组织管理 角色组没有创建或管理无作用域角色组的权限。这是为了防止对无作用域角色组的误创建或误修改。组织管理 角色组可将“无作用域的角色管理”管理角色委派给自身和其他角色受理人。有关如何创建未区分范围的顶级管理角色的详细信息，请参阅[创建一个未区分范围的角色](create-an-unscoped-role-exchange-2013-help.md)。

返回顶部

## 自定义管理角色

如果内置管理角色不符合用户的需要，可以基于内置 Exchange 角色创建自定义管理角色。创建自定义管理角色后，新的子角色将会继承父角色的所有管理角色条目。然后可以选择要保留在自定义管理角色中的管理角色条目，并删除所有不需要的条目。

自定义角色将成为创建新角色所使用角色的子项。您只能在新子角色中使用父角色中存在的管理角色条目。有关详细信息，请参阅本主题后面的章节：

  - 管理角色层次结构

  - 管理角色条目

创建自定义管理角色需要多个步骤，并且它是一项高级任务，一般极少需要执行。在创建自定义管理角色之前，确信现有内置管理角色中的任何一个都无法提供您所需的权限。有关内置管理角色的详细信息，或者要创建自定义管理角色，请参阅下列主题：

  - [内置管理角色](built-in-management-roles-exchange-2013-help.md)

  - [高级权限](advanced-permissions-exchange-2013-help.md)

有关如何创建管理角色的详细信息，请参阅[创建角色](create-a-role-exchange-2013-help.md)。

返回顶部

## 管理角色层次结构

管理角色存在父级和子级层次结构。默认情况下，层次结构的顶级是 Exchange 2013 中提供的内置管理角色。在创建角色时，将构建父角色的副本。新角色是所复制角色的子项。然后可以对新角色进行自定义，以满足您要为他们分配该角色的管理员或用户的需要。

可以使用自定义角色来创建角色。从现有自定义角色创建角色后，现有自定义角色仍然为其父角色的子级，同时还会成为新角色的父级。在每次复制角色时，新的子角色只能包含存在于直接父角色中的角色条目。

每个管理角色被赋予的角色类型都无法更改。角色类型用于定义角色使用的基本上下文。在创建子角色时，将从父角色复制角色类型。

**管理角色层次结构**

![RBAC 管理角色层次结构图](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "RBAC 管理角色层次结构图")

上图说明了若干个管理角色的层次结构关系。Mail Recipients 和 Help Desk 角色均为内置角色。从这些角色派生的所有子角色都将继承各个内置角色的角色类型。例如，从 Mail Recipients 角色直接或间接派生的所有子角色都将继承 `MailRecipients` 角色类型。

Seattle Recipient Administrators 自定义角色是 Mail Recipients 内置角色的子项，同时也是 Seattle Sales Recipient Administrators 自定义角色和 Seattle Legal Recipient Administrators 自定义角色的父项。Seattle Recipient Administrators 自定义角色仅包含 Mail Recipients 角色中可用的 cmdlet 子集。Seattle Recipient Administrators 自定义角色的子角色只能包含也存在于该角色中的 cmdlet。例如，如果某个 cmdlet 存在于 Mail Recipients 角色中，但该 cmdlet 不存在于 Seattle Recipient Administrators 自定义角色中，则不能将此 cmdlet 添加到 Seattle Sales Recipient Administrators 自定义角色中。

所有自定义角色都遵循与以上讨论的角色相同的模式。有关如何在管理角色上控制对 cmdlet 的访问的详细信息，请参阅本主题的下一节管理角色条目。

返回顶部

## 管理角色条目

每个管理角色，无论是自定义 Exchange 角色还是无作用域角色，都必须至少有一个管理角色条目。角色条目包含单个 cmdlet 及其参数、脚本或您希望使其可用的特殊权限。如果 cmdlet 或脚本在某个管理角色上未作为项出现，则将无法通过该角色访问此 cmdlet 或脚本。同样，如果参数不存在于某个项中，将无法通过该角色访问此 cmdlet 或脚本上的参数。

使用 Exchange 2013，可以管理基于内置 Exchange 管理顶级角色的角色条目和基于未区分范围的顶级管理角色的角色条目。基于内置 Exchange 顶级角色的角色只能包含作为 Exchange 2013 cmdlet 的角色条目。若要添加自定义脚本或非 Exchange cmdlet 以供用户使用，则需要将其作为未区分范围角色条目添加到未区分范围的顶级角色中。有关无作用域角色条目的详细信息，请参阅本主题中后面的未区分范围的顶级角色条目一节。

所有角色条目，无论该角色条目是基于 Exchange cmdlet 的角色条目还是无作用域的角色条目，都遵循相同的原则，这些原则将在下面的章节中说明。

有关管理角色条目的详细信息，请参阅[管理角色和角色条目](management-roles-and-role-entries-exchange-2013-help.md)。

## 父项和子项管理角色关系

如先前所述，管理角色条目，包括 cmdlet 及其参数，必须存在于直接父角色中，才能将该项添加到子角色中。例如，如果父角色没有 **New-Mailbox** 项，则无法向子角色分配此 cmdlet。此外，如果 **Set-Mailbox** 在父角色中，但 *Database* 参数已从该项中删除，则不能将 **Set-Mailbox** cmdlet 上的 *Database* 参数添加到子角色上的条目中。

由于当管理角色条目未出现在父角色中时，不能将这些条目添加到子角色中，而且由于角色基于特定角色类型，因此在要创建自定义角色时，必须慎重选择要复制的父角色。

返回顶部

## 管理角色条目名称

管理角色条目名称是其所关联的管理角色和 cmdlet 或脚本的名称的组合。角色名称与 cmdlet 或脚本用反斜杠字符 (\\) 分隔。例如，Mail Recipients 角色上的 **Set-Mailbox** cmdlet 的角色条目名称为 `Mail Recipients\Set-Mailbox`。如果角色条目的名称中包含空格，则必须使用引号 (") 将整个名称括起来。

可以在角色条目名称中使用通配符 (\*) 来返回与提供的输入匹配的所有角色条目。通配符可在反斜杠字符的任一端使用。下表列出了有关如何在角色条目名称中使用通配符的一些不同方法。

**带通配符的管理角色条目名称**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>示例</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>返回所有角色的所有角色条目的列表。</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>返回包含 <strong>Set-Mailbox</strong> cmdlet 的所有角色条目的列表。</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>返回 Mail Recipients 角色中的所有角色条目的列表。</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>返回 Mail Recipients 角色中包含以 Mailbox 结尾的 cmdlet 的所有角色条目列表。</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>返回以 My 开头的所有角色的、cmdlet 名称中包含字符串 Group 的所有角色条目的列表。</p></td>
</tr>
</tbody>
</table>


## 未区分范围的顶级角色条目

未区分范围的顶级角色条目可以与未区分范围的顶级管理角色一起使用，以便基于自定义脚本或非 Exchange cmdlet 创建角色。每个无作用域的角色条目都与单个自定义脚本或非 Exchange cmdlet 相关联。若要表明要在未区分范围角色上创建未区分范围的角色条目，需要对 **Add-ManagementRoleEntry** cmdlet 指定 *UnscopedTopLevel* 参数。

在添加无作用域的角色条目时，需要指定可以与脚本或非 Exchange cmdlet 一起使用的所有参数。Exchange 会尝试验证您在添加角色条目时所提供的参数。只有在创建角色条目时添加到角色条目中的参数，才可用于分配给该无作用域角色的用户。如果将参数添加到脚本或非 Exchange cmdlet，或者对参数进行了重命名，则必须手动更新该角色条目。Exchange 不会检查无作用域角色条目上的现有参数是否已经更改。如果在脚本中更改了角色条目上的参数，则当您尝试使用该参数时，该命令会失败。

添加到无作用域角色条目的脚本必须位于管理员和用户使用 Exchange 2013 命令行管理程序进行连接的每个服务器上的 Exchange 脚本目录中。如果尝试添加无作用域的角色条目，而将用于添加角色条目的服务器上的 Exchange 2013 脚本目录中不存在所基于的脚本，则会发生错误。Exchange 2013 脚本目录的默认安装位置为 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts。

添加到无作用域角色条目的非 Exchange cmdlet 必须安装在管理员和用户使用命令行管理程序进行连接并将使用其 cmdlet 的每个 Exchange 2013 服务器上。如果尝试添加无作用域的角色条目，而将用于添加角色条目的 Exchange 服务器上未安装所基于的非 Exchange 2013 cmdlet，则会发生错误。在添加非 Exchange cmdlet 时，必须指定包含非 Windows cmdlet 的 Exchange PowerShell 管理单元名称。

有关如何添加无作用域管理角色条目的详细信息，请参阅[向角色添加角色](add-a-role-entry-to-a-role-exchange-2013-help.md)。

返回顶部

## 管理角色类型

管理角色类型是所有管理角色的基础。类型定义隐式作用域，隐式作用域将在某个特定角色类型的所有管理角色上定义，而且类型还充当相关角色的逻辑分组。派生自父级内置管理角色的所有管理角色都具有相同的角色类型。有关此关系的说明，请参阅本主题前面的管理角色层次结构图。管理角色类型还表示可以添加到与角色类型关联的角色中的 cmdlet 及其参数的最大集合。

管理角色类型分为以下类别：

  - **管理或专家：** 与管理或专家角色类型关联的角色在 Exchange 组织中具有更广泛的影响作用域。此角色类型的角色可以启用以下任务：服务器或收件人管理、组织配置、合规性管理和审核等。

  - **以用户为中心：** 与以用户为中心的角色类型关联的角色具有与单个用户密切相关的影响范围。此角色类型的角色可以启用以下任务：用户配置文件配置与自我管理、对用户拥有的通讯组的管理等。
    
    与以用户为中心角色类型相关联的角色名称，以及以用户为中心的角色类型名称均以 My 开头。

  - **专用：** 与专用角色类型相关联的角色可以启用不属于管理或以用户为中心角色类型的任务。此角色类型的角色可以启用诸如应用程序模拟和使用非 Exchange cmdlet 或脚本等任务。

下表列出了 Exchange 2013 中的所有“管理”管理角色类型，以及该角色类型允许的配置将应用于整个 Exchange 组织，还是仅应用于单台服务器。有关与这些角色类型相关联的每个管理角色的详细信息，包括每个角色的描述、谁可以通过分配该角色而获益以及其他信息，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

**管理角色类型**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色类型</th>
<th>内置管理角色</th>
<th>描述</th>
<th>组织或服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory 权限角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够配置组织中的 Active Directory 权限。使用 Active Directory 权限或访问控制列表 (ACL) 的部分功能包括传输“接收”和“发送”连接器以及邮箱的“代理发送”和“代表发送”权限。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>直接在 Active Directory 对象上设置的权限不能通过 RBAC 强制应用。</td>
</tr>
</tbody>
</table>

</td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">地址列表角色</a></p></td>
<td><p>与此角色类型相关联的角色类型使管理员能够管理组织中的地址列表、全局地址列表 (GAL) 和脱机地址列表。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 角色</a></p></td>
<td><p>与此角色类型相关联的角色类型使应用程序能够模拟组织中的用户来代表用户执行任务。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 角色</a></p></td>
<td><p>与此角色类型相关联的角色使合作伙伴应用程序能够将项目存档到组织的用户邮箱中。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">审核日志角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的管理员审核日志记录配置。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">cmdlet 扩展代理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的 cmdlet 扩展代理。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">数据丢失防护角色</a></p></td>
<td><p>与此角色类型相关联的角色可以在组织中创建和管理数据丢失预防 (DLP) 策略以及这些策略内的规则。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">数据库可用性组角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的数据库可用性组 (DAG)。直接或间接被分配此角色的管理员是负责组织中高可用性配置的最高级别管理员。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">数据库副本角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在单台服务器上管理数据库副本。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">数据库角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在各个服务器上创建、管理、装载和卸除邮箱数据库。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">灾难恢复角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中还原邮箱和邮箱数据库、创建邮箱数据库以及执行数据库可用性组的数据中心来回切换。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">通讯组角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中创建和管理通讯组和通讯组成员。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">边缘订阅角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中 Exchange 2010 边缘传输服务器与 Exchange 2013 邮箱服务器之间的边缘同步和订阅配置。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">电子邮件地址策略角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的电子邮件地址策略。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange 连接器角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够创建、修改、查看并删除传递代理连接器。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange Server 证书角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在单台服务器上创建、导入、导出和管理 Exchange 服务器证书。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange 服务器角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在单台服务器上管理 Exchange 服务器配置。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange 虚拟目录角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在各个服务器上管理 Outlook Web App、Microsoft ActiveSync、脱机通讯簿 (OAB)、自动发现、Windows PowerShell 和 Exchange 管理中心虚拟目录。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">联合共享角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的跨林和跨组织共享。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">信息权限管理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中 Exchange 的信息权限管理 (IRM) 功能。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">日记角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的日记配置。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">法定保留角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够配置邮箱中的数据是否应保留用于组织的诉讼目的。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">邮箱导入导出角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够导入和导出邮箱内容，以及清除邮箱中不需要的内容。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">邮箱搜索角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中搜索一个或多个邮箱的内容。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 角色</a></p></td>
<td><p>与此角色类型相关联的角色使合作伙伴应用程序能够在组织中设置和查看邮箱的合法保留状态。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">启用邮件的公用文件夹角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够将组织中的各个公用文件夹配置为是启用还是禁用邮件功能。</p>
<p>使用此角色类型只能管理公用文件夹的电子邮件属性。它不允许您管理不属于电子邮件属性的公用文件夹属性。要管理不属于电子邮件属性的公用文件夹属性，需要分配与 <code>PublicFolders</code> 角色类型相关联的角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">邮件收件人创建角色</a></p>
<p></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中创建邮箱、邮件用户、邮件联系人、通讯组和动态通讯组。可以将与此角色类型相关联的角色与 <code>MailRecipients</code> 类型结合使用，以便能够创建和管理收件人。</p>
<p>此角色类型不允许针对公用文件夹启用邮件功能。若要针对公用文件夹启用邮件功能，必须获得与 <code>MailEnabledPublicFolders</code> 角色类型相关联的角色。</p>
<p>如果在贵组织维护的拆分权限模型中，创建收件人的组不同于管理收件人的组，请将 <code>MailRecipientCreation</code> 角色分配给创建收件人的组，并将 <code>MailRecipients</code> 角色分配给管理收件人的组。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">邮件收件人角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中现有邮箱、邮件用户和邮件联系人、通讯组和动态通讯组。与此角色类型相关联的角色无法创建这些收件人，但可以将此角色同那些与 <code>MailRecipientCreation</code> 角色类型相关联的角色结合使用，以创建和管理收件人。</p>
<p>无法使用此类角色管理启用了邮件功能的公用文件夹或通讯组。若要管理已启用邮件功能的公用文件夹，必须获得与 <code>MailEnabledPublicFolders</code> 角色类型相关联的角色。若要管理通讯组，必须获得与 <code>DistributionGroups</code> 角色类型相关联的角色。</p>
<p>如果在贵组织维护的拆分权限模型中，创建收件人的组不同于管理收件人的组，请将 <code>MailRecipientCreation</code> 角色分配给创建收件人的组，并将 <code>MailRecipients</code> 角色分配给管理收件人的组。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">邮件提示角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的邮件提示。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">邮件跟踪角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够跟踪组织中的邮件。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">迁移角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够将邮箱和邮箱内容迁入或迁出服务器。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">监视角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够监视组织中的 Microsoft Exchange 服务和组件可用性。除了管理员，与此角色类型相关联的角色还可以与监视应用程序所使用的服务帐户结合使用来收集有关 Exchange 服务器状态的信息。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">移动邮箱角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中的服务器之间以及本地组织和其他组织之间的服务器之间移动邮箱。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 角色</a></p></td>
<td><p>与此角色类型相关联的角色使 Microsoft Office 扩展应用程序能够访问组织中的用户邮箱。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">组织的自定义应用角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中查看和修改其组织的自定义应用。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">组织市场应用角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中查看和修改其组织的商城应用。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">组织客户端访问角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的客户端访问服务器设置。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">组织配置角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中组织范围的设置。可以通过该角色类型控制的组织配置包括（但不限于）以下配置：</p>
<ul>
<li><p>是否为组织启用或禁用邮件提示。</p></li>
<li><p>托管文件夹主页的 URL。</p></li>
<li><p>Microsoft Exchange 收件人 SMTP 地址和备选电子邮件地址。</p></li>
<li><p>资源邮箱属性架构配置。</p></li>
<li><p>Exchange 管理中心和 Outlook Web App 的帮助 URL。</p></li>
</ul>
<p>此角色类型不包括 <code>OrganizationClientAccess</code> 或 <code>OrganizationTransportSettings</code> 角色类型中所包含的权限。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">组织传输设置角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织范围的传输设置，如组织中的系统消息、Active Directory 站点配置和其他组织范围内的传输设置。</p>
<p>使用此角色无法创建或管理传输接收或发送连接器、队列、安全机制、代理、远程和接受域或规则。若要创建或管理每个传输功能，必须获得与以下角色类型相关联的角色：</p>
<ul>
<li><p><strong>接收连接器：</strong> <code>ReceiveConnectors</code></p></li>
<li><p><strong>发送连接器：</strong> <code>SendConnectors</code></p></li>
<li><p><strong>传输队列：</strong> <code>TransportQueues</code></p></li>
<li><p><strong>传输安全机制：</strong> <code>TransportHygiene</code></p></li>
<li><p><strong>传输代理：</strong> <code>TransportAgents</code></p></li>
<li><p><strong>远程域和接受域：</strong> <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>传输规则：</strong> <code>TransportRules</code></p></li>
</ul></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 和 IMAP4 协议角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在单台服务器上管理 POP3 和 IMAP4 配置，如身份验证和连接设置。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">公用文件夹角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的公用文件夹。</p>
<p>此角色类型不允许管理公用文件夹是否已启用邮件。若要针对公用文件夹启用或禁用邮件功能，必须获得与 <code>MailEnabledPublicFolders</code> 角色类型相关联的角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">接收连接器角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理传输接收连接器配置，如对单台服务器的大小限制。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">收件人策略角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的收件人策略，如设置和移动设备策略。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">远程域和接受的域角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的远程域和接受域。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">重置密码角色</a></p></td>
<td><p>与此角色类型相关联的角色使组织中的用户能够重置各自的密码，使管理员能够重置用户的密码。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">保留管理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的保留策略。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">角色管理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的管理角色组、角色分配策略、管理角色、角色条目、角色分配和作用域。</p>
<p>获得与此角色类型相关联角色的用户可以覆盖 <strong>role group managed by</strong>、配置任何角色组，并可在任何角色组中添加或删除成员。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">安全组创建和成员身份角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够创建和管理组织中的 USG 及其成员身份。</p>
<p>如果在贵组织维护的拆分权限模型中，创建和管理 USG 的组不同于管理 Exchange 服务器的组，请将与此角色类型相关联的角色分配给该组。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">发送连接器角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的传输发送连接器。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">支持诊断角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在 Microsoft 支持服务人员的指导下在组织中执行高级诊断。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>与此角色类型相关联的角色授予对 cmdlet 和脚本的权限，而且这些 cmdlet 和脚本只应当在 Microsoft 客户服务和支持人员的指导下使用。</td>
</tr>
</tbody>
</table>

</td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">团队邮箱角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中定义一个或多个站点邮箱设置策略和管理站点邮箱。分配了与此角色类型相关联的角色的管理员可以管理不属于自己的站点邮箱。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 角色</a></p></td>
<td><p>与此角色类型相关联的角色使合作伙伴应用程序能够更新组织中的站点邮箱生命周期状态。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">传输代理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的传输代理。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">传输清洁角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的反垃圾邮件和防恶意软件功能。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">传输队列角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理单台服务器上的传输队列。</p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">传输规则角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的传输规则。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM 邮箱角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中邮箱和其他收件人的统一消息 (UM) 配置。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM 提示语角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中创建和管理自定义的 UM 语音提示。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">统一消息角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的统一消息服务。</p>
<p>使用此角色无法管理 UM 专用邮箱配置或 UM 提示语。若要管理特定于 UM 的邮箱配置，请使用与 <code>UMMailboxes</code> 角色类型相关联的角色。若要管理 UM 提示语，请使用与 <code>UMPrompts</code> 角色类型相关联的角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">无作用域的角色管理角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够在组织中创建和管理未区分范围的顶级管理角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">用户选项角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够查看组织中用户的 Outlook Web App 选项。可以使用与此角色类型相关联的角色来帮助用户诊断其配置问题。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 角色</a></p></td>
<td><p>与此角色类型相关联的角色使合作伙伴应用程序能够在组织中代表最终用户操作。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">仅查看审核日志角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够搜索组织中的管理员审核日志。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">仅查看配置角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够查看组织中所有的非收件人 Exchange 配置设置。可查看的配置示例为服务器配置、传输配置、数据库配置和整个组织配置。</p>
<p>可以将与此角色类型相关联的角色同那些与 <code>ViewOnlyRecipients</code> 角色类型相关联的角色结合使用，以创建可以查看组织中每个对象的角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">仅查看收件人角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够查看收件人的配置，如邮箱、邮件用户、邮件联系人、通讯组和动态通讯组。</p>
<p>可以将与此角色类型相关联的角色同那些与 <code>ViewOnlyConfiguration</code> 角色类型相关联的角色结合使用，以创建可以查看组织中每个对象的角色。</p></td>
<td><p>组织</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 角色</a></p></td>
<td><p>与此角色类型相关联的角色使管理员能够管理组织中的工作负荷管理策略。管理员可配置资源健康定义、工作负载分类并启用或禁用工作负载管理。</p></td>
<td><p>组织</p></td>
</tr>
</tbody>
</table>


下表列出了 Exchange 2013 中所有以用户为中心的管理角色类型及其关联内置管理角色。

**以用户为中心的角色类型**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色类型</th>
<th>以用户为中心的内置角色</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够查看和修改各自邮箱的基本配置和相关设置。</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">MyAddressInformation 角色</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 角色</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">MyMobileInformation 角色</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">MyPersonalInformation 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够修改自己的联系信息。该信息包括用户的地址和电话号码。</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">我的自定义应用角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够查看和修改其自定义应用。</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 角色</a></p></td>
<td><p>此角色类型与使各个用户能够对其邮箱执行基本诊断（如检索日历诊断信息）的角色相关联。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够在组织内查看和修改其在通讯组中的成员身份，但前提是这些通讯组允许操纵组成员身份。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够创建、修改和查看通讯组，并在他们所拥有的通讯组中修改、查看、删除和添加成员。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">MyDisplayName 角色</a></p>
<p><a href="myname-role-exchange-2013-help.md">MyName 角色</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够修改其名称。</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">我的市场应用角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够查看和修改其商城应用。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够查看其保留标记，并查看和修改其保留标记设置和默认设置。</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够创建站点邮箱并将它们连接到 Microsoft SharePoint 站点。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够创建、查看和修改其短信服务设置。</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 角色</a></p></td>
<td><p>与此角色类型相关联的角色使各个用户能够查看和修改其语音邮件设置。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 详细信息

[New-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/zh-cn/library/dd335173\(v=exchg.150\))

