---
title: '安装程序无法将 Exchange 安装到只读域控制器_ComputerRODC: Exchange 2013 Help'
TOCTitle: 安装程序无法将 Exchange 安装到只读域控制器_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50490485
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 安装程序无法将 Exchange 安装到只读域控制器\_ComputerRODC

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安装程序无法继续安装，因为目标计算机为只读域控制器 (RODC)。

只读域控制器是 Windows Server 2008 Active Directory 的一项功能。RODC 是一种域控制器安装选项，可以安装于可能具有较低级别物理安全性的远程网站上。

Exchange 安装程序需要对目标安装计算机具有写入访问权限。

要解决此问题，请选择未指定为 RODC 的目标安装计算机，然后重新运行安装程序。

