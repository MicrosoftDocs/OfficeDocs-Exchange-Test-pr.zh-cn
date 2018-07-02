---
title: '查看角色作用域: Exchange 2013 Help'
TOCTitle: 查看角色作用域
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 50489895
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看角色作用域

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-03_

管理角色作用域确定向用户提供哪些对象，以便可以使用 cmdlet 以及为其分配的参数更改这些对象。可以查看作用域，以确定哪些作用域已添加到组织、确定特定作用域的配置或确定哪些作用域是孤立作用域。

有关 Microsoft Exchange Server 2013 中管理角色作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

要查找与角色作用域相关的其他管理任务吗？请查看[高级权限](advanced-permissions-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [角色管理权限](role-management-permissions-exchange-2013-help.md)主题中的\&quot;管理作用域\&quot;条目。

  - 您必须使用命令行管理程序执行这些过程。

  - 本主题使用了管道传输和 **Format-List** cmdlet。有关这些概念的详细信息，请参阅下列主题：
    
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

## 查看特定作用域

可以查看作用域的详细信息，方法是将 **Get-ManagementScope** cmdlet 的输出通过管道传递给 **Format-List** cmdlet。

若要查看特定作用域的详细信息，请使用以下语法。

    Get-ManagementScope <scope name> | Format-List

此示例将检索 Seattle Servers 作用域的详细信息。

    Get-ManagementScope "Seattle Servers" | Format-List

有关语法和参数的详细信息，请参阅 [Get-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd298180\(v=exchg.150\))。

## 列出所有作用域

此示例将检索组织中的作用域列表。

    Get-ManagementScope

此 cmdlet 将检索独占作用域和常规作用域。如果要仅返回独占作用域或常规作用域，请参阅本主题后面的\&quot;仅列出所有独占作用域或常规作用域\&quot;。

有关语法和参数的详细信息，请参阅 [Get-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd298180\(v=exchg.150\))。

## 列出所有孤立作用域

*\&quot;孤立作用域\&quot;*是尚未与任何管理角色分配关联的作用域。

此示例将检索孤立作用域列表。

    Get-ManagementScope -Orphan

有关语法和参数的详细信息，请参阅 [Get-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd298180\(v=exchg.150\))。

## 仅列出所有独占作用域或常规作用域

默认情况下，**Get-ManagementScope** cmdlet 会返回一个包含独占作用域和常规作用域的作用域列表。如果要仅返回独占作用域或仅返回常规作用域，请使用以下语法。

    Get-ManagementScope -Exclusive < $true | $false >

此示例将仅返回独占作用域。

    Get-ManagementScope -Exclusive $true

此示例将仅返回常规作用域列表。

    Get-ManagementScope -Exclusive $false

有关语法和参数的详细信息，请参阅 [Get-ManagementScope](https://technet.microsoft.com/zh-cn/library/dd298180\(v=exchg.150\))。

