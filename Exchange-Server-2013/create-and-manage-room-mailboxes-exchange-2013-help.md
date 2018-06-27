---
title: '创建和管理会议室邮箱: Exchange 2013 Help'
TOCTitle: 创建和管理会议室邮箱
ms:assetid: f70752ad-fce0-4e14-8428-fc5ac63f6c54
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ215781(v=EXCHG.150)
ms:contentKeyID: 50489808
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建和管理会议室邮箱

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2017-02-02_

估计完成时间：5 分钟。

会议室邮箱是分配给物理位置（例如会议室、礼堂或培训室）的资源邮箱。在管理员创建会议室邮箱后，用户可通过在会议请求中包含会议室邮箱来轻松预留会议室。有关详细信息，请查看[收件人](recipients-exchange-2013-help.md)。

有关另一种资源邮箱类型的信息，请参阅[管理设备邮箱](manage-equipment-mailboxes-exchange-2013-help.md)。

## 您想执行什么操作？

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您运行的是 Exchange 2013 混合方案，请务必在适当的位置上创建会议室邮箱。在本地为您的本地组织创建会议室邮箱，并且应在云中为 Exchange Online 端创建会议室邮箱。</td>
</tr>
</tbody>
</table>



## 创建会议室邮箱

## 使用 Exchange 管理中心创建会议室邮箱

1.  在 Exchange 管理中心，导航到“收件人”\>“资源”。

2.  若要创建会议室邮箱，请单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\>“会议室邮箱”。

3.  使用页面上的选项指定新资源邮箱的设置。
    
      - “会议室名称”   使用此框可以键入会议室邮箱的名称。这是在 Exchange 管理中心的资源邮箱列表和贵组织的通讯簿中列出的名称。此名称必填，同时不能超过 64 个字符。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>尽管存在描述会议室详细信息的其他字段（例如，“位置”和“容量”），但可以考虑使用一致的命名约定来总结会议室名称中最重要的详细信息。为什么？通过这样做，当用户在会议请求中从通讯簿选择会议室时，可以轻易地查看详细信息。</td>
        </tr>
        </tbody>
        </table>
    
      - “\* 电子邮件地址”   会议室邮箱具有电子邮件地址，因此可以收到预订请求。电子邮件地址由 @ 符号左侧的别名（必须在林中是唯一的）和右侧的域名组成。电子邮件地址必填。
    
      - **位置**、**电话**、**容量**   使用这些字段可输入有关会议室的详细信息。但是，如上所述，您可在会议室名称中包含所有这些信息或其中一部分，以方便用户查看。

4.  完成后，请单击“保存”创建会议室邮箱。

创建会议室邮箱之后，您可以编辑会议室邮箱，以更新关于预定选项、邮件提示和邮箱委派的信息。参阅下面的“使用 Exchange 管理中心”部分，更改会议室邮箱属性

## 使用 Exchange PowerShell 创建会议室邮箱

本示例将创建具有下列配置的会议室邮箱：

  - 会议室邮箱位于 Mailbox Database 1 上。

  - 邮箱的名称是 ConfRoom1。此名称还将用于创建会议室的电子邮件地址。

  - Exchange 管理中心和通讯簿中的显示名称是 Conference Room 1。

  - *Room* 开关指定此邮箱将创建为会议室邮箱。

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name ConfRoom1 - -DisplayName "Conference Room 1" -Room

有关语法和参数的详细信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道这有效？

您可以确保您已通过下列不同的方法，正确创建了会议室邮箱：

  - 在 Exchange 管理中心，导航到“收件人”\>“资源”。邮箱列表中将显示新的会议室邮箱。在“邮箱类型”下，该类型是“会议室”。

  - 在 Exchange PowerShell 中，运行以下命令以显示有关新会议室邮箱的信息。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 创建会议室列表

如果打算设立一百多个会议室或已经设立一百多个会议室，则使用会议室列表帮助你组织这些会议室。如果公司在多个建筑物内的会议室都可以预订举行会议，则创建每个建筑物的会议室列表可能会非常有用。会议室列表特别标记为通讯组，使用方法与通讯组一样。但是，只能使用 Exchange 命令行管理程序创建会议室列表。

## 使用 Exchange PowerShell 创建会议室列表

本示例为建筑物 32 创建会议室列表。

    New-DistributionGroup -Name "Building 32 Conference Rooms" -OrganizationalUnit "contoso.com/rooms" -RoomList

## 使用 Exchange PowerShell 向会议室列表添加会议室

本示例向建筑物 32 会议室列表添加 confroom3223。

    Add-DistributionGroupMember -Identity "Building 32 Conference Rooms" -Member confroom3223@contoso.com

## 使用 Exchange PowerShell 将通讯组转换为会议室列表

您可能之前已经创建了包含会议室的通讯组。您无需重新创建；我们可以快速将其转换为会议室列表。

本示例将通讯组（建筑物 34 会议室）转换为会议室列表。

    Set-DistributionGroup -Identity "Building 34 Conference Rooms" -RoomList

## 更改会议室邮箱属性

创建会议室邮箱后，您可以使用 Exchange 管理中心或 Exchange PowerShell 进行更改或设置其他属性。

## 使用 Exchange 管理中心更新会议室邮箱属性

1.  在 Exchange 管理中心，导航到“收件人”\>“资源”。

2.  在资源邮箱列表，单击您希望更改属性的会议室邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“会议室邮箱属性”页面上，单击以下部分之一以查看或更改属性。
    
      - 常规
    
      - 委派
    
      - 预订选项
    
      - 联系人信息
    
      - 电子邮件地址
    
      - 邮件提示

## 常规

使用“一般”部分查看或更改有关资源的基本信息。

  - “\* 会议室名称”   该名称显示在 Exchange 管理中心的资源邮箱列表和贵组织的通讯簿中。如果更改信息，它的长度不能超过 64 个字符。

  - “\* 电子邮件地址”   该只读框显示会议室邮箱的电子邮件地址。您可以在 电子邮件地址 部分更改它。

  - “容量”   使用此框输入安全占有会议室的最大人员数量。

单击“更多选项”查看或更改以下这些额外的属性：

  - “组织单位”   此只读框显示包含会议室邮箱帐户的组织单位 (OU)。您必须使用 Active Directory 用户和计算机移动帐户到其他 OU。

  - “邮箱数据库”   此只读框显示托管此会议室邮箱的邮箱数据库的名称。使用 Exchange 管理中心中的“迁移”页面移动邮箱到其他数据库。

  - “\* 别名” 使用此框以更改会议室邮箱的别名。

  - “不显示在地址列表中”：选中此复选框以防止会议室邮箱显示在通讯簿以及在 Exchange 组织中定义的其他地址列表中。选中此复选框后，用户仍可使用电子邮件地址发送预订邮件到会议室邮箱。

  - “部门”   使用此框以指定与会议室关联的部门名称。您可以使用此属性以为动态通讯组和通讯簿创建收件人条件。

  - “公司”   使用此框以指定与会议室关联的公司（如果适用）。与“部门”属性一样，您可以使用此属性以为动态通讯组和通讯簿创建收件人条件。

  - “通讯簿策略”   使用此选项指定会议室邮箱的通讯簿策略 (ABP)。ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。若要了解详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。
    
    在下拉列表中，选择要与此邮箱关联的策略。

  - “自定义属性”   本部分将显示为会议室邮箱定义的自定义属性。要指定自定义属性值，请单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。最多可为收件人指定 15 个自定义属性。

## 委派

使用此部分以查看或更改会议室邮箱如何处理预订请求，并定义在未自动完成的情况下，可以接受或拒绝预订请求的人。

  - “预定请求”   选择以下选项之一以处理预定请求。
    
      - “自动接受或拒绝预定请求”   有效的会议请求将自动预定会议室。如果出现某个日程安排与现有预定发生冲突的情况，或者预定请求超出了资源的日程安排限制（例如，预定持续时间太长），则将自动拒绝会议请求。
    
      - “选择可以接受或谢绝预定请求的代理”   资源代理负责接受或拒绝发送到会议室邮箱的会议请求。如果指定了多个资源代理，则只需一个代理处理特定的会议请求。

  - “委派”   如果您选择需要发送委派的预定请求的选项，将列出指定的委派。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 或“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以从列表添加或删除委派。

## 预订选项

使用“预订选项”部分查看或更改预订策略设置，这将定义何时可以计划会议室、可以保留的时间长短以及可以提前多长时间预订。

  - “允许重复会议”   该设置允许或防止会议室的重复会议。默认情况下，启用此设置以允许定期会议。

  - “仅允许工作时间期间的计划”   该设置将接受或拒绝不在未为会议室定义的工作时间期间的会议请求。默认情况下，该设置将被禁用，从而在工作时间之外允许会议请求。默认情况下，工作时间为周一至周五 8:00 A.M. 至 5:00 P.M.。您可在日历页面上的“外观”部分配置会议室邮箱的工作时间。

  - “如果结束日期超出该限制始终拒绝”   通过最大预定提前期设置，该设置可控制延伸到指定日期之外的行为或重复会议。
    
      - 如果您启用该设置，重复预定请求将在预定在“最大预定提前期”框中的值指定的日期之前或之后自动拒绝重复预定请求，同时它们超出指定日期。这是默认设置。
    
      - 如果您禁用该设置，重复预定请求将在预定在“最大预定提前期”框中的值指定的日期之前或之后自动接受重复预定请求，同时它们超出指定日期。但是，预定数量会减少，以便不会在指定日期之后进行预定。

  - “最大预订提前期（天）”   该部分指定可提前预订会议室的最大天数。有效输入是介于 0 和 1080 之间的整数。 默认值为 180 天。

  - “最长持续时间（天）”   该设置将指定在预订请求中可以预留会议室的最长持续时间。默认值为 24 小时。
    
    对于重复预定请求，最长预定持续时间适用于每个 Exchange 管理中心请求实例的时长。

该页面上还有一个框，其中您可用于编写邮件以发送给发送预订请求以预留会议室的用户。

## 联系人信息

使用“联系信息”部分来查看或更改会议室的联系信息。该页上的信息显示在通讯簿中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以使用“州/省”框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。</td>
</tr>
</tbody>
</table>


## 电子邮件地址

使用“电子邮件地址”部分查看或更改与会议室邮箱关联的电子邮件地址。这包括邮箱的主 SMTP 地址和任何关联代理地址。主 SMTP 地址（也称为“回复地址”）在地址列表中以粗体显示，大写的 **SMTP** 值显示在“类型”列中。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。单击此按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
    
      - “EUM”   EUM（Exchange 统一消息）地址由 Microsoft Exchange Unified Messaging 使用，以在 Exchange 2010 组织中查找已启用 UM 的收件人。EUM 地址包含已启用 UM 的用户的分机号和 UM 拨号计划。单击该按钮，并在“地址/扩展名”框中键入分机号。然后，单击“浏览”并选择邮箱的拨号计划。
    
      - “自定义地址类型”   单击此按钮，然后在“\* 电子邮件地址”框中键入一个支持的非 SMTP 电子邮件地址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。您必须确保所指定的自定义地址符合该地址类型的格式要求。</td>
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
    <td>当添加新电子邮件地址时，您将拥有使其成为主 SMTP 地址的选项。</td>
    </tr>
    </tbody>
    </table>


  - “基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址”   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。

## 邮件提示

使用“邮件提示”部分可添加邮件提示，以便在用户向会议室邮箱发送预订请求之前提醒用户存在潜在的问题。邮件提示是在将此收件人添加到新电子邮件的“收件人”、“抄送”或“密件抄送”行中时，信息栏中显示的文本。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。</td>
</tr>
</tbody>
</table>


## 使用 Exchange PowerShell 更改会议室邮箱属性

使用以下 cmdlet 集查看和更改会议室邮箱属性：**Get-Mailbox** 和 **Set-Mailbox** cmdlet 以查看和更改会议室邮箱的一般属性和电子邮件地址。使用 **Get-CalendarProcessing** 和 **Set-CalendarProcessing** cmdlet 查看和更改委派和预定选项。

  - **Get-User** 和 **Set-User**   使用这些 cmdlet 查看和设置一般属性，如位置、部门和公司名。

  - **Get-Mailbox** 和 **Set-Mailbox**   使用这些 cmdlets 查看和设置邮箱属性，如电子邮件地址和邮箱数据库。

  - **Get-CalendarProcessing** 和 **Set-CalendarProcessing**   使用这些 cmdlet 查看和设置预定选项和委派。

有关这些 cmdlet 的信息，请参阅下列主题：

  - [Get-User](https://technet.microsoft.com/zh-cn/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-cn/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/zh-cn/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/zh-cn/library/dd335046\(v=exchg.150\))

这里是使用 Exchange PowerShell 更改会议室邮箱属性的一些示例：

这些示例将更改显示名称、主 SMTP 地址（名为默认回复地址）和会议室容量。此外，之前的回复地址将保留为代理地址。

    Set-Mailbox "Conf Room 123" -DisplayName "Conf Room 31/123 (12)" -EmailAddresses SMTP:Rm33.123@contoso.com,smtp:rm123@contoso.com -ResourceCapacity 12

本示例将配置会议室邮箱，以允许仅在工作时间期间计划预订请求，并设置最长持续时间为 9 个小时。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true -MaximumDurationInMinutes 540

本示例将使用 **Get-User** cmdlet 查找对应于私有会议室的所有会议室邮箱，然后使用 **Set-CalendarProcessing** cmdlet 发送预订请求到名为 Robin Wood 的代理以接受或拒绝。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox') -and (DisplayName -like 'Private*')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Robin Wood"

## 您如何知道这有效？

要验证已成功更改会议室邮箱的属性，请执行下列操作：

  - 在 Exchange 管理中心中，选择邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看您更改的属性或功能。根据您更改的属性，它可能显示在所选邮箱的“详细信息”窗格中。

  - 在 Exchange PowerShell 中，使用 **Get-Mailbox** cmdlet 验证更改。使用 Exchange PowerShell 的一个优势是，您可查看多个邮箱的多个属性。在预订请求仅能在工作时间期间计划，同时最长持续时间为 9 个小时的以上示例中，请运行以下命令以验证新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'RoomMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours,MaximumDurationInMinutes

若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>

