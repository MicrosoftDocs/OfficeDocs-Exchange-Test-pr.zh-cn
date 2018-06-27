---
title: '了解管理角色作用域: Exchange 2013 Help'
TOCTitle: 了解管理角色作用域
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50490226
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解管理角色作用域

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

“管理角色作用域”使您能够在创建管理角色分配时，定义对管理角色产生影响的特定作用域。应用作用域时，分配给该角色的角色受理人只能修改该作用域内包含的对象。角色受理人可以是一个管理角色组、管理角色、管理角色分配策略、用户或通用安全组 (USG)。有关管理角色的详细信息，请参阅[了解基于角色的访问控制](understanding-role-based-access-control-exchange-2013-help.md)。

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


无论是内置角色还是自定义角色，每个管理角色都具有管理作用域。管理作用域有以下两种类型：

  - **常规：**“常规作用域”不是独占的。它将确定分配了管理角色的用户在 Active Directory 中可以查看或修改对象的位置。通常，管理角色指示您可以创建或修改的内容，而管理角色作用域指示您可以创建或修改的位置。“常规作用域”可以是隐式作用域或显式作用域，本主题后面将讨论这两种作用域。

  - **独占：**“独占作用域”和常规作用域的作用几乎一样。主要区别在于如果用户未分配与独占作用域相关联的角色，则独占作用域可以拒绝这些用户访问独占作用域内包含的对象。所有独占作用域都是显式作用域，这将在本主题的后面部分中进行讨论。
    
    有关独占作用域的详细信息，请参阅[了解独占作用域](understanding-exclusive-scopes-exchange-2013-help.md)。

作用域可以从管理角色继承，指定为对管理角色分配的预定义相对作用域，或使用自定义筛选器创建并添加到管理角色分配。从管理角色继承的作用域称为“隐式作用域”，而预定义和自定义的作用域称为“显式作用域”。以下部分分别介绍了这两种作用域：

  - 隐式作用域

  - 显式作用域

  - 预定义相对作用域

  - 自定义作用域
    
      - 收件人筛选作用域
    
      - 配置作用域

每个角色可以具有以下类型的作用域：

  - **收件人读取作用域：**隐式收件人读取作用域将确定分配了管理角色的用户可从 Active Directory 读取的收件人对象。

  - **收件人写入作用域：**隐式收件人写入作用域将确定分配了管理角色的用户可在 Active Directory 中修改的收件人对象。

  - **配置读取作用域：**隐式配置读取作用域将确定分配了管理角色的用户可从 Active Directory 读取的配置对象。

  - **配置写入作用域：**隐式配置写入作用域将确定分配了管理角色的用户可在 Active Directory 中修改的组织对象、数据库对象和服务器对象。

收件人对象包括邮箱、通讯组、启用邮件的用户和其他对象。配置对象包括运行 Microsoft Exchange Server 2013 的服务器以及位于运行 Exchange 的服务器上的数据库。每种类型的作用域都可以是隐式作用域或显式作用域。

## 隐式作用域

隐式作用域是应用于管理角色类型的默认作用域。因为隐式作用域与管理角色类型相关联，所以相同角色类型的所有父项和子项管理角色也具有相同的隐式作用域。隐式作用域不仅应用于内置管理角色，还应用于自定义管理角色。有关管理角色和管理角色类型的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

下表列出了可在管理角色上定义的所有隐式作用域。

### 对管理角色定义的所有隐式作用域

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>隐式作用域</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>Organization</code>，则该角色可以创建或修改 Exchange 组织内的收件人对象。</p>
<p>如果角色的收件人读取作用域中存在 <code>Organization</code>，则该角色可以查看 Exchange 组织内的任何收件人对象。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>MyGAL</code>，则该角色可以查看当前用户的全局地址列表 (GAL) 内任何收件人的属性。</p>
<p>如果角色的收件人读取作用域中存在 <code>MyGAL</code>，则该角色可以查看当前 GAL 内任何收件人的属性。</p>
<p>此类作用域只能与收件人读取作用域一起使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>Self</code>，则该角色只能修改当前用户邮箱的属性。</p>
<p>如果角色的收件人读取作用域中存在 <code>Self</code>，则该角色只能查看当前用户邮箱的属性。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>MyDistributionGroups</code>，则该角色可以创建或修改当前用户所有的通讯组列表对象。</p>
<p>如果角色的收件人读取作用域中存在 <code>MyDistributionGroups</code>，则该角色可以查看当前用户所有的通讯组列表对象。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>如果角色的配置写入作用域中存在 <code>OrganizationConfig</code>，则该角色可以创建或修改 Exchange 组织内的任何服务器或数据库配置对象。</p>
<p>如果角色的配置读取作用域中存在 <code>OrganizationConfig</code>，则该角色可以查看 Exchange 组织内的任何服务器或数据库配置对象。</p>
<p>此类作用域只能与配置读取和写入作用域一起使用。</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>如果作用域中存在 <code>None</code>，则该作用域对角色不可用。例如，角色的收件人写入作用域中存在 <code>None</code>，则其不能修改 Exchange 组织中的收件人对象。</p></td>
</tr>
</tbody>
</table>


如果某角色分配到某个角色受理人且未指定预定义或自定义作用域，则在该角色上定义的隐式作用域将用于控制用户可查看或修改的收件人或组织对象。

一个角色的隐式写入作用域总是等于或小于隐式读取作用域。这意味着一个角色永远不能修改作用域内看不见的对象。

您无法更改对管理角色定义的隐式作用域。但是可以覆盖管理角色上的隐式写入作用域和配置作用域。当预定义相对作用域或自定义作用域用于角色分配时，该角色的隐式写入作用域将被覆盖，而优先使用新的作用域。该角色的隐式读取作用域无法被覆盖并且始终应用。有关详细信息，请参阅预定义相对作用域和自定义作用域。

展开下表，以查看所有内置管理角色及其隐式作用域的列表。有关每个内置角色的详细信息，请参阅[内置管理角色](built-in-management-roles-exchange-2013-help.md)。

## 内置管理角色隐式作用域


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>管理角色</th>
<th>收件人读取作用域</th>
<th>收件人写入作用域</th>
<th>配置读取作用域</th>
<th>配置写入作用域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 显式作用域

显式作用域是指您自己设置的作用域，用于控制管理角色可以修改的对象。隐式作用域针对管理角色进行定义，而显式作用域针对管理角色分配进行定义。这将使隐式作用域可以一致地应用于所有管理角色，除非您选择使用覆盖显式作用域。有关管理角色分配的详细信息，请参阅[了解管理角色分配](understanding-management-role-assignments-exchange-2013-help.md)。

显式作用域会覆盖管理角色的隐式写入和配置作用域。它们不会覆盖管理角色的隐式读取作用域。隐式读取作用域将继续定义管理角色可以读取的对象。

当管理角色的隐式读取作用域不能满足您的业务需求时，显式作用域将很有用。只要新的作用域不超过隐式读取作用域的界限，可以添加一个显式作用域，用来包含几乎所有您想要的内容。cmdlet 作为管理角色的一部分，必须能够读取有关对象或包含 cmdlet 要创建或修改对象的容器的信息。例如，如果管理角色上的隐式读取作用域设置为 `Self`，则您不能添加 `Organization` 的显式写入作用域，因为显式写入作用域超出了隐式读取作用域的界限。

有关详细信息，请参阅以下各部分：

  - 预定义相对作用域

  - 自定义作用域

## 预定义相对作用域

Exchange 2013 提供了若干个预定义相对写入作用域，可以用于修改管理角色的作用域。预定义相对作用域提供了一种轻松的方式来更好地满足业务需求，而无需手动创建自定义作用域。它们之所以称为相对作用域，是因为它们对应于关联角色分配将分配到的角色受理人。例如，`Self` 预定义相对作用域使该写入作用域仅限于当前用户。`MyDistributionGroups` 预定义相对作用域使写入作用域仅限于当前用户所有的通讯组。预定义相对作用域只能用于确定收件人对象的作用域。预定义相对作用域不能用于确定配置对象的作用域。下表列出了可用的几种预定义相对作用域。

### 预定义相对作用域

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>隐式作用域</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>Organization</code>，则该角色可以创建或修改 Exchange 组织内的收件人对象。</p>
<p>如果角色的收件人读取作用域中存在 <code>Organization</code>，则该角色可以查看 Exchange 组织内的任何收件人对象。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>Self</code>，则该角色只能修改当前用户邮箱的属性。</p>
<p>如果角色的收件人读取作用域中存在 <code>Self</code>，则该角色只能查看当前用户邮箱的属性。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>如果角色的收件人写入作用域中存在 <code>MyDistributionGroups</code>，则该角色可以创建或修改当前用户所有的通讯组列表对象。</p>
<p>如果角色的收件人读取作用域中存在 <code>MyDistributionGroups</code>，则该角色可以查看当前用户所有的通讯组列表对象。</p>
<p>此类作用域只能与收件人读取和写入作用域一起使用。</p></td>
</tr>
</tbody>
</table>


新建管理角色分配时可以应用预定义相对作用域。使用 **New-ManagementRoleAssignment** cmdlet 创建角色分配时，可以使用 *RecipientRelativeWriteScope* 参数指定预定义相对作用域。新建角色分配时，新的预定义角色会覆盖管理角色的隐式写入作用域。在创建具有预定义相对作用域的角色分配时，不能指定自定义收件人作用域。但是，如果需要，可以指定自定义配置作用域。

有关如何添加具有预定义相对作用域的管理角色分配，请参阅[向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

## 自定义作用域

当隐式写入作用域和预定义相对作用域都不能满足业务需求时，则需要使用自定义作用域。通过自定义作用域，您能够精细地定义管理角色将应用到的作用域。例如，您可能想把特定的组织单位 (OU) 和/或特定类型的收件人作为目标。或者，您可能只希望允许一组管理员能够管理一组特定的邮箱数据库。

和预定义相对作用域一样，自定义作用域会覆盖在管理角色上定义的隐式写入和组织配置作用域。管理角色上的隐式读取作用域将继续适用，并且生成的自定义作用域不得超过隐式读取作用域的界限。您可以创建以下三种类型的自定义作用域：

  - **OU 作用域**   OU 作用域是最简单的自定义作用域，使用 **New-ManagementRoleAssignment** cmdlet 的 *RecipientOrganizationalUnitScope* 参数来创建。通过在分配角色时指定 OU 作用域，分配了该角色的角色受理人仅可以修改此 OU 内的收件人对象。有关如何添加带有 OU 作用域的管理角色分配，请参阅[向用户或 USG 添加角色](add-a-role-to-a-user-or-usg-exchange-2013-help.md)。

  - **收件人筛选作用域**   收件人筛选作用域按收件人类型或其他收件人属性（如部门、管理员、位置等），使用筛选器将特定的收件人作为目标。有关详细信息，请参阅收件人筛选作用域一节。

  - **配置作用域**   配置作用域按服务器列表或可以在服务器上定义的可筛选属性（如 Active Directory 站点或服务器角色），使用筛选器或列表将特定的服务器作为目标。配置作用域还可以按数据库列表或可筛选数据库属性，使用数据库作用域将特定的数据库作为目标。有关详细信息，请参阅配置作用域一节。

使用 **New-ManagementScope** cmdlet 可以创建简单且粗略或复杂且精细的收件人和配置自定义作用域。当您创建收件人或配置作用域时，仅返回与各自的作用域匹配的收件人、服务器或数据库对象。使用 **New-ManagementRoleAssignment** 或 **Set-ManagementRoleAssignment** cmdlet 将这些作用域应用于角色分配时，分配了该角色的角色受理人只能修改与作用域匹配的对象。自定义作用域创建后，不能更改作用域类型。收件人作用域始终是收件人作用域，而配置作用域始终是配置作用域。

默认情况下，自定义作用域使角色受理人可以访问与定义的作用域匹配的对象集。但是，它们不会主动地排除其他未分配相同或等同作用域的角色受理人的访问权限。如果自定义作用域上的多个列表或筛选器与相同对象匹配，则这些作用域都可以访问这些相同的对象。有些对象可能不需要此行为，比如说主管人员。您可以为这些对象定义独占作用域。独占作用域和常规作用域使用筛选器或列表的方式相同，但和常规作用域不同的是，它拒绝不是相同或等同独占作用域中的一部分的任何人访问作用域内的对象。有关独占作用域的详细信息，请参阅[了解独占作用域](understanding-exclusive-scopes-exchange-2013-help.md)。

## 收件人筛选作用域

使用收件人筛选作用域可以按照您在筛选语句中指定的值来评估收件人对象的一个或多个属性，从而控制角色受理人可以管理的收件人对象。收件人作用域中包括的收件人为邮箱、启用邮件的用户、通讯组和邮件联系人。针对该角色分配的角色受理人只能管理与所指定的筛选器匹配的收件人。筛选语句的一个示例为 `{ Name -Eq "David" }`，其中 **Name** 为正在评估的收件人对象属性，**David** 为要用于评估属性的值。**-Eq** 比较运算符指示该属性中存储的值必须等于指定的值，才能与筛选器匹配。如果与筛选器匹配，则该收件人包含在作用域中。

通过使用 **New-ManagementScope** cmdlet 的 *RecipientRestrictionFilter* 参数指定要使用的收件人筛选器，来创建收件人筛选作用域。默认情况下，**New-ManagementScope** cmdlet 创建常规作用域。如果您要创建独占作用域，请随 *RecipientRestrictionFilter* 参数一起包括 *Exclusive* 开关。

在创建收件人限制筛选器时，Exchange 在默认情况下会对组织中的每个收件人对象评估您提供的筛选器。如果您要限制作用域评估哪些收件人，则可以将 *RecipientRestrictionFilter* 参数与 *RecipientRoot* 参数结合使用。*RecipientRoot* 参数接受 OU。在使用 *RecipientRoot* 参数时，Exchange 仅按照您提供的筛选器评估指定 OU 中包括的收件人。

在向角色分配添加收件人筛选作用域时，请在 **New-ManagementRoleAssignment** cmdlet（如果正在创建新角色分配）或 **Set-ManagementRoleAssignment** cmdlet（如果正在更新现有角色分配）的 *CustomRecipientWriteScope* 参数中指定收件人作用域的名称。每个角色分配都可以具有一个收件人作用域，包括预定义相对作用域。您可以向添加了收件人作用域的相同角色分配添加一个配置作用域。

有关筛选器语法的详细信息以及收件人的可筛选收件人属性的完整列表，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

## 配置作用域

下面是 Exchange 2013 中提供的两种类型的配置作用域：

  - **服务器作用域**   有两种类型的服务器作用域，即服务器筛选作用域和服务器列表作用域。如果服务器作用域中包含服务器对象，则可以管理服务器配置，包括接收连接器、传输队列、服务器证书、虚拟目录等。
    
      - **服务器筛选作用域**   使用服务器筛选作用域可以按照您在筛选语句中指定的值来评估服务器对象的一个或多个属性，从而控制角色受理人可以管理的服务器对象。若要创建服务器筛选作用域，请使用 **New-ManagementScope** cmdlet 的 *ServerRestrictionFilter* 参数。
    
      - **服务器列表作用域**   使用服务器列表作用域可以定义角色受理人可以访问的服务器的列表，从而控制角色受理人可以管理的服务器对象。若要创建服务器列表作用域，请使用 **New-ManagementScope** cmdlet 的 *ServerList* 参数。

  - **数据库作用域**   有两种类型的数据库作用域，即数据库筛选作用域和数据库列表作用域。在数据库对象包括在数据库作用域中时可以管理的数据库配置包括数据库配额限制、数据库维护、公用文件夹复制、是否装入数据库等。除数据库配置之外，数据库作用域还可以用于控制能够创建收件人的数据库。如果您的组织中具有 Exchange 2010 SP1 之前的服务器，请参阅本主题后面的数据库作用域和早期 Exchange 版本部分。
    
      - **数据库筛选作用域**   使用数据库筛选作用域可以按照您在筛选语句中指定的值来评估数据库对象的一个或多个属性，从而控制角色受理人可以管理的数据库对象。若要创建数据库筛选作用域，请使用 **New-ManagementScope** cmdlet 的 *DatabaseRestrictionFilter* 参数。
    
      - **数据库列表作用域**   使用数据库列表作用域可以定义角色受理人可以访问的数据库的列表，从而控制角色受理人可以管理的数据库对象。若要创建数据库列表作用域，请使用 **New-ManagementScope** cmdlet 的 *DatabaseList* 参数。

有关筛选器语法的详细信息以及可筛选服务器和数据库属性的完整列表，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

可以通过指定要在其各自作用域中包括的每个服务器和数据库来定义服务器和数据库列表。可以通过使用逗号分隔服务器和数据库名称，在其各自作用域中指定多个服务器或数据库。

在向角色分配添加服务器或数据库配置作用域时，请在 **New-ManagementRoleAssignment** cmdlet（如果正在创建新角色分配）或 **Set-ManagementRoleAssignment** cmdlet（如果正在更新现有角色分配）的 *CustomConfigWriteScope* 参数中指定服务器或数据库配置作用域的名称。每个角色分配只能有一个配置作用域。

除了控制角色受理人可以管理哪些数据库之外，使用数据库作用域还可以控制角色受理人可以在哪些数据库上创建邮箱。这不同于对角色受理人可以管理哪些收件人的控制。如果角色受理人有权创建新邮箱、对现有用户启用邮件或移动邮箱，则您可以通过使用数据库作用域控制在其上创建邮箱的数据库或将邮箱移动至的数据库，来进一步优化其权限。使用在 **New-ManagementRoleAssignment** 或 **Set-ManagementRoleAssignment** cmdlet 的 *CustomRecipientWriteScope* 参数中指定的收件人作用域，可控制角色受理人可以管理的收件人。使用在相同 cmdlet 的 *CustomConfigurationWriteScope* 参数中指定的数据库作用域，可控制可以在其上创建邮箱或将邮箱移动至的数据库。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以使用数据库作用域控制自动邮箱分发。</td>
</tr>
</tbody>
</table>


Exchange 功能可能需要管理服务器作用域和/或数据库作用域。如果某个功能需要同时管理服务器和数据库作用域，则必须创建两个角色分配，并将其分配给应有权管理该功能的角色受理人。一个角色分配应与服务器作用域相关联，一个角色分配应与数据库作用域相关联。

某些 cmdlet 可能使用不是那么显而易见的配置作用域。下表列出了 cmdlet 以及可用于控制其使用的配置作用域。对于收件人功能区中包括的 cmdlet，使用配置作用域可以控制可以在哪些数据库上创建收件人。它们不控制可以管理的收件人。“必需的作用域”列可以包含以下各项：

  - **数据库**   若要运行 cmdlet，向角色受理人分配的角色分配必须具有包括要管理的数据库的数据库作用域，或者角色的隐式配置写入作用域必须包括要管理的数据库。

  - **服务器**   若要运行 cmdlet，向角色受理人分配的角色分配必须具有包括要管理的服务器的服务器作用域，或者角色的隐式配置写入作用域必须包括要管理的服务器。

  - **服务器或数据库**   若要运行 cmdlet，向角色受理人分配的角色分配必须具有包括要管理的数据库的数据库作用域，或者具有包括数据库所在的服务器的服务器作用域。或者，角色的隐式配置写入作用域必须包含要管理的数据库或包含数据库所在的服务器，并且角色分配不能具有自定义写入作用域。

  - **服务器和数据库**   若要运行此 cmdlet，必须向角色受理人分配两个角色分配。第一个角色分配必须包括数据库作用域，其中包含要管理的数据库。第二个角色分配必须包括服务器作用域，其中包含数据库所在的服务器。这两个角色分配可以定义自定义配置作用域，也可以从角色继承隐式配置写入作用域。若要从角色继承隐式写入作用域，角色分配不能具有自定义写入作用域。

### 功能区以及适用的数据库和服务器作用域

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能区</th>
<th>Cmdlet</th>
<th>必需的作用域</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>数据库</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="even">
<td><p>数据库</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="odd">
<td><p>数据库</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>服务器和数据库</p></td>
</tr>
<tr class="even">
<td><p>数据库</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="odd">
<td><p>数据库</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>服务器</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>服务器</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="odd">
<td><p>高可用性</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="even">
<td><p>高可用性</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>服务器或数据库</p></td>
</tr>
<tr class="odd">
<td><p>收件人</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="even">
<td><p>收件人</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="odd">
<td><p>收件人</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="even">
<td><p>收件人</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>数据库</p></td>
</tr>
<tr class="odd">
<td><p>故障排除</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>数据库</p></td>
</tr>
</tbody>
</table>


## 数据库作用域和早期 Exchange 版本

数据库作用域起初在 Microsoft Exchange 2010 Service Pack 1 (SP1) 中引入，并且在 Exchange 2013 中继续受到支持。Exchange 2010 SP1 之前的 Exchange 版本仅支持收件人作用域和服务器配置作用域。如果您在 Exchange 2010 SP1 或更高版本的服务器上新建数据库作用域，则会看到以下警告：

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

您创建的数据库作用域仅应用于连接到运行 Exchange 2010 SP1 或更高版本的服务器的用户。系统不会向连接到 Exchange 2010 SP1 之前的服务器的用户应用任何与数据库作用域相关的角色分配。也就是说，如果用户连接到 Exchange 2010 SP1 之前的服务器，则系统不会向此类用户授予这些角色分配所提供的任何权限。不能使用 Exchange 2010 SP1 之前的服务器创建、删除、修改或查看数据库作用域。

数据库作用域可以包含 Exchange 组织中的任何数据库。这包括 Exchange Server 2007、Exchange 2010 和 Exchange 2013 服务器。这样，您便可以控制用户可以管理的数据库，而不必考虑 Exchange 版本。与其他数据库作用域一样，与包含 Exchange 2007 和 Exchange 2010 数据库的数据库作用域相关联的角色分配仅应用于连接到 Exchange 2010 SP1 或更高版本服务器的用户。

连接到 Exchange 2010 SP1 之前的服务器的用户可以查看和修改与数据库作用域相关联的角色分配。这包括将现有角色分配上的配置作用域更改为服务器作用域（如果配置作用域当前与数据库作用域相关联）。不过，如果角色分配上的配置作用域更改为服务器作用域，并且用户以后希望更改回数据库作用域，或者用户想要将配置作用域更改为另一个数据库作用域，则用户必须在连接到 Exchange 2010 SP1 或更高版本服务器时进行更改。如果用户连接到 Exchange 2010 SP1 之前的服务器，则用户在更改角色分配上的配置作用域时只能指定服务器作用域。

