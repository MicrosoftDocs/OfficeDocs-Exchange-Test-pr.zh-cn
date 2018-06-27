---
title: 'Exchange Online 和 Exchange Server 中的默认保留策略: Exchange 2013 Help'
TOCTitle: 默认保留策略
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625571
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Online 和 Exchange Server 中的默认保留策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Exchange 在您的 Exchange Online 和内部部署 Exchange 组织中创建保留策略“默认 MRM 策略”。此策略会自动应用于 Exchange Online 中的新用户。在内部部署组织中，当您为邮箱创建存档时，将应用此策略。您可以随时更改应用于用户的保留策略。

您可以修改默认 MRM 策略中包含的标记。例如，更改保留时间或保留操作、禁用标记或者通过添加或删除其中标记来修改该策略。更新后的策略将在下次由托管文件夹助理处理时应用于邮箱

## 链接到“默认 MRM 策略”的保留标记

下表列出了链接到“默认 MRM 策略”的默认保留标记。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>类型</th>
<th>保留时间（天）</th>
<th>保留操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认 2 年后移动到存档</p></td>
<td><p>默认策略标记 (DPT)</p></td>
<td><p>730</p></td>
<td><p>移动到存档</p></td>
</tr>
<tr class="even">
<td><p>可恢复邮件 14 天后移动到存档</p></td>
<td><p>“可恢复的项目”文件夹</p></td>
<td><p>14</p></td>
<td><p>移动到存档</p></td>
</tr>
<tr class="odd">
<td><p>个人 1 年后移动到存档</p></td>
<td><p>个人标记</p></td>
<td><p>365</p></td>
<td><p>移动到存档</p></td>
</tr>
<tr class="even">
<td><p>个人 5 年后移动到存档</p></td>
<td><p>个人标记</p></td>
<td><p>1,825</p></td>
<td><p>移动到存档</p></td>
</tr>
<tr class="odd">
<td><p>个人永远不会移动到存档</p></td>
<td><p>个人标记</p></td>
<td><p>不适用</p></td>
<td><p>移动到存档</p></td>
</tr>
<tr class="even">
<td><p>1 周后删除</p></td>
<td><p>个人标记</p></td>
<td><p>7</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="odd">
<td><p>1 个月后删除</p></td>
<td><p>个人标记</p></td>
<td><p>30</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="even">
<td><p>6 个月后删除</p></td>
<td><p>个人标记</p></td>
<td><p>180</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="odd">
<td><p>1 年后删除</p></td>
<td><p>个人标记</p></td>
<td><p>365</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="even">
<td><p>5 年后删除</p></td>
<td><p>个人标记</p></td>
<td><p>1,825</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
<tr class="odd">
<td><p>从不删除</p></td>
<td><p>个人标记</p></td>
<td><p>不适用</p></td>
<td><p>删除但允许恢复</p></td>
</tr>
</tbody>
</table>


## 通过“默认 MRM 策略”可以执行什么操作


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>您可以…</th>
<th>在 Exchange Online 中…</th>
<th>在 Exchange Server 中…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>将“默认 MRM 策略”自动应用于新用户</p></td>
<td><p>是，默认应用。不需要执行任何操作。</p></td>
<td><p>是，当您也为新用户创建存档时默认应用。</p>
<p>如果您稍后为用户创建存档，仅当用户没有现有保留策略时自动应用此策略。</p></td>
</tr>
<tr class="even">
<td><p>修改链接到此策略的保留标记的保留时间或保留操作</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>禁用链接到策略的保留标记</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>将保留标记添加到策略</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>从策略中删除保留标记</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>将其他策略设置为将自动应用到新用户的默认保留策略</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
</tbody>
</table>


## 更多信息

  - 保留标记可以链接到多个保留策略。有关管理[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)的详细信息，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

  - 默认 MRM 策略不包含用于自动删除项目的 DPT（但它确实包含使用删除保留操作的个人标记，用户可以将此类标记应用于邮箱项目）。如果您想在指定的时间段后自动删除项目，则可以创建使用相应删除操作的 DPT，然后将其添加到策略中。有关详细信息，请参阅[创建保留策略](create-a-retention-policy-exchange-2013-help.md)和[向保留策略添加保留标记或从中删除保留标记](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md)。

  - 保留策略适用于邮箱用户。相同的策略适用于用户的邮箱和存档。

