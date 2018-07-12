---
title: '重新设定搜索目录种子: Exchange 2013 Help'
TOCTitle: 重新设定搜索目录种子
ms:assetid: 9d873bd4-0422-4975-b5e2-82a347479115
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633475(v=EXCHG.150)
ms:contentKeyID: 52061542
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 重新设定搜索目录种子

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

如果邮箱数据库副本的内容索引目录损坏，则可能需要对目录重新设定种子。应用程序事件日志中通过以下事件指示损坏的内容索引。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>事件 ID</th>
<th>级别</th>
<th>来源</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>123</p></td>
<td><p>错误</p></td>
<td><p>ExchangeStoreDB</p></td>
<td><p>设定 &lt;<em>时间戳</em>&gt; 时，此服务器上的 Microsoft Exchange 信息存储数据库 &lt;<em>标识</em>&gt; 副本遇到损坏的搜索目录。有关错误的更有针对性的信息，请参阅服务器上其他“ExchangeStoreDb”和“MSExchange 搜索索引器”事件的事件日志。建议通过“Update-MailboxDatabaseCopy”任务对目录重新设定种子。</p></td>
</tr>
</tbody>
</table>


如果邮箱数据库副本所在的服务器是数据库可用性组 (DAG) 的一部分，您可以从另一个 DAG 成员中为内容索引目录重新设定种子。

如果该邮箱数据库副本是唯一的副本，您必须手动创建一个新的内容索引目录。

有关与 Exchange 搜索相关的其他管理任务，请参阅[Exchange 搜索过程](exchange-search-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 预计完成时间：2 分钟。实际重新设定种子时间可能因重新设定种子的内容索引目录的大小而异。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“Exchange 搜索”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 如果邮箱数据库是 DAG 的一部分，请为内容索引目录重新设定种子

如果该邮箱数据库所在的服务器是 DAG 的一部分，请采取以下措施之一。

## 对来自任何来源的内容索引目录重新设定种子

本示例可从 DAG 中拥有该数据库副本的任意源服务器中为邮箱服务器 MBX1 上的数据库副本 DB1 的内容索引目录重新设定种子。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -CatalogOnly

有关详细的语法和参数信息，请参阅 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\))。

## 对来自特定来源的内容索引目录重新设定种子

本示例对邮箱服务器 MBX1 上的数据库副本 DB1 的内容索引目录重新设定种子，其中 MBX1 来自具有该数据库副本的邮箱服务器 MBX2。

    Update-MailboxDatabaseCopy -Identity DB1\MBX1 -SourceServer MBX2 -CatalogOnly

有关详细的语法和参数信息，请参阅 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\))。

## 如果该邮箱数据库只有一个副本，请为内容索引目录重新设定种子。

如果该邮箱数据库只有一个副本，您必须通过重新创建内容索引目录手动为搜索目录重新设定种子。

1.  运行以下命令以停止 Microsoft Exchange Search 和 Microsoft Exchange Search Host Controller 服务。
    ```
        Stop-Service MSExchangeFastSearch
    ```
    ```
        Stop-Service HostControllerService
    ```

2.  删除、移动或重命名包含 Exchange 内容索引目录的文件夹。此文件夹命名为 `%ExchangeInstallPath\Mailbox\<name of mailbox database>_Catalog\<GUID>12.1.Single`。例如，您可能会将该文件夹重命名为 `C:\Program Files\Microsoft\Exchange Server\V15\Mailbox\Mailbox Database 0657134726_Catalog\F0627A72-9F1D-494A-839A-D7C915C279DB12.1.Single_OLD`。
    
    > [!NOTE]  
    > 删除此文件夹会腾出额外的磁盘空间。或者，您可能想要出于故障诊断目的移动或重命名该文件夹。


3.  运行以下命令以重启 Microsoft Exchange Search 和 Microsoft Exchange Search Host Controller 服务。
    ```
        Start-Service MSExchangeFastSearch
    ```
    ```
        Start-Service HostControllerService
    ```
    
    在您重启这些服务之后，Exchange Search 会重新生成内容索引目录。

## 您如何知道这样可行？

Exchange Search 为内容索引目录重新设定种子可能要花费一些时间。运行以下命令以显示重新设定种子进程的状态。

    Get-MailboxDatabaseCopyStatus | FL Name,*Index*

当为搜索目录重新设定种子时，*ContentIndexState* 属性的值是 **Crawling**。当重新设定种子完成时，该值变为 **Healthy**。

