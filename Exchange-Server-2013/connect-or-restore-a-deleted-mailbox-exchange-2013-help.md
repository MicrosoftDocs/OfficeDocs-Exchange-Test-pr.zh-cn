---
title: '连接或还原已删除的邮箱: Exchange 2013 Help'
TOCTitle: 连接或还原已删除的邮箱
ms:assetid: a5e6ac44-5901-4eab-9017-c6fae80a0f83
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863438(v=EXCHG.150)
ms:contentKeyID: 50556650
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 连接或还原已删除的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-05-04_

可以使用 EAC 或命令行管理程序将已删除的邮箱连接到 Active Directory 用户帐户。在删除邮箱时，Exchange 会将邮箱保留在邮箱数据库中，并将邮箱切换到禁用状态。关联的 Active Directory 用户帐户也会被删除。邮箱会保留到被删除邮箱的保留期（默认为 30 天）结束，然后会从邮箱数据库中永久删除（即*清除*）。

在从 Exchange 邮箱数据库中永久删除被删除的邮箱之前，可以使用 EAC 或命令行管理程序将其连接到 Active Directory 用户帐户。还可以使用命令行管理程序将删除的邮箱中的内容还原到现有的邮箱。

若要进一步了解断开连接的邮箱以及执行其他相关管理任务，请参阅以下主题：

  - [断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)

  - [禁用或删除邮箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [连接禁用的邮箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 在 Active Directory 中新建一个要将删除的邮箱连接到的用户帐户。或者在命令行管理程序中使用 **Get-User** cmdlet 验证要将删除的邮箱连接到的 Active Directory 用户帐户是否存在，以及该帐户是否已与其他邮箱关联。若要将删除的邮箱连接到某个用户帐户，该帐户必须存在，并且 *RecipientType* 属性的值必须为 `User`（表示该帐户尚未启用邮箱）。
    
    对于内部部署 Exchange 组织，也可以在“Active Directory 用户和计算机”中验证此信息。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在连接删除的链接邮箱、资源邮箱或共享邮箱时，要将邮箱连接到的 Active Directory 用户帐户必须处于禁用状态。</td>
    </tr>
    </tbody>
    </table>


  - 若要验证邮箱数据库中存在要将用户帐户连接到的已删除邮箱，并且这些邮箱不是软删除的邮箱，请运行以下命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    邮箱数据库中必须存在删除的邮箱，并且 *DisconnectReason* 属性的值必须为 `Disabled`。如果已将邮箱从数据库中清除，则该命令不会返回任何结果。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 您想执行什么操作？

## 连接已删除的邮箱

连接到已删除的邮箱时，要将该邮箱与未启用邮件（即没有现有邮箱）的用户帐户关联。若要将删除的邮箱与有邮箱的用户帐户连接，必须还原删除的邮箱。有关详细信息，请参阅本主题后面的还原已删除的邮箱。

## 使用 EAC 连接已删除的邮箱

以下过程展示了如何将删除的用户邮箱连接到用户帐户。也可以使用此过程将已删除的链接邮箱、资源邮箱和共享邮箱连接到用户帐户。

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  单击“更多”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，然后单击“连接邮箱”。
    
    将显示在 Exchange 组织中选定的 Exchange 服务器上断开连接的邮箱列表。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>这个断开连接邮箱列表包括了禁用的、删除的和软删除的邮箱。</td>
    </tr>
    </tbody>
    </table>


3.  单击要将用户连接到的已删除邮箱，然后单击“连接”。

4.  在询问您是否确定要连接该邮箱的窗口中，单击“是”。
    
    此时将显示一个未启用邮件的用户帐户列表。

5.  单击要将删除的邮箱连接到的用户，然后单击“确定”。
    
    Exchange 会将删除的邮箱连接到选择的用户帐户。

## 使用命令行管理程序连接已删除的邮箱

在命令行管理程序中使用 **Connect-Mailbox** cmdlet 可将删除的邮箱连接到未启用邮件的用户帐户。必须指定要连接的邮箱的类型。以下示例展示了用于重新连接用户邮箱、链接邮箱、会议室邮箱、设备邮箱和共享邮箱的语法。在所有示例中，可选的 *Alias* 参数用于指定电子邮件别名，即电子邮件地址中 @ 符号的左侧部分。如果不包括 *Alias* 参数，则使用 *User* 或 *LinkedMasterAccount* 参数中指定的值为重新连接的邮箱的电子邮件地址创建别名。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如前所述，在连接链接邮箱、资源邮箱或共享邮箱时，要将邮箱链接到的 Active Directory 用户帐户必须处于禁用状态。</td>
</tr>
</tbody>
</table>


此示例将连接用户邮箱。*Identity* 参数指定邮箱数据库 MBXDB01 中保留的已删除邮箱的显示名。*User* 参数指定要将邮箱连接到的 Active Directory 用户帐户。

    Connect-Mailbox -Identity "Paul Cannon" -Database MBXDB01 -User "Robin Wood" -Alias robinw

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>还可以使用 <code>LegacyDN</code> 或 <code>MailboxGuid</code> 属性的值来标识删除的邮箱。</td>
</tr>
</tbody>
</table>


本示例将连接链接的邮箱。*Identity* 参数指定邮箱数据库 MBXDB02 上的已删除邮箱。*LinkedMasterAccount* 参数指定帐户林中要将邮箱连接到的 Active Directory 用户帐户。*LinkedDomainController* 参数指定帐户林中的域控制器。

    Connect-Mailbox -Identity "Temp User" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount danpark@fabrikam.com -Alias dpark

本示例将连接会议室邮箱。

    Connect-Mailbox -Identity "rm2121" -Database "MBXResourceDB" -User "Conference Room 2121" -Alias ConfRm2121 -Room

本示例将连接设备邮箱。

    Connect-Mailbox -Identity "MotorPool01" -Database "MBXResourceDB" -User "Van01 (12 passengers)" -Alias van01 -Equipment

此示例将连接共享邮箱。

    Connect-Mailbox -Identity "Printer Support" -Database MBXDB01 -User "Corp Printer Support" -Alias corpprint -Shared

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>还可以使用 <code>LegacyDN</code> 或 <code>MailboxGuid</code> 值来标识删除的邮箱。</td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Connect-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997878\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功将已删除的邮箱连接到用户帐户，请执行下列操作之一：

  - 在 EAC 中，单击“收件人”，导航到连接的邮箱类型的相应页面，单击“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")，然后验证是否列出了邮箱。

  - 在“Active Directory 用户和计算机”中，右键单击连接到邮箱的用户帐户，再单击“属性”。在“常规”选项卡上，请注意，“电子邮件”框已经填充了连接的邮箱的电子邮件地址。

  - 在此命令行管理程序中，运行以下命令。
    
        Get-User <identity>
    
    *RecipientType* 属性的 **UserMailbox** 值表示用户帐户和邮箱已经连接。也可以运行 **Get-Mailbox \<identity\>** 命令来验证邮箱是否已连接。

## 还原已删除的邮箱

可以使用命令行管理程序，使用 **New-MailboxRestoreRequest** cmdlet 将已删除的邮箱还原到现有的邮箱。在还原删除的邮箱时，会将邮箱的内容复制到现有的邮箱（称为*目标邮箱*）。在还原了删除的邮箱之后，该邮箱仍保留在邮箱数据库中，直到管理员将其永久删除，或者在删除的邮箱的保留期结束时将其清除。

默认情况下，在成功完成邮箱还原请求之后，会将邮箱保留 30 天后再删除。可以使用 **Remove-StoreMailbox** cmdlet 将其提前删除。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 还原删除的邮箱。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序还原已删除的邮箱

若要创建邮箱还原请求，必须使用已删除邮箱的显示名、旧版可分辨名称 (DN) 或邮箱 GUID。使用 **Get-MailboxStatistics** cmdlet 可显示要还原的已删除邮箱的 `DisplayName`、`MailboxGuid` 和 `LegacyDN` 属性的值。例如，运行以下命令可为组织中所有已禁用和已删除的邮箱返回此信息。

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "Disabled"} | fl DisplayName,MailboxGuid,LegacyDN,Database

此示例将已删除的邮箱还原到目标邮箱 Debra Garcia；已删除的邮箱用 *SourceStoreMailbox* 参数标识，并且位于 MBXDB01 邮箱数据库上。因为使用了 *AllowLegacyDNMismatch* 参数，因此可将源邮箱还原到一个不同的邮箱（没有相同的旧 DN 值的邮箱）。

    New-MailboxRestoreRequest -SourceStoreMailbox e4890ee7-79a2-4f94-9569-91e61eac372b -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

此示例将 Pilar Pinilla 的已删除存档邮箱还原到其当前的存档邮箱。*AllowLegacyDNMismatch* 参数不是必需的，因为主邮箱及其对应的存档邮箱有相同的旧 DN。

    New-MailboxRestoreRequest -SourceStoreMailbox "Personal Archive - Pilar Pinilla" -SourceDatabase "MDB01" -TargetMailbox pilarp@contoso.com -TargetIsArchive

有关语法和参数的详细信息，请参阅 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\))。

## 使用命令行管理程序还原已删除的公用文件夹邮箱

如果您硬删除了公用文件夹邮箱，现在想要还原并且该邮箱在已删除项目保留时间限制内（请参阅[配置已删除邮件的保留时间和可恢复邮件配额](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)），您可以依次使用 `Connect-Mailbox` cmdlet 和 `Update-StoreMailboxState` cmdlet。有关语法和参数的详细信息，请参阅 [Connect-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997878\(v=exchg.150\)) 和 [Update-StoreMailboxState](https://technet.microsoft.com/zh-cn/library/jj860462\(v=exchg.150\))。

您将需要已删除公用文件夹邮箱的 GUID 以及包含该公用文件夹邮箱的邮箱数据库的 GUID 或名称。如果没有此信息，您可以执行以下步骤：

1.  通过运行以下 cmdlet 获取 Active Directory 林和域控制器完全限定的域名 (FQDN)：
    
        Get-OrganizationConfig | fl OriginatingServer

2.  利用步骤 1 返回的信息，搜索 Active Directory 中的“已删除对象”容器以获取公用文件夹邮箱的 GUID 和包含已删除公用文件夹邮箱的邮箱数据库的 GUID 或名称。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>您可以使用自定义脚本或 Ldp 实用程序搜索已删除对象，该实用程序可以通过在 Powershell 提示符处键入 <strong>ldp.exe</strong> 打开。</td>
    </tr>
    </tbody>
    </table>


当知道了已删除公用文件夹邮箱 GUID 和包含该公用文件夹邮箱的邮箱数据库的名称或 GUID 后，运行以下命令来还原公用文件夹邮箱。

1.  通过运行以下命令新建一个 Active Directory 对象（可能会提示您提供适当的凭据）：
    
        New-MailUser <mailUserName> -ExternalEmailAddress <emailAddress> 
        
        Get-MailUser <mailUserName> | Disable-MailUser
    
    其中 `<mailUserName>`、`<emailAddress>` 以及 `<mailUserName>` 是您选择的值。在下一个步骤中，您将需要用到相同的 `<mailUserName>` 值。

2.  运行以下命令将已删除公用文件夹邮箱连接至刚才创建的 Active Directory 对象：
    
        Connect-Mailbox -Identity <public folder mailbox GUID> -Database <database name or GUID> -User <mailUserName>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><code>Identity</code> 参数指定 Exchange 数据库中要连接到 Active Directory 用户对象的邮箱对象。上面的示例指定了公用文件夹邮箱的 GUID，但您也可以使用“显示名称”值或 LegacyExchangeDN 值。</td>
    </tr>
    </tbody>
    </table>


3.  根据下面的示例，在公用文件夹邮箱上运行 `Update-StoreMailboxState`：
    
        Update-StoreMailboxState -Identity <public folder mailbox GUID> -Database <database name or GUID>
    
    如步骤 2 所示，`Identity` 参数将接受公用文件夹邮箱的 GUID、显示名称或 LegacyExchangeDN 值。

## 您如何知道这有效？

若要验证是否已成功还原已删除的公用文件夹邮箱，请运行 **Get-publicfolder GetChildren-\<公用文件夹邮箱 GUID\>** cmdlet。如果还原已成功，此 cmdlet 会正常工作。

有关详细信息，请参阅：

  - [Connect-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997878\(v=exchg.150\))

  - [Update-StoreMailboxState](https://technet.microsoft.com/zh-cn/library/jj860462\(v=exchg.150\))

