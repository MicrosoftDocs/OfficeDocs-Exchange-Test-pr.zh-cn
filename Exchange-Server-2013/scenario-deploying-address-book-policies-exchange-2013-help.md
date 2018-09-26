---
title: '方案：部署通讯簿策略: Exchange 2013 Help'
TOCTitle: 方案：部署通讯簿策略
ms:assetid: 6ac3c87d-161f-447b-afb2-149ae7e3f1dc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657455(v=EXCHG.150)
ms:contentKeyID: 50490764
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 方案：部署通讯簿策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

## 部署方案

以下三个方案描述了三种不同组织类型的可能部署解决方案。虽然还有许多其他方案，但此处所介绍的是最常见的方案。这些方案中的地址列表和全局地址列表 (GAL) 是根据将对象按逻辑分组的筛选器（如“自定义属性”）创建的。

## 方案 1：两个单独的公司 - 一个 Exchange 组织

此方案适用于共享基础结构，但是不共享报告链且没有公共员工的政府部门、分支或部门。此外，这些分支没有任何特殊的安全或隐私问题。在此方案中，会创建两个通讯簿策略，其中员工在查看 GAL 或查看其他通讯组的成员身份时只能查看相同组织的成员。此外，没有用户是跨整个组织的通讯组的成员。

![具有两个独立公司的通讯簿策略](images/JJ657455.b4fc82da-a659-4ade-ba33-d55d90dcf204(EXCHG.150).gif "具有两个独立公司的通讯簿策略")

Contoso 和 Humungous Insurance ABP 是使用以下地址列表、全局地址列表、会议室列表和 OAB 创建的，OAB 是使用通过筛选器（如自定义属性）对对象进行分组的收件人筛选器创建的。因为两家公司是独立的，相互之间没有任何交互，因此没有任何共同的地址列表。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Contoso</p></td>
<td><p>Humungous Insurance</p></td>
</tr>
<tr class="even">
<td><p>地址列表</p></td>
<td><p>AL_CON_Groups</p>
<p>AL_CON_Users</p>
<p>AL_CON_Contacts</p></td>
<td><p>AL_HI_Groups</p>
<p>AL_HI_Users</p>
<p>AL_HI_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>全局地址列表</p></td>
<td><p>GAL_CON</p></td>
<td><p>GAL_HI</p></td>
</tr>
<tr class="even">
<td><p>会议室地址列表</p></td>
<td><p>AL_CON_Rooms</p></td>
<td><p>AL_HI_Rooms</p></td>
</tr>
<tr class="odd">
<td><p>脱机通讯簿 (OAB)</p></td>
<td><p>OAB_CON</p></td>
<td><p>OAB_HI</p></td>
</tr>
</tbody>
</table>


## 方案 2：共有一个 CEO 的两家公司

在此方案中，Fabrikam 和 Tailspin Toys 共享相同的 Exchange 组织并共有相同的 CEO。CEO 是两家公司之间唯一的公共人员。此方案需要具有以下特征的三个 ABP：

  - Tailspin Toys 中的用户在浏览 GAL 时只能查看 Tailspin Toys 用户。

  - Fabrikam 中的用户在浏览 GAL 时只能查看 Fabrikam 用户。

  - 在每家公司中，有一个 SeniorLeaders 通讯组，其中包括该公司的高层领导和 CEO。

  - 可查看 CEO 的组成员身份的用户只能看到属于该用户所在公司的组。他们不会看到不在自己公司中的组。

  - 创建了三个 ABP：“Fab”、“Tail”和“CEO”。

![两个公司一个 CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "两个公司一个 CEO")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Fabrikam</p></td>
<td><p>Tailspin Toys</p></td>
<td><p>CEO</p></td>
</tr>
<tr class="even">
<td><p>地址列表</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p></td>
<td><p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
<td><p>AL_FAB_Users_DGs</p>
<p>AL_FAB_Contacts</p>
<p>AL_TAIL_Users_DGs</p>
<p>AL_TAIL_Contacts</p></td>
</tr>
<tr class="odd">
<td><p>全局地址列表</p></td>
<td><p>GAL_FAB</p></td>
<td><p>GAL_TAIL</p></td>
<td><p>默认 GAL</p></td>
</tr>
<tr class="even">
<td><p>会议室地址列表</p></td>
<td><p>AL_FAB_Rooms</p></td>
<td><p>AL_TAIL_Rooms</p></td>
<td><p>默认所有房间</p></td>
</tr>
<tr class="odd">
<td><p>脱机通讯簿 (OAB)</p></td>
<td><p>OAB_FAB</p></td>
<td><p>OAB_TAIL</p></td>
<td><p>默认 OAB</p></td>
</tr>
</tbody>
</table>


如果将 CEO 添加到每个组织的通讯组中，并且 CEO 在每家公司的 ABP 的作用域内，则 CEO 将对每家公司都显示。CEO 可以创建跨这两家公司并且会在每家公司的 GAL 中显示的通讯组，但是该通讯组的成员只能查看自己组织内的组的成员。

## 方案 3：教育

此方案适用于必须分教室以确保学生隐私的学校或大学。教育方案具有以下特征：

  - 每个班级的学生只能查看其班级中的其他学生、自己的教师以及校长。

  - 教师只能查看自己教室中的学生。

  - 教师可以查看其他所有教师和校长。

  - 为每个班级的父级和教职工创建通讯组。

![通讯簿策略教育方案](images/JJ657455.435f3b1a-9752-4c61-ab8a-80115c643d12(EXCHG.150).gif "通讯簿策略教育方案")


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Students_ClassA</p></td>
<td><p>Teachers_ClassA</p></td>
<td><p>校长</p></td>
</tr>
<tr class="even">
<td><p>地址列表</p></td>
<td><p>AL_ClassAAL_Principal</p></td>
<td><p>AL_ClassAAL_AllTeachersAL_AllGroupsAL_Principal</p></td>
<td><p>AL_ClassA</p>
<p>AL_ClassB</p>
<p>AL_AllTeachers</p>
<p>AL_AllStudents</p>
<p>AL_AllGroups</p></td>
</tr>
<tr class="odd">
<td><p>全局地址列表</p></td>
<td><p>GAL_StudentsClassA</p></td>
<td><p>GAL_TeachersClassA</p></td>
<td><p>GAL_Everyone</p></td>
</tr>
<tr class="even">
<td><p>会议室地址列表</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>AL_BlankRoom</p></td>
<td><p>默认所有房间</p></td>
</tr>
<tr class="odd">
<td><p>脱机通讯簿 (OAB)</p></td>
<td><p>OAB_StudentsClassA</p></td>
<td><p>OAB_TeachersClassA</p></td>
<td><p>默认 OAB</p></td>
</tr>
</tbody>
</table>


## 注意事项和最佳实践

在组织中使用 ABP 时需要考虑以下事项：

  - 为了使 ABP 正常工作，应用 ABP 的用户邮箱必须位于 Exchange 2010 SP3 或 Exchange 2013 服务器上。

  - 不要在全局目录服务器上运行 Exchange 2010 客户端访问服务器角色。这样做将导致 Active Directory 被用于名称服务提供程序接口 (NSPI)，而不是用于 Microsoft Exchange 通讯簿服务。您可在全局目录服务器上运行 Exchange 2013 服务器角色，并让 ABP 正常工作，但是我们不建议在域控制器上安装 Exchange。

  - 不能同时使用分层通讯簿 (HAB) 和 ABP。若要了解详细信息，请参阅[分层通讯簿](https://docs.microsoft.com/zh-cn/exchange/address-books/hierarchical-address-books/hierarchical-address-books)。

  - 任何分配有 ABP 的用户都应存在于自己的 GAL 中。

  - 如果允许客户端应用程序通过 LDAP 直接访问 Active Directory，则它们将跳过 ABP 的内置逻辑。因为 Outlook for Mac 2011 和 Entourage 2008 使用直接 LDAP 查询访问 Active Directory，因此，如果自动发现服务为这些客户端应用程序指定或提供了域控制器或全局目录服务器，则它们将不会正常使用 ABP。Outlook for Mac 2011 可以使用 EWS 或本地 OAB 来访问目录信息。但是，如果 Outlook for Mac 2011 可以直接访问 LDAP 服务，它将不会尝试这样做。

  - ABP 中使用的 GAL 必须至少包含 ABP 中定义和指定的所有地址列表（包括房间地址列表）。不要创建包含的对象数少于同一 ABP 中任何地址列表的 GAL。

  - 我们建议创建不会跨越虚拟组织边界的通讯组。创建包含多个虚拟组织的成员的通讯组会导致以下问题：
    
      - 如果组成员在向通讯组发送邮件时请求送达或已读回，他们将可以看到属于其他虚拟组织的组成员的电子邮件地址
    
      - 如果向通讯组发送加密邮件，并且有些组成员没有有效的数字 ID，则发件人将收到警告消息，其中包括没有有效ID 的成员总数及其电子邮件地址的列表。但是，如果没有有效数字 ID 成员中的有些成员所在的组织与发件人不同，则警告消息将包括正确的计数，但不包括其他组织中的成员的电子邮件地址。因此，总数与成员地址列表会不匹配。
        
        例如，如果某个通讯组总共含有来自两个组织（机构 A 和机构 B）的五个成员。三个组成员来自机构 A，并且其中一个成员具有无效的数字 ID。其他两个成员来自机构 B，并且他们的数字 ID 均无效。如果来自 Agency A 的某个成员向通讯组发送了一封加密邮件，则该成员将收到一条警告消息，指示总共有三个收件人没有有效的数字 ID。但是，警告消息中将仅列出来自 Agency A 的收件人的电子邮件地址。
    
      - ABP 不适用于 **Get-Group** cmdlet。因此，可以运行 **Get-Group** 的任何用户或进程都会看到其有权访问的任何组的所有成员。
        
        我们建议修改 OWA 选项的组管理设置，使用户无法使用 Outlook Web App 来管理组。若要防止用户使用 OWA 选项来管理组，请将用户从 MyDistributionGroupMembership RBAC 角色中排除。有关详细信息，请参阅 [MyDistributionGroupMembership 角色](mydistributiongroupmembership-role-exchange-2013-help.md)。
    
      - 如果允许用户使用 Outlook 或 Outlook Web App 来管理组，则组的所有者必须可以全权查看组成员资格列表。

  - 所有 ABP 都必须包含一个房间地址列表。但是，如果组织不使用房间地址列表，则可创建一个空的默认房间地址列表。

  - 部署 ABP 不会阻止一个虚拟组织中的用户向另一个虚拟组织中的用户发送电子邮件。如果要阻止用户跨组织发送电子邮件，我们建议创建一条传输规则。例如，若要创建一条传输规则以阻止 Contoso 用户接收来自 Fabrikam 用户的邮件，但仍允许 Fabrikam 的高级领导团队向 Contoso 用户发送邮件，请运行以下命令行管理程序命令：
    
    ```powershell
        New-TransportRule -Name "StopFabrikamtoContosoMail" -FromMemberOf "AllFabrikamEmployees" -SentToMemberOf "AllContosoEmployees" -DeleteMessage -ExceptIfFrom seniorleadership@fabrikam.com
    ```

  - 如果要在 Lync 客户端中强制执行与 ABP 相似的功能，则可对特定的用户对象设置 `msRTCSIP-GroupingID` 属性。有关详细信息，请参阅 [PartitionByOU 被替换为 msRTCSIP-GroupingID](https://go.microsoft.com/fwlink/p/?linkid=232306) 主题。

## 一般部署步骤

## 从地址列表分段迁移到 ABP

如果组织使用白皮书[在 Exchange 2007 中配置虚拟组织和地址列表分段](http://go.microsoft.com/fwlink/p/?linkid=109601)中的说明配置了合适的 Exchange 2007 地址列表分段解决方案，则您应先使用[从 Exchange Server 2007 地址列表分段迁移到 Exchange Server 2010 通讯簿策略](https://go.microsoft.com/fwlink/p/?linkid=235967)中概述的步骤迁移到 Exchange Server 2010。此过程需要组织停机一段时间，因此您需要进行相应的规划。

## ABP 的新部署

如果组织正在部署 Exchange 2013 ABP 并且未使用 Exchange 2007 地址列表分段，则可以使用这些说明在组织中部署 ABP。

此部分中的步骤将引导您查看方案 2：方案 2：共有一个 CEO 的两家公司。在此方案中，Fabrikam 和 Tailspin Toys 是单独的两家公司，但是共有一个 CEO 和高级领导团队。

## 步骤 1：安装并配置通讯簿策略路由代理

如果您正在使用 ABP，并且不希望各虚拟组织中的用户查看彼此潜在的私人信息，则可以开启通讯簿策略路由代理。通讯簿策略路由代理是可以在邮箱服务器上运行的一种传输代理，可控制组织中解析收件人的方式。在安装并配置通讯簿策略路由代理后，分配有不同 GAL 的用户会成为外部收件人，因为他们无法查看外部收件人的联系卡。

有关详细说明，请参阅[安装并配置通讯簿策略路由代理](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)。

## 步骤 2：划分您的虚拟组织

您需要制定一种方法来划分您的组织。建议使用邮箱、联系人和组的 CustomAttribute1-15 属性而不是固有条件属性（如 Company、Department 或 StateOrProvince）来划分虚拟组织，原因如下：

  - 并非对象的所有收件人类型在 Active Directory 中都有固有条件属性。例如，通讯组和动态通讯组不支持公司、部门或省/市/自治区属性。

  - 并非所有固有条件属性都会在 cmdlet 中对有些收件人公开。例如，对于邮件用户、联系人、通讯组和已启用邮件的公用文件夹，*Company*、*department* 和 *StateOrProvince* 参数在 cmdlet 中不可进行公开。

  - 在使用固有条件属性时，需要多个 cmdlet 来对收件人进行分段。例如，在运行 **New-Mailbox** 或 **Set-Mailbox** cmdlet 之后，需要运行 Set-User 来为 UserMailbox 标记 *Company*、*Department*、*StateOrProvince*。

  - 对于每种收件人类型，*CustomAttributeX* 参数都在 Set-\* cmdlet 中公开，可以通过单个 Set- cmdlet 为该类型完成所有分段

  - 已显式保留 CustomAttributeX 属性，以用于组织自定义，并且，这些属性完全由组织管理员控制。

对组织进行分段时要考虑实现的另一种最佳做法是在通讯组和动态通讯组的名称中使用公司标识符。Exchange 具有组命名策略功能，该功能会基于创建通讯组的用户的许多属性（包括通讯组创建者的 Company、StateorProvince、Title 以及 CustomAttribute1 到 CustomAttribute15），自动向通讯组的名称添加后缀或前缀。如果允许用户创建自己的通讯组，则组命名策略尤其重要。有关详细信息，请参阅[创建通讯组命名策略](https://technet.microsoft.com/zh-cn/library/jj218693(v=exchg.150))。

组命名策略不应用于动态通讯组，因此需要手动对其进行分段并手动应用命名策略。

## 步骤 3：创建地址列表、GAL 和 OAB

在创建地址列表和全局地址列出时，请勿使用“IncludedRecipient”和“ConditionalX”参数，如 ConditionalCompany 和 ConditionalCustomAttribute5。应改用收件人筛选器。必须使用命令行管理程序创建收件人筛选器。有关收件人筛选器的详细信息，请参阅[边缘传输服务器上的收件人筛选](recipient-filtering-on-edge-transport-servers-exchange-2013-help.md)

在创建 ABP 时，根据您希望用户在 Outlook 或 Outlook Web App 中查看地址列表的方式，来创建多个地址列表。此组织具有四个地址列表：

  - AL\_FAB\_Users\_DGs

  - AL\_FAB\_Contacts

  - AL\_TAIL\_Users\_DGs

  - AL\_TAIL\_Contacts

此示例将创建地址列表 AL\_TAIL\_Users\_DGs。该地址列表包含 CustomAttribute15 等于 TAIL 的所有用户和通讯组。

```powershell
    New-AddressList -Name "AL_TAIL_Users_DGs" -RecipientFilter {((RecipientType -eq 'UserMailbox') -or (RecipientType -eq "MailUniversalDistributionGroup") -or (RecipientType -eq "DynamicDistributionGroup")) -and (CustomAttribute15 -eq "TAIL")}
```

有关使用收件人筛选器创建地址列表的详细信息，请参阅[使用收件人筛选器创建地址列表](https://docs.microsoft.com/zh-cn/exchange/address-books/address-lists/use-recipient-filters-to-create-an-address-list)。

若要创建 ABP，必须提供会议室地址列表。如果您的组织没有资源邮箱（如会议室邮箱或设备邮箱），我们建议您创建一个空白会议室地址列表。以下示例创建一个空白会议室地址列表，因为组织中没有会议室邮箱。

```powershell
    New-AddressList -Name AL_BlankRoom -RecipientFilter {(Alias -ne $null) -and ((RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox'))}
```

但是，在此方案中，Fabrikam 和 Contoso 都有会议室邮箱。此示例使用 CustomAttribute15 等于 FAB 的收件人筛选器为 Fabrikam 创建会议室列表。

```powershell
    New-AddressList -Name AL_FAB_Room -RecipientFilter {(Alias -ne $null) -and (CustomAttribute15 -eq "FAB")-and (RecipientDisplayType -eq 'ConferenceRoomMailbox') -or (RecipientDisplayType -eq 'SyncedConferenceRoomMailbox')}
```

ABP 中使用的全局地址列表必须是地址列表的一个超集。不要创建包含的对象数少于 ABP 中任何或所有地址列表中存在的对象数的 GAL。此示例为 Tailspin Toys 创建包含地址列表和会议室地址列表中存在的所有收件人的全局地址列表。

```powershell
    New-GlobalAddressList -Name "GAL_TAIL" -RecipientFilter {(CustomAttribute15 -eq "TAIL")}
```

有关详细信息，请参阅[创建全局地址列表](https://docs.microsoft.com/zh-cn/exchange/address-books/address-lists/create-global-address-list)。

在创建 OAB 时，应在提供 New-OfflineAddressBook 或 Set-OfflineAddressBook 的 *AddressLists* 参数时包含合适的 GAL 以确保不会意外缺少任何条目。基本上，可以通过在 New/Set-OfflineAddressBook 的 AddressLists 中指定 AddressLists 的列表，来自定义用户会看到的条目集或减小 OAB 的下载大小。但是，如果您希望用户看到 OAB 中完整的 GAL 条目集，请确保将 GAL 包括在 AddressLists 中。

此示例为 Fabrikam 创建名为 OAB\_FAB 的 OAB。

```powershell
New-OfflineAddressBook -Name "OAB_FAB" -AddressLists "GAL_FAB"
```

有关详细信息，请参阅[创建脱机通讯簿](https://technet.microsoft.com/zh-cn/library/bb124339(v=exchg.150))。

## 步骤 4：创建 ABP

在创建了所有所需对象之后，可以创建 ABP。此示例创建名为 ABP\_TAIL 的 ABP。

```powershell
    New-AddressBookPolicy -Name "ABP_TAIL" -AddressLists "AL_TAIL_Users_DGs"," AL_TAIL_Contacts" -OfflineAddressBook "\OAB_TAIL" -GlobalAddressList "\GAL_TAIL" -RoomList "\AL_TAIL_Rooms"
```

有关详细信息，请参阅[创建通讯簿策略](https://technet.microsoft.com/zh-cn/library/hh529931(v=exchg.150))。

## 步骤 5：将 ABP 分配给邮箱

将 ABP 分配给用户是该过程的最后一步。ABP 会在用户的应用程序连接到客户端访问服务器上的 Microsoft Exchange 通讯簿服务时生效。当 ABP 应用于用户的帐户时，如果用户已经连接到 Outlook 或 Outlook Web App，该用户将需要关闭并重新启动客户端应用程序，然后才能看到其新地址列表和 GAL。

此示例将 ABP\_FAB 分配给 CustomAttribute15 等于“FAB”的所有邮箱。

```powershell
    Get-Mailbox -resultsize unlimited | where {$_.CustomAttribute15 -eq "TAIL"} | Set-Mailbox -AddressBookPolicy "ABP_TAIL"
```

有关详细信息，请参阅[将通讯簿策略分配给邮件用户](https://technet.microsoft.com/zh-cn/library/hh529942(v=exchg.150))。

