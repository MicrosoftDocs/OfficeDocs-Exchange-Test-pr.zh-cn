---
title: '管理设备邮箱: Exchange 2013 Help'
TOCTitle: 管理设备邮箱
ms:assetid: e5f58b3a-83e1-4742-8846-85103a44ee18
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ215770(v=EXCHG.150)
ms:contentKeyID: 50489800
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理设备邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-10-09_

“设备邮箱”是分配给非特定于位置的资源（例如便携式计算机、投影仪、麦克风或公司汽车）的资源邮箱。在管理员创建设备邮箱之后，用户可通过在会议请求中加入相应的设备邮箱方便地保留设备。您可使用 EAC 和命令行管理程序来创建设备邮箱或更改设备邮箱属性。有关详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

有关另一种类型的资源邮箱（会议室邮箱）的信息，请参阅[创建和管理会议室邮箱](create-and-manage-room-mailboxes-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建设备邮箱

## 使用 EAC 创建设备邮箱

1.  在 EAC 中，导航到“收件人”\>“资源”。

2.  若要创建设备邮箱，请单击“新建”\>“设备邮箱”。若要创建会议室邮箱，请单击“新建”\>“会议室邮箱”。

3.  使用页面上的选项指定新资源邮箱的设置。
    
      - “\* 设备名称”   使用此框可以键入设备邮箱的名称。这是在 EAC 的资源邮箱列表和贵组织的通讯簿中列出的名称。此名称必填，同时不能超过 64 个字符。
        
        > [!tip]
        > 尽管存在描述会议室详细信息的其他字段（例如“容量”），但可以考虑使用一致的命名约定来总结设备名称中最重要的详细信息。为什么？通过这样做，当用户在会议请求中从通讯簿选择设备时，可以轻易地查看详细信息。
    
      - “\* 电子邮件地址”   设备邮箱具有一个电子邮件地址，从而可接收预定请求。电子邮件地址由 @ 符号左侧的别名（必须在林中是唯一的）和右侧的域名组成。电子邮件地址必填。

4.  完成后，请单击“保存”创建设备邮箱。

创建设备邮箱之后，您可以编辑设备邮箱，以更新关于预定选项、邮件提示和委派的信息。参阅下面的“更改设备邮箱属性”部分更改会议室邮箱属性

## 使用命令行管理程序创建设备邮箱

本示例将创建具有下列配置的设备邮箱：

  - 设备邮箱位于 Mailbox Database 1 上。

  - 设备名称为 MotorVehicle2 并且该名称将在 GAL 中显示为 Motor Vehicle 2。

  - 电子邮件地址是 MotorVehicle2@contoso.com。

  - 此邮箱位于 Equipment 组织单位中。

  - *Equipment* 参数指定此邮箱将创建为设备邮箱。

<!-- end list -->

    New-Mailbox -Database "Mailbox Database 1" -Name MotorVehicle2 -OrganizationalUnit Equipment -DisplayName "Motor Vehicle 2" -Equipment

有关语法和参数的详细信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道这有效？

要检查是否成功创建了用户邮箱，可进行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“资源”。邮箱列表中将显示新的用户邮箱。在“邮箱类型”下，该类型是“设备”。

  - 在命令行管理程序中运行以下命令来显示有关新设备邮箱的信息。
    
        Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 更改设备邮箱属性

创建设备邮箱后，您可以使用 EAC 或命令行管理程序，进行更改并设置其他属性。

## 使用 EAC 更改设备邮箱属性

1.  在 EAC 中，导航到“收件人”\>“资源”。

2.  在资源邮箱列表中，单击要更改其属性的设备邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在设备邮箱属性页面上，单击以下部分之一以查看或更改属性。
    
      - 常规
    
      - 委派
    
      - 预订选项
    
      - 联系人信息
    
      - 电子邮件地址
    
      - 邮件提示

## 常规

使用“一般”部分查看或更改有关资源的基本信息。

  - “\* 设备名称”   该名称出现在 EAC 中的资源邮箱列表和贵组织的通讯簿中。如果更改信息，它的长度不能超过 64 个字符。

  - “\* 电子邮件地址”   该只读框显示设备邮箱的电子邮件地址。您可以在 电子邮件地址 部分更改它。

  - “容量”   使用该框输入可使用资源的最大人数（如果适用，例如，如果设备邮箱与小汽车对应，您可输入 **4**）。

单击“更多选项”查看或更改以下这些额外的属性：

  - “组织单位”   此只读框显示包含设备邮箱帐户的组织单位 (OU)。您必须使用 Active Directory 用户和计算机移动帐户到其他 OU。

  - “邮箱数据库”   此只读框显示托管此设备邮箱的邮箱数据库的名称。使用 EAC 中的“迁移”页面移动邮箱到其他数据库。

  - “\* 别名”使用此框更改设备邮箱的别名。

  - “不显示在地址列表中”   选中此复选框可以防止设备邮箱出现在通讯簿和在您的 Exchange 组织中定义的其他地址列表中。选中此复选框后，用户仍可使用电子邮件地址向设备邮箱发送预定邮件。

  - “部门”   使用此框指定资源与之关联的部门名称。您可以使用此属性以为动态通讯组和通讯簿创建收件人条件。

  - “公司”   使用此框指定资源与之关联的公司。与“部门”属性一样，您可以使用此属性以为动态通讯组和通讯簿创建收件人条件。

  - “通讯簿策略”   使用此选项可为资源指定通讯簿策略 (ABP)。ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。若要了解详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。
    
    在下拉列表中，选择要与此邮箱关联的策略。

  - “自定义属性”   该部分显示为设备邮箱定义的自定义属性。要指定自定义属性值，请单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。最多可为收件人指定 15 个自定义属性。

## 委派

使用该部分来查看或更改设备邮箱处理保留请求的方式并定义谁可以接受或拒绝预定请求（如果没有自动完成）。

  - “预定请求”   选择以下选项之一以处理预定请求。
    
      - “自动接受或拒绝预定请求”   有效的会议请求将自动预定资源。如果出现某个日程安排与现有预定发生冲突的情况，或者预定请求超出了资源的日程安排限制（例如，预定持续时间太长），则将自动拒绝会议请求。
    
      - “选择用于接受或谢绝预定请求的代理”   资源代理负责接受或拒绝发送到设备邮箱的会议请求。如果指定了多个资源代理，则只需一个代理处理特定的会议请求。

  - “委派”   如果您选择需要发送委派的预定请求的选项，将列出指定的委派。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 或“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以从列表添加或删除委派。

## 预订选项

使用“预定选项”部分来查看或更改预定策略的设置，该策略定义何时可计划资源、可以将资源保留多久以及可提前多久保留。

  - “允许定期会议”   该设置可允许或防止资源的重复会议。默认情况下，启用此设置以允许定期会议。

  - “只允许在工作时间内进行调度”   该设置可接受或拒绝未在为资源定义的工作时间期间的会议请求。默认情况下，该设置将被禁用，从而在工作时间之外允许会议请求。默认情况下，工作时间为周一至周五 8:00 A.M. 至 5:00 P.M.。您可在日历页上的“外观”部分配置设备邮箱的工作时间。

  - “如果结束日期超出该限制始终拒绝”   通过最大预定提前期设置，该设置可控制延伸到指定日期之外的行为或重复会议。
    
      - 如果您启用该设置，重复预定请求将在预定在“最大预定提前期”框中的值指定的日期之前或之后自动拒绝重复预定请求，同时它们超出指定日期。这是默认设置。
    
      - 如果您禁用该设置，将在预定请求在“最大预定提前期”框中的值指定的日期或之前自动接受重复预定请求，同时它们超出指定日期。但是，预定数量会减少，以便不会在指定日期之后进行预定。

  - “最大预定提前期（天）”   该设置指定可以提前预定资源的最大天数。有效输入是介于 0 和 1080 之间的整数。 默认值为 180 天。

  - “最大持续时间（小时）”   该设置指定资源可在预定请求中保留的最大持续时间。默认值为 24 小时。
    
    对于重复预定请求，最长预定持续时间适用于每个重复预定请求实例的时长。

在该页上还有一个框，可用该框来编写消息，该消息将发送至要发送会议请求以保留资源的用户。

## 联系人信息

使用“联系信息”部分来查看或更改资源的联系信息。该页上的信息显示在通讯簿中。

> [!tip]
> 可以使用“州/省”框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。


## 电子邮件地址

使用“电子邮件地址”部分可以查看或更改与设备邮箱关联的电子邮件地址。这包括邮箱的主 SMTP 地址和任何关联代理地址。主 SMTP 地址（也称为“回复地址”）在地址列表中以粗体显示，大写的 **SMTP** 值显示在“类型”列中。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。单击此按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
    
      - “EUM”   EUM（Exchange 统一消息）地址由 Microsoft Exchange Unified Messaging 使用，以在 Exchange 2010 组织中查找已启用 UM 的收件人。EUM 地址包含已启用 UM 的用户的分机号和 UM 拨号计划。单击该按钮，并在“地址/扩展名”框中键入分机号。然后，单击“浏览”并选择邮箱的拨号计划。
    
      - “自定义地址类型”   单击此按钮，然后在“\* 电子邮件地址”框中键入一个支持的非 SMTP 电子邮件地址。
        
        > [!NOTE]
    > 除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。您必须确保所指定的自定义地址符合该地址类型的格式要求。
    
    > [!NOTE]
    > 当添加新电子邮件地址时，您将拥有使其成为主 SMTP 地址的选项。


  - “基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址”   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。

## 邮件提示

使用“邮件提示”部分可添加邮件提示，以便在用户向设备邮箱发送预定请求之前提醒用户存在潜在的问题。邮件提示是在将此收件人添加到新电子邮件的“收件人”、“抄送”或“密件抄送”行中时，信息栏中显示的文本。

> [!NOTE]
> 邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。


## 使用命令行管理程序更改设备邮箱属性

使用以下 cmdlet 集来查看和更改设备邮箱属性：** Get-Mailbox** 和 **Set-Mailbox** cmdlets 来查看和更改设备邮箱的一般属性和电子邮件地址。使用 **Get-CalendarProcessing** 和 **Set-CalendarProcessing** cmdlet 查看和更改委派和预定选项。

  - **Get-User** 和 **Set-User**   使用这些 cmdlet 来查看和设置诸如部门和公司名称等一般属性。

  - **Get-Mailbox** 和 **Set-Mailbox**   使用这些 cmdlets 查看和设置邮箱属性，如电子邮件地址和邮箱数据库。

  - **Get-CalendarProcessing** 和 **Set-CalendarProcessing**   使用这些 cmdlet 查看和设置预定选项和委派。

有关这些 cmdlet 的信息，请参阅下列主题：

  - [Get-User](https://technet.microsoft.com/zh-cn/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-cn/library/aa998221\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Get-CalendarProcessing](https://technet.microsoft.com/zh-cn/library/dd298137\(v=exchg.150\))

  - [Set-CalendarProcessing](https://technet.microsoft.com/zh-cn/library/dd335046\(v=exchg.150\))

这里是一些使用命令行管理程序更改设备邮箱属性的示例。

该示例为 MotorPool 1 设备邮箱更改显示名称和主要 SMTP 地址（称为默认回复地址）。以前的回复地址保留为代理地址。

    Set-Mailbox "MotorPool 1" -DisplayName "Motor Pool 1 - Compact" -EmailAddresses SMTP:MP1.compact@contoso.com,smtp:MP.1@contoso.com

该示例配置设备邮箱以允许仅在工作时间期间计划预定请求。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Set-CalendarProcessing -ScheduleOnlyDuringWorkHours $true

本示例使用 **Get-User** cmdlet 来查找视听部门中的所有设备邮箱，然后使用 **Set-CalendarProcessing** cmdlet 将预定请求发送至名为 Ann Beebe 的代理来接受或拒绝。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox') -and (Department -eq 'Audio Visual')} | Set-CalendarProcessing -AllBookInPolicy $false -AllRequestInPolicy $true -ResourceDelegates "Ann Beebe"

## 您如何知道这有效？

要检查是否成功更改了设备邮箱的属性，可进行以下操作之一：

  - 在 EAC 中，选择邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看您更改的属性或功能。根据您更改的属性，它可能显示在所选邮箱的“详细信息”窗格中。

  - 在命令行管理程序中，使用 **Get-Mailbox** cmdlet 验证更改。使用命令行管理程序的一个优势是，您可查看多个邮箱的多个属性。在上面的示例中（其中只能在工作时间计划预定请求），运行以下命令来验证新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'EquipmentMailbox')} | Get-CalendarProcessing | fl Identity,ScheduleOnlyDuringWorkHours

