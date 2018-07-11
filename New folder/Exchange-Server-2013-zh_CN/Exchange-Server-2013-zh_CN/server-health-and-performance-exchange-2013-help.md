---
title: '服务器运行状况和性能: Exchange 2013 Help'
TOCTitle: 服务器运行状况和性能
ms:assetid: 9d1fdec8-8273-4c71-88f1-b4edfd542c4f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150551(v=EXCHG.150)
ms:contentKeyID: 50491225
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 服务器运行状况和性能

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

了解服务器运行状况和性能对于设计和维护高性能邮件基础结构至关重要。Microsoft Exchange Server 2013 介绍了服务器运行状况和性能方面的改进。

若要了解所有服务器运行状况和性能主题的列表，请参阅服务器运行状况和性能文档。

## 托管可用性

Exchange 2013 引入了*托管可用性*的概念。托管可用性在所有 Exchange 2013 服务器上运行。它包括两个进程，即 Exchange Health Manager Service (MSExchangeHMHost.exe) 和 Exchange Health Manager Worker 进程 (MSExchangeHMWorker.exe)，以及下列异步组件：

  - **探测器引擎** *探测器引擎*在服务器上进行测量。

  - **监控探测器引擎** *监控探测器引擎*存储有关运行状况构成的业务逻辑。它可以充当模式识别引擎，查找不同于运行状况的模式和测量值，然后评估组件或功能是否正常运行。

  - **响应程序引擎**   当*响应程序引擎*收到有关组件无法正常运行的提醒时，首先采取的措施便是尝试恢复该组件。托管可用性支持多级恢复操作。第一次可以尝试重新启动应用程序池，第二次可以尝试重新启动相应的服务，第三次可以尝试重新启动服务器。最后可以尝试使服务器脱机，以便不再接受通信。如果上述所有操作均失败，将向帮助中心发送警报。

有关托管可用性的详细信息，请参阅[托管可用性](managed-availability-exchange-2013-help.md)。

## 工作负载管理

Exchange 2013 工作负载管理包括以下组件：

  - *用户工作负载管理*是 Exchange Server 2010 用户限制功能的新名称。您可以根据环境需求自定义这些设置。

  - *系统工作负载管理*是 Exchange 2013 中的新增功能，用于通过监控关键服务器资源的运行状况自动限制 Exchange 工作负载。只能在 Microsoft 客户服务和支持人员的指导下自定义这些设置。

有关详细信息，请参阅[Exchange 工作负载管理](exchange-workload-management-exchange-2013-help.md)。

## 服务器运行状况和性能文档

下表包含的主题链接将帮助您了解和在 Exchange 2013 中管理服务器运行状况和性能。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="exchange-workload-management-exchange-2013-help.md">Exchange 工作负载管理</a></p></td>
<td><p>了解如何通过控制各个用户使用资源的方式来管理 Exchange 工作负载。</p></td>
</tr>
<tr class="even">
<td><p><a href="managed-availability-exchange-2013-help.md">托管可用性</a></p></td>
<td><p>了解 Exchange 2013 中内嵌的资源监控技术和恢复操作。</p></td>
</tr>
</tbody>
</table>

