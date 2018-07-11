---
title: '管理收件人的权限: Exchange Online Help'
TOCTitle: 管理收件人的权限
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51408136
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理收件人的权限

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2018-04-20_

可以使用 EAC 或命令行管理程序将权限分配给用户或组（称为*代理*）以允许他们从其他邮箱打开或发送邮件。可以分配用户邮箱、链接的邮箱、资源邮箱和共享邮箱的权限。还可以将权限分配给通讯组、动态通讯组和启用邮件的安全组以允许代理代表组发送邮件。可以为代理分配下列权限以代表邮箱或组访问邮箱或发送邮件：

  - **完全访问权限**   该权限允许代理打开用户邮箱并访问邮箱内容。但是，分配完全访问权限不允许代理从邮箱发送邮件。必须为代理分配\&quot;代理发送\&quot;或\&quot;代表发送\&quot;权限才能发送邮件。
    
    当为组配置权限时完全访问权限不可用。

  - **代理发送**   该权限允许代理使用邮箱发送邮件。在将该权限分配给某个代理后，代理通过该邮箱发送的所有邮件都将显示为已由邮箱所有者发送。但是该权限不会允许代理登录用户邮箱。它仅允许用户打开邮箱。如果此权限分配给组，则代理发送的邮件将显示为已由组发送。

  - **代表发送**   该权限也允许代理使用该邮箱发送邮件。该权限分配给代理后，代理发送的任何邮件中的\&quot;发件人\&quot;地址指示该邮件已由代理代表邮箱所有者发送。

> [!NOTE]  
> 如果您分配完全访问权限、代理发送权限或代表发送权限以访问地址列表中隐藏的邮箱，则代理无法打开该邮箱或发送邮件。


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：2 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 分配邮箱的权限

如上所述，可以为代理分配用户邮箱、链接的邮箱、资源邮箱和共享邮箱的权限。您还可以使用命令行管理程序，为代理分配权限以访问发现邮箱。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题的\&quot;收件人设置权限\&quot;部分中的\&quot;权限和委派\&quot;条目。

## 使用 EAC 分配权限

以下步骤说明了如何分配用户邮箱的权限。您可以按照类似步骤，通过导航到 EAC 中的\&quot;资源\&quot;或\&quot;共享\&quot;页并选择要分配其权限的邮箱，来分配资源或共享邮箱的权限。

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在邮箱列表中，单击要分配其权限的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱委派\&quot;。

4.  要将权限分配给代理，请单击相应权限下面的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示页面，该页面将列出 Exchange 组织内可分配该权限的所有收件人。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
    
    要删除收件人的权限，请在相应权限下，选择收件人，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

5.  单击\&quot;保存\&quot;保存更改。

## 使用 EAC 批量分配权限

使用以下步骤批量分配权限。

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  选择您要为其分配权限的邮箱。

3.  在右窗格中单击或点击\&quot;更多选项\&quot;，并在\&quot;邮箱委派\&quot;下选择\&quot;添加\&quot;。

4.  在\&quot;批量添加委派\&quot;页面，单击或点击相应权限下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")以显示一个页面，其中列出了您可以分配权限的 Exchange 组织中的所有收件人。选择所需收件人，将它们添加到列表中，然后单击\&quot;确定\&quot;。
    
    要删除收件人的权限，请在相应权限下，选择收件人，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

## 使用 EAC 为用户分配从另一个用户的邮箱发送电子邮件的权限

以下步骤显示如何为用户分配从另一个用户的邮箱发送电子邮件的权限。

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在邮箱列表中，单击要分配代理发送权限的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱委派\&quot;。

4.  若要将权限分配给代理，请单击\&quot;代理发送\&quot;或\&quot;代表发送\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，显示一个列出 Exchange 组织中可被分配该权限的所有收件人的页面。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
    
    \&quot;代理发送\&quot;权限允许代理从此邮箱发送电子邮件。
    
    \&quot;代表发送\&quot;权限允许代理代表此邮箱发送电子邮件。代理发送的任何邮件中的\&quot;发件人\&quot;行都将指明该邮件是由代理代表邮箱所有者发送的。
    
    > [!NOTE]  
    > 如果用户还需要能够打开并查看该邮箱的内容，您必须为此用户分配&amp;quot;完全访问&amp;quot;权限。


5.  单击\&quot;保存\&quot;保存更改。

## 使用 EAC 为用户分配从组发送电子邮件的权限。

以下步骤显示如何为用户分配从组发送电子邮件的权限。

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;。

2.  在组列表中，单击要分配代理发送权限的组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在组属性页上，单击\&quot;组委派\&quot;。

4.  若要将权限分配给代理，请单击\&quot;代理发送\&quot;或\&quot;代表发送\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，显示一个列出 Exchange 组织中可被分配该权限的所有收件人的页面。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
    
    \&quot;代理发送\&quot;权限允许代理从此组发送电子邮件。
    
    \&quot;代表发送\&quot;权限允许代理代表此组发送电子邮件。代理发送的任何邮件中的\&quot;发件人\&quot;行都将指明该邮件是由代理代表该组发送的。

5.  单击\&quot;保存\&quot;保存更改。

## 使用 EAC 分配完全访问权限

以下步骤显示如何向用户邮箱分配完全访问权限。

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在邮箱列表中，单击要分配完全访问权限的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击\&quot;邮箱委派\&quot;。

4.  若要将权限分配给代理，请单击\&quot;完全访问\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示页面，该页面将列出 Exchange 组织内可分配该权限的所有收件人。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
    
    \&quot;完全访问\&quot;权限允许代理打开用户邮箱并访问邮箱内容。
    
    > [!NOTE]  
    > 分配&amp;quot;完全访问&amp;quot;权限不允许代理从邮箱发送邮件。您必须为代理分配&amp;quot;代理发送&amp;quot;或&amp;quot;代表发送&amp;quot;权限才能发送邮件。


5.  单击\&quot;保存\&quot;保存更改。

## 使用命令行管理程序分配权限

下面的章节演示如何使用命令行管理程序管理邮箱的完全访问权限、代理发送和代表发送权限。

## 管理完全访问权限

下面的示例演示如何使用 **Add-MailboxPermission** 和 **Remove-MailboxPermission** cmdlet 管理完全访问权限。

此示例为 Raymond Sam 分配 Terry Adams 的邮箱的完全访问权限。

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

此示例为 Esther Valle 分配组织的默认发现搜索邮箱的完全访问权限。

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

此示例为支持人员通讯组的成员分配支持人员票证共享邮箱的完全访问权限。

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

此示例删除 Jim Hance 对 Ayla Kol 邮箱的完全访问权限。

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

有关语法和参数的详细信息，请参阅下列主题：

  - [Add-MailboxPermission](https://technet.microsoft.com/zh-cn/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/zh-cn/library/bb125153\(v=exchg.150\))

## 管理\&quot;代理发送\&quot;权限

下面的示例演示如何在 Exchange Server 2013 和 Exchange Online 中管理\&quot;代理发送\&quot;权限。在 Exchange 2013 中，必须使用 **Add-ADPermission** 和 **Remove-ADPermission** cmdlet；在 Exchange Online 中，必须使用 **Add-RecipientPermission** 和 **Remove-RecipientPermission** cmdlet。在这两种情况下，需要使用 *Identity* 参数指定应添加或删除\&quot;代理发送\&quot;权限的邮箱的名称，使用 *User* 或 *Trustee* 参数指定将被分配或取消分配\&quot;代理发送\&quot;权限的代理（例如用户或组）。

> [!TIP]  
> 使用 <strong>Get-Recipient</strong> cmdlet 可检索邮箱和代理的 <em>Name</em> 属性。使用这些值可分配&amp;quot;代理发送&amp;quot;权限。


## Exchange Server 2013

此示例将\&quot;代理发送\&quot;权限分配给共享邮箱 Helpdesk Support 团队中的 Helpdesk 组。

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

此示例删除用户 Pilar Pinilla 在 James Alvord 邮箱中的\&quot;代理发送\&quot;权限。

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

有关详细的语法和参数信息，请参阅：

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-cn/library/aa996048\(v=exchg.150\))

## Exchange Online

此示例将\&quot;代理发送\&quot;权限分配给共享邮箱 Contoso Printer Support 中的 Printer Support 组。

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

此示例删除用户 Karen Toh 在 Yan Li 邮箱中的\&quot;代理发送\&quot;权限。

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

有关详细的语法和参数信息，请参阅：

  - [Add-RecipientPermission](https://technet.microsoft.com/zh-cn/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/zh-cn/library/ff945794\(v=exchg.150\))

## 管理\&quot;代表发送\&quot;权限

下列示例演示如何使用 **Set-Mailbox** cmdlet 管理\&quot;代表发送\&quot;权限。

此示例为代理 Holly Holt 分配 Sean Chai 邮箱的\&quot;代表发送\&quot;权限。

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

此示例删除 Contoso Executives 共享邮箱中分配给 Temporary Executive Assistants 组的\&quot;代表发送\&quot;权限。

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

有关详细的语法和参数信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道操作成功？

要验证是否已成功分配邮箱或共享邮箱的权限，请执行以下操作之一：

  - 在 EAC 中：
    
    1.  导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;或\&quot;共享\&quot;，单击邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    2.  在邮箱属性页上，单击\&quot;邮箱委派\&quot;。
    
    3.  如果您将权限分配给收件人，请确认相应权限下列出了该用户或组。如果您删除了权限，请确认相应权限下未列出收件人。

或

  - 在命令行管理程序中，根据管理的权限，运行下列命令之一。
    
      - **完全访问权限**
        
            Get-MailboxPermission -Identity <mailbox>
        
        要验证是否为特定代理分配了邮箱的完全访问权限，请运行下列命令。
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **代理发送**
        
        在 Exchange Server 2013 中，运行以下命令。
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        在 Exchange Online 中，运行以下命令。
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **代表发送**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## 将权限分配给组

如上所述，可以将\&quot;代理发送\&quot;和\&quot;代表发送\&quot;权限分配给通讯组、动态分配组和启用邮件的安全组，以允许代理作为组或代表组发送邮件。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题的\&quot;收件人设置权限\&quot;中的\&quot;通讯组\&quot;和\&quot;动态通讯组\&quot;条目。

## 使用 EAC 分配权限

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;。

2.  在组列表中，单击为其分配权限的组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在组属性页上，单击\&quot;组委派\&quot;。

4.  若要向代理分配权限，请单击相应权限下面的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示页面，该页面将显示 Exchange 组织内可分配该权限的所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
    
    要删除收件人的权限，请在相应权限下，选择收件人，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

5.  单击\&quot;保存\&quot;保存更改。

## 使用命令行管理程序分配权限

下面的章节演示如何使用命令行管理程序来管理组的\&quot;代理发送\&quot;和\&quot;代表发送\&quot;权限。

## 管理\&quot;代理发送\&quot;权限

下面的示例演示如何在 Exchange Server 2013 和 Exchange Online 中管理组的\&quot;代理发送\&quot;权限。在 Exchange 2013 中，必须使用 **Add-ADPermission** 和 **Remove-ADPermission** cmdlet。在 Exchange Online 中，必须使用 **Add-RecipientPermission** 和 **Remove-RecipientPermission** cmdlet。在这两种情况下，需要使用 *Identity* 参数指定应添加或删除\&quot;代理发送\&quot;权限的组的名称，使用 *User* 或 *Trustee* 参数指定将被分配或取消分配\&quot;代理发送\&quot;权限的代理（例如用户或组）。

> [!TIP]  
> 使用 <strong>Get-Recipient</strong> cmdlet 可检索组和代理的 <em>Name</em> 属性。使用这些值可分配&amp;quot;代理发送&amp;quot;权限。


## Exchange Server 2013

此示例将\&quot;代理发送\&quot;权限分配给 Contoso Sales Info 组的 Sales Admins 组。这允许 Sales Admins 组的成员以 Contoso Sales Information 组身份发送邮件。

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

此示例删除 Corporate IT Admins 组中用户 Alan Shen 的\&quot;代理发送\&quot;权限。

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

有关详细的语法和参数信息，请参阅：

  - [Add-ADPermission](https://technet.microsoft.com/zh-cn/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/zh-cn/library/aa996048\(v=exchg.150\))

## Exchange Online

此示例将\&quot;代理发送\&quot;权限分配给 Emergency Broadcast Messages 动态通讯组中的 Contoso Admins 组。

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

此示例删除 Printer Resources 安全组中用户 Walter Harp 的\&quot;代理发送\&quot;权限。

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

有关详细的语法和参数信息，请参阅：

  - [Add-RecipientPermission](https://technet.microsoft.com/zh-cn/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/zh-cn/library/ff945794\(v=exchg.150\))

## 管理\&quot;代表发送\&quot;权限

下列示例演示如何使用 **Set-DistributionGroup** 和 **Set-DynamicDistributionGroup** cmdlet 管理组的\&quot;代表发送\&quot;权限。

此示例为代理 Sara Davis 分配 Printer Support 通讯组的\&quot;代表发送\&quot;权限。

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

此示例为代理 Administrator 分配 All Employees 动态通讯组的\&quot;代表发送\&quot;权限。

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

此示例删除 All Employees 动态通讯组中分配给管理员的\&quot;代表发送\&quot;权限。

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

有关详细的语法和参数信息，请参阅：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb123796\(v=exchg.150\))

## 您如何知道操作成功？

要检查是否已成功将权限分配给组，可执行以下操作之一：

  - 在 EAC 中：
    
    1.  导航到\&quot;收件人\&quot;\>\&quot;组\&quot;，单击组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    2.  在组属性页上，单击\&quot;组委派\&quot;。
    
    3.  如果您将权限分配给收件人，请确认相应权限下列出了该用户或组。如果您删除了权限，请确认相应权限下未列出收件人。

或

  - 在命令行管理程序中，根据管理的权限，运行下列命令之一。
    
      - **代理发送**
        
        在 Exchange Server 2013 中，运行以下命令。
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        在 Exchange Online 中，运行以下命令。
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **代表发送**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        或
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

