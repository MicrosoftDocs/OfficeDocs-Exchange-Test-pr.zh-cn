---
title: '诊断 Exchange 搜索问题: Exchange 2013 Help'
TOCTitle: 诊断 Exchange 搜索问题
ms:assetid: 8cfa26f4-ccf0-42dd-8570-67018188b4e8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123701(v=EXCHG.150)
ms:contentKeyID: 52061528
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 诊断 Exchange 搜索问题

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Exchange Search 可对 Exchange 邮箱中的邮箱和受支持附件编制索引。Exchange 搜索增加了电子邮件的数量以及邮箱大小和存储配额、为用户配置了存档邮箱，并引入了可执行发现搜索的就地电子数据展示，已成为 Microsoft Exchange Server 2013 组织中关键的邮箱服务器组件。Exchange 搜索存在的问题可能会影响用户工作效率和就地电子数据展示功能。

有关 Exchange 搜索的详细信息，请参阅[Exchange 搜索](exchange-search-exchange-2013-help.md)。

若要了解与管理 Exchange Search 相关的管理任务，请参阅[Exchange 搜索过程](exchange-search-procedures-exchange-2013-help.md)。

## 使用 Test-ExchangeSearch Cmdlet

本主题中的过程的步骤 5 介绍了如何运行 **Test-ExchangeSearch** cmdlet 来帮助诊断 Exchange Search 问题。您可以使用 **Test-ExchangeSearch** cmdlet 测试邮箱服务器、邮箱数据库或特定邮箱的 Exchange Search 功能。此 cmdlet 会向指定邮箱发送测试邮件（如果未指定邮箱，则向数据库的系统邮箱发送），然后执行搜索以确定邮件是否已编制索引，包括编制索引所花的时间。正常情况下，Exchange Search 会在邮件创建或发送到邮箱后 10 秒左右对邮件编制索引。测试完毕后，测试邮件将自动删除。

有关语法和参数的详细信息，请参阅 [Test-ExchangeSearch](https://technet.microsoft.com/zh-cn/library/bb124733\(v=exchg.150\))。

## 检索不可搜索的项目

您可以使用 [Get-FailedContentIndexDocuments](https://technet.microsoft.com/zh-cn/library/dd351154\(v=exchg.150\)) cmdlet 检索 Exchange 搜索无法成功编制索引的不可搜索邮箱项目的列表。可以对邮箱服务器、邮箱数据库或特定邮箱运行 cmdlet。Cmdlet 会返回每个不可搜索项目的详细信息。无法搜索邮箱项目的原因有若干个。例如，可能是因为电子邮件中可能包含无法编制索引以供搜索的附件文件类型，也可能是因为搜索筛选器未安装或已禁用。如果相应文件类型的搜索筛选器可用，则您可以将它安装在 exExchangeNoVersionExchange 服务器上。

> [!IMPORTANT]  
> 由 Microsoft 提供的搜索筛选器已经过测试并由 Microsoft 提供支持。我们建议您先在测试环境中测试所有的第三方搜索筛选器，然后再将此类搜索筛选器安装在生产环境中的 exExchangeNoVersionExchange 服务器上。


若要详细了解不可搜索的项目，请参阅：

  - [由 Exchange 搜索编制索引的文件格式](file-formats-indexed-by-exchange-search-exchange-2013-help.md)

  - [Exchange 电子数据展示中不可搜索的项目](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

## 诊断 Exchange 搜索问题

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“Exchange 搜索”条目。

1.  **检查服务状态**   Microsoft Exchange Search (MSExchangeFastSearch) 服务是否已在邮箱服务器上启动？如果是，请转至步骤 2。如果不是，请使用 MMC 服务管理单元验证 MSExchangeFastSearch 服务是否正在运行，如下所示：
    
    1.  单击“开始”，指向“管理工具”，然后单击“服务”。
    
    2.  在“服务”中，确认“Microsoft Exchange 搜索”服务的“状态”为“已启动”。

2.  **检查邮箱数据库配置：** 用户邮箱数据库的 *IndexEnabled* 参数是否设置为 true？如果是，请转至步骤 3。如果不是，请在命令行管理程序中运行以下命令以验证 *IndexEnabled* 标志是否设置为 true。
    
    ```powershell
Get-MailboxDatabase | Format-Table Name,IndexEnabled
```
    
    有关语法和参数的详细信息，请参阅 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\))。

3.  **检查邮箱数据库爬网状态**   是否已对 Exchange 数据库进行爬网？如果是，请转至步骤 4。如果不是，请使用可靠性和性能监视器检查“MSExchange 搜索索引”性能对象的“爬网程序: 剩余邮箱”计数器。执行下列步骤：
    
    1.  打开“性能监视器”(perfmon.exe)。
    
    2.  在控制台树中的“监视工具”下，单击“性能监视器”。
    
    3.  在性能监视器窗格中，单击“添加”（绿色加号）。
    
    4.  在“添加计数器”的“从计算机选择计数器”列表中，选择要监视的邮箱数据库所在的服务器。
    
    5.  在“从计算机中选择计数器”列表下方不带标签的框中，选择“MSExchange 搜索索引”性能对象。
    
    6.  在“所选对象实例”框中，选择用户邮箱数据库的实例。
    
    7.  单击“添加”，然后单击“确定”。
        
        在“性能监视器”窗格中，“MSExchange 搜索索引”性能对象列在“对象”列中，其各个计数器列在“计数器”列中。
    
    8.  查看“爬网程序: 剩余邮箱”计数器。任何值为 1 或大于 1 均表示仍在对数据库中的邮箱进行爬网。爬网完成时，该值为“0”。
    
    若要了解如何使用性能监视器，请参阅 [Windows Server 2008 中性能和可靠性监视的入门指南](https://go.microsoft.com/fwlink/p/?linkid=178005)

4.  **检查数据库副本索引运行状况：** 内容索引状态是否正常？使用 **Get-MailboxDatabaseCopyStatus** cmdlet 可检查数据库副本的内容索引运行状况。
    
        Get-MailboxDatabaseCopyStatus -Server $env:ComputerName | Format-Table Name,Status,ContentIndex* -Auto
    
    有关语法和参数的详细信息，请参阅 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/zh-cn/library/dd298044\(v=exchg.150\))。

5.  **运行 Test-ExchangeSearch cmdlet：** 如果邮箱数据库已爬网，则可以对邮箱数据库或特定邮箱运行 **Test-ExchangeSearch** cmdlet。
    
    ```powershell
Test-ExchangeSearch -Identity AlanBrewer@contoso.com
```
    
    有关语法和参数的详细信息，请参阅 [Test-ExchangeSearch](https://technet.microsoft.com/zh-cn/library/bb124733\(v=exchg.150\))。

6.  **检查应用程序事件日志：** 使用事件查看器或命令行管理程序检查应用程序事件日志中与搜索相关的错误消息。检查以下事件源。
    
      - **MSExchangeFastSearch**
    
      - **MSExchangeIS**
    
    有关详细信息，请参阅事件日志条目中的链接。

7.  **重新启动 Microsoft Exchange 搜索服务**   使用服务 MMC 管理单元或命令行管理程序停止 MicrosoftExchange 搜索 (MSExchangeFastSearch) 服务，然后重新启动：
    
    1.  单击“开始”，指向“管理工具”，然后单击“服务”。
    
    2.  在“服务”中，右键单击“Microsoft Exchange 搜索”，然后单击“停止”。服务停止后，再次右键单击此服务，然后单击“开始”。

8.  **重新设定搜索目录种子：** 在某些情况下，例如搜索目录损坏时，您可能需要对该目录重新设定种子。如果需要对搜索目录重新设定种子，Exchange Search 将在应用程序事件日志中记录，向您发出通知。有关对搜索目录重新设定种子的详细信息，请参阅[重新设定搜索目录种子](reseed-the-search-catalog-exchange-2013-help.md)。

