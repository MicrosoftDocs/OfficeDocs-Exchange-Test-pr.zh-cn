---
title: '了解独占作用域: Exchange 2013 Help'
TOCTitle: 了解独占作用域
ms:assetid: 32492622-3b01-4e3b-8288-ed39525eea75
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638110(v=EXCHG.150)
ms:contentKeyID: 50490283
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 了解独占作用域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

“独占作用域”是一种特殊类型的显式管理作用域，可与管理角色分配关联。独占作用域旨在实现这样一种情况：您可以在其中包含一组很重要的对象（例如 CEO 邮箱），并可以严密控制具有管理这些对象的访问权限的用户。

包含独占作用域的角色分配称为“互斥角色分配”。

创建独占作用域时，只有分配有该独占作用域或等效独占作用域的用户才可以修改与作用域匹配的对象。没有分配该独占作用域或等效独占作用域的角色代理人无法修改与作用域匹配的对象，即使他们自己的角色有包括对象的作用域也是如此。独占作用域会覆盖任何其他不是独占作用域的常规作用域。此行为类似于 Active Directory 访问控制列表 (ACL) 上的拒绝访问控制项 (ACE) 的作用。

“等效独占作用域”是指与其他独占作用域的一些相同对象匹配的另一个独占作用域。此类作用域不必与相同的一整套对象匹配。这两种作用域都能够修改与它们匹配的某些对象或所有对象。

## 创建独占作用域

独占作用域的创建方式与任何其他显式作用域类似。您可以指定预构建的相对作用域；收件人筛选器、数据库筛选器或服务器筛选器；或者数据库或服务器列表。常规作用域只有在将作用域与管理角色分配相关联后才会生效，而独占作用域的拒绝方面会立即生效。这意味着，只要创建了独占作用域，任何用户在创建角色分配之前都不能再访问该作用域中包含的对象。

在创建分配后，独占作用域会为这些分配有管理角色和作用域的用户提供访问权限。如果另一等效独占作用域与相同的对象匹配，则与该独占作用域相关联的角色分配仍然能够访问这些对象。

有关管理作用域筛选器的详细信息，请参阅[了解管理角色作用域筛选器](understanding-management-role-scope-filters-exchange-2013-help.md)。

> [!important]
> 在更改任何管理角色组件（包括独占作用域）时，都应该考虑 Active Directory 复制时间。


如果对象包含在多个独占作用域中，则将对象分配给任何一个独占作用域都能提供对这些对象的访问权限。有关详细信息，请参阅本主题后面的独占作用域和常规作用域交互。

独占作用域仅控制显式收件人或角色分配的配置写入作用域。隐式收件人或分配给用户或组的角色的配置读取作用域仍然适用。这意味着以下适用：

  - 这些分配有角色的用户或组可以继续查看与此角色的隐式读取作用域匹配的对象。

  - 如果其他角色的读取作用域包括这些对象，则分配其他角色的这些用户或组能够查看独占作用域中包含的对象。但是，这些对象只能由分配有与独占作用域关联的角色的人员修改。

独占作用域只能与管理角色或专家角色一起使用，不能与最终用户角色一起使用。有关角色的详细信息，请参阅[了解管理角色](understanding-management-roles-exchange-2013-help.md)。

## 独占作用域和常规作用域交互

本节末尾的图说明了各独占作用域之间以及与常规作用域之间如何交互。图中的用户都包含与其关联的下列属性。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>User</th>
<th>City</th>
<th>Title</th>
<th>Department</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Terry</p></td>
<td><p>温哥华</p></td>
<td><p>会计</p></td>
<td><p>会计部门</p></td>
</tr>
<tr class="even">
<td><p>David</p></td>
<td><p>温哥华</p></td>
<td><p>作家</p></td>
<td><p>营销</p></td>
</tr>
<tr class="odd">
<td><p>Walter</p></td>
<td><p>温哥华</p></td>
<td><p>Manager</p></td>
<td><p>营销</p></td>
</tr>
<tr class="even">
<td><p>Bob</p></td>
<td><p>温哥华</p></td>
<td><p>CEO</p></td>
<td><p>董事会成员</p></td>
</tr>
<tr class="odd">
<td><p>Christine</p></td>
<td><p>温哥华</p></td>
<td><p>总裁</p></td>
<td><p>董事会成员</p></td>
</tr>
<tr class="even">
<td><p>Fred</p></td>
<td><p>温哥华</p></td>
<td><p>CFO</p></td>
<td><p>高级管理人员</p></td>
</tr>
<tr class="odd">
<td><p>Martin</p></td>
<td><p>温哥华</p></td>
<td><p>CIO</p></td>
<td><p>高级管理人员</p></td>
</tr>
<tr class="even">
<td><p>Kim</p></td>
<td><p>温哥华</p></td>
<td><p>副总裁，运营</p></td>
<td><p>高级管理人员</p></td>
</tr>
<tr class="odd">
<td><p>Jennifer</p></td>
<td><p>温哥华</p></td>
<td><p>副总裁，技术</p></td>
<td><p>高级管理人员</p></td>
</tr>
</tbody>
</table>


图中的下列三个管理角色分配管理上表中的用户。每个角色都有一个关联的作用域，其中一些是独占作用域。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>角色分配</th>
<th>作用域筛选器</th>
<th>互斥或常规</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>收件人管理员</p></td>
<td><p>城市 = 温哥华</p></td>
<td><p>Regular</p></td>
</tr>
<tr class="even">
<td><p>VIP Administrators</p></td>
<td><p>职务 = CEO 或 CFO 或 CIO 或总裁</p></td>
<td><p>独占</p></td>
</tr>
<tr class="odd">
<td><p>Executive Administrators</p></td>
<td><p>部门 = 主管人员</p></td>
<td><p>独占</p></td>
</tr>
</tbody>
</table>


Recipient Administrators 角色分配包含一个与所有用户匹配的作用域，因为每个用户都在温哥华。没有任何独占作用域，这就意味着 Recipient Administrators 角色分配可以管理任何用户。但是，此组织已创建两个独占作用域：VIP Administrators 和 Executive Administrators。这些独占作用域限制谁可以管理与其各自的作用域筛选器匹配的用户。VIP Administrator 角色分配包含一个与职务为 CEO、CFO、CIO 或总裁的任何用户匹配的作用域筛选器。Executive Administrators 角色分配包含一个与 Executives 部门中任何用户匹配的作用域筛选器。

评估常规和独占作用域时，会出现以下结果：

  - Recipient Administrators 角色分配可以管理用户 Terry、David 和 Walter。此角色分配无法管理任何其他用户，因为他们与 VIP Administrator 和 Executive Administrators 角色分配的独占作用域筛选器匹配。

  - VIP Administrator 角色分配可以管理用户 Bob、Christine、Fred 和 Martin。这是因为与此角色分配关联的独占作用域筛选器与这些对象的属性匹配。此角色分配无法管理用户 Kim 和 Jennifer，因为他们的属性与此独占作用域不匹配。

  - Executive Administrators 角色分配可以管理用户 Kim、Jennifer、Fred 和 Martin。这是因为与此角色分配关联的独占作用域筛选器与这些对象的属性匹配。此角色分配无法管理用户 Bob 和 Christine，因为他们的属性与此独占作用域不匹配。

请注意，这两个独占作用域都可以访问 Fred 和 Martin。这是因为，这两个用户的属性都与这两个独占作用域的筛选器匹配。

**独占作用域和常规作用域之间的交互**

![独占作用域和常规作用域交互](images/Dd638110.0aa26d1d-1fa6-44d8-802d-83d75cd2624c(EXCHG.150).jpg "独占作用域和常规作用域交互")

有关管理作用域的详细信息，请参阅[了解管理角色作用域](understanding-management-role-scopes-exchange-2013-help.md)。

