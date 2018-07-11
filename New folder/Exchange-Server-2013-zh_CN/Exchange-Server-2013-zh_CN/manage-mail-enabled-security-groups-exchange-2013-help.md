---
title: '管理启用邮件的安全组: Exchange Online Help'
TOCTitle: 管理启用邮件的安全组
ms:assetid: 80b3b537-4786-4d02-9202-44e373811a25
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123521(v=EXCHG.150)
ms:contentKeyID: 50489695
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理启用邮件的安全组

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-10-04_

启用邮件的安全组不仅可用于分发邮件，还可用于授予对 Active Directory 中资源的访问权限。有关详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;通讯组\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建已启用邮件的安全组

## 使用 EAC 创建安全组

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;。

2.  单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") \>\&quot;安全组\&quot;。

3.  在\&quot;新建安全组\&quot;页上，填写下列字段：
    
      - **\* 显示名称**   使用此框键入显示名称。此名称将出现在共享的通讯簿中、\&quot;收件人:\&quot;行中（电子邮件发送到该组时），以及 EAC 的\&quot;组\&quot;列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。它在林中必须也是唯一的。
        
        > [!NOTE]
        > 如果已应用组命名策略，则必须遵循对组织强制执行的命名约束。有关详细信息，请参阅<a href="create-a-distribution-group-naming-policy-exchange-2013-help.md">创建通讯组命名策略</a>。如果要替代组织的组命名策略，请参阅<a href="override-the-distribution-group-naming-policy-exchange-2013-help.md">重命名策略的通讯组</a>。
    
      - **\*别名**   在此框中键入安全组的别名。别名的长度不能超过 64 个字符，并且在林中必须是唯一的。当用户在电子邮件的\&quot;收件人:\&quot;行中键入别名时，别名会解析为相应组的显示名称。
    
      - **描述**   使用此框可以对安全组进行说明，以便用户了解组的用途。
    
      - \&quot;组织单位\&quot;   可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为 Active Directory 域中的\&quot;用户\&quot;容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的\&quot;用户\&quot;容器。如果将收件人范围设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择其他 OU，请单击\&quot;**浏览**\&quot;。此时，对话框中会显示林中指定范围内的所有 OU。选择所需的 OU，然后单击\&quot;**确定**\&quot;。
    
      - **\* 所有者**   默认情况下，创建组的人即为所有者。所有组都必须至少有一个所有者。可以通过单击\&quot;添加\&quot;来添加所有者。
    
      - \&quot;成员\&quot;   使用此部分可以添加成员并指定是否需要对人员加入或退出此组进行审批。
        
        组所有者不必是组的成员。使用\&quot;将组所有者添加为成员\&quot;可以将所有者添加为成员，或删除所有者的成员身份。
        
        若要在组中添加成员，请单击\&quot;**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\&quot;。添加完成员后，单击\&quot;**确定**\&quot;，返回到\&quot;**新建安全组**\&quot;页。
        
        如果你希望组所有者接收用户发出的加入组请求，请选中\&quot;**需要所有者审批**\&quot;复选框。选中此选项后，只有组所有者才能删除成员。

4.  完成后，请单击\&quot;保存\&quot;以创建安全组。

> [!NOTE]
> 默认情况下，所有启用邮件的新安全组都要求对所有发件人进行身份验证。这样一来，可防止外部发件人将邮件发送到启用邮件的安全组。若要将启用邮件的安全组配置为接受所有收件人发送的邮件，必须修改相应组的邮件传递限制设置。


## 使用命令行管理程序创建安全组

此示例创建一个别名为 fsadmin 的 File Server Managers 安全组。此安全组是在默认 OU 中创建，经组所有者批准后，任何人都可以加入此组。

    New-DistributionGroup -Name "File Server Managers" -Alias fsadmin -Type security

有关使用命令行管理程序创建已启用邮件的安全组的详细信息，请参阅 [New-DistributionGroup](https://technet.microsoft.com/zh-cn/library/aa998856\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否成功创建了已启用邮件的安全组，请执行以下操作之一：

  - 在 EAC 中，依次转到\&quot;**收件人**\&quot;\>\&quot;**组**\&quot;。此时，新建的启用邮件的安全组会显示在组列表中。在\&quot;**组类型**\&quot;下，组类型是\&quot;**安全组**\&quot;。

  - 在命令行管理程序中，运行以下命令可显示有关新的已启用邮件的安全组的信息。
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

## 更改已启用邮件的安全组属性

## 使用 EAC 更改已启用邮件的安全组属性

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;。

2.  在组列表中，单击要查看或更改的安全组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在组属性页面上，单击以下部分之一来查看或更改属性。
    
      - General
    
      - Ownership
    
      - Membership
    
      - Membership approval
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## 常规

使用此部分可以查看或更改有关组的基本信息。

  - **\* 显示名称**   此名称将会出现在通讯簿中、电子邮件中的\&quot;收件人:\&quot;行中（电子邮件发送到该组时），以及\&quot;组\&quot;列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。显示名称在域中还必须是唯一的。

  - \&quot;\* 别名\&quot;   这是电子邮件地址中出现在 (@) 符号左侧的部分。如果更改别名，组的主 SMTP 地址也会更改，并包含新的别名。同时，带有之前别名的电子邮件地址将作为该组的代理地址保留。

  - \&quot;描述\&quot;   使用此框可以对组进行说明，以便用户了解组的用途。此说明出现在通讯簿和 EAC 的\&quot;详细信息\&quot;窗格中。

  - **在地址列表中隐藏此组** 如果你不希望用户在通讯簿中看到此组，请选中此复选框。选中此复选框后，发件人必须在\&quot;收件人:\&quot;或\&quot;抄送:\&quot;行上键入组的别名或电子邮件地址，才能将邮件发送到相应组。
    
    > [!tip]
    > 应考虑隐藏安全组，原因是这些组通常用于向组成员分配权限，而不是用于发送电子邮件。


  - **部门**   此只读框显示包含安全组的部门 (OU)。必须使用 Active Directory 用户和计算机，才能将组移到其他 OU 中。

## 所有权

在此部分中可以分配组所有者。组所有者不仅可以在组中添加成员，还能批准或拒绝加入组请求。默认情况下，组创建者即为组所有者。每个组都至少必须有一个所有者。

可以通过单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")来添加所有者。通过选中一个所有者然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")，可以删除该所有者。

## 成员身份

使用此部分可以添加或删除成员。组所有者不必是组的成员。在\&quot;成员\&quot;下，可通过单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")来添加成员。可通过在成员列表中选择一个用户然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")来删除成员。

## 成员身份审批

在此部分中可以指定用户是否需要获得所有者批准才能加入组。如果你选中\&quot;**需要所有者审批**\&quot;复选框，一名或多名组所有者会收到请求审批加入组的电子邮件。如前所述，只有所有者才能从组中删除成员。

> [!NOTE]
> 由于存在与安全相关的限制，因此无法对启用邮件的安全组使用这个选项。


## 传递管理

使用此部分可以管理谁将电子邮件发送到该组。

  - **仅属于您所在组织的发件人**   选择此选项可以仅允许组织中的发件人向此组发送邮件。这意味着如果组织外部的某个人向此组发送电子邮件，邮件将被拒绝。这是默认设置。

  - **允许组织内外的发件人**   选择此选项可以允许任何人向此组发送邮件。
    
    您可以通过仅允许特定发件人向此组发送邮件，来进一步限制可以将邮件发送到此组的发件人。单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择一个或多个收件人。向此列表中添加发件人后，这些发件人将是唯一能够向此组发送邮件的人员。不在此列表中的任何人发送的邮件都将被拒绝。
    
    若要从列表中删除个人或组，请从列表中选择相应的个人或组，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。
    
    > [!important]
    > 如果您已将此组配置为只允许组织内部的发件人向此组发送邮件，则从邮件联系人发送的电子邮件将被拒绝，即使这些联系人已添加到此列表中也是如此。


## 邮件审批

使用此部分可以设置用于仲裁组的选项。审阅人可以在发送到此组的邮件到达组成员之前批准或拒绝邮件。

  - **发送到此组的邮件必须由审查方批准**   默认情况下，此复选框处于未选中状态。如果你选中此复选框，传入的邮件在传递前会先由组审查方进行检查。组审查方可以批准或拒绝传入的邮件。

  - **组审查方**   若要添加组审查方，请单击\&quot;**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\&quot;。若要删除审查方，请选择相应审查方，然后单击\&quot;**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")\&quot;。如果已选中\&quot;发送到此组的邮件必须由审查方批准\&quot;，但未选择审查方，则发送到此组的邮件将会发送给组所有者以供审批。

  - **无需审查其邮件的发件人**   若要添加可以绕过组审查的个人或组，请单击\&quot;**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\&quot;。若要删除个人或组，请选择相应项，然后单击\&quot;**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")\&quot;。

  - **选择审阅通知** 使用此部分可以设置如何通知用户有关邮件审批的情况。
    
      - **当发件人的邮件未得到批准时，通知所有发件人**   这是默认设置，即在组织内外发件人的邮件未得到批准时，通知这些发件人。
    
      - \&quot;当组织中发件人的邮件未得到批准时，通知这些发件人\&quot;如果选择此选项，则在审阅人未批准组织中的个人或组发送到此组的邮件时仅通知相应的发件人。
    
      - \&quot;某邮件未通过批准时，不通知任何人\&quot;   如果选择此选项，则不会向组审阅人未批准其邮件的邮件发件人发送通知。

## 电子邮件选项

使用此部分可以查看或更改与该组关联的电子邮件地址。这包括组的主 SMTP 地址和任何关联的代理地址。主 SMTP 地址（也称为\&quot;回复地址\&quot;）在地址列表中以粗体显示，大写的 **SMTP** 值显示在\&quot;类型\&quot;列中。

  - \&quot;添加\&quot;   单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - \&quot;SMTP\&quot;   这是默认的地址类型。单击此按钮，然后在\&quot;\* 电子邮件地址\&quot;框中键入新的 SMTP 地址。
        
        > [!NOTE]
        > 若要将新地址设为相应组的主 SMTP 地址，请选中&amp;quot;<strong>将此设为答复地址</strong>&amp;quot;复选框。仅当未选中&amp;quot;<strong>基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址</strong>&amp;quot;复选框时，才能看到此复选框。
    
      - \&quot;自定义地址类型\&quot;   单击此按钮，然后在\&quot;\* 电子邮件地址\&quot;框中键入一个支持的非 SMTP 电子邮件地址。
        
        > [!NOTE]
        > 除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。您必须确保所指定的自定义地址符合该地址类型的格式要求。


  - \&quot;编辑\&quot;   要更改与组关联的电子邮件地址，在列表中选择该地址，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    > [!NOTE]
    > 若要将现有地址设为相应组的主 SMTP 地址，请选中&amp;quot;<strong>将此设为答复地址</strong>&amp;quot;复选框。如前所述，仅当未选中&amp;quot;<strong>基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址</strong>&amp;quot;复选框时，才能看到此复选框。


  - \&quot;移除\&quot;   要删除与组关联的电子邮件地址，在列表中选择该地址，然后单击\&quot;移除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

  - **基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址**   选中此复选框后，可根据对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。默认情况下，此框处于选中状态。

## MailTip

使用此部分可以添加邮件提示，以便在用户向该组发送邮件时提醒用户存在潜在的问题。邮件提示是在将该组添加到新电子邮件的\&quot;收件人\&quot;、\&quot;抄送\&quot;或\&quot;密件抄送\&quot;行时，信息栏中显示的文本。例如，对于较大的组，可添加邮件提示来提醒潜在的发送人：他们的邮件将会发送给很多人。

> [!NOTE]
> 邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。


## 组代理

使用此部分可以向用户分配权限（称为\&quot;代理\&quot;），允许他们以组身份发送邮件或代表组发送邮件。可以分配以下权限：

  - \&quot;发送身份\&quot;   此权限允许代理以组身份发送邮件。分配此权限后，代理可选择将组添加到\&quot;发件人\&quot;行以指示该邮件由组发送。

  - \&quot;代表以下用户发送\&quot;   此权限也允许代理代表组发送邮件。在分配该选项后，代理可选择在\&quot;发件人\&quot;行中添加组。邮件将显示为由组发送，并将说明该邮件由代理代表组发送。

若要向代理分配权限，请单击相应权限下的\&quot;**添加**\&quot;，调出\&quot;**选择收件人**\&quot;页，其中列出了 Exchange 组织内可分配有此权限的所有收件人。选择所需的收件人，将其添加到列表中，然后单击\&quot;**确定**\&quot;。也可以搜索特定的收件人，具体方法为在搜索框中键入收件人的姓名，然后单击\&quot;**搜索**![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")\&quot;。

## 使用命令行管理程序更改安全组属性

使用 **Get-DistributionGroup** 和 **Set-DistributionGroup** cmdlet 可查看和更改安全组的属性。命令行管理程序的优势在于，能够更改 EAC 中不可更改的属性，并能更改多个安全组的属性。若要了解哪些参数对应哪些通讯组属性，请参阅下列主题：

  - [Get-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\))

下面是使用命令行管理程序更改安全组属性的一些示例。

此示例显示组织中所有安全组的列表。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')}

此示例将 Seattle Administrators 安全组的主 SMTP 地址（也称为\&quot;答复地址\&quot;）从 admins@contoso.com 更改为 seattle.admins@contoso.com。以前的答复地址将保持为代理地址。

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.admins@contoso.com,smtp:admins@contoso.com

此示例在通讯簿中隐藏组织中的所有安全组。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} | Set-DistributionGroup -HiddenFromAddressListsEnabled $true

## 您如何知道这有效？

要验证是否已成功更改安全组的属性，请执行以下操作：

  - 在 EAC 中选择组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看已更改的属性或功能。根据所更改的属性，它可能显示在选定组的\&quot;详细信息\&quot;窗格中。

  - 在命令行管理程序中，使用 **Get-DistributionGroup** cmdlet 可验证更改。命令行管理程序的一大优势在于，可查看多个组的多个属性。上面的示例在通讯簿中隐藏所有安全组。在此示例中，运行以下命令即可验证新值。
    
        Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalSecurityGroup')} |
         fl Name,HiddenFromAddressListsEnabled


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="&amp;quot;领英学习&amp;quot;短图标" alt="&amp;quot;领英学习&amp;quot;短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

