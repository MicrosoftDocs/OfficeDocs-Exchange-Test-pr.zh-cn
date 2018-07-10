---
title: 'Exchange Server 2013 性能建议: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 性能建议
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63895117
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 性能建议

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Exchange Server 2013当您的环境已适当调整了大小并进行过规划时，性能调整和故障排除最有效。虽然 Exchange 2013 旨在简化基本资源基础结构，但它仍会消耗大量的系统资源，如内存、存储容量和 CPU 容量。

此部分中的文章由 Exchange 性能团队撰写。文章中包含来自 Exchange 产品组的专业知识，以及从客户支持案例中总结的最佳实践。这些文章的目标就是帮助您了解 Exchange 2013 中引入的变化所带来的影响，以及正确调整 Exchange 2013 基础结构大小的重要性。我们还介绍了有关识别性能问题的建议优化和指导。

## Exchange 2013 中的体系结构更改和其他资源

Exchange 2013 中的体系结构更改已经在 TechNet 和 [Exchange 团队博客](https://go.microsoft.com/fwlink/p/?linkid=35786)中作出了说明。我们将首先介绍几个应该考虑的高级别更改，以便更好地了解性能成本和大小调整。接下来，我们介绍了一个建议引用的列表，以进一步提供这些重要领域的上下文和背景。

> [!NOTE]
> 请参阅 <a href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 虚拟化</a>，了解有关在虚拟化环境中部署 Exchange Server 2013 的性能优化指导。


在 Exchange 2013 中，客户端访问服务器角色是一个无状态代理服务器。现在，客户端访问服务器角色的主要职责是对传入的请求进行身份验证，然后将每个请求代理到相应的邮箱服务器和托管用户邮箱主动副本的服务器。这意味着，不再需要在客户端访问服务器和负载平衡器之间为特定协议配置关联。

Exchange 2013 中的另一个值得注意的更改是在信息存储中。现在信息存储包括两种进程：主机进程和工作进程。每个数据库实例与其自己的 Microsoft.Exchange.Store.Worker.exe 进程相关联。这样允许对有问题的数据库问题进行更好地隔离，并能将数据库问题的性能影响减少到只对此数据库的一个工作实例产生影响。

Microsoft Exchange 复制服务负责与邮箱服务器角色相关的所有高可用性服务。此复制服务托管活动管理器组件，该组件负责监视失败，并采取纠正措施。

可以在 [Exchange 2013 服务器角色体系结构](https://go.microsoft.com/fwlink/p/?linkid=523735)中找到一篇有关体系结构更改的有用文章，其中包括从较早版本重新调整 Exchange 2013 环境大小的影响。

可以在以下网址中找到有关 Exchange 2013 体系结构更改的详细信息以及其他相关领域的背景信息：

[Exchange Server 2013 体系结构](https://go.microsoft.com/fwlink/p/?linkid=523769)

[正确地进行规划：Exchange Server 2013 大小调整方案](https://go.microsoft.com/fwlink/p/?linkid=523773)

[监视并调整 Microsoft Exchange Server 2013 性能](https://go.microsoft.com/fwlink/p/?linkid=523774)

[实现 Exchange Server 2013：(01) 升级并部署 Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523775)

[实现 Exchange Server 2013：(02) 正确地进行规划：Exchange Server 2013 大小调整](https://go.microsoft.com/fwlink/p/?linkid=523776)

[实现 Exchange Server 2013：(03) Exchange Server 2013 虚拟化最佳实践](https://go.microsoft.com/fwlink/p/?linkid=523777)

[实现 Exchange Server 2013：(04) Exchange 体系结构：高可用性和站点恢复](https://go.microsoft.com/fwlink/p/?linkid=523779)

[实现 Exchange Server 2013：(05) Outlook 连接性](https://go.microsoft.com/fwlink/p/?linkid=523781)

[首选体系结构](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Exchange 2013 客户端访问服务器角色](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 虚拟化最佳实践](https://go.microsoft.com/fwlink/p/?linkid=523783)

[负载平衡](load-balancing-exchange-2013-help.md)

[Exchange Server 更新：内部版本号和发行日期](https://technet.microsoft.com/zh-cn/library/hh135098\(v=exchg.150\))

[Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)

[Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)

[IIS 7.5、IIS 7.0 和 IIS 6.0 上的 ASP.NET 线程使用](https://go.microsoft.com/fwlink/p/?linkid=169626)

