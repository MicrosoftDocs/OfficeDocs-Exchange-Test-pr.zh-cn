---
title: '分层通讯簿: Exchange 2013 Help'
TOCTitle: 分层通讯簿
ms:assetid: a1d277a0-5437-40af-aade-e4730a0d1308
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff629379(v=EXCHG.150)
ms:contentKeyID: 50491242
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 分层通讯簿

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-03-26_

通过使用分层通讯簿 (HAB)，最终用户可以利用组织的分层结构查找通讯簿中的收件人。通常，用户仅限于默认全局地址列表 (GAL) 及其收件人属性，GAL 的结构通常不会反映组织中收件人的管理或资历关系。能够自定义 HAB 以反映您的组织独特的业务结构，这可以为您的用户提供查找内部收件人的高效方法。

## 使用分层通讯簿

在 HAB 中，根组织（例如，Contoso, Ltd）用作顶层。在该顶层下面，可以添加若干子层来创建按分部、部门或其他任何要指定的组织层划分的自定义 HAB。下图使用以下结构说明 Contoso, Ltd 的 HAB：

  - 顶层代表根组织 Contoso, Ltd。

  - 第二级子层代表 Contoso Ltd 内的业务分部：Corporate Office、Product Support Organization 和 Sales & Marketing Organization。

  - 第三级子层代表 Corporate Office 分部内的部门：Human Resources、Accounting Group 和 Administration Group。

**Contoso, Ltd 的示例 HAB**

![分层通讯簿对话框](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "分层通讯簿对话框")

使用 *SeniorityIndex* 参数可以在层次结构中新增层级。创建 HAB 时，使用 *SeniorityIndex* 参数在这些组织层内按资历对各个收件人或组织组进行分级。该分级指定收件人或组在 HAB 中显示的顺序。例如，在上述示例中，Corporate Office 分部中的收件人的 *SeniorityIndex* 参数设置如下：

  - David Hamilton 为 `100`

  - Rajesh M. Patel 为 `50`

  - Amy Alberts 为 `25`

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果没有设置 <em>SeniorityIndex</em> 参数，或两个或更多用户的此参数值相同，那么 HAB 排序顺序使用 <em>PhoneticDisplayName</em> 参数值，以字母升序顺序列出用户。如果没有设置 <em>PhoneticDisplayName</em> 参数值，HAB 排序顺序默认为 <em>DisplayName</em> 参数值，并以字母升序顺序列出用户。</td>
</tr>
</tbody>
</table>


## 配置分层通讯簿

[启用或禁用层次通讯簿](enable-or-disable-hierarchical-address-books-exchange-2013-help.md)主题中包含了创建 HAB 的详细说明。一般步骤如下：

1.  创建用于根组织（顶层）的通讯组。如果需要，可以将 Exchange 林中现有的组织单位用作通讯组。

2.  创建子层的通讯组并将其指定为 HAB 成员。修改这些组的 *SeniorityIndex* 参数，使其以正确的层次结构顺序在根组织内列出。

3.  添加组织成员。修改成员的 *SeniorityIndex* 参数，使其以正确的层次结构顺序在子层内列出。

4.  出于提供辅助功能的目的，可以使用 *PhoneticDisplayName* 参数，它指定了 *DisplayName* 参数的拼音发音。

