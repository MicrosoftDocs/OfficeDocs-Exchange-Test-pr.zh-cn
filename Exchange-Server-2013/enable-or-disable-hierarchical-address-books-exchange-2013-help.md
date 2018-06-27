---
title: '启用或禁用层次通讯簿: Exchange 2013 Help'
TOCTitle: 启用或禁用层次通讯簿
ms:assetid: b4c3a175-ce5e-4bfb-a4a0-92d25f3644b3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff607473(v=EXCHG.150)
ms:contentKeyID: 50491432
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用或禁用层次通讯簿

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

您可以配置 Microsoft Outlook 2010 或更高版本中对最终用户可用的一个功能：分层通讯簿 (HAB)。通过 HAB，用户可以使用基于资历或管理结构的组织层次结构，在 Exchange 组织中查找收件人。有关 HAB 的详细信息，请参阅[分层通讯簿](hierarchical-address-books-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 小时。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“通讯组”条目。

  - 不能使用 Exchange 管理中心 (EAC) 执行此过程。必须使用命令行管理程序。

  - 在开始之前，请阅读主题[分层通讯簿](hierarchical-address-books-exchange-2013-help.md)。您应该了解 HAB 是否适合您的 Exchange 组织。

  - 了解当前在您的 Exchange 组织中，组织单位 (OU)、组、用户和联系人是如何配置的。

  - 了解下表中的 cmdlet 和相关参数，它们是配置 HAB 所必需的。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Cmdlet</th>
    <th>参数</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/zh-cn/library/aa997443(v=exchg.150)">Set-OrganizationConfig</a></p></td>
    <td><p><em>HierarchicalAddressBookRoot</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/zh-cn/library/bb123770(v=exchg.150)">Set-Group</a></p></td>
    <td><p><em>IsHierarchicalGroup</em></p>
    <p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="odd">
    <td><p><a href="https://technet.microsoft.com/zh-cn/library/aa998221(v=exchg.150)">Set-User</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    <tr class="even">
    <td><p><a href="https://technet.microsoft.com/zh-cn/library/bb124535(v=exchg.150)">Set-Contact</a></p></td>
    <td><p><em>SeniorityIndex</em></p>
    <p><em>PhoneticDisplayName</em></p></td>
    </tr>
    </tbody>
    </table>


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

## 使用命令行管理程序启用 HAB

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管不能使用 EAC 启用 HAB，但启用 HAB 后可以使用 EAC 管理组织层次结构中的组成员身份。</td>
</tr>
</tbody>
</table>


例如，将要为 HAB 创建名为 HAB 的 OU。组织的域名为 Contoso-dom，Contoso,Ltd 将成为层次结构中顶级组织（“根组织”）的名称。将在 Contoso,Ltd. 下创建名为 Corporate Office、Product Support Organization 和 Sales & Marketing Organization 的下属组作为其子组织。此外，将在 Corporate Office 下创建组 Human Resources、Accounting Group 和 Administration Grou 作为其子组织。

有关创建通讯组的详细信息，请参阅[创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)。

1.  在 Contoso 组织中创建名为 HAB 的 OU。您可以使用 Active Directory 用户和计算机，或在命令提示符中键入下列内容。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>或者，您可以使用 Exchange 林中的某个现有的 OU。</td>
    </tr>
    </tbody>
    </table>
    
        dsadd ou "OU=HAB,DC=Contoso-dom,DC=Contoso,DC=com"
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=198986">新建组织单位</a>。</td>
    </tr>
    </tbody>
    </table>


2.  为 HAB 创建根通讯组 Contoso，Ltd。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>为本主题提供了命令行管理程序示例。但是，您也可以使用 EAC 创建通讯组。有关详细信息，请参阅<a href="create-and-manage-distribution-groups-exchange-2013-help.md">创建和管理通讯组</a>。</td>
    </tr>
    </tbody>
    </table>
    
        New-DistributionGroup -Name "Contoso,Ltd" -DisplayName "Contoso,Ltd" -Alias "ContosoRoot" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "ContosoRoot" -Type "Distribution"

3.  将 Contoso，Ltd 指定为 HAB 的根组织。
    
        Set-OrganizationConfig -HierarchicalAddressBookRoot "Contoso,Ltd"

4.  在 HAB 中创建其他层的通讯组。例如，您要创建下列组：Corporate Office、Product Support Organization、Sales & Marketing Organization、Human Resources、Accounting Group 和 Administration Group。本示例创建通讯组 Corporate Office。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>为本主题提供了命令行管理程序示例。但是，您也可以使用 EAC 创建通讯组。有关详细信息，请参阅<a href="create-and-manage-distribution-groups-exchange-2013-help.md">创建和管理通讯组</a>。</td>
    </tr>
    </tbody>
    </table>
    
        New-DistributionGroup -Name "Corporate Office" -DisplayName "Corporate Office" -Alias "CorporateOffice" -OrganizationalUnit "Contoso-dom.Contoso.com/HAB" -SamAccountName "CorporateOffice" -Type "Distribution"

5.  将每个组指定为 HAB 成员。例如，您要将下列组指定为层次结构组：Contoso,Ltd、Corporate Office、Product Support Organization、Sales & Marketing Organization、Human Resources、Accounting Group 和 Administration Group。该示例将通讯组 Contoso,Ltd 指定为 HAB 的成员。
    
        Set-Group -Identity "Contoso,Ltd" -IsHierarchicalGroup $true

6.  将每个下属组添加为根组织的成员。例如，在 HAB 中将通讯组 Corporate Office、Product Support Organization 和 Sales & Marketing Organization 添加为根组织 Contoso,Ltd 的成员。该示例将 Corporate Office 通讯组添加为 Contoso,Ltd 根通讯组的成员。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该示例使用了通讯组的别名。</td>
    </tr>
    </tbody>
    </table>
    
        Add-DistributionGroupMember -Identity "ContosoRoot" -Member "CorporateOffice"

7.  将附属于通讯组 Corporate Office 的每个组添加为该组的成员。例如，将通讯组 Human Resources、Accounting Group 和 Administration Group 添加为通讯组 Corporate Office 的成员。该示例将 Human Resources 通讯组添加为 Corporate Office 通讯组的成员。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>该示例使用通讯组的别名，并假定 Human Resources 通讯组的别名为 HumanResources。</td>
    </tr>
    </tbody>
    </table>
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "HumanResources"

8.  在 HAB 中将用户添加到组。例如，David Hamilton（SMTP 地址 DHamilton@contoso.com）是 OU Contoso-dom.Contoso.com/Users 中现有的用户，将添加到组 Corporate Office。在 HAB 中重复此步骤将其他用户添加到组。
    
        Add-DistributionGroupMember -Identity "CorporateOffice" -Member "DHamilton"

9.  为 HAB 中的组设置 *SeniorityIndex* 参数。例如，Corporate Office 组包含三个子组：Human Resources、Accounting Group 和 Administration Group。相较于默认的将组按字母升序排列，首选排序为 Human Resources (*SeniorityIndex* = 100)、Accounting Group (*SeniorityIndex* = 50)，然后是 Administration Group (*SeniorityIndex* = 25)。该示例将 Human Resources 组的 *SeniorityIndex* 参数设置为 100。
    
        Set-Group -Identity "Human Resources" -SeniorityIndex 100
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><em>SeniorityIndex</em> 参数是数字值，用于在 HAB 中将组或用户按数字降序进行排列。如果没有设置 <em>SeniorityIndex</em> 参数，或两个或更多用户的此参数值相同，那么 HAB 排序顺序使用 <em>PhoneticDisplayName</em> 参数值，以字母升序顺序列出用户。如果没有设置 <em>PhoneticDisplayName</em> 值，HAB 排序顺序默认为 <em>DisplayName</em> 参数值，并以字母升序顺序列出用户。</td>
    </tr>
    </tbody>
    </table>


10. 为 HAB 组中的用户设置 *SeniorityIndex* 参数。例如，Corporate Office 组包含三位用户：Amy Alberts、David Hamilton 和 Rajesh M. Patel。相较于默认的将用户按照字母升序排列，首选排序为 David Hamilton (*SeniorityIndex* = 100)、Rajesh M. Patel (*SeniorityIndex* = 50)，然后是 Amy Alberts (*SeniorityIndex* = 25)。该示例将用户 David Hamilton 的 *SeniorityIndex* 参数设置为 100。
    
        Set-User -Identity "DHamilton@contoso.com" -SeniorityIndex 100

完成上述步骤之后，HAB 将显示在 Outlook 中。若要查看 HAB，请打开 Outlook，然后单击“通讯簿”。HAB 显示在“组织”选项卡上，与下图类似。

**Contoso，Ltd 的示例 HAB**

![分层通讯簿对话框](images/Ff629379.d8cc782f-61cd-44c4-9c74-432ebea0c3db(EXCHG.150).gif "分层通讯簿对话框")

创建 HAB 后，您可以在组织层次结构中使用 EAC 管理组成员身份。但是，您必须使用命令行管理程序修改任何新的组或用户的 *SeniorityIndex* 参数。

有关语法和参数的详细信息，请参阅下列内容：

  - [New-DistributionGroup](https://technet.microsoft.com/zh-cn/library/aa998856\(v=exchg.150\))

  - [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))

  - [Set-Group](https://technet.microsoft.com/zh-cn/library/bb123770\(v=exchg.150\))

  - [Add-DistributionGroupMember](https://technet.microsoft.com/zh-cn/library/bb124340\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-cn/library/aa998221\(v=exchg.150\))

## 使用命令行管理程序禁用分层通讯簿

本示例禁用用于 HAB 的根组织。

    Set-OrganizationConfig -HierarchicalAddressBookRoot $null

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>该命令不会删除用于 HAB 结构的根组织或子组，也不会重置组或用户的 <em>SeniorityIndex</em> 值。仅阻止 HAB 显示于 Outlook 中。要再次启用具有相同配置设置的 HAB，您只需再次启用根组织。</td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))。

