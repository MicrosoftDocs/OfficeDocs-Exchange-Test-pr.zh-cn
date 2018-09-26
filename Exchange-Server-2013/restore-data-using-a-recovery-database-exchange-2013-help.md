---
title: '使用恢复数据库还原数据: Exchange 2013 Help'
TOCTitle: 使用恢复数据库还原数据
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50491632
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用恢复数据库还原数据

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-10-01_

恢复数据库 (RDB) 是一种特殊的邮箱数据库，通过它您可以从在恢复操作中还原的邮箱数据库装入和提取数据。RSG 使您能够从备份或数据库副本中恢复数据，而不会影响用户对当前数据的访问。

创建 RDB 之后，可以通过使用备份应用程序或通过将数据库及其日志文件复制到 RDB 文件夹结构，将邮箱数据库还原到该 RDB 中。然后，可以使用 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\)) cmdlet 从恢复的数据库中提取数据。提取数据后，可以将该数据导出到某个文件夹或合并到某个现有的邮箱中。

有关与 RDB 相关的额外管理任务，请参阅[恢复数据库](recovery-databases-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 分钟再加上将数据库置于干净关闭状态并提取数据所花费的时间。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮箱恢复\&quot;条目。

  - 某些备份应用程序能够将 Exchange 数据直接还原到恢复数据库。Windows 服务器备份只能将文件级备份还原到恢复数据库。它不能用于将应用程序级备份还原到恢复数据库。

  - 必须将包含恢复数据的数据库和日志文件还原或复制到 RDB 文件夹结构中。

  - 数据库必须处于一种干净关闭状态。因为 RDB 是所有数据库的备用恢复位置，所以所有还原的数据库都将处于异常关闭状态。必须使用 **Eseutil /R** 将还原的数据库置于干净关闭状态。

## 通过命令行管理程序使用恢复数据库恢复数据

1.  复制恢复的数据库及其日志文件，或将数据库及其日志文件还原到将要供恢复数据库使用的位置。

2.  使用 Eseutil 将该数据库置于干净关闭状态。在以下示例中，EXX 是数据库的日志生成前缀（例如，E00、E01、E02 等等）。
    
    ```powershell
    Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    ```
    
    以下示例说明了 E01 日志生成前缀、恢复数据库和日志文件路径 E:\\Databases\\RDB1：
    
    ```powershell
    Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1
    ```

3.  创建一个恢复数据库。为该恢复数据库指定一个唯一的名称，但要将数据库文件的名称和路径用于 EdbFilePath 参数，将恢复的日志文件的位置用于 LogFolderPath 参数。
    
    ```powershell
       New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    ```        
    
    以下示例说明了创建一个将用来恢复 DB1.edb 及其日志文件（位于 E:\\Databases\\RDB1）的恢复数据库。
    
    ```powershell
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"
    ```        

4.  重新启动 Microsoft Exchange 信息存储服务：
    
    ```powershell
    Restart-Service MSExchangeIS
    ```

5.  装入恢复数据库：
    
    ```powershell
    Mount-database <RDBName>
    ```

6.  验证已装入的数据库包含您希望还原的邮箱：
    
    ```powershell
    Get-MailboxStatistics -Database <RDBName> | ft -auto
    ```

7.  使用 New-MailboxRestoreRequest cmdlet 将邮箱或项目从恢复数据库还原到生产邮箱中。
    
    以下示例将邮箱数据库 DB1 上具有 MailboxGUID 1d20855f-fd54-4681-98e6-e249f7326ddd 的源邮箱还原到具有别名 Morris 的目标邮箱。
    
    ```powershell
    New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    ```
    
    以下示例将邮箱数据库 DB1 上具有显示名称 Morris Cornejo 的源邮箱的内容还原至 Morris@contoso.com 存档邮箱。
    
    ```powershell
    New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive
    ```

8.  使用 [Get-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829907\(v=exchg.150\)) 定期检查邮箱还原请求的状态。
    
    当还原状态为\&quot;已完成\&quot;时，使用 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829910\(v=exchg.150\)) 删除还原请求。例如：
    
    ```powershell
    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
    ```

## 您如何知道这有效？

要验证是否成功恢复了邮箱数据，使用 Outlook 或 Outlook Web App 打开目标邮箱并验证是否存在恢复的数据。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

