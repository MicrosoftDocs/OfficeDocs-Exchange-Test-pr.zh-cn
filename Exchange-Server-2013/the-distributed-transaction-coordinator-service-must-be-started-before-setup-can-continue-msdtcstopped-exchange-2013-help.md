---
title: '必须先安装可以 continue_MSDTCStopped 启动分布式事务处理协调器服务: Exchange 2013 Help'
TOCTitle: 必须先安装可以 continue_MSDTCStopped 启动分布式事务处理协调器服务
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 50491203
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 必须先安装可以 continue\_MSDTCStopped 启动分布式事务处理协调器服务

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因目标计算机上未启动分布式事务处理协调器服务致使安装客户端访问服务器角色或统一消息服务器角色的尝试失败，进而导致 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求在即将安装 Microsoft Exchange 的计算机上将分布式事务处理协调器服务的状态设置为\&quot;已启动\&quot;。

分布式事务处理协调器服务所提供的服务旨在确保事务的成功和完整，即使在出现系统故障、进程故障和通信故障的情况下也是如此。

参与分布式事务的每台计算机管理其自己的资源和数据并与交易记录中的其他计算机也在音乐会中的作用。最重要的是，分布式的事务必须提交或中止其工作完全参与的所有计算机上。分布式事务处理协调器对所涉及的组件执行事务协调角色，并作为管理交易记录每台计算机的事务管理器。

客户端访问服务器和统一消息服务器角色都依赖于分布式事务处理协调器服务。

若要解决此问题，请验证在本地计算机上分布式事务处理协调器服务的状态是否设置为\&quot;已启动\&quot;，再重新运行 Microsoft Exchange 安装程序。

将分布式事务处理协调器服务的状态设置为\&quot;已启动\&quot;

1.  右键单击\&quot;我的电脑\&quot;，再单击\&quot;管理\&quot;。

2.  展开\&quot;服务和应用程序\&quot;节点，再单击\&quot;服务\&quot;节点。

3.  在右侧窗格中，找到\&quot;分布式事务处理协调器\&quot;。

4.  右键单击\&quot;分布式事务处理协调器\&quot;，再单击\&quot;属性\&quot;。

5.  将\&quot;启动类型\&quot;设置为\&quot;自动\&quot;，并将\&quot;服务状态\&quot;设置为\&quot;已启动\&quot;。

6.  依次单击\&quot;应用\&quot;和\&quot;确定\&quot;。

