---
title: 'AutoReseed: Exchange 2013 Help'
TOCTitle: AutoReseed
ms:assetid: 61f9a8be-070e-4c62-b505-52644fcff0c5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn789209(v=EXCHG.150)
ms:contentKeyID: 62523839
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# AutoReseed

 

_**适用于：** Exchange Server 2013 SP1_

_**上一次修改主题：** 2015-03-09_

自动重新设定种子（即 AutoReseed）是通常是由管理员驱动的响应磁盘故障、数据库崩溃或其他必需重新为数据库副本设定种子的问题的而进行的操作的替代功能。AutoReseed 旨在当磁盘故障发生后通过使用系统提供的备用磁盘自动还原数据库冗余。

## Autoreseed 概述

在 Autoreseed 配置中，使用标准存储呈现结构，并由管理员选择起点。AutoReseed 是为了在驱动器出现故障之后尽快还原冗余。这涉及使用装入点预映射一组卷（包括备用卷）和数据库。对于磁盘不再可供操作系统使用或不再可写的磁盘故障，系统会分配备用卷，并会自动对受影响的数据库副本进行种子重新设定。

1.  Microsoft Exchange 复制服务定期扫描是否存在状态为 FailedAndSuspended 的副本。如果为 AutoReseed 配置的卷上的所有数据库副本连续 15 分钟处于 FailedandSuspended 状态，则启动 AutoReseed 工作流。

2.  AutoReseed 至多会进行进行 3 次尝试，以恢复失败和挂起的副本，每次尝试间隔 5 分钟。有时，恢复 FailedandSuspended 数据库副本后，该副本仍处于\&quot;Failed\&quot;状态。出现这种情况的原因有多种，因此此步骤旨在处理这些情况；AutoReseed 将自动挂起已连续 10 分钟处于\&quot;Failed\&quot;状态的数据库副本，以确保工作流继续运行。如果挂起和恢复操作并未产生正常的数据库副本，则该工作流继续运行。

3.  当其发现某个副本处于该状态时，则其会执行某些先决条件检查。例如，它将验证备用磁盘是否可用，验证数据库及其日志文件是否配置在相同的卷上，以及所在的适当位置是否符合要求的命名约定。

4.  如果成功通过先决条件检查，Microsoft Exchange Replication 服务中的 Disk Reclaimer 功能会根据下表中的日程表分配、重映射和格式化空闲磁盘。AutoReseed 将至多进行 5 次分配备用卷的尝试，每次尝试间隔 1 小时。

5.  分配备用卷后，AutoReseed 将通过 SafeDeleteExistingFiles 种子设定开关执行 InPlaceSeed 操作。通过将数据库的主动副本作为种子源对受影响的磁盘上的所有数据库重新设定种子。

6.  在设定种子操作完成后，Microsoft Exchange Replication 服务验证重新定义种子后的副本处于正常状态。

用完所有重试次数后，工作流停止运行。3 天后，如果数据库副本仍处于 FailedandSuspended 状态，则重置工作流并且从步骤 1 重新开始。此重置/恢复行为非常有用（且有针对性），因为它可以花费几天时间来复制故障磁盘、控制器等。

此时，如果故障是磁盘故障，就需要操作员或管理员手动介入移除和替换故障磁盘并将替换磁盘重新配置为备用。

AutoReseed 通过使用 DAG 的三个属性进行配置。其中两个属性指使用的两个装入点。Exchange 2013 利用了 Windows Server 允许每个卷具有多个装入点这一情况。*AutoDagVolumesRootFolderPath* 属性指包含所有可用卷的装入点。这包括托管数据库的卷和备用卷。*AutoDagDatabasesRootFolderPath* 属性指包含数据库的装入点。第三个 DAG 属性 *AutoDagDatabaseCopiesPerVolume* 用于配置每个卷的数据库副本数。

下面说明了 AutoReseed 配置示例。

**AutoReseed 配置示例**

![自动重新设定种子配置示例](images/Dn789209.e3af7306-f5b4-4ec4-9ccf-222ec452699b(EXCHG.150).gif "自动重新设定种子配置示例")

在此示例中，有三个卷，其中两个卷包含数据库（VOL1 和 VOL2），另一个卷为空白的格式化备用卷 (VOL3)。

配置 AutoReseed：

1.  所有三个卷都在单个装入点下装入。在此示例中，使用了装入点 C:\\ExchVols。这表示用于获取 Exchange 数据库存储的目录。

2.  系统会将邮箱数据库的根目录作为另一个装入点进行装入。在此示例中，使用装入点 C:\\ExchDBs。接下来，创建目录结构，以便为数据库创建父目录，并在父目录下创建两个子目录：一个用于存储数据库文件，一个用于存储日志文件。

3.  数据库即被创建。上面的示例说明了对每个卷使用单个数据库的简单设计。因此，在 VOL1 上有三个目录：一个父目录和两个子目录（一个用于存储 MDB1 的数据库文件，一个用于存储其日志）。虽然示例图像中没有指明，但在 VOL2 上也存在三个目录：一个父目录，在该目录下有两个目录，一个用于存储 MDB2 的数据库文件，一个用于存储其日志文件。

在此配置中，如果 MDB1 或 MDB2 出现故障，则故障数据库的副本将重新自动设定为 VOL3 的种子。

## Disk Reclaimer

分配和格式化备用磁盘的 AutoReseed 组件称为 *Disk Reclaimer*。Disk Reclaimer 组件在不定期自动格式化备用磁盘为自动设定种子做准备，时间间隔取决于磁盘状态。为了使 Disk Reclaimer 格式化磁盘，必须满足特定的条件：

  - 必须启用 Disk Reclaimer。默认情况下已启用，但是可通过使用 [Set-DatabaseAvailabilityGroup](https://technet.microsoft.com/zh-cn/library/dd297934\(v=exchg.150\)) 将其停用。

  - 卷必须在根卷路径（默认情况下为 C:\\ExchangeVolumes）下有一个装入点。

  - 卷必须在数据库卷路径（默认情况下为 C:\\ExchangeVolumes）下不存在装入点。

  - 如果卷中包含任何文件，其中的文件无需必须被接触 24 个小时。

除了上述条件，Disk Reclaimer 将只尝试一天一次地格式化给定卷。下表描述 Disk Reclaimer 的格式化行为。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>磁盘和数据库副本的状态</th>
<th>格式化的时间间隔</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>磁盘未格式化，或已格式化但是为空，或已格式化但是包含未被接触 24 个小时的文件，并且在本地 Active Directory 站点中有可用作种子设定源的健康活动数据库副本。</p></td>
<td><p>1 天</p></td>
</tr>
<tr class="even">
<td><p>磁盘未格式化，或已格式化但是为空，或已格式化但是包含未被接触 24 个小时的文件，但是在本地 Active Directory 站点中没有可用作种子设定源的健康活动数据库副本。</p></td>
<td><p>2 天</p></td>
</tr>
<tr class="odd">
<td><p>磁盘未格式化，或已格式化但是为空，或已格式化但是包含未被接触 24 个小时的文件，并且在本地 Active Directory 站点中有可用作种子设定源的健康活动数据库副本，但是在数据库文件（EDB 文件）和日志文件以外有未知文件。</p></td>
<td><p>2 周</p></td>
</tr>
<tr class="even">
<td><p>磁盘未格式化，或已格式化但是为空，或已格式化但是包含未被接触 24 个小时的文件，并且在本地 Active Directory 站点中有可用作种子设定源的健康活动数据库副本，但是有不显示在 Active Directory 下的数据库的一个或多个数据库文件（EDB 文件）。</p></td>
<td><p>2 周</p></td>
</tr>
</tbody>
</table>

