---
title: '使用 Windows 服务器备份来备份和还原 Exchange 数据: Exchange 2013 Help'
TOCTitle: 使用 Windows 服务器备份来备份和还原 Exchange 数据
ms:assetid: 0fac891a-5713-42b6-afd5-c91b2b88f966
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876851(v=EXCHG.150)
ms:contentKeyID: 50489922
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 使用 Windows 服务器备份来备份和还原 Exchange 数据

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

Microsoft 的[首选体系结构](https://blogs.technet.com/b/exchange/archive/2014/04/21/the-preferred-architecture.aspx)的Exchange Server 2013利用了称为Exchange本机数据保护的概念。Exchange本机数据保护依赖本机Exchange功能来保护您的邮箱数据，而无需使用传统的备份。但如果您想要创建的备份，包括插件Windows Server备份 (WSB) 使您能够创建 Exchange 的基于卷影复制服务 VSS 备份Exchange数据的Exchange 。若要支持 Exchange 的备份，您必须安装 WSB 功能。

插件 WSBExchange.exe 作为名为\&quot;Microsoft Exchange Server Extension for Windows Server Backup\&quot;（此服务的简称是 WSBExchange）的服务运行。该服务会在所有邮箱服务器上自动安装并配置为手动启动。该插件使 WSB 能够创建 Exchange 感知的 VSS 备份。

使用 WSB 来备份 Exchange 数据之前，建议您先熟悉一下此插件的以下功能和选项：

  - 使用 WSB 进行的备份发生在卷级别，并且执行应用程序级别备份和还原的唯一方式是选择整个卷。要备份数据库及其日志流，您必须备份包含数据库和日志在内的整个卷，而不仅仅是某个文件夹。如果不备份包含该数据的整个卷，就无法备份任何数据。

  - 必须在正在备份的服务器上以本地方式运行备份，并且无法使用此插件进行远程 VSS 备份。不提供 WSB 或此插件的远程管理。但是可以使用远程桌面服务或终端服务远程管理备份。

  - 可以在本地驱动器或远程网络共享上创建备份。

  - 只应该执行完整备份。仅在包含 Exchange 数据库的卷或文件夹的 VSS 完整备份成功完成后，才会发生日志截断。

  - 还原数据时，可以只还原 Exchange 数据。此数据可以还原到其原始位置或备用位置。如果将数据还原到其原始位置，WSB 和插件将自动处理恢复过程，包括卸载任何现有数据库并将日志重播到已恢复的数据库中。

  - 还原过程不支持 Exchange 恢复数据库 (RDB)。如果要使用 RDB，您必须将数据还原到备用位置，然后手动将已还原的数据从该位置复制或移动到 RDB 文件夹结构。

  - 还原 Exchange 数据时，所有备份的数据库都必须一起还原。不能还原单个数据库。

  - 使用 WSB 时支持裸机还原；但是，对于 Exchange 服务器，建议的恢复方法是恢复 Exchange 服务器，然后还原数据。如果您正在使用第三方备份应用程序（例如非 Microsoft），则您的备份应用程序供应商可能会提供 Exchange 裸机还原支持。

下表描述了可用于包含 WSB 的 Exchange 2013 的备份和恢复选项的可支持性。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您...</th>
<th>则执行...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>备份完整服务器...</p></td>
<td><p>将执行 VSS 副本备份，并且服务器上的数据库事务日志不会发生截断。</p></td>
</tr>
<tr class="even">
<td><p>执行自定义备份，然后选择要备份的一个或多个卷...</p></td>
<td><p>可以选择 VSS 完整备份，允许选定卷上的数据库的事务日志在成功备份完成时发生截断。</p></td>
</tr>
<tr class="odd">
<td><p>执行自定义备份，然后选择要备份的一个或多个文件夹...</p></td>
<td><p>可以选择 VSS 完整备份，日志文件将发生截断；但是，备份的还原将会限制在文件还原范围内，作为应用程序级别的还原将不作为选项可用。</p></td>
</tr>
</tbody>
</table>


有关使用 WSB 备份 Exchange 的详细步骤，请参阅[使用 Windows 服务器备份来备份 Exchange](use-windows-server-backup-to-back-up-exchange-exchange-2013-help.md)。

有关从使用 WSB 备份中还原数据的详细步骤，请参阅[使用 Windows Server 备份还原 Exchange 的备份](use-windows-server-backup-to-restore-a-backup-of-exchange-exchange-2013-help.md)。

