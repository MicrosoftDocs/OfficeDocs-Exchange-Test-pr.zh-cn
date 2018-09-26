---
title: '执行拨号音恢复: Exchange 2013 Help'
TOCTitle: 执行拨号音恢复
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51408198
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 执行拨号音恢复

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-27_

使用拨号音可移植性，用户可以在其原始邮箱正在还原或修复的过程中使用一个临时邮箱来发送和接收电子邮件。该临时邮箱可以位于同一个 Exchange 2013 邮箱服务器上，也可以位于组织中的任何其他 Exchange 2013 邮箱服务器上。使用拨号音可移植性的过程称为\&quot;拨号音恢复\&quot;，拨号音恢复需要在邮箱服务器上创建一个空数据库来替换故障数据库。若要了解详细信息，请参阅[拨号音可移植性](dial-tone-portability-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟，再加上还原和移动数据所花费的时间。

  - 部署的数据库必须小于最大数据库数才能创建拨号音数据库。Exchange 2013 标准版在每个服务器上最多支持 5 个数据库。Exchange 2013 企业版在 RTM 和 CU1 中最多为每个服务器支持 50 个数据库，但在 CU2 和更高版本中为每个服务器支持 100 个数据库。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序在单个服务器上执行拨号音恢复

> [!NOTE]  
> 无法使用 EAC 在单个服务器上执行拨号音恢复。


1.  确保保留要恢复的数据库的任何现有文件，以供以后执行恢复操作时使用。

2.  使用 [New-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997976\(v=exchg.150\)) cmdlet 可以创建拨号音数据库，如本例中所示。
    
    ```powershell
    New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB
    ```

3.  使用 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 可以重新放置正在恢复的数据库上所驻留的用户邮箱，如本例中所示。
    
    ```powershell
    Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1
    ```

4.  使用 [Mount-Database](https://technet.microsoft.com/zh-cn/library/aa998871\(v=exchg.150\)) cmdlet 可以装入数据库，使客户端计算机可以访问数据库，并发送和接收邮件，如本例中所示。
    
    ```powershell
    Mount-Database -Identity DTDB1
    ```

5.  创建恢复数据库 (RDB)，并还原或复制包含要恢复到 RDB 中的数据的数据库和日志文件。有关详细步骤，请参阅[创建恢复数据库](create-a-recovery-database-exchange-2013-help.md)。

6.  在将数据复制到 RDB 之后和在装入还原数据库之前，将任何日志文件从失败的数据库复制到恢复数据库日志文件夹，以便对还原的数据库播放这些日志文件。

7.  装入 RDB，然后使用 [Dismount-Database](https://technet.microsoft.com/zh-cn/library/bb124936\(v=exchg.150\)) cmdlet 将其卸除，如本例中所示。
    
    ```powershell
    Mount-Database -Identity RDB1
    Dismount-Database -Identity RDB1
    ```

8.  在卸除 RDB 之后，将 RDB 文件夹中的当前数据库和日志文件移动到安全位置。该操作将在准备交换恢复的数据库和拨号音数据库的过程中完成。

9.  卸除拨号音数据库，如本例中所示。注意，在卸除此数据库时，最终用户将遇到服务中断。
    
    ```powershell
    Dismount-Database -Identity DTDB1
    ```

10. 将数据库和日志文件从拨号音数据库文件夹移入 RDB 文件夹。

11. 将数据库和日志文件从包含已恢复数据库的安全位置移入拨号音数据库文件夹，然后装入该数据库，如本例中所示。
    
    ```powershell
    Mount-Database -Identity DTDB1
    ```
    
    这将结束最终用户的服务中断。用户可以访问其原始生产数据库，并发送和接收邮件。

12. 装入 RDB，如本例中所示。
    

    ```powershell
    Mount-Database -Identity RDB1
    ```

13. 使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) 和 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\)) cmdlet 可以从 RDB 导出数据，并将其导入恢复的数据库，如本例中所示。这会将使用拨号音数据库发送和接收的所有邮件导入生产数据库中。
    
    ```powershell
    $mailboxes = Get-Mailbox -Database DTDB1
    ```        

    ```powershell
    $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }
    ```

    
14. 在还原操作完成之后，可以卸除并删除 RDB，如本例中所示。
    
    ```powershell
    Dismount-Database -Identity RDB1
    Remove-MailboxDatabase -Identity RDB1
    ```

有关详细的语法和参数信息，请参阅下列主题：

  - [New-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/zh-cn/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/zh-cn/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/aa997931\(v=exchg.150\))

## 您如何知道操作成功？

若要验证是否成功移动了邮箱，请执行以下操作：

  - 使用 Microsoft Office Outlook Web App 打开邮箱。

  - 使用 Microsoft Outlook 打开邮箱。

