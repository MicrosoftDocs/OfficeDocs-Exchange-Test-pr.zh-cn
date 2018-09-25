---
title: '永久删除邮箱: Exchange 2013 Help'
TOCTitle: 永久删除邮箱
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50556690
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 永久删除邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-11-16_

永久删除活动邮箱和断开连接的邮箱时，将从 Exchange 邮箱数据库中清除所有邮箱内容，并将永久丢失数据。 在永久删除活动邮箱时，也会删除关联的 Active Directory 用户帐户。

永久删除邮箱的替代方法是将其断开连接。 默认情况下，断开连的接邮箱将在邮箱数据库中保留 30 天。 这样便有机会在将邮箱从数据库中清除之前重新连接或还原邮箱。

若要进一步了解断开连接的邮箱以及执行其他相关管理任务，请参阅以下主题：

  - [断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)

  - [禁用或删除邮箱](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [连接禁用的邮箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

> [!NOTE]  
> 不能使用 EAC 永久删除活动邮箱或断开连接的邮箱。


## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 永久删除活动邮箱

## 使用命令行管理程序永久删除活动邮箱

运行以下命令可永久删除活动邮箱和关联的 Active Directory 用户帐户。

```powershell
Remove-Mailbox -Identity <identity> -Permanent $true
```

> [!NOTE]  
> 如果不加入 <em>Permanent</em> 参数，则在默认情况下，删除的邮箱在被永久删除之前，将在邮箱数据库中保留 30 天。


有关语法和参数的详细信息，请参阅 [Remove-Mailbox](https://technet.microsoft.com/zh-cn/library/aa995948\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已永久删除活动邮箱，请执行以下操作：

1.  验证在 EAC 中是否已不再列出邮箱。

2.  验证在“Active Directory 用户和计算机”中是否已不再列出关联的用户帐户。

3.  运行以下命令验证是否从 Exchange 邮箱数据库中成功清除了邮箱。
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where {         Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
    ```
    
    如果已成功清除邮箱，则该命令将不返回任何结果。 如果未清除邮箱，则该命令将返回有关邮箱的信息。

## 永久删除断开连接的邮箱

## 使用命令行管理程序永久删除断开连接的邮箱

有两种类型的断开连接的邮箱： 禁用和软删除。 在运行 cmdlet 永久删除邮箱之前，必须指定其中一种类型。如果指定的类型与断开连接的邮箱的实际类型不匹配，则该命令会失败。

运行以下命令可确定断开连接的邮箱是被禁用还是被软删除。

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason
```

断开连接的邮箱的 *DisconnectReason* 属性的值将为 `Disabled` 或 `SoftDeleted`。

可以运行以下命令显示组织中所有断开连接的邮箱的类型。

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason
```

> [!WARNING]  
> 使用 <strong>Remove-StoreMailbox</strong> cmdlet 永久删除断开连接的邮箱时，将从邮箱数据库中清除其所有内容，并会永久丢失数据。


此示例从邮箱数据库 MBD01 中永久删除 GUID 为 2ab32ce3-fae1-4402-9489-c67e3ae173d3 的禁用邮箱。

```powershell
Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled
```

此示例从邮箱数据库 MBD01 中永久删除 Dan Jump 的软删除邮箱。

```powershell
Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted
```

此示例从邮箱数据库 MBD01 中永久删除所有软删除邮箱。

```powershell
Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}
```

有关语法和参数的详细信息，请参阅 [Remove-StoreMailbox](https://technet.microsoft.com/zh-cn/library/ff829913\(v=exchg.150\)) 和 [Get-MailboxStatistics](https://technet.microsoft.com/zh-cn/library/bb124612\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否永久删除了断开连接的邮箱，以及是否已成功将其从 Exchange 邮箱数据库中清除，请运行以下命令。

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {     Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```

如果已成功清除邮箱，则该命令将不返回任何结果。 如果未清除邮箱，则该命令将返回有关邮箱的信息。

