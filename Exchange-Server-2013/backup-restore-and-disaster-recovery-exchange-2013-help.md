---
title: '备份、还原和灾难恢复: Exchange 2013 Help'
TOCTitle: 备份、还原和灾难恢复
ms:assetid: 394fc4ed-fa02-41fa-9159-cc2754ff8875
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876874(v=EXCHG.150)
ms:contentKeyID: 50490325
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 备份、还原和灾难恢复

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

作为数据保护规划的一部分，了解如何保护数据以及确定最适合组织需求的方法十分重要。数据保护规划是一个复杂的过程，它依赖于在部署的规划阶段所做出的很多决策。

通常情况下，备份用于以下情况：

  - **灾难恢复**   如果硬件或软件发生故障，则 DAG 中的多个数据库副本可通过快速故障转移实现高可用性，且不会丢失数据。这样可以省去停机时间，并且可以避免由于从过去某个时间点备份恢复到磁盘或磁带需要大量成本而导致的生产率降低。DAG 可扩展到多个站点，并且可以针对磁盘、服务器、网络和数据中心故障提供弹性。

  - **意外删除项目的恢复**   一直以来，在用户删除了项目但需将其恢复的情况下，都会涉及到查找存储需要恢复的数据的备份媒体，然后以某种方式获取所需项目并将其提供给用户。使用 Exchange 2013 中新的“可恢复项目”文件夹以及适用于此文件夹的保留策略，可在指定的时间段内保留所有删除和修改的数据，因此，恢复这些项目既方便又快捷。这通过帮助最终用户恢复他们自己意外删除的项目来减轻 Exchange 管理员和 IT 技术支持的负担，从而降低了与单个项目恢复相关的复杂程度和管理成本。有关详细信息，请参阅[邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md)和[数据丢失预防](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)。

  - **长期数据存储**   备份也会被用作存档，并且由于受到遵从性要求的约束，通常将磁带用于在更长的一段时间内保留数据的时间点快照。Exchange 2013 中的新存档、多邮箱搜索和邮件保留功能提供了一种机制，可在更长的一段时间内有效地保留数据并使最终用户可以访问。这消除了从磁带恢复的高昂成本，提高了生产率。有关详细信息，请参阅[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)、[就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)和[就地保留和诉讼保留](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-and-litigation-holds)。

  - **时间点数据库快照**   如果组织需要邮箱数据某个过去时间点的副本，则 Exchange 可在 DAG 环境中创建滞后数据库副本。此功能对于某种少见事件会有所用处，即逻辑损坏在 DAG 中复制到多个数据库副本中，从而导致需要返回到前一时间点。如果管理员意外删除了邮箱或用户数据，此功能也非常有用。从滞后副本恢复可能比从备份还原更快，因为滞后副本不需要从备份服务器到 Exchange 服务器的耗时复制过程。此功能可通过缩短停机时间显著降低总拥有成本。

因为有高效经济的本地 Exchange 2013 功能来应付这些情况，您可以减少或避免在您的环境中使用传统备份。

Exchange 本机数据保护

支持的备份技术

Exchange 2013 VSS 书写器

Exchange Server Recovery

统一联系人存储恢复

恢复数据库

数据库可移植性

拨号音可移植性

## Exchange 本机数据保护

适用于 Exchange Server 2013 的 Microsoft [首选体系结构](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx)使用称为 Exchange 本机数据保护的概念。Exchange 本地数据保护依赖于内置的 Exchange 功能来保护您的邮箱数据，而无需使用备份（尽管您仍可以使用那些功能以及创建备份）。Exchange 2013 包含了一些新功能和核心更改，一旦正确部署和配置，即可提供本地数据保护，而无需对您的数据进行传统备份。使用 Exchange 2013 内置的高可用性功能，可以在发生灾难时最大限度地减少停机时间和数据丢失，还可以减少邮件系统的总拥有成本。通过将这些功能与其他内置功能（如合法保留）组合在一起，您可以减少或避免使用传统时间点备份，并降低相关成本。

除确定 Exchange 2013 是否能够脱离传统时间点备份外，我们还建议您评估当前备份基础结构的成本。尝试使用现有备份基础结构从灾难中恢复时，考虑最终用户停机和数据损失的成本。还包括硬件、安装和许可成本，以及与恢复数据和维护备份相关的管理成本。具有至少三个邮箱数据库副本的纯 Exchange 2013 环境所需的总拥有成本很可能比具有备份的环境低，具体取决于组织的需求。

对于作为传统备份的替代而内置于 Exchange 2013 中的这些功能，在使用之前，您应该考虑一些问题。可能也有对您的组织所特有的考虑。请考虑下列问题，但请注意，这不是一个详尽的列表：

  - 您应该确定需要部署多少个数据库副本。我们强烈建议在取消对数据库的传统形式的保护（如独立磁盘冗余阵列 (RAID) 或传统的基于 VSS 的备份）之前，至少应部署三个（非滞后）邮箱数据库副本。

  - 应明确定义您的恢复时间目标和恢复点目标，并且应使用代替传统备份的内置功能组合集进行创建以实现这些目标。

  - 您应该确定每个数据库需要多少个副本，以应对系统将提供保护的各种故障情形。

  - 您应该确定，如果不使用 DAG 或者其部分成员，是否可以获得足够的成本来支持传统的备份解决方案。如果是，则应该确定，此解决方案是否可以改进恢复时间目标或恢复点目标服务级别协议 (SLA)。

  - 您应该确定，如果托管副本的 DAG 成员遇到影响副本或副本完整性的故障，您是否可以承受丢失时间点副本。

  - Exchange 2013 允许您部署更大的邮箱，但建议邮箱数据库最大不超过 2 TB（当使用两个或更多高可用性邮箱数据库副本时）。如果激活数据库副本或滞后数据库副本时必须重播大量的日志记录文件，则您应该确定，基于大多数组织可能会部署的更大邮箱，您的恢复点目标是什么。

  - 您应该确定如何检测和防止主动数据库副本中的逻辑损坏复制到被动数据库副本中。这包括确定这种情况下的恢复计划以及过去出现这种情况的频率。如果您的组织中经常发生逻辑损坏，我们建议您在设计中考虑此情况时使用一个或多个滞后副本，通过足够的重播延迟窗口，您可以在逻辑损坏已经发生但是尚未复制到其他数据库副本时对其进行检测和处理。

在成功的完整备份或增量备份结束时所执行的功能之一是截断数据库恢复不再需要的事务日志文件。如果没有进行备份，则不会发生日志截断的情况。要防止累积日志文件，请为复制的数据库启用循环日志记录。如果将循环日志记录和连续复制组合使用，则会产生被称为连续复制循环日志记录 (CRCL) 的新型循环日志记录，连续复制循环日志记录与可扩展存储引擎 (ESE) 循环日志记录不同。ESE 循环日志记录由 Microsoft Exchange 信息存储服务执行和管理，而 CRCL 由 Microsoft Exchange 复制服务执行和管理。启用 ESE 循环日志记录时，并不会另外生成日志文件，而需要时会覆盖当前日志文件。但是，在连续复制环境中，需要使用日志文件进行日志传送和重播。因此，启用 CRCL 时，不会覆盖当前的日志文件，并且会生成用于日志传送和重播过程的已关闭的日志文件。

具体而言，Microsoft Exchange 复制服务管理 CRCL 以维持日志连续性，当仍然需要日志进行复制时，不会删除这些日志。Microsoft Exchange 复制服务和 Microsoft Exchange 信息存储服务使用与可以删除的日志文件有关的远程过程调用 (RPC) 进行通信。

若要在高可用（非滞后）邮箱数据库副本上进行截断，以下情况都必须为“真”：

  - 备份了日志文件，或启用了 CRCL。

  - 日志文件在检查点的下方。

  - 数据库的其他非滞后副本同意删除。

  - 数据库的所有滞后副本都检查了日志文件。

若要在滞后数据库副本上进行截断，以下情况都必须为“真”：

  - 日志文件在检查点的下方。

  - 日志文件比 ReplayLagTime + TruncationLagTime 更旧。

  - 在数据库的主动副本上删除了日志文件。

Exchange 本机数据保护

## 支持的备份技术

Exchange 2013 只支持基于 VSS 的 Exchange 可感知备份。Exchange 2013 包括一个 Windows Server 备份插件，使您能创建和还原 Exchange 数据的基于 VSS 的备份。要备份和还原 Exchange 2013，必须使用支持 Exchange 2013 的 VSS 书写器的 Exchange 感知应用程序，如 Windows Server 备份工具（带有 VSS 插件）、Microsoft System Center 2012 数据保护管理器，或基于 VSS 的第三方 Exchange 感知应用程序。

有关使用 Exchange 备份来备份和还原 Windows Server 数据的详细步骤，请参阅[使用 Windows 服务器备份来备份和还原 Exchange 数据](using-windows-server-backup-to-back-up-and-restore-exchange-data-exchange-2013-help.md)。

Exchange 本机数据保护

## Exchange 2013 VSS 书写器

与 Exchange 2010 和 Exchange 2007 中使用的 VSS 书写器相比，Exchange 2013 中的 VSS 书写器架构有了显著变化。这些较早的 Exchange 版本包含两个 VSS 书写器：一个位于 Microsoft Exchange Information Store 服务 (store.exe) 内，另一个位于 Microsoft Exchange Replication 服务 (msexchangerepl.exe) 内。在 Exchange 中，之前位于 Microsoft Exchange Information Store 服务内的 VSS 书写器功能已移至 Microsoft Exchange Replication 服务。新的书写器名为 Microsoft Exchange Writer，现在基于 VSS 的 Exchange 感知应用程序使用它来备份主动和被动数据库副本，以及还原已备份的数据库副本。虽然新书写器运行在 Microsoft Exchange 复制服务中，但仍需要 Microsoft Exchange 信息存储服务保持运行状态，以便书写器可以进行播发。因此，为了能够备份或还原 Exchange 数据库，这两项服务都是必需的。

Exchange 本机数据保护

## Exchange Server Recovery

邮箱服务器和客户端访问服务器的几乎所有配置设置都存储在 Active Directory 中。和 Exchange 以前的版本一样，Exchange 2013 也包括用于恢复丢失服务器的安装程序参数。此参数 */m:RecoverServer* 用于通过使用存储在 Active Directory 中的设置和配置信息来重建和重新创建丢失服务器。但是，请注意一些设置不会被还原，如对本地 web.config 文件和其他配置文件所作的更改。此外，自定义的注册表条目也不会还原。我们建议使用可靠的更改管理过程来跟踪和重新创建这些更改。

有关如何对丢失的 Exchange 2013 服务器执行服务器恢复的详细步骤，请参阅[恢复 Exchange 服务器](recover-an-exchange-server-exchange-2013-help.md)。有关如何对丢失的服务器（数据库可用性组成员 (DAG)）执行恢复的详细步骤，请参阅[恢复数据库可用性组成员服务器](recover-a-database-availability-group-member-server-exchange-2013-help.md)。

Exchange 本机数据保护

## 统一联系人存储恢复

当 Exchange 2013 环境中使用了 Microsoft Lync Server 2013 时，用户的 Lync 联系人信息存储在用户邮箱内的一个特殊联系人文件夹中。这称为统一联系人存储 (UCS)。如果您还原某个迁移了 UCS 的邮箱，目标用户的即时消息联系人列表可能受到影响。如果在最后一次备份后对用户进行了迁移，则还原邮箱将导致用户的联系人列表完全丢失。在不太严重的情况下，用户自最后一次备份起对联系人列表所做的修改将会丢失。要减轻这种潜在的数据丢失风险，请确保在还原邮箱之前将用户迁移回即时消息服务器。

Exchange 本机数据保护

## 恢复数据库

恢复数据库是一种特殊的邮箱数据库，您可以通过它装入还原的邮箱数据库，并且可以在恢复操作中从还原的数据库提取数据。您可以使用 [New-MailboxRestoreRequest](https://technet.microsoft.com/zh-cn/library/ff829875\(v=exchg.150\)) cmdlet 从恢复数据库提取数据。提取后，可将数据导出到一个文件夹或者合并到一个现有邮箱中。恢复数据库使您能够从备份或数据库副本中恢复数据，而不会干扰用户对当前数据的访问。

不支持对任何以前版本的 Exchange 的邮箱数据库使用恢复数据库。此外，用于数据合并和提取的目标邮箱必须与恢复数据库中装入的数据库位于同一个 Active Directory 林。

有关详细信息，请参阅[恢复数据库](recovery-databases-exchange-2013-help.md)。有关如何创建恢复数据库的详细步骤，请参阅[创建恢复数据库](create-a-recovery-database-exchange-2013-help.md)。有关如何使用恢复数据库的详细步骤，请参阅[使用恢复数据库还原数据](restore-data-using-a-recovery-database-exchange-2013-help.md)。

Exchange 本机数据保护

## 数据库可移植性

数据库可移植性是使 Exchange 2013 邮箱数据库移动到并装入同一组织中的任何其他 Exchange 2013 邮箱服务器的功能。通过使用数据库可移植性，可以免除恢复过程中容易导致错误的多个手动步骤，从而提高可靠性。此外，数据库可移植性可减少各种故障情况的总恢复时间。

有关详细信息，请参阅[数据库可移植性](database-portability-exchange-2013-help.md)。有关使用数据库可移植性的详细步骤，请参阅[使用数据库可移植性移动邮箱数据库](move-a-mailbox-database-using-database-portability-exchange-2013-help.md)。

Exchange 本机数据保护

## 拨号音可移植性

拨号音可移植性功能可针对影响邮箱数据库、服务器或整个站点的故障提供有限的业务连续性解决方案。通过拨号音可移植性，用户可以在原始邮箱还原或修复的过程中使用一个临时邮箱来发送和接收电子邮件。该临时邮箱可以位于同一个 Exchange 2013 邮箱服务器上，也可以位于组织中的任何其他 Exchange 2013 邮箱服务器上。这样备用服务器可以存放之前位于不再可用的服务器上的用户邮箱。支持自动发现的客户端（如 Microsoft Outlook）将被自动重定向到新服务器，而不必手动更新用户的桌面配置文件。在还原用户的原始邮箱数据后，管理员可以将用户的已恢复邮箱和用户的拨号音邮箱合并成一个最新的邮箱。

使用拨号音可移植性的过程称为“拨号音恢复”。拨号音恢复需要在邮箱服务器上创建一个空数据库来替换故障数据库。通过此空数据库（称为“拨号音数据库”），用户可在恢复故障数据库的同时发送和接收电子邮件。恢复故障数据库之后，会将拨号音数据库和所恢复的数据库进行交换，然后将来自拨号音数据库的数据合并到所恢复的数据库中。

有关详细信息，请参阅[拨号音可移植性](dial-tone-portability-exchange-2013-help.md)。有关执行拨号音恢复的详细步骤，请参阅[执行拨号音恢复](perform-a-dial-tone-recovery-exchange-2013-help.md)。

Exchange 本机数据保护

