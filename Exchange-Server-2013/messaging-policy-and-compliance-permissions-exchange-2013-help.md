---
title: '邮件策略和遵从性权限: Exchange 2013 Help'
TOCTitle: 邮件策略和遵从性权限
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50491888
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件策略和遵从性权限

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

配置邮件策略和遵从性所需的权限取决于要执行的步骤和要运行的 cmdlet。有关邮件策略和遵从性的详细信息，请参阅[邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md)。

若要了解执行过程或运行 cmdlet 所需的权限，请执行以下操作：

1.  在下表中查找与所要执行的过程或要运行的 cmdlet 最相关的功能。

2.  接下来，查看该功能所需的权限。您必须被分配到其中一个角色组、等效的自定义角色组或等效的管理角色。还可以单击角色组查看其管理角色。如果某个功能列出多个角色组，则您只需要被分配到其中一个角色组就可以使用此功能。有关角色组和管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

3.  现在运行 **Get-ManagementRoleAssignment** cmdlet 以查看分配给您的角色组或管理角色，以便确定您是否具有管理该功能所需的权限。
    
    > [!NOTE]
    > 必须分配了 Role Management 管理角色才能运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet。如果没有运行 <strong>Get-ManagementRoleAssignment</strong> cmdlet 的权限，则请求 Exchange 管理员检索分配给您的角色组或管理角色。


如果要将管理一项功能的权限委派给另一个用户，请参阅[委派角色分配](delegate-role-assignments-exchange-2013-help.md)。

> [!NOTE]
> 要管理的某些功能可能存在于边缘传输服务器上。若要管理边缘传输服务器上的功能，需要成为要管理的边缘传输服务器上 Local Administrators 组的成员。边缘传输服务器不使用基于角色的访问控制 (RBAC)。在下表中，可在边缘传输服务器上管理的功能所对应的“所需权限”列中标识有“边缘传输本地管理员”。


## 邮件策略和遵从性权限

可以使用下表中的功能来配置邮件策略和遵从性功能。其中列出了配置每个功能所需的角色组。

分配了 View-Only Management 角色组的用户可以查看下表中功能的配置。有关详细信息，请参阅[仅查看组织管理](view-only-organization-management-exchange-2013-help.md)。


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
<td><p>防止数据丢失 (DLP)</p></td>
<td><p>如果使用 Office 365：</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 全局管理</a>（自动包含 Exchange <a href="organization-management-exchange-2013-help.md">组织管理</a>）</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 服务管理</a>以及 Exchange 中的<a href="organization-management-exchange-2013-help.md">组织管理</a>管理角色组</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 密码管理</a></p></li>
</ul>
<p>如果仅使用 Exchange Server 2013 或 Exchange Online：</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>删除邮箱内容（将 <a href="https://technet.microsoft.com/zh-cn/library/dd298173(v=exchg.150)">Search-Mailbox</a> cmdlet 与 <em>DeleteContent</em> 开关一起使用）</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">发现管理</a> <strong>和</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">邮箱导入导出角色</a></p>

> [!NOTE]
> 默认情况下，不会将 Mailbox Import Export 角色分配给任何角色组。您可以将管理角色分配给内置或自定义角色组、用户或通用安全组。建议将角色分配给角色组。有关详细信息，请参阅<a href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">向用户或 USG 添加角色</a>。

</td>
</tr>
<tr class="odd">
<td><p>发现邮箱——创建</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="even">
<td><p>日记功能</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮箱审核日志记录</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>邮件分类</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件记录管理</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>In-Place eDiscovery</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">发现管理</a></p>

> [!NOTE]
> 默认情况下，Discovery Management 角色组中没有任何成员。用户（包括管理员）都不具有搜索邮箱所需的权限。有关详细信息，请参阅<a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">在 Exchange 中分配电子数据展示权限</a>。

</td>
</tr>
<tr class="odd">
<td><p>就地保留</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">发现管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>

> [!important]
> 创建基于查询的就地保留，用户需要直接或通过分配了两个角色的角色组中的成员分配邮箱搜索或诉讼保留角色。要不使用查询创建就地保留（将所有邮箱邮件置于暂停状态），则必须分配诉讼保留角色。会向发现管理角色组分配这两个角色。<br />
> 会向组织管理角色组分配诉讼保留角色。组织管理角色组的成员可对邮箱中的所有邮件实施就地保留，但不能创建基于查询的就地保留。

</td>
</tr>
<tr class="even">
<td><p>就地存档</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p></td>
</tr>
<tr class="odd">
<td><p>就地存档 – 测试连接性</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="server-management-exchange-2013-help.md">服务器管理</a></p></td>
</tr>
<tr class="even">
<td><p>信息权限管理 (IRM) 配置</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">遵从性管理</a></p>
<p><a href="organization-management-exchange-2013-help.md">组织管理</a></p></td>
</tr>
<tr class="odd">
<td><p>保留策略——应用</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="recipient-management-exchange-2013-help.md">收件人管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
<tr class="even">
<td><p>保留策略 - 创建</p></td>
<td><p>请参阅邮件记录管理的条目</p></td>
</tr>
<tr class="odd">
<td><p>传输规则</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">组织管理</a></p>
<p><a href="records-management-exchange-2013-help.md">记录管理</a></p></td>
</tr>
</tbody>
</table>

