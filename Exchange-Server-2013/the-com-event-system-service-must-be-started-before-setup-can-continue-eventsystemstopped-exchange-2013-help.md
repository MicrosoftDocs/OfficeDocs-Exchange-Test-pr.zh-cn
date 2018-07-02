---
title: '必须先启动 COM+ Event System 服务，安装程序才能继续进行_EventSystemStopped: Exchange 2013 Help'
TOCTitle: 必须先启动 COM+ Event System 服务，安装程序才能继续进行_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50490356
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 必须先启动 COM+ Event System 服务，安装程序才能继续进行\_EventSystemStopped

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因目标计算机上未启动 COM+ Event System 服务致使安装客户端访问服务器角色或边缘传输服务器角色的尝试失败，进而导致 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求，必须在即将安装 Microsoft Exchange 的计算机上，将 COM+ 事件系统服务状态设置为\&quot;已启动\&quot;。

COM+ Event System 服务支持 COM+ 组件的系统事件通知，从而使事件能够自动分发到订阅的 COM 组件。

客户端访问服务器角色和边缘传输服务器角色都依赖于订阅 COM+ Event System 服务的 COM+ 组件。

若要解决此问题，请验证在本地计算机上 COM+ Event System 服务的状态是否设置为\&quot;已启动\&quot;，再重新运行 Microsoft Exchange 安装程序。

将 COM+ Event System 服务的状态设置为\&quot;已启动\&quot;

1.  右键单击\&quot;我的电脑\&quot;，然后单击\&quot;管理\&quot;。

2.  展开\&quot;服务和应用程序\&quot;节点，再单击\&quot;服务\&quot;节点。

3.  在右侧窗格中，找到 **Com+ Event System**。

4.  右键单击\&quot;Com+ 事件系统\&quot;，然后单击\&quot;属性\&quot;。

5.  将\&quot;启动类型\&quot;设置为\&quot;自动\&quot;，并将\&quot;服务状态\&quot;设置为\&quot;已启动\&quot;。

6.  依次单击\&quot;应用\&quot;和\&quot;确定\&quot;。

