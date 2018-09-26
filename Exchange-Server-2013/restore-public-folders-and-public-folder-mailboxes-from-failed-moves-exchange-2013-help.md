---
title: '恢复失败的移动公用文件夹和公用文件夹的邮箱: Exchange 2013 Help'
TOCTitle: 恢复失败的移动公用文件夹和公用文件夹的邮箱
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52061493
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 恢复失败的移动公用文件夹和公用文件夹的邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-13_

如果公用文件夹或公用文件夹邮箱的移动请求失败，那么只要满足以下条件，您就可以还原相应的文件夹或邮箱：

  - **公用文件夹移动失败**   公用文件夹的软删除副本仍存在于源公用文件夹邮箱中，且仍处于保留期。

  - **公用文件夹邮箱移动失败**   公用文件夹邮箱的软删除副本仍存在于源公用文件夹邮箱数据库中，且仍处于邮箱保留期。

如果邮箱保持期已过，则可以从备份中恢复单个公用文件夹的邮箱。然后从已还原的邮箱中提取数据并将其复制到目标文件夹或将其合并使用另一个邮箱。有关详细信息，请参阅[使用恢复数据库还原数据](restore-data-using-a-recovery-database-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱还原请求\&quot;条目。

  - 无法使用 EAC 执行此过程。必须使用命令行管理程序。

  - 若要创建还原请求，您必须提供软删除的公用文件夹邮箱的 *DisplayName*、*LegacyDN* 或 *MailboxGUID* 参数值。

  - 默认情况下，转储程序文件夹将还原与常规的文件夹。这可以通过使用*ExcludeDumpster*参数来防止。

  - 恢复公用文件夹的邮箱与不同还原正则的邮箱，如果它们不存在于目标邮箱，将不会创建文件夹。缺少的文件夹将显示在恢复请求的末尾一条警告消息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 要执行什么操作？

## 还原软删除的公用文件夹

本示例将公用文件夹 \\Dev\\CustomerEnagagements 还原到目标公用文件夹邮箱 Development01 中。

```powershell
    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements
```

有关语法和参数的详细信息，请参阅 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\))。

## 还原软删除的公用文件夹邮箱

本示例将公用文件夹邮箱 PF\_Singapore 还原为新的公用文件夹邮箱 PF\_Singapore\_Restore。

```powershell
    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch
```

有关语法和参数的详细信息，请参阅 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\))。

