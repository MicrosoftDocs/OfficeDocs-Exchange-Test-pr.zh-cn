---
title: '还原软删除的邮箱: Exchange 2013 Help'
TOCTitle: 还原软删除的邮箱
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50556574
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 还原软删除的邮箱

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2012-11-29_

使用命令行管理程序将软删除的邮箱连接到 Active Directory 用户帐户。 当邮箱移动到另一不同邮箱数据库时，它在源邮箱数据库中将变为“软删除”。 移动完成后，Exchange 不会将该邮箱从源邮箱数据库中完全删除。而是将源邮箱数据库中的邮箱切换为软删除状态。 这样，如果移动期间出现错误，导致邮箱在目标数据库中出现故障或损坏，则您可以还原源邮箱。 如果确实出现错误，则可还原源邮箱，然后尝试重新移动。

软删除邮箱将保留在源数据库中，直到已删除邮箱保留期过期或直到使用 **Remove-StoreMailbox** cmdlet 清除软删除邮箱为止。 直到软删除邮箱从 Exchange 邮箱数据库中永久删除之后，您才可以使用命令行管理程序将软删除邮箱的内容还原至现有邮箱或存档邮箱。

若要了解有关软删除邮箱的详细信息并执行其他相关的管理任务，请参阅以下主题：

  - [断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)

  - [连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [管理邮箱还原请求](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 本主题中的此过程只能在命令行管理程序中执行。 不能使用 EAC 还原软删除的邮箱。

  - 运行以下命令，验证要连接用户帐户的软删除邮箱仍位于邮箱数据库中，且不是已禁用邮箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    
    软删除邮箱必须位于邮箱数据库中，且 *DisconnectReason* 属性值必须为 `SoftDeleted`。 如果邮箱已从数据库中清除，则命令不会返回任何结果。
    
    或者，运行以下命令显示组织中的所有软删除邮箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 使用命令行管理程序还原软删除的邮箱

您可以使用命令行管理程序，通过 **New-MailboxRestoreRequest** cmdlet 将软删除邮箱还原至现有邮箱。 还原软删除邮箱时，其内容将复制到名为“目标邮箱”的现有邮箱中。 默认情况下，邮箱还原请求成功完成之后，该请求将保留 30 天，然后再删除。可以通过使用 **Remove-MailboxRestoreRequest** cmdlet 提前将它删除。

软删除邮箱还原之后，该邮箱将保留在邮箱数据库中，直到管理员永久删除或已删除邮箱保留期过期时清除为止。

若要创建邮箱还原请求，则必须使用显示名、邮箱 GUID 或软删除邮箱的旧版可分辨名称 (DN)。 使用 **Get-MailboxStatistics** cmdlet，显示要还原的软删除邮箱的 **DisplayName**、**MailboxGuid** 和 **LegacyDN** 属性值。 例如，运行以下命令可为组织中所有已禁用邮箱和软删除邮箱返回此信息。

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database

此示例可将 *SourceStoreMailbox* 参数中由显示名标识、且位于 MBXDB01 邮箱数据库中的软删除邮箱还原至名为 Debra Garcia 的目标邮箱。 我们使用了 *AllowLegacyDNMismatch* 参数，以便源邮箱能够还原至一个与软删除邮箱没有相同旧版 DN 值的邮箱中。

    New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

本示例将 Pilar Pinilla 的软删除存档邮箱（由邮箱 GUID 标识）还原至其当前的存档邮箱中。 *AllowLegacyDNMismatch* 参数并非必要参数，这是因为主邮箱及其对应的存档邮箱均具有相同的旧版 DN。

    New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive

有关语法和参数的详细信息，请参阅 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功将软删除邮箱还原至目标邮箱中，请运行 **Get-MailboxRestoreRequest** cmdlet 或 **Get-MailboxRestoreRequestStatistics** cmdlet，以显示还原请求的相关信息。 如果还原请求已成功创建，则 *Status* 属性将拥有 **Queued**、**InProgress**或**Completed**值。 还原请求完成之后，软删除邮箱的内容将显示在目标邮箱中。

有关详细信息，请参阅：

  - [管理邮箱还原请求](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/zh-cn/library/ff829912\(v=exchg.150\))

