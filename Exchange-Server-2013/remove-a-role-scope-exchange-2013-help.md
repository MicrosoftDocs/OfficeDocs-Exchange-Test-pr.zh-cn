---
title: '删除角色的作用域: Exchange 2013 Help'
TOCTitle: 删除角色的作用域
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50491294
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除角色的作用域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-02_

管理角色的作用域确定哪些对象可供用户就可以更改使用的 cmdlet 和分配给用户的参数对象。如果您不再使用的作用域，它可以被删除。有关 Microsoft Exchange Server 2013中的管理角色作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理作用域\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 可以删除作用域之前，必须将作用域删除任何可能正在使用的管理角色分配。有关如何从角色分配中删除作用域的详细信息，请参阅[更改角色分配](change-a-role-assignment-exchange-2013-help.md)。

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


## 使用命令行管理程序删除作用域

若要删除作用域，请使用以下语法。

    Remove-ManagementScope <scope name>

例如，要删除\&quot;Dublin Servers\&quot;作用域，请使用以下命令。

    Remove-ManagementScope "Dublin Servers"

