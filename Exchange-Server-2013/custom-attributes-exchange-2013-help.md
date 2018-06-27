---
title: '自定义属性: Exchange 2013 Help'
TOCTitle: 自定义属性
ms:assetid: 2b043878-0b34-4563-a9c2-28a9efa7447e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423541(v=EXCHG.150)
ms:contentKeyID: 50490119
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 自定义属性

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-17_

Microsoft Exchange Server 2013 包含 15 个扩展属性。您可以使用这些属性添加有关收件人的信息，例如员工 ID、组织单位 (OU) 或者其他一些没有现有属性的自定义值。在 Active Directory 中，这些自定义属性标记为 **ms-Exch-Extension-Attribute1** 到 **ms-Exch-Extension-Attribute15**。在 Exchange 命令行管理程序中，相应的参数是 *CustomAttribute1* 到 *CustomAttribute15*。任何 Exchange 组件都不使用这些属性。它们可用于存储 Active Directory 数据，而无须扩展 Active Directory 架构。

在 Exchange Server 2003 及更早版本中，如果希望将此信息存储在 Active Directory 中，则必须扩展 Active Directory 架构以创建某个属性。架构扩展要求为新属性规划并购买对象标识符 (OID)，并且先在测试环境中测试扩展进程后，再在生产环境中执行。在 Exchange 2013 中，架构扩展无法用于地址列表、电子邮件地址策略和动态通讯组所使用的收件人筛选器中。

**目录**

自定义属性的优点

自定义属性示例

使用 ConditionalCustomAttributes 参数的自定义属性示例

使用 ExtensionCustomAttributes 参数的自定义属性示例

## 自定义属性的优点

使用自定义属性的一些优点包括：

  - 可避免扩展 Active Directory 架构。

  - 属性由 Exchange 安装程序创建。

  - 可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序来管理属性。不需要构建自定义控件或编写脚本来填充和显示这些属性。

  - 这些属性是可筛选属性，可用于包含收件人 cmdlet（例如 **Get-Mailbox**）的 *Filter* 参数。它们也可用在 EAC 和命令行管理程序中，为电子邮件地址策略、地址列表和动态通讯组创建筛选器。

## 多值自定义属性

在 Exchange 2010 Service Pack 2 (SP2) 中，向 Exchange 中添加了五个多值自定义属性用于存储邮件收件人的其他信息（如果传统自定义属性不能满足您的需求）。*ExtensionCustomAttribute1* 到 *ExtensionCustomAttribute5* 参数中的每个参数最多都可以存放 1,300 个值。可以逗号分隔列表形式指定多个值。以下 cmdlet 支持这些新参数：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-cn/library/aa995950\(v=exchg.150\))

  - [Set-MailPublicFolder](https://technet.microsoft.com/zh-cn/library/bb123707\(v=exchg.150\))

  - [Set-RemoteMailbox](https://technet.microsoft.com/zh-cn/library/ff607302\(v=exchg.150\))

有关多值属性的详细信息，请参阅[修改多值属性](modifying-multivalued-properties-exchange-2013-help.md)。

## 自定义属性示例

在许多 Exchange 部署中，为 OU 中的所有收件人创建一个电子邮件地址策略是一种常见方案。OU 不是可用于电子邮件地址策略或地址列表的 *RecipientFilter* 参数中的可筛选属性。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>动态通讯组具有一个附加参数，可用于将其限制到特定 OU 或容器中的收件人。</td>
</tr>
</tbody>
</table>


如果该 OU 中的收件人未共享任何可作为筛选条件的通用属性（例如部门或位置），则可以使用某个公用值填充其中一个自定义属性，如此例所示。

    Get-Mailbox -OrganizationalUnit Sales | Set-Mailbox CustomAttribute1 "SalesOU"

现在可以为具有 *CustomAttribute1* 属性（等于 SalesOU）的所有收件人创建电子邮件地址策略，如此例所示。

    New-EmailAddressPolicy -Name "Sales" -RecipientFilter { CustomAttribute1 -eq "SalesOU"} -EnabledEmailAddressTemplates "SMTP:%s%2g@sales.contoso.com"

## 使用 ConditionalCustomAttributes 参数的自定义属性示例

创建动态通讯组、电子邮件地址策略或地址列表时，不需要使用 *RecipeintFilter* 参数指定自定义属性。可以改为使用 *ConditionalCustomAttribute1* 到 *ConditionalCustomAttribute15* 参数。

此示例根据其 *CustomAttribute1* 设置为 SalesOU 的收件人创建动态通讯组。

    New-DynamicDistributionGroup -Name "Sales Users and Contacts" -IncludedRecipients "MailboxUsers,MailContacts" -ConditionalCustomAttribute1 "SalesOU"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果使用 <em>Conditional</em> 参数，则必须使用 <em>IncludedRecipients</em> 参数。此外，如果使用 <em>RecipientFilter</em> 参数，则不能使用 <em>Conditional</em> 参数。如果希望包括其他筛选器以创建动态通讯组、电子邮件地址策略或地址列表，则应使用 <em>RecipientFilter</em> 参数。</td>
</tr>
</tbody>
</table>


## 使用 ExtensionCustomAttributes 参数的自定义属性示例

在此示例中，Kweku 的邮箱将更新 *ExtensionCustomAttribute1* 以反映他登记了以下教育课程：MATH307、ECON202 和 ENGL300。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 MATH307,ECON202,ENGL300

接下来，通过使用 *RecipientFilter* 参数创建登记了 MATH307 的所有学生的动态通讯组，其中 *ExtensionCustomAttribute1* 等于 MATH307。使用 *ExtentionCustomAttributes* 参数时，可以使用 `-eq` 运算符代替 `-like` 运算符。

    New-DynamicDistributionGroup -Name Students_MATH307 -RecipientFilter {ExtensionCustomAttribute1 -eq "MATH307"}

在此示例中，Kweku 的 *ExtensionCustomAttribute1* 值进行更新以反映他添加了课程 ENGL210 并删除了课程 ECON202。

    Set-Mailbox -Identity Kweku -ExtensionCustomAttribute1 @{Add="ENGL210"; Remove="ECON202"}

