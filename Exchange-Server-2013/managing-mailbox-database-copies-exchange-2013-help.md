---
title: '管理邮箱数据库副本: Exchange 2013 Help'
TOCTitle: 管理邮箱数据库副本
ms:assetid: 28cedf1d-365a-4e36-b2ba-6bf81af8684f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335158(v=EXCHG.150)
ms:contentKeyID: 50490107
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理邮箱数据库副本

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-08-26_

在创建、配置并使用邮箱服务器成员填充数据库可用性组 (DAG) 之后，可以使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序通过灵活和精细的方式添加邮箱数据库副本。

## 管理数据库副本

在创建数据库的多个副本之后，可以使用 EAC 或命令行管理程序监视每个副本的运行状况和状态，并执行与数据库副本关联的其他管理任务。您可能需要执行的某些管理任务包括挂起或恢复数据库副本、为数据库副本设定种子、监视数据库副本、配置数据库副本设置以及删除数据库副本。

## 挂起和恢复数据库副本

出于多种原因（如执行计划维护），可能需要挂起和恢复对数据库副本的连接复制活动。此外，某些管理任务（如设定种子）需要先挂起数据库副本。我们建议在更改数据库路径或其日志文件时挂起所有复制活动。可以使用 EAC 或通过在命令行管理程序中运行 **Suspend-MailboxDatabaseCopy** 和 **Resume-MailboxDatabaseCopy** cmdlet 来挂起和恢复数据库副本活动。有关如何挂起或恢复数据库副本的连续复制活动的详细步骤，请参阅[挂起或恢复邮箱数据库副本](suspend-or-resume-a-mailbox-database-copy-exchange-2013-help.md)。

## 为数据库副本设定种子

*种子设定*（也称为*更新*）是一个过程，在此过程中将数据库（空白数据库或生产数据库副本）添加到与活动数据库相同的 DAG 中其他邮箱服务器上的目标副本位置。这将成为该服务器维护的副本的基线数据库。

根据实际情况，设定种子可以是自动过程，也可以是手动启动的过程。添加数据库副本时，将自动设定副本种子，但前提是正确配置了目标服务器及其存储。如果您想手动植入数据库副本的种子，而不想在创建副本时自动植入种子，可以在运行 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 时使用 *SeedingPostponed* 参数。

在初始种子设定已经发生之后，数据库副本很少需要重新设定种子。但如果需要重新设定种子，或者要手动为数据库副本设定种子而不是系统自动为副本设定种子，则可以通过在 EAC 中使用更新邮箱数据库副本向导或者在命令行管理程序中使用 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 来执行这些任务。在为数据库副本设定种子之前，必须首先挂起邮箱数据库副本。有关如何为数据库副本设定种子的详细步骤，请参阅[更新邮箱数据库副本](update-a-mailbox-database-copy-exchange-2013-help.md)。

在完成手动设定种子操作之后，将自动恢复对已设定种子的邮箱数据库副本的复制。如果不希望自动恢复复制，则可以在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 的同时使用 *ManualResume* 参数。

## 选择要设定的种子

执行种子设定操作时，可以选择为邮箱数据库副本、邮箱数据库副本的内容索引目录设定种子，或者同时为数据库副本和内容索引目录副本设定种子。

更新邮箱数据库副本向导和 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 的默认行为是同时为邮箱数据库副本和内容索引目录副本设定种子。若只要为邮箱数据库副本设定种子，而不为内容索引目录设定种子，请在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 时使用 *DatabaseOnly* 参数。若只要为内容索引目录副本设定种子，请在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 时使用 *CatalogOnly* 参数。

## 选择种子设定源

任何状况良好的数据库副本都可以用作该数据库其他副本的种子设定源。在具有已跨多个物理位置进行扩展的 DAG 时，这特别有用。例如，考虑一下四成员 DAG 部署的情况，其中两名成员（MBX1 和 MBX2）在俄勒冈州的波特兰、另两名成员（MBX3 和 MBX4）在纽约州的纽约市。名为 DB1 的邮箱数据库在 MBX1 上处于活动状态，并在 MBX2 和 MBX3 上有 DB1 的被动副本。将 DB1 的副本添加到 MBX4 后，您可以选择将 MBX3 上的副本用作种子设定源。这样做可以避免通过波特兰和纽约之间的广域网 (WAN) 链路来设定种子。

若要在添加新数据库副本时使用特定副本作为种子设定源，则会执行以下操作：

  - 在运行 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) cmdlet 的同时使用 *SeedingPostponed* 参数添加数据库副本。如果不使用 *SeedingPostponed* 参数，则将使用数据库的活动副本作为源为数据库副本显式设定种子。

  - 可以在 EAC 中指定要用作更新邮箱数据库副本向导一部分的源服务器，也可以在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 时使用 *SourceServer* 参数指定所需源服务器以进行种子设定。在前面的示例中，您会指定 MBX3 作为源服务器。如果不使用 *SourceServer* 参数，则将通过数据库的主动副本为数据库副本显式设定种子。

## 种子设定和网络

除选择特定的源服务器为邮箱数据库副本设定种子外，还可以使用命令行管理程序指定要使用的 DAG 网络，并且可以选择在种子设定操作期间替代 DAG 网络的压缩和加密设置。

> [!NOTE]  
> 对上下文索引目录设定种子仅可通过 MAPI 网络实现。如果在 Update-MailboxDatabaseCopy cmdlet 中使用 <code>-Network</code> 参数，这也同样适用。


若要指定要用于种子设定的网络，请在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 的同时使用 *Network* 参数，并指定要使用的 DAG 网络。如果不使用 *Network* 参数，则系统会使用以下默认行为来选择要用于种子设定操作的网络：

  - 如果源服务器和目标服务器在相同子网上并且已配置包括该子网的复制网络，则将使用该复制网络。

  - 如果源服务器和目标服务器在不同子网上，即使已配置包含这些子网的复制网络，但还是将客户端 (MAPI) 网络用于种子设定。

  - 如果源服务器和目标服务器在不同数据中心中，则客户端 (MAPI) 网络将用于种子设定。

在 DAG 级别 上，将 DAG 网络配置为加密和压缩。默认设置是仅对不同子网上的通信使用加密和压缩。如果源和目标在不同子网上并且以 *NetworkCompression* 和 *NetworkEncryption* 的默认值配置 DAG，则可以在运行 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 的同时使用 *NetworkCompressionOverride* 和 *NetworkEncryptionOverride* 参数分别覆盖这些值。

## 种子设定过程

使用 [Add-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298105\(v=exchg.150\)) 或 [Update-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335201\(v=exchg.150\)) cmdlet 启动种子设定过程时，将执行以下任务：

1.  从 Active Directory 读取数据库属性以验证指定的数据库和服务器，并且验证源和目标服务器正在运行 Exchange 2013、它们都是同一 DAG 的成员以及指定的数据库不是恢复数据库。还读取数据库文件路径。

2.  从目标服务器上的 Microsoft Exchange 复制服务准备重新设定种子检查。

3.  目标服务器上的 Microsoft Exchange 复制服务会检查数据库和事务日志文件在步骤 1 中由 Active Directory 检查读取的文件目录中是否存在。

4.  Microsoft Exchange 复制服务将状态信息从目标服务器返回到从其运行 cmdlet 的管理界面。

5.  如果所有初级检查已经完成，则会继续之前提示您确认操作。如果您确认操作，则继续执行该过程。如果在初级检查期间遇到错误，则报告错误，并且操作失败。

6.  从目标服务器上的 Microsoft Exchange 复制服务启动种子设定操作。

7.  Microsoft Exchange 复制服务挂起活动数据库副本的数据库复制。

8.  由 Microsoft Exchange 复制服务会更新数据库的状态信息，以反映种子设定的状态。

9.  如果目标服务器已经没有目标数据库和日志文件的目录，则创建它们。

10. 将为数据库设定种子的请求从目标服务器上的 Microsoft Exchange 复制服务传递使用 TCP 的源服务器上的 Microsoft Exchange 复制服务。这个为数据库设定种子的请求和后续通信将在已配置为复制网络的 DAG 网络上进行。

11. 源服务器上的 Microsoft Exchange 复制服务通过 Microsoft Exchange 信息存储服务界面启动可扩展存储引擎 (ESE) 流式备份。

12. Microsoft Exchange 信息存储服务将数据库数据流式传输到 Microsoft Exchange 复制服务。

13. 数据库数据从源服务器的 Microsoft Exchange 复制服务移动到目标服务器的 Microsoft Exchange 复制服务。

14. 目标服务器上的 Microsoft Exchange 复制服务将数据库副本写入位于名为“temp-seeding”的主数据库目录中的临时目录。

15. 源服务器上的流式备份操作随着到达数据库最后一行而结束。

16. 目标服务器上的写入操作完成，并且数据库从 temp-seeding 目录移动到最后位置。将删除 temp-seeding 目录。

17. 在目标服务器上，Microsoft Exchange 复制服务代理向 Microsoft Exchange 搜索服务代理发出请求，要求装入数据库副本的内容索引编录（如果有）。如果数据库副本的以前实例中有已过时的编录文件，则装入操作失败，这将激发从源服务器复制编录的需求。同样，如果目标服务器上的数据库副本的新实例上不存在编录，则编录的副本是必需的。从源复制新编录时，Microsoft Exchange 复制服务会指示 Microsoft Exchange 搜索服务挂起对数据库副本的索引编制操作。

18. 目标服务器上的 Microsoft Exchange 复制服务向源服务器上的 Microsoft Exchange 复制服务发送为编录设定种子的请求。

19. 在源服务器上，Microsoft Exchange 复制服务请求来自 Microsoft Exchange 搜索服务的目录信息，并且请求挂起索引编制操作。

20. 源服务器上的 Microsoft Exchange 搜索服务将搜索编录目录信息返回到 Microsoft Exchange 复制服务。

21. 源服务器上的 Microsoft Exchange 复制服务从目录读取编录文件。

22. 源服务器上的 Microsoft Exchange 复制服务使用跨复制网络的连接将编录数据移动到目录服务器上的 Microsoft Exchange 复制服务。在读取完成之后，Microsoft Exchange 复制服务将请求发送给 Microsoft Exchange 搜索服务以恢复源数据库的索引编制操作。

23. 如果目录中出现任何目标服务器上的现有编录文件，则目标服务器上的 Microsoft Exchange 复制服务会删除它们。

24. 目标服务器上的 Microsoft Exchange 复制服务将编录数据写入名为“CiSeed.Temp”的临时目录，直到完整传输数据为止。

25. Microsoft Exchange 复制服务将完成的编录数据移动到最终位置。

26. 目标服务器上的 Microsoft Exchange 复制服务恢复对目标数据库上的索引搜索。

27. 目标服务器上的 Microsoft Exchange 复制服务返回完成状态。

28. 操作的最后结果将传递到从其调用 cmdlet 的管理界面。

## 配置数据库副本

在创建数据库副本之后，可以在需要时查看和修改其配置设置。通过在 EAC 中检查数据库副本的“属性”页，可以查看某些配置信息。还可以使用命令行中的 [Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\)) 和 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298104\(v=exchg.150\)) cmdlet 来查看和配置数据库副本设置，如重播延迟时间、截断延迟时间和激活首选项顺序。有关如何查看和配置数据库副本设置的详细步骤，请参阅[配置邮箱数据库副本属性](configure-mailbox-database-copy-properties-exchange-2013-help.md)。

## 使用重播延迟和截断延迟选项

邮箱数据库副本支持使用“重播延迟时间”和“截断延迟时间”，这两个选项都是按分钟配置的。通过设置重播延迟时间，可以取回特定时间点的数据库副本。通过设置截断延迟时间，可以使用被动数据库副本上的日志来恢复在活动数据库副本上丢失的日志文件。因为这两个功能都会导致临时积累日志文件，所以使用其中任一功能都会影响存储设计。

## 重播延迟时间

重播延迟时间是邮箱数据库副本的属性，它以分钟为单位指定延迟数据库副本的日志重播。在日志文件复制到被动副本并成功通过检查之后，启动重播延迟计时器。通过延迟数据库副本日志重播，可以将数据库恢复到过去的某特定时间点。重播延迟时间配置为大于 0 的邮箱数据库副本称为*滞后邮箱数据库副本*，或简称为*滞后副本*。

在 Exchange 2013 中使用数据库副本和诉讼保留功能的策略可以针对通常会导致数据丢失的故障范围提供保护。但是，这些功能无法在发生逻辑损坏的情况下为数据丢失提供保护，尽管逻辑损坏的情况很少见，但它会导致数据丢失。滞后副本旨在发生逻辑损坏的情况下防止数据丢失。通常，有两种类型的逻辑损坏：

  - **数据库逻辑损坏** 数据库页校验和匹配，但页上的数据逻辑错误。当 ESE 尝试写入数据库页时，这种情况可能会发生，而且即使操作系统返回成功消息，也不能将数据写入磁盘或错误位置。这称为“丢失刷新”。若要防止丢失刷新丢失数据，ESE 在数据库中包括丢失刷新检测机制和页面修补功能（单页还原）。

  - **存储逻辑损坏** 以用户不希望的方式添加、删除或操作数据。这些情况通常都是由第三方应用程序引起的。通常在用户将其看作损坏时才认为是损坏的。Exchange 存储会考虑产生一系列有效 MAPI 操作的逻辑损坏的事务。Exchange 2013 中的诉讼保留功能提供针对存储逻辑损坏的防护（因为它可防止用户或应用程序永久删除内容）。但是在某些情况下，用户邮箱的损坏程度非常严重，以至于将数据库还原到损坏之前的时间点，然后导出用户邮箱以检索未损坏的数据会更加容易。

数据库副本、保留策略及 ESE 单页还原的组合可以仅留下少见但灾难性的存储逻辑损坏情况。是否使用具备重播延迟的数据库副本（滞后副本）将取决于所使用的第三方应用程序及组织的存储逻辑损坏的历史记录。

在特定情况下，滞后副本可以通过调用自动日志重播来减少日志文件，在 Exchange 2013 中进行自我管理：

  - 当达到磁盘空间不足阈值时

  - 当滞后副本发生物理损坏并且需要进行页面修补时

  - 当在超过 24 小时的时间内可用正常副本（仅主动或被动；不计入滞后数据库副本）少于三个时

可通过此自动减少功能对滞后副本进行页面修补。如果系统检测到滞后的副本需要页面修补，日志将自动重放到滞后副本以执行页面修补。当达到低磁盘空间阈值，以及检测到滞后副本在指定时间段内是唯一可用副本时，滞后的副本还将触发此自动重复功能。

滞后副本减少行为在默认情况下会被禁用，可以通过运行以下命令来启用。

```powershell
Set-DatabaseAvailabilityGroup <DAGName> -ReplayLagManagerEnabled $true
```

启用后，在少于三个副本时，会出现减少行为。可以通过修改以下 DWORD 注册表值来更改默认值 3。

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagManagerNumAvailableCopies**

若要针对磁盘空间不足阈值启用减少功能，必须对下列注册表项进行配置。

**HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters\\ReplayLagLowSpacePlaydownThresholdInMB**

在配置这些注册表设置的任何一个之后，重新启动 Microsoft Exchange DAG 管理服务以使更改生效。

例如，考虑这样一种环境，其中给定的数据库有 4 个副本（3 个为高可用副本，1 个为滞后副本），默认设置被用于 ReplayLagManagerNumAvailableCopies。如果非滞后副本由于某种原因（例如被挂起，等等）而停用，那么滞后副本会在 24 小时内自动减少其日志文件。

如果选择在不启用 `ReplayLagManagerEnabled` 参数的情况下使用滞后副本，请注意以下含义：

  - 重播延迟时间是管理员配置的值，默认情况下它是被禁用的。

  - 重播延迟时间设置的默认设置为 0 天，最大设置为 14 天。

  - 不应将滞后副本视为高可用副本。它们旨在从灾难中恢复，以防止出现存储逻辑损坏情况。

  - 设置的重播延迟时间越长，数据库恢复过程就越长。根据恢复期间需要重播的日志文件数以及硬件可以重播这些文件的速度，恢复数据库可能需要几小时或更长时间。

  - 我们建议您确定滞后副本是否对总体灾难恢复策略至关重要。如果它们的使用对您的策略至关重要，则我们建议使用多个滞后副本，或者使用独立磁盘 (RAID) 的冗余阵列保护单个滞后副本（如果没有多个滞后副本）。如果失去磁盘或出现损坏情况，则不会丢失滞后的时间点。

  - 使用 ESE 单页还原功能无法修补滞后副本。如果滞后副本发生数据库页损坏（例如 -1018 错误），则必须为其重新设定种子（这将丢失该副本的滞后内容）。

如果要数据库重播所有日志文件并使数据库副本当前可用，则很容易激活和恢复滞后的邮箱数据库副本。如果要重播截止到特定时间点的日志文件，操作将更加困难，因为您必须手动操作日志文件并运行 Exchange 服务器数据库实用程序 (Eseutil.exe)。

有关如何激活滞后邮箱数据库副本的详细步骤，请参阅[激活滞后的邮箱数据库副本](activate-a-lagged-mailbox-database-copy-exchange-2013-help.md)。

## 截断延迟时间

截断延迟时间是邮箱数据库副本的属性，它以分钟为单位指定在将日志文件重播到数据库副本后延迟删除数据库副本日志的时间量。在日志文件复制到被动副本、成功通过检查并成功重播到数据库副本之后，启动截断延迟计时器。通过从数据库副本延迟日志文件的截断，可以从影响数据库活动副本的日志文件的故障中恢复。

## 数据库副本和日志截断

日志截断在 Exchange 2013 中的功能与在 Exchange 2010 中一样。截断行为由副本的重播延迟时间和截断延迟时间决定。

当延迟设置保留其默认值 0（已禁用）时，必须满足以下条件才能截断数据库副本的日志文件：

  - 必须已成功备份日志文件，或者必须启用循环日志记录。

  - 日志文件必须在数据库检查点（恢复需要的最小日志文件）的下面。

  - 所有其他滞后副本必须检查该日志文件。

  - 所有其他副本（非滞后副本）必须重播在日志文件。

必须满足以下条件，才能对滞后数据库副本执行截断：

  - 在日志文件必须在数据库检查点的下面。

  - 日志文件必须早于 ReplayLagTime + TruncationLagTime。

  - 必须截断活动副本上的日志文件。

在 Exchange 2013 中，当一个或多个被动副本挂起时，活动邮箱数据库副本不会发生日志截断。如果计划维护活动将花很长时间（例如，几天时间），可能会累积大量的日志文件。为了防止事务日志填满日志驱动器，可以删除受影响的被动数据库副本，而不是将其挂起。当计划维护完成时，可以重新添加被动数据库副本。

Exchange 2013 Service Pack 1 (SP1) 引入了一种称为“松散截断”的功能，此功能默认是禁用的。在正常操作过程中，每个数据库副本都会保留需要传送到其他数据库副本的日志，直到数据库的所有副本均确认已重播（被动副本）或收到（延迟副本）日志文件。这是默认日志截断操作。如果数据库副本由于某些原因处于脱机状态，日志文件就会开始在数据库的其他副本使用的磁盘上堆积。如果受影响的数据库副本在较长时间内保持脱机状态，则可能会导致其他数据库副本用完磁盘空间。

启用宽松截断后，截断行为是不同的。每个数据库副本跟踪自己的可用磁盘空间，并在可用空间不足时应用宽松截断行为。对于主动副本，最旧的延迟副本（日志重播中远远落后的被动数据库副本）会遭到忽略，而截断会考虑剩余的最旧被动副本。活动数据库副本是计算全局截断的位置。被动副本会尝试考虑主动副本上的截断决定。无论 MinCopiesToProtect 名称的含义是什么，Exchange 都只会忽略截断运行时已知的最旧延迟副本。对于被动副本，如果空间不足，它会独立使用如下所述的配置参数截断自己的日志文件。

如果脱机数据库重新处于联机状态，将丢失从其他正常副本检测到的日志文件，其数据库副本状态将为 FailedAndSuspended。在这种情况下，如果配置了 Autoreseed，则会自动重新设定受影响的副本种子。如果未配置 Autoreseed，则将需要管理员手动设定数据库副本种子。

所需正常副本数量、可用磁盘空间阈值，以及要保留的日志数量均为可配置参数。默认情况下，可用磁盘空间阈值是 204800MB (200GB)，被动副本保留的日志数量为 100,000MB (100GB)，主动副本保留的日志数量为 10,000MB (10GB)。

通过编辑每个 DAG 成员的 Windows 注册表启用松散截断和配置松散截断参数。可以配置三个注册表值，均存储在 HKLM\\Software\\Microsoft\\ExchangeServer\\v15\\BackupInformation 下。默认情况下，BackupInformation 键及其下的 DWORD 值不存在，必须手动创建。BackupInformation 下的 DWORD 注册表值在下表中进行了说明：


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>注册表值</th>
<th>描述</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>LooseTruncation_MinCopiesToProtect</p></td>
<td><p>此键用于启用宽松截断。它代表在数据库的主动副本上的宽松截断中要保护的被动副本的数量。将此键的值设置为 0，禁用松散截断。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p>LooseTruncation_MinDiskFreeSpaceThresholdInMB</p></td>
<td><p>触发宽松截断的可用磁盘空间（以 MB 为单位）阈值。如果可用磁盘空间低于此值，就会触发松散截断。</p></td>
<td><p>如果没有配置此注册表值，则宽松截断使用的默认值是 200GB。</p></td>
</tr>
<tr class="odd">
<td><p>LooseTruncation_MinLogsToProtect</p></td>
<td><p>要在进行日志截断的正常副本上保留的日志文件的数量下限。如果配置了此注册表值，那么所配置的值适用于主动副本和被动副本。</p></td>
<td><p>如果没有配置此注册表值，则被动数据库副本使用的默认值是 100,000，主动数据库副本使用的默认值是 10,000。</p></td>
</tr>
</tbody>
</table>


使用 LooseTruncation\_MinLogsToProtect 注册表值时，请注意，主动和被动数据库副本的行为是不一样的。在主动数据库副本上，这是在受保护的被动副本和主动副本所需的范围之前就保留的额外日志数量。在被动数据库副本上，这是从最新可用日志保留的日志数量。此数量的 1/10 还用于在此被动副本的所需范围之前保留日志。这两个限制旨在确保延迟数据库副本不会占用太多空间，因为它们所需的范围通常非常大。

## 数据库激活策略

在某些情况下，您可能希望创建邮箱数据库副本，并阻止系统在出现故障的情况下自动激活该副本。例如：

  - 将一个或多个邮箱数据库副本部署到替换或备用数据中心时。

  - 配置滞后数据库副本以进行恢复时。

  - 正在执行服务器的维护或升级时。

在上述每种情况下，您都具有不希望系统自动激活的数据库副本。若要阻止系统自动激活邮箱数据库副本，您可以将该副本配置为阻止激活（挂起）。这允许系统通过日志传送和重播维护数据库的货币，但会阻止系统自动激活并使用该副本。阻止激活的副本必须由管理员手动激活。可以使用 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\)) cmdlet 为整个服务器配置数据库激活策略，或通过使用 [Set-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd298104\(v=exchg.150\)) cmdlet 将 *DatabaseCopyAutoActivationPolicy* 参数设置为 Blocked，为单个数据库副本配置数据库激活策略。

有关配置数据库激活策略的详细信息，请参阅[配置邮箱数据库副本的激活策略](configure-activation-policy-for-a-mailbox-database-copy-exchange-2013-help.md)。

## 邮箱移动对连续复制的影响

在日志生成率较高的非常繁忙的邮箱数据库上，如果对被动数据库副本的复制无法跟上日志生成，则更可能出现数据丢失。可能产生较高日志生成率的一种情况是邮箱移动。Exchange 2013 中包含一个数据保证 API。诸多服务（如 Microsoft Exchange 邮箱复制服务 (MRS)）使用此 API 并根据 *DataMoveReplicationConstraint* 参数的值（由系统或管理员设置）来检查数据库副本体系结构的运行状况。具体而言，数据保证 API 可以用于：

  - **检查复制运行状况** 确认是否有必备数量的数据库副本可用。

  - **检查复制刷新** 确认是否对必备数量的数据库副本重播了所需日志文件。

执行时，API 向调用应用程序返回以下状态信息：

  - **Retry** 表示存在阻止针对数据库检查某个条件的暂时性错误。

  - **Satisfied** 表示数据库满足所需条件或不复制数据库。

  - **NotSatisfied** 表示数据库不满足所需条件。此外，还会向调用应用程序提供有关为何返回“NotSatisfied”响应的信息。

邮箱数据库的 *DataMoveReplicationConstraint* 参数值确定应在请求中评估的数据库副本数。*DataMoveReplicationConstraint* 参数具有以下可能值：

  - `None` 创建邮箱数据库后，默认情况下会设置此值。设置此值时，会忽略数据保证 API 条件。只应将此设置用于不复制的邮箱数据库。

  - `SecondCopy` 这是在添加邮箱数据库的第二个副本时的默认值。设置此值时，必须至少有一个被动数据库副本满足数据保证 API 条件。

  - `SecondDatacenter` 设置此值时，另一个 Active Directory 站点中必须至少有一个被动数据库副本满足数据保证 API 条件。

  - `AllDatacenters` 设置此值时，每个 Active Directory 站点中必须至少有一个被动数据库副本满足数据保证 API 条件。

  - `AllCopies` 设置此值时，邮箱数据库的所有副本都必须满足数据保证 API 条件。

**检查复制运行状况**

当执行数据保证 API 以评估数据库副本基础结构的运行状况时，会评估几个项目。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果 <em>DataMoveReplicationConstraint</em> 参数设置为…</th>
<th>则对于给定数据库…</th>
<th>条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SecondCopy</code></p></td>
<td><p>复制的数据库的至少一个被动数据库副本必须满足下一列中的条件。</p></td>
<td><p>被动数据库副本必须：</p>
<ul>
<li><p>状况良好。</p></li>
<li><p>具有重播延迟时间在 10 分钟内的重播队列。</p></li>
<li><p>具有少于 10 个日志的复制队列长度。</p></li>
<li><p>具有少于 10 个日志的平均复制队列长度。平均复制队列长度基于应用程序查询数据库状态的次数进行计算。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SecondDatacenter</code></p></td>
<td><p>另一个 Active Directory 站点中的至少一个被动数据库副本必须满足下一列中的条件。</p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><code>AllDatacenters</code></p></td>
<td><p>必须装入主动副本，并且每个 Active Directory 站点中的一个被动副本必须满足下一列中的条件。</p></td>
<td></td>
</tr>
<tr class="even">
<td><p><code>AllCopies</code></p></td>
<td><p>必须装入主动副本，并且所有被动数据库副本都必须满足下一列中的条件。</p></td>
<td></td>
</tr>
</tbody>
</table>


**检查复制刷新**

数据保证 API 还可以用于验证是否有必备数量的数据库副本重播了所需事务日志。验证这一点的方法是将上个日志重播时间戳与调用服务的提交时间戳（在大多数情况下，这是包含所需数据的上一个日志文件的时间戳）加上额外五秒（用于处理系统时间时钟偏差或偏移）的时间进行比较。如果重播时间戳大于提交时间戳，则满足 *DataMoveReplicationConstraint* 参数。如果重播时间戳小于提交时间戳，则不满足 *DataMoveReplicationConstraint*。

在将大量邮箱移动到或移动自 DAG 中的复制数据库时，建议根据以下情况对每个邮箱数据库配置 *DataMoveReplicationConstraint* 参数：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果部署的是…</th>
<th>将 DataMoveReplicationConstraint 设置为…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>没有任何数据库副本的邮箱数据库</p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p>单个 Active Directory 站点中的 DAG</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="odd">
<td><p>使用扩展 Active Directory 站点的多个数据中心中的 DAG</p></td>
<td><p><code>SecondCopy</code></p></td>
</tr>
<tr class="even">
<td><p>跨两个 Active Directory 站点的 DAG，并且在每个站点中具有高可用数据库副本</p></td>
<td><p><code>SecondDatacenter</code></p></td>
</tr>
<tr class="odd">
<td><p>跨两个 Active Directory 站点的 DAG，并且在第二个站点中只有滞后数据库副本</p></td>
<td><p><code>SecondCopy</code></p>
<p>这是因为数据保证 API 不保证提交数据，直至将日志文件重播到数据库副本中，并且由于滞后数据库副本的性质，此约束会使移动请求失败，除非之后数据库副本 ReplayLagTime 值小于 30 分钟。</p></td>
</tr>
<tr class="even">
<td><p>跨三个或更多 Active Directory 站点的 DAG，并且每个站点都会包含高可用数据库副本</p></td>
<td><p><code>AllDatacenters</code></p></td>
</tr>
</tbody>
</table>


## 平衡数据库副本

由于 DAG 的固有性质，数据库切换和故障转移会导致活动邮箱数据库副本在 DAG 的生存期内多次更改主机。因此，DAG 在活动邮箱数据库副本分布方面可能变得不平衡。下表显示了一个主动数据库副本分布不平衡的 DAG 示例，该 DAG 具有四个数据库，每个数据库有四个副本（每个服务器上总共有 16 个数据库）。

### 主动副本分布不平衡的 DAG

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器</th>
<th>活动数据库的数量</th>
<th>被动数据库的数量</th>
<th>已装入数据库的数量</th>
<th>已卸除数据库的数量</th>
<th>首选项计数列表</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>5</p></td>
<td><p>11</p></td>
<td><p>5</p></td>
<td><p>0</p></td>
<td><p>4, 4, 3, 5</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 8, 6, 1</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>0</p></td>
<td><p>13, 2, 1, 0</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>1</p></td>
<td><p>15</p></td>
<td><p>1</p></td>
<td><p>0</p></td>
<td><p>1, 1, 5, 9</p></td>
</tr>
</tbody>
</table>


在上面的示例中，每个数据库有四个副本，因此激活首选项只有四个可能值（1、2、3 或 4）。“首选项计数列表”列显示与其中的每个值对应的数据库计数。例如，在 EX3 上，对于激活首选项 1 有 13 个数据库副本，对于激活首选项 2 有 2 个副本，对于激活首选项 3 有 1 个副本，对于激活首选项 4 没有副本。

如您所见，此 DAG 在每个 DAG 成员托管的活动数据库数、每个 DAG 成员托管的被动数据库数或托管数据库的激活首选项计数方面并不平衡。

可以使用 RedistributeActiveDatabases.ps1 脚本在 DAG 间平衡主动邮箱数据库副本。此脚本会使数据库在其副本之间进行移动，以尝试使 DAG 中每个服务器上装入的数据库数量相等。如有必要，该脚本还尝试在站点间平衡活动数据库。

该脚本为在 DAG 中平衡主动数据库副本提供了两种选项：

  - **BalanceDbsByActivationPreference**   指定此选项时，该脚本会尝试将数据库移动到其第一首选副本（基于激活首选项），而不考虑 Active Directory 站点。

  - **BalanceDbsBySiteAndActivationPreference**   指定此选项时，该脚本会尝试将活动数据库移动到其第一首选副本，同时还尝试在每个 Active Directory 站点中平衡活动数据库。

使用第一个选项运行该脚本之后，先前不平衡的 DAG 会达到平衡，如下表所示。

### 主动副本分布平衡的 DAG

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器</th>
<th>活动数据库的数量</th>
<th>被动数据库的数量</th>
<th>已装入数据库的数量</th>
<th>已卸除数据库的数量</th>
<th>首选项计数列表</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EX1</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX2</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="odd">
<td><p>EX3</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
<tr class="even">
<td><p>EX4</p></td>
<td><p>4</p></td>
<td><p>12</p></td>
<td><p>4</p></td>
<td><p>0</p></td>
<td><p>4, 4, 4, 4</p></td>
</tr>
</tbody>
</table>


如上表所示，现在此 DAG 在每个服务器上的活动数据库数和被动数据库数以及服务器间的激活首选项方面达到平衡。

下表列出了 RedistributeActiveDatabases.ps1 脚本的可用参数。

### RedistributeActiveDatabases.ps1 脚本参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>指定要重新平衡的 DAG 的名称。如果省略此参数，则会使用本地服务器所属的 DAG。</p></td>
</tr>
<tr class="even">
<td><p><em>BalanceDbsByActivationPreference</em></p></td>
<td><p>指定该脚本应将数据库移动到其第一首选副本，而不考虑 Active Directory 站点。</p></td>
</tr>
<tr class="odd">
<td><p><em>BalanceDbsBySiteAndActivationPreference</em></p></td>
<td><p>指定该脚本应尝试将活动数据库移动到其第一首选副本，同时还尝试在每个 Active Directory 站点中平衡活动数据库。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowFinalDatabaseDistribution</em></p></td>
<td><p>指定在重新分布完成后显示当前数据库分布的报告。</p></td>
</tr>
<tr class="odd">
<td><p><em>AllowedDeviationFromMeanPercentage</em></p></td>
<td><p>指定站点间活动数据库的允许变化率，以百分比形式表示。默认为 20%。例如，如果三个站点之间分布了 99 个数据库，则理想分布应是每个站点中包含 33 个数据库。如果允许变化率为 20%，则该脚本会尝试平衡数据库，以便每个站点包含的数据库数与此数字相比，上下不超过 10%。33 的 10% 是 3.3，向上舍入为 4。因此，该脚本会尝试使每个站点包含 29 至 37 个数据库。</p></td>
</tr>
<tr class="even">
<td><p><em>ShowDatabaseCurrentActives</em></p></td>
<td><p>指定该脚本为每个数据库生成一个报告，该报告详细说明数据库的移动方式以及它在其第一首选副本上现在是否处于活动状态。</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowDatabaseDistributionByServer</em></p></td>
<td><p>指定该脚本为每个服务器生成一个报告，该报告显示服务器的数据库分布。</p></td>
</tr>
<tr class="even">
<td><p><em>RunOnlyOnPAM</em></p></td>
<td><p>指定该脚本仅在当前具有 PAM 角色的 DAG 成员上运行。该脚本验证其是否从 PAM 运行。如果它不是从 PAM 运行，则该脚本会退出。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogEvents</em></p></td>
<td><p>指定该脚本记录事件（MsExchangeRepl 事件 4115），其中包含操作摘要。</p></td>
</tr>
<tr class="even">
<td><p><em>IncludeNonReplicatedDatabases</em></p></td>
<td><p>指定该脚本在确定如何重新分布活动数据库时应包括非复制数据库（没有副本的数据库）。虽然无法移动非复制数据库，但是这些数据库可能会影响复制数据库的分布。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>Confirm 开关可用于禁止显示确认提示，当运行此脚本时，会在默认情况下显示此确认提示。若要禁止显示确认提示，请使用语法 -Confirm:$False。您必须在语法中包含冒号 (:)。</p></td>
</tr>
</tbody>
</table>


## RedistributeActiveDatabases.ps1 示例

此示例演示某个 DAG 的当前数据库分布，包括首选项计数列表。

```powershell
  RedistributeActiveDatabases.ps1 -DagName DAG1 -ShowDatabaseDistributionByServer | Format-Table
```

此示例使用不提示进行输入的激活首选项在 DAG 中重新分布和平衡主动邮箱数据库副本。

```powershell
  RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -Confirm:$False
```

此示例使用激活首选项在 DAG 中重新分布和平衡活动邮箱数据库副本，并生成分布摘要。

  ```powershell
    RedistributeActiveDatabases.ps1 -DagName DAG1 -BalanceDbsByActivationPreference -ShowFinalDatabaseDistribution
  ```

## 监视数据库副本

如果发生影响数据库活动副本的故障，数据库副本是第一个防御措施。因此，若要确保数据库副本在需要时可用，则监视其运行状况和状态至关重要。可以通过在 EAC 中检查数据库副本的详细信息来查看各种信息，包括复制队列长度、重播队列长度、状态和内容索引状态信息。还可以使用命令行中的 **Get-MailboxDatabaseCopyStatus** cmdlet 来查看数据库副本的各种状态信息。

有关监视数据库副本的详细信息，请参阅[监视数据库可用性组](monitoring-database-availability-groups-exchange-2013-help.md)。

## 删除数据库副本

通过使用 EAC 或在命令行管理程序中使用 **Remove-MailboxDatabaseCopy** cmdlet 可以随时删除数据库副本。删除数据库副本之后，必须手动从删除数据库副本的服务器上删除任何数据库和事务日志文件。有关如何删除数据库副本的详细步骤，请参阅[删除邮箱数据库副本](remove-a-mailbox-database-copy-exchange-2013-help.md)。

## 数据库切换

承载数据库活动副本的邮箱服务器称为“邮箱数据库主机”。激活被动数据库副本的过程会更改数据库的邮箱数据库主机，并将被动副本转换为新的主动副本。此过程称为数据库切换。在数据库切换，在一个邮箱服务器上卸除数据库的活动副本，并该数据库的被动副本装入另一个邮箱服务器上的新活动邮箱数据库。执行切换时，可以选择覆盖新邮箱数据库主机上的数据库装入拨号设置。

通过检查 EAC 中的“数据库副本”选项卡下的右侧列，可以快速标识哪个邮箱服务器是当前邮箱数据库主机。通过在 EAC 中使用“激活”链接或在命令行管理程序中使用 **Move-ActiveMailboxDatabase** cmdlet 可以执行切换。

在激活被动副本之前，需执行几个内部检查：

  - 检查数据库副本的状态。如果数据库副本处于失败状态，则阻止切换。使用 **Move-ActiveMailboxDatabase** cmdlet 的 *SkipHealthChecks* 参数可以覆盖此行为并绕过运行状况检查。此参数允许在失败状态中将活动副本移动到数据库副本。

  - 将检查主动数据库副本以了解它当前是否为数据库的任何被动副本的种子设定源。如果主动副本当前用作种子设定源，则会阻止切换。使用 **Move-ActiveMailboxDatabase** cmdlet 的 *SkipActiveCopyChecks* 参数可以替代此行为并绕过种子设定源检查。此参数允许移动正用作种子设定源的主动副本。使用此参数会导致取消种子设定操作并将该操作视为失败。

  - 检查数据库副本的复制队列和重播队列长度，以确保它们的值符合已配置的条件。此外，还验证数据库副本，以确保当前未将其用作种子设定源。如果队列长度的值超出已配置的条件，或者数据库当前用作种子设定源，则阻止切换。使用 **Move-ActiveMailboxDatabase** cmdlet 的 *SkipLagChecks* 参数可以覆盖此行为并绕过这些检查。此参数允许要激活的副本具有超出已配置条件的重播队列和复制队列。

  - 检查数据库副本的搜索目录（内容索引）的状态。如果搜索目录不是最新的且运行状况不正常或已损坏，则阻止切换。使用 **Move-ActiveMailboxDatabase** cmdlet 的 *SkipClientExperienceChecks* 参数可以覆盖此行为并绕过搜索目录检查。此参数将导致搜索跳过目录运行状况检查。如果正在激活的数据库副本的搜索目录处于不正常运行状况或不可用状态，并且使用此参数跳过目录运行状况检查和激活数据库副本，则需要重新对搜索目录进行爬网或设定种子。

执行数据库切换时，还可以覆盖装入拨号设置，这些设置是为承载正在激活的被动数据库副本的服务器而配置的。使用 **Move-ActiveMailboxDatabase** cmdlet 的 *MountDialOverride* 参数指示目标服务器覆盖自己的装入拨号设置，并且使用这些由 *MountDialOverride* 参数指定的设置。

有关如何执行数据库副本切换的详细步骤，请参阅[激活邮箱数据库副本](activate-a-mailbox-database-copy-exchange-2013-help.md)。

