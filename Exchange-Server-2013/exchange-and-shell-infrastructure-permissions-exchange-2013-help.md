---
title: 'Exchange 和命令行管理程序基础结构权限: Exchange 2013 Help'
TOCTitle: Exchange 和命令行管理程序基础结构权限
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 50490276
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 和命令行管理程序基础结构权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

执行配置 Microsoft Exchange Server 2013 各种组件的任务所需要的权限取决于要执行的步骤或要运行的 cmdlet。请参见本主题中的各节以获取有关其各自功能的详细信息。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    > [!NOTE]  
    > 必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

> [!NOTE]  
> 某些功能可能要求在要管理的服务器上拥有本地管理员权限。若要管理这些功能，必须是该服务器上 Local Administrators 组的成员。


## Exchange 基础结构权限

下表列出了执行配置 Exchange 2013 常规设置的任务所需要的权限。

分配了仅限查看管理角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>所需的权限</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>管理员审核日志记录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 管理中心配置设置</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 管理中心连接性</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 服务器配置设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 帮助设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮件类别</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="odd">
<td><p>产品密钥</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>测试系统运行状况</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>仅查看管理员审核日志记录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p>

> [!NOTE]  
> 还可以手动将“仅查看审核日志”管理角色分配给管理角色组。有关详细信息，请参阅<a href="view-only-audit-logs-role-exchange-2013-help.md">仅查看审核日志角色</a>。

</td>
</tr>
<tr class="even">
<td><p>写入审核日志</p></td>
<td><p>属于任何角色组或分配了任何管理角色的用户都可以写入管理员审核日志。</p></td>
</tr>
</tbody>
</table>


## 命令行管理程序基础结构权限

下表列出了执行配置各种功能控制 Exchange 命令行管理程序如何运行所需要的权限。

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
<td><p>Active Directory 域服务服务器设置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="um-management-exchange-2013-help.md">UM 管理</a></p></td>
</tr>
<tr class="even">
<td><p>Cmdlet 扩展代理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>PowerShell 虚拟目录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>PowerShell 和 WinRM 安装</p></td>
<td><p>本地服务器管理员</p></td>
</tr>
<tr class="odd">
<td><p>远程命令行管理程序</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


## 联合身份验证和证书权限

下表列出了执行与联合信任、OAuth 配置、证书管理及混合部署配置相关的任务所需的权限。

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
<td><p>证书管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>联合信任、OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>测试联合信任、OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">仅查看组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>混合部署配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>组织内部连接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
</tbody>
</table>

