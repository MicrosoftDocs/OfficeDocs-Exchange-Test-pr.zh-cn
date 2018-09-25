---
title: '移动邮箱数据库副本的邮箱数据库路径: Exchange 2013 Help'
TOCTitle: 移动邮箱数据库副本的邮箱数据库路径
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50490281
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 移动邮箱数据库副本的邮箱数据库路径

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-05-07_

在创建邮箱数据库之后，通过使用 EAC 或命令行管理程序，可以将其移动到另一个卷、文件夹、位置或路径。有关如何移动非复制邮箱数据库的数据库路径的分步说明，请参阅[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

如果要移动的邮箱数据库复制到一个或多个邮箱数据库副本，则必须按照此主题中的过程来移动邮箱数据库路径。邮箱数据库的所有副本都必须位于承载副本的每个服务器上的相同路径中。例如，如果数据库 DB1 位于服务器 EX1 上的 C:\\mountpoints\\DB1 中，则 DB1 在 EX2、EX3 等服务器上的副本也必须位于 C:\\mountpoints\\DB1 中。

若要了解与邮箱数据库副本相关的其他管理任务，请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：两分钟，加上移动数据的时间，具体取决于各种因素，例如数据库大小、速度、可用带宽和网络延迟以及存储速度。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;邮箱数据库副本\&quot;条目。

  - 若要执行移动操作，必须暂时卸除数据库，使所有用户都无法对其进行访问。如果此时卸除数据库，操作完成后将无法重新装入。

  - 若要执行移动操作，必须对所有副本禁用数据库复制。这不足以搁置复制；必须通过使用 [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335119\(v=exchg.150\)) cmdlet 删除数据库副本来禁用复制。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序将复制邮箱数据库移动到新路径

> [!NOTE]  
> 不能使用 EAC 将复制邮箱数据库移动到新路径。


1.  记下要移动的邮箱数据库的所有副本的任何重播延迟设置或截断延迟设置。通过使用 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\)) cmdlet 可以获取此信息，如本例中所示。
    
    ```powershell
    Get-MailboxDatabase DB1 | Format-List *lag*
    ```

2.  如果为数据库启用循环日志记录，则在继续之前必须先禁用它。通过使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet 可以禁用邮箱数据库的循环日志记录，如本例中所示。
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
    ```

3.  删除要移动的数据库的所有邮箱数据库副本。有关详细步骤，请参阅[删除邮箱数据库副本](remove-a-mailbox-database-copy-exchange-2013-help.md)。在删除所有副本之后，通过将要从中删除数据库副本的每个服务器中的数据库和事务日志文件移动到另一个位置，保留这些日志文件。由于保留了这些文件，因此，在重新添加数据库副本后，就不需要重新将它们设定为种子。

4.  将邮箱数据库路径移动到新位置。有关详细步骤，请参阅[Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。
    
    > [!IMPORTANT]  
    > 在移动操作期间，必须卸除要移动的数据库。在完成移动之前，此过程将导致服务中断，并将使正在移动的数据库上的所有用户都会遭遇邮箱中断的问题。移动操作完成后，会自动装入数据库。


5.  在以前包含移动邮箱数据库被动副本的每个邮箱服务器上创建必要的文件夹结构。例如，如果将数据库移动到了 C:\\mountpoints\\DB1，则必须在将要承载邮箱数据库副本的每个邮箱服务器上创建此同一路径。

6.  在创建文件夹结构之后，将邮箱数据库及其日志流的被动副本移动到新位置。这些是在步骤 3 之后留下并保留的文件。对在步骤 3 中删除的每个数据库副本重复此过程。

7.  添加在步骤 3 中删除的所有数据库副本。有关详细步骤，请参阅[添加邮箱数据库副本](add-a-mailbox-database-copy-exchange-2013-help.md)。

8.  在包含要移动的邮箱数据库副本的每个服务器上，运行以下命令以停止并重新启动内容索引服务。
    
    ```PowerShell
    Net stop MSExchangeFastSearch
    Net start MSExchangeFastSearch
    ```

9.  （可选）通过使用 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet 启用循环日志记录，如本例所示。
    
    ```powershell
    Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
    ```

10. 通过使用 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298104\(v=exchg.150\)) cmdlet 为重播延迟时间和截断延迟时间配置任何以前的设置值，如本例所示。
    
    ```powershell
    Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00
    ```

11. 当添加每个副本时，我们建议在添加下一个副本之前验证该副本的运行状况和状态。可以通过以下方式验证运行状况和状态：
    
    1.  检查事件日志是否有与数据库或数据库副本相关的任何错误或警告事件。
    
    2.  使用 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\)) cmdlet 检查数据库副本连续复制的运行状况和状态。
    
    3.  使用 [Test-ReplicationHealth](https://technet.microsoft.com/zh-cn/library/bb691314\(v=exchg.150\)) cmdlet 验证数据库可用性组和连续复制的运行状况和状态。

有关语法和参数的详细信息，请参阅下列主题：

  - [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/zh-cn/library/bb691314\(v=exchg.150\))

## 您如何知道这有效？

要验证您是否已成功移动了邮箱数据库副本的路径，请执行下列操作：

  - 在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;数据库\&quot;。选择复制的数据库。在\&quot;详细信息\&quot;窗格中，会显示数据库副本的状态及其内容索引，并连同当前副本队列长度一起显示。验证状态是否为\&quot;正常\&quot;。

  - 在命令行管理程序中，运行以下命令验证是否已创建邮箱数据库副本以及它是否处于正常运行状态。
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    ```
    
    状态和内容索引状态应该为健康。

