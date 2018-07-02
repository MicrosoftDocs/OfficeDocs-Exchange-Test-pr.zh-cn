﻿---
title: '邮件流权限: Exchange 2013 Help'
TOCTitle: 邮件流权限
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50491986
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件流权限

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

执行与邮件流有关的任务所需的权限视所执行的过程或要运行的 cmdlet 而定。有关传输功能的详细信息，请参阅[邮件流](mail-flow-exchange-2013-help.md)。

该主题列出了管理 Microsoft Exchange Server 2013 中的邮件流功能所需的权限。有关 Office 365 权限与 Exchange 权限如何关联的信息，请参阅 [Office 365 中的权限](https://go.microsoft.com/fwlink/p/?linkid=335814)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。</td>
    </tr>
    </tbody>
    </table>


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>要管理的某些功能可能存在于边缘传输服务器上。若要管理边缘传输服务器上的功能，需要成为要管理的边缘传输服务器上 Local Administrators 组的成员。边缘传输服务器不使用基于角色的访问控制 (RBAC)。在下表中，可在边缘传输服务器上管理的功能所对应的“所需权限”列中标识有“边缘传输本地管理员”。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>某些功能可能要求在要管理的服务器上拥有本地管理员权限。若要管理这些功能，必须是该服务器上 Local Administrators 组的成员。</td>
</tr>
</tbody>
</table>


## 邮件流权限

您可以使用下表中的功能在客户端访问服务器的前端传输服务、邮箱服务器的传输服务、邮箱服务器和边缘传输服务器上的邮箱传输服务中配置邮件流设置。其中列出了配置每个功能所需的权限。

分配了 View Only Management 角色组的用户可以查看下表所示功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。

**邮箱服务器和客户端访问服务器**


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
<td><p>接受域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>Active Directory 站点和站点链接管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>反垃圾邮件功能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="even">
<td><p>反垃圾邮件更新</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="odd">
<td><p>证书管理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>传递代理连接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>外部连接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>前端传输服务</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="odd">
<td><p>日记功能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱访问权限</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱垃圾邮件配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="help-desk-exchange-2013-help.md">帮助中心</a></p></td>
</tr>
<tr class="even">
<td><p>邮箱传输服务</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="odd">
<td><p>MailTips</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮件分类</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件跟踪</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>中继传输</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>队列</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>接收连接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="odd">
<td><p>远程域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>安全列表聚合</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="odd">
<td><p>发送连接器</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="even">
<td><p>卷影冗余</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>测试邮件流</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>测试传输规则处理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>传输代理</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>传输配置</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>传输日志</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>传输规则</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="odd">
<td><p>传输服务</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">清洁管理</a></p></td>
</tr>
<tr class="even">
<td><p>x.400 域</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
</tbody>
</table>


**边缘传输服务器**


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
<td><p>接受的域 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="even">
<td><p>地址重写 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="odd">
<td><p>边缘传输服务器</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="odd">
<td><p>队列 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="even">
<td><p>接收连接器 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="odd">
<td><p>发送连接器 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="even">
<td><p>传输配置 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="odd">
<td><p>传输日志 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
<tr class="even">
<td><p>传输规则 - 边缘传输</p></td>
<td><p>边缘服务器本地管理员</p></td>
</tr>
</tbody>
</table>

