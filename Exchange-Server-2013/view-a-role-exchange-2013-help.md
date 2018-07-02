---
title: '查看某个角色: Exchange 2013 Help'
TOCTitle: 查看某个角色
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50489966
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看某个角色

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

管理角色可以列入的各种方式，具体取决于所需的信息。例如，您可以选择返回只有特定角色类型，只有特定的 cmdlet 和参数，包含角色的角色或查看特定管理角色的详细信息。有关 Microsoft Exchange Server 2013中的管理角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

如果要在角色上查看所有管理角色条目的列表，请参阅[查看角色条目](view-role-entries-exchange-2013-help.md)。

若要了解与角色相关的其他管理任务，请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理角色\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 本主题将使用流水线技术， **Format-List**和**Format-Table** cmdlet。有关这些概念的详细信息，请参阅下列主题 ︰
    
      - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))
    
      - [使用命令输出](working-with-command-output-exchange-2013-help.md)

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


## 您想执行什么操作？

## 查看特定管理角色

还可以通过检索特定角色来查看特定角色的详细信息，方法是使用 **Get-ManagementRole** cmdlet 并将输出通过管道传输给 **Format-List** cmdlet。

要查看特定角色的详细信息，请使用以下语法。

    Get-ManagementRole <role name> | Format-List

本示例检索有关\&quot;邮件收件人\&quot;管理角色的详细信息。

    Get-ManagementRole "Mail Recipients" | Format-List

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出所有的管理角色

可以通过运行**Get-ManagementRole** cmdlet 时不指定任何角色来查看您的组织中的所有管理角色的列表。默认情况下，角色名称和角色类型的每个角色都包括在结果中。

本示例返回贵组织中所有角色的列表。

    Get-ManagementRole

若要返回您的组织中的特定属性的所有角色的列表，可以**Format-Table** cmdlet 将结果和在结果列表中指定所需的属性。使用以下语法。

    Get-ManagementRole | Format-Table <property 1>, <property 2...>

此示例返回组织中所有角色的列表，并包括 **Name** 属性和属性名以单词 **Implicit** 开头的任何属性。

    Get-ManagementRole | Format-Table Name, Implicit*

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出包含特定 cmdlet 的管理角色

通过在 **Get-ManagementRole** cmdlet 上使用 *Cmdlet* 参数，可以返回包含指定的 cmdlet 的角色列表。

要返回包含指定的 cmdlet 的角色列表，请使用以下语法。

    Get-ManagementRole -Cmdlet <cmdlet>

本示例返回包含 **New-Mailbox** cmdlet 的角色列表。

    Get-ManagementRole -Cmdlet New-Mailbox

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出包含特定参数的管理角色

您可以返回角色上**Get-ManagementRole** cmdlet 使用*CmdletParameters*参数中包含一个或多个指定的参数的列表。返回包含指定的所有参数的唯一角色。

当您使用*CmdletParameters*参数时，您可以选择包含*Cmdlet*参数。如果在*Cmdlet*参数，则返回包含您可以在您指定 cmdlet 指定的参数的唯一角色。如果不包括*Cmdlet*参数，包含的参数指定，角色而不考虑该 cmdlet 它们，则返回。

要返回包含指定参数的角色列表，请使用以下语法。

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

此示例返回包含 *Database* 和 *Server* 参数的角色列表，与这些参数所在的 cmdlet 无关。

    Get-ManagementRole -CmdletParameters Database, Server

此示例返回其中 *EmailAddresses* 参数仅存在于 **Set-Mailbox** cmdlet 上的角色的列表。

    Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses

还可以配合 *Cmdlet* 或 *CmdletParameters* 参数使用通配符 (\*) 以匹配部分 cmdlet 或参数名称。

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出特定角色类型的管理角色

通过在 **Get-ManagementRole** cmdlet 上使用 *RoleType* 参数，可以返回基于指定角色类型的角色列表。

要返回匹配指定角色类型的角色列表，请使用以下语法。

    Get-ManagementRole -RoleType <roletype>

本示例返回基于 `UmMailboxes` 角色类型的角色列表。

    Get-ManagementRole -RoleType UmMailboxes

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出父角色的直接子角色

您可以返回上**Get-ManagementRole** cmdlet 使用*GetChildren*参数指定的父角色的直接子级的角色的列表。返回包含指定为父角色的角色的角色。

要返回父角色的直接子角色的列表，请使用以下语法。

    Get-ManagementRole <parent role name> -GetChildren

此示例返回灾难恢复角色的直接子角色的列表。

    Get-ManagementRole "Disaster Recovery" -GetChildren

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

## 列出父角色下的所有子角色

可以通过在**Get-ManagementRole** cmdlet 使用*Recurse*参数的整个链的角色的列表从指定的父角色返回到最后子角色。*Recurse*参数指示**Get-ManagementRole** cmdlet 要向下递归通过发现直到到达最后一个子角色的每个父级和子级关系。在列表中，则返回包含父角色。

此示例返回父角色的所有子角色的列表。

    Get-ManagementRole <parent role name> -Recurse

本示例返回\&quot;邮件收件人\&quot;角色的所有子角色。

    Get-ManagementRole "Mail Recipients" -Recurse

有关语法和参数的详细信息，请参阅 [Get-ManagementRole](https://technet.microsoft.com/zh-cn/library/dd351125\(v=exchg.150\))。

