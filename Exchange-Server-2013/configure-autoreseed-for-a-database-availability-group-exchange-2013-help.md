---
title: '为数据库可用性组配置 AutoReseed: Exchange 2013 Help'
TOCTitle: 为数据库可用性组配置 AutoReseed
ms:assetid: 4a8bd779-b52a-40ed-8040-4d76eabeb41e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ619303(v=EXCHG.150)
ms:contentKeyID: 50490479
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为数据库可用性组配置 AutoReseed

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-04-15_

借助自动重新设定种子功能，可在发生磁盘故障后快速还原数据库冗余。如果某个磁盘出现故障，那么该磁盘上存储的数据库副本会自动重新设定种子到邮箱服务器上预配置的备用磁盘。可按本主题中介绍的步骤操作，为数据库可用性组 (DAG) 配置自动重新设定种子。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>自动重新设定种子功能不会为你执行任何先决条件配置任务。手动正确安装磁盘、向系统添加备用磁盘、更换故障磁盘以及格式化新磁盘必须都由管理员完成。</td>
</tr>
</tbody>
</table>


有关 DAG 的更多管理任务，请参阅[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的\&quot;数据库可用性组\&quot;条目。

  - 必须创建每个物理磁盘的单个逻辑磁盘/分区。

  - 必须使用以下步骤中描述的特定数据库和日志文件夹结构。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您该如何做？

## 第 1 步：为数据库和卷配置根路径

第 1 步包括为数据库 (*AutoDagDatabasesRootFolderPath*) 和 DAG 使用的卷 (*AutoDagVolumesRootFolderPath*) 配置根目录。默认路径分别是 C:\\ExchangeDatabases 和 C:\\ExchangeVolumes。如果要使用默认路径，可以略去这一步。

下列示例说明了如何配置数据库的根路径。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabasesRootFolderPath "C:\ExchDbs"

下列示例说明了如何配置存储卷的根路径。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagVolumesRootFolderPath "C:\ExchVols"

## 您如何知道此步骤有效？

若要验证是否已成功配置数据库和卷的根路径，请运行以下命令。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabasesRootFolderPath* 和 *AutoDagVolumesRootFolderPath* 的输出应反映已配置的路径。

## 第 2 步：逐卷配置数据库数量

下一步，为 DAG 配置每个卷的数据库数量 (*AutoDagDatabaseCopiesPerVolume*)。

本示例说明了如何为每个卷配置了 4 个数据库的 DAG 配置此自动种子重新设定设置。

    Set-DatabaseAvailabilityGroup DAG1 -AutoDagDatabaseCopiesPerVolume 4

## 您如何知道此步骤有效？

要验证是否已成功配置每个卷的数据库数量，请运行以下命令。

    Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

*AutoDagDatabaseCopiesPerVolume* 的输出应反映已配置的值。

## 第 3 步：为数据库和卷创建根目录

下一步，创建与步骤 1 中配置的根目录相对应的目录。本示例显示了如何使用命令提示符创建默认目录。

    md C:\ExchangeDatabases
    md C:\ExchangeVolumes

## 您如何知道此步骤有效？

若要验证是否已成功配置数据库和卷的根目录，请运行以下命令。

    Dir C:\

创建的目录应出现在输出列表中。

## 第 4 步：装载卷文件夹

对于要对数据库使用的每个卷（包括备用卷），使用 Windows 磁盘管理应用程序 (diskmgmt.msc) 将每个卷装载到 C:\\ExchangeVolumes\\ 下的已装载文件夹中。例如，如果有 2 个卷包含数据库，还有 1 个备用卷，请将这些卷装载到下列已装载文件夹中：

  - C:\\ExchangeVolumes\\Volume1

  - C:\\ExchangeVolumes\\Volume2

  - C:\\ExchangeVolumes\\Volume3

已装入文件夹的名称可以是任意文件夹名称，只要将文件夹装入根卷路径下即可。

## 您如何知道此步骤有效？

要验证是否已成功装入卷文件夹，请运行以下命令。

    Dir C:\

装入的卷应出现在输出列表中。

## 第 5 步：创建数据库文件夹

下一步，在根路径 C:\\ExchangeDatabases 下创建数据库目录。此示例展示了如何针对每个卷上有 4 个数据库的存储配置创建目录。

    md c:\ExchangeDatabases\db001

    md c:\ExchangeDatabases\db002

    md c:\ExchangeDatabases\db003

    md c:\ExchangeDatabases\db004

## 您如何知道此步骤有效？

要验证是否已成功装入数据库文件夹，请运行以下命令。

    Dir C:\ExchangeDatabases

创建的目录应出现在输出列表中。

## 第 6 步：创建数据库装载点

为每个数据库创建装载点，然后将装载点链接到正确的卷。例如，db001 的已装载文件夹应位于 C:\\ExchangeDatabases\\db001。可以使用 diskmgmt.msc 或 mountvol.exe 执行此操作。此示例展示了如何使用 mountvol.exe 将 db001 装载到 C:\\ExchangeDatabases\\db001。

    Mountvol.exe c:\ExchangeDatabases\db001 \\?\Volume (GUID)

## 您如何知道此步骤有效？

要验证是否已成功创建数据库装入点，请运行以下命令。

    Mountvol.exe C:\ExchangeDatabases\db001 /L

已装入的卷应出现在装载点列表中。

## 第 7 步：创建数据库目录结构

接下来，在第 5 步中创建的文件夹下创建两个目录，一个用于装载各个数据库，另一个用于装载存储在同一卷中的各个数据库日志流。目录结构必须采用以下格式：

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.db

C:\\\< *DatabaseFolderName*\>\\*DatabaseName*\\\<*DatabaseName*\>.log

本示例说明了如何为即将存储在卷 1 中的 4 个数据库创建目录：

    md c:\ExchangeDatabases\db001\db001.db

    md c:\ExchangeDatabases\db001\db001.log

    md c:\ExchangeDatabases\db002\db002.db

    md c:\ExchangeDatabases\db002\db002.log

    md c:\ExchangeDatabases\db003\db003.db

    md c:\ExchangeDatabases\db003\db003.log

    md c:\ExchangeDatabases\db004\db004.db

    md c:\ExchangeDatabases\db004\db004.log

对每个卷中的数据库重复上述命令。

## 您如何知道此步骤有效？

要验证是否已成功创建数据库目录结构，请运行以下命令。

    Dir C:\ExchangeDatabases /s

创建的目录应出现在输出列表中。

## 第 8 步：创建数据库

创建数据库，其日志和数据库路径已通过相应的文件夹进行配置。此示例展示了如何创建存储在新建的目录和装载点结构中的数据库。

    New-MailboxDatabase -Name db001 -Server MBX1 -LogFolderPath C:\ExchangeDatabases\db001\db001.log -EdbFilePath C:\ExchangeDatabases\db001\db001.db\db001.edb

## 您如何知道此步骤有效？

要验证是否已成功在相应的文件夹中创建数据库，请运行以下命令。

    Get-MailboxDatabase db001 | Format List *path*

返回的数据库属性应指示数据库文件和日志文件正存储在上述文件夹中。

## 您如何知道此任务有效？

要验证是否已为 DAG 成功配置自动种子重新设定，请执行以下操作：

1.  运行以下命令来验证 DAG 配置是否正确。
    
        Get-DatabaseAvailabilityGroup DAG1 | Format-List *auto*

2.  运行以下命令来验证目录结构配置是否正确（下面是默认路径，如果有必要，将这些路径替换为您正在使用的路径）。
    
        Dir c:\ExchangeDatabases /s
    
        Dir c:\ExchangeVolumes /s

