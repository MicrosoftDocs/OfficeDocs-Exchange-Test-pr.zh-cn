---
title: '连接禁用的邮箱: Exchange 2013 Help'
TOCTitle: 连接禁用的邮箱
ms:assetid: a8abd399-75fd-4ee2-b2e4-634b55e4f79f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863439(v=EXCHG.150)
ms:contentKeyID: 50556631
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 连接禁用的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-13_

可以使用 EAC 或命令行管理程序将已禁用的邮箱连接到 Active Directory 用户帐户。 在禁用邮箱时，Exchange 会将邮箱保留在邮箱数据库中，并将邮箱切换到禁用状态。 Exchange 属性也会从对应的 Active Directory 用户帐户中删除，但用户帐户会保留。 邮箱会保留到被删除邮箱的保留期（默认为 30 天）结束，然后会从邮箱数据库中永久删除（即*清除*）。

在从 Exchange 邮箱数据库中永久删除禁用的邮箱之前，可以使用 EAC 或命令行管理程序将其重新连接到原始 Active Directory 用户帐户。

若要进一步了解断开连接的邮箱以及执行其他相关管理任务，请参阅以下主题：

  - [断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)

  - [禁用或删除邮箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 在命令行管理程序中运行 **Get-User** cmdlet 验证要将禁用的邮箱连接到的 Active Directory 用户帐户是否存在，以及该帐户是否已与其他邮箱关联。 若要将禁用的邮箱连接到某个用户帐户，该帐户必须存在，并且 *RecipientType* 属性的值必须为 `User`（表示该帐户尚未启用邮箱）。
    
    对于内部部署 Exchange 组织，也可以在“Active Directory 用户和计算机”中验证此信息。

  - 运行以下命令可以验证邮箱数据库中存在要将用户帐户连接到的已禁用邮箱，并且这些邮箱不是软删除的邮箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,Database,DisconnectReason
    
    若要连接禁用的邮箱，邮箱数据库中必须存在相应的邮箱，并且 *DisconnectReason* 属性的值必须为 `Disabled`。 如果已将邮箱从数据库中清除，则该命令不会返回任何结果。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 您想执行什么操作？

## 使用 EAC 连接已禁用的邮箱

以下过程展示如何连接已禁用的用户邮箱。 也可以将禁用的链接邮箱和禁用的共享邮箱重新连接到对应的用户帐户。

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


3.  单击要重新连接的已禁用邮箱，再单击“连接”。

4.  在询问您是否确定要重新连接该邮箱的窗口中，单击“是”。
    
    Exchange 会将已禁用的邮箱重新连接到对应的用户帐户。

## 使用命令行管理程序连接已禁用的邮箱

在命令行管理程序中使用 **Connect-Mailbox** cmdlet 可以将用户帐户连接到禁用的邮箱。必须指定要连接的邮箱的类型。 以下示例展示了用于重新连接用户邮箱、链接邮箱和共享邮箱的语法。

此示例将连接用户邮箱。*Identity* 参数指定 Exchange 数据库中断开连接的邮箱。 *User* 参数指定要将邮箱重新连接到的 Active Directory 用户帐户。

    Connect-Mailbox -Identity "Jeffrey Zeng" -Database MBXDB01 -User "Jeffrey Zeng"

本示例将连接链接的邮箱。*Identity* 参数指定 Exchange 数据库中断开连接的邮箱。 *LinkedMasterAccount* 参数指定帐户林中要将邮箱重新连接到的 Active Directory 用户帐户。 *Alias* 参数指定重新连接的邮箱的别名；别名是电子邮件地址中 @ 符号左侧的部分。

    Connect-Mailbox -Identity "Kai Axford" -Database MBXDB02 -LinkedDomainController FabrikamDC01 -LinkedMasterAccount kai.axford@fabrikam.com -Alias kaia

此示例将连接共享邮箱。

    Connect-Mailbox -Identity "Corporate Shared Mailbox" -Database "Mailbox Database 03" -User "Corporate Shared Mailbox" -Alias corpshared -Shared

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在运行 <strong>Connect-Mailbox</strong> cmdlet 时不包括 <em>Alias</em> 参数，则使用<em>User</em> 或 <em>LinkedMasterAccount</em> 参数中指定的值为重新连接的邮箱创建电子邮件地址别名。</td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Connect-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997878\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功将已禁用的邮箱连接到用户帐户，请执行下列操作之一：

  - 在 EAC 中，单击“收件人”，导航到重新连接的邮箱类型的相应页面，单击“刷新”![刷新图标](images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif "刷新图标")，然后验证是否列出了邮箱。

  - 在“Active Directory 用户和计算机”中，右键单击禁用了邮箱的用户帐户，再单击“属性”。 在“常规”选项卡上，观察“电子邮件”框已经填充了重新连接的邮箱的电子邮件地址。

  - 在此命令行管理程序中，运行以下命令。
    
        Get-User <identity>
    
    *RecipientType* 属性的 **UserMailbox** 值表示用户帐户和邮箱已经连接。 也可以运行 **Get-Mailbox** cmdlet 验证邮箱是否存在。

