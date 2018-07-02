---
title: '本地计算机是一个子域的域控制器_LocalComputerIsDCInChildDomain: Exchange 2013 Help'
TOCTitle: 本地计算机是一个子域的域控制器_LocalComputerIsDCInChildDomain
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50491068
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本地计算机是一个子域的域控制器\_LocalComputerIsDCInChildDomain

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为本地计算机是子域的域控制器，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

不能将 Exchange 2007 安装程序安装到子域的域控制器上，除非域控制器是全局编录服务器。

若要解决此问题，请将域控制器提升到全局编录服务器，或将 Exchange 2007 安装到子域中的非域控制器的成员服务器上，然后重新运行 Microsoft Exchange 安装程序。

通过使 Exchange 服务器成为全局编录服务器来解决此警告问题

1.  在域控制器中，单击\&quot;开始\&quot;，指向\&quot;程序\&quot;，单击\&quot;管理工具\&quot;，然后单击\&quot;Active Directory 站点和服务\&quot;。

2.  在控制台树中，双击\&quot;站点\&quot;，双击该站点的名称，然后双击\&quot;服务器\&quot;。

3.  双击目标域控制器。

4.  在结果窗格中，右键单击\&quot;NTDS 设置\&quot;，然后单击\&quot;属性\&quot;。

5.  在\&quot;常规\&quot;选项卡上，单击以选中\&quot;全局编录\&quot;复选框。

6.  重新启动域控制器。

