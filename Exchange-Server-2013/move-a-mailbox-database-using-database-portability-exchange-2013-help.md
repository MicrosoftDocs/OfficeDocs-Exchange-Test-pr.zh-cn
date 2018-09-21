---
title: '使用数据库可移植性移动邮箱数据库: Exchange 2013 Help'
TOCTitle: 使用数据库可移植性移动邮箱数据库
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51408256
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用数据库可移植性移动邮箱数据库

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-16_

您可以利用数据库可移植性在同一组织中的 Exchange 2013 邮箱服务器之间移动 Microsoft Exchange Server 2013 邮箱数据库。这有助于减少一些故障情况的总恢复时间。若要了解详细信息，请参阅[数据库可移植性](database-portability-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟，再加上还原数据、移动数据库文件以及等待 Active Directory 复制完成所花费的时间。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

  - 无法使用 EAC 以利用数据库可移植性将用户邮箱移动到已恢复数据库或拨号音数据库。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序，利用数据库可移植性将用户邮箱移动到已恢复数据库或拨号音数据库

1.  验证要移动的数据库是否处于干净关闭状态。如果数据库不处于干净关闭状态，则执行软恢复。
    
    > [!NOTE]  
    > 执行软恢复时，任何未提交的日志文件都会提交到数据库。如果没有所有需要的日志文件，则无法完成软恢复过程。继续执行步骤 2。
    
    要将所有未提交的日志文件提交到数据库，请在命令提示符下运行以下命令。
    
    ```powershell
ESEUTIL /R <Enn>
```
    
    > [!NOTE]  
    > &lt;E<em>nn</em>&gt; 为要将日志文件重播到的数据库指定日志文件前缀。由 &lt;E<em>nn</em>&gt; 指定的日志文件前缀是 Eseutil /r 的必需参数。


2.  使用下面的语法在服务器上创建数据库：
    
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>

3.  使用以下语法设置 *This database can be over written by restore* 属性：
    
    ```powershell
Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true
```

4.  当您在上面创建一个新数据库时，移动原始数据库文件（.edb 文件、日志文件和 Exchange Search 目录）至您指定的数据库文件夹。

5.  使用以下语法装入数据库：
    
    ```powershell
Mount-Database <DatabaseName>
```

6.  装入数据库之后，使用 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 修改用户帐户设置，以便帐户指向新邮箱服务器上的邮箱。要将所有用户从旧数据库移动到新数据库，请使用以下语法。
    
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>

7.  使用以下语法触发保留在队列中的任何邮件的传递。
    
    ```powershell
Get-Queue <QueueName> | Retry-Queue -Resubmit $true
```

Active Directory 复制完成之后，所有用户都可以访问其在新 Exchange 服务器上的邮箱。大部分客户端均通过自动发现进行重定向。Microsoft Office Outlook Web App 也能被自动重新定向。

## 您如何知道操作成功？

若要验证是否成功移动了邮箱，请执行以下操作：

  - 使用 Outlook Web App 打开邮箱。

  - 使用 Microsoft Outlook 打开邮箱。

