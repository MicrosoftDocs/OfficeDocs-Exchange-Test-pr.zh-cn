---
title: Exchange Server 2013 Management Pack 入门
TOCTitle: Exchange Server 2013 Management Pack 入门
ms:assetid: 72d1609f-ab32-44d8-aa40-b1de587442d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn195908(v=EXCHG.150)
ms:contentKeyID: 53275725
ms.date: 04/03/2015
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 Management Pack 入门

 

_**上一次修改主题：**  2013-04-08_

Exchange Server 2013 管理包在 SCOM 控制台的“监视”部分中添加容器。当您展开 Exchange Server 2013 容器时，会看到它的下面只有三个视图。

![Exchange 2013 管理包容器](images/Dn195908.253b4ec5-2103-4b0c-a22e-5ebd24d08600(EXCHG.150).png "Exchange 2013 管理包容器")

## 活动警报 – Exchange 是否有任何错误？

**活动警报**视图为您显示 Exchange 组织中生成的当前处于活动状态的所有警报。您单击任何警报，即可在详细信息窗格中看到有关该警报的详细信息。此视图本质上为“我的 Exchange 部署是否有任何错误？”提供了“是/否”答案每个警报对应于特定运行状况设置的一个或多个问题。另外，根据具体问题，可能生成多个警报。

## 组织运行状况 – 有什么影响？

如果您在活动警报视图中看到警报，要做的第一件事情是检查**组织运行状况**视图。这是整个组织运行状况的主要信息来源。它为您具体提供了组织中影响您的因素，如 Active Directory 站点和数据库可用性组。

![组织运行状况](images/Dn195908.603c920b-7b88-4956-87d9-09d93fa6cba3(EXCHG.150).png "组织运行状况")

## 服务器运行状况 – 我需要排除哪个服务器的故障？

**服务器运行状况**视图提供有关组织中个别服务器的详细信息。您可以在此处查看所有服务器的个别运行状况。使用此视图，可以将任何问题缩小到特定服务器。

![服务器运行状况](images/Dn195908.c863be83-fc4b-4daf-a18b-27b1aae15b1d(EXCHG.150).png "服务器运行状况")

## 监视类别

当浏览 Exchange Server 2013 主控板中的三个视图时，您可能注意到除了“状态”列，还有四个附加运行状况指示器。

![Exchange 运行状况指示器](images/Dn195908.dd10ed0b-abe5-41aa-8d43-b4fb10133984(EXCHG.150).png "Exchange 运行状况指示器")

这些运行状况指示器中的每个指示器提供了特定 Exchange 部署方面的概述。

  - **客户触点** 此指示器为您的用户显示了遇到的状况。如果此指示器正常，这意味着该问题可能不会影响您的用户。例如，假设 DAG 成员有问题，但是数据库已成功故障转移。在这种情况下，您会看到该特定 DAG 的不正常指示器，但是由于用户可能不会遇到任何服务中断，因此客户触点指示器将显示正常。

  - **服务组件** 此指示器会为您显示与该组件关联的特定服务的状态。例如，OWA 的服务组件指示器指示整个 OWA 服务是否正常。

  - **服务器资源** 此指示器会为您显示影响服务器功能的物理资源状态。

  - **主要依赖项** 此指示器为您显示 Exchange 依赖的外部资源（如网络连接、DNS 或 Active Directory）的状态。

Exchange Server 2013 管理包视图提供简单但强大的视图，可用于简便快速地确定您的组织运行状况是否正常。但是，视图的结构方式还可帮助您在发生警报时快速确定问题根源。若要了解使用 Exchange Server 2013 管理包解决问题的详细信息，请参阅[使用 Exchange Server 2013 管理包进行故障排除](using-the-exchange-server-2013-management-pack-for-troubleshooting.md)。

