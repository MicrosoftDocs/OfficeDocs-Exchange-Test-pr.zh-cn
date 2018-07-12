---
title: '活动目录域处于混合 mode_LocalDomainModeMixed: Exchange 2013 Help'
TOCTitle: 活动目录域处于混合 mode_LocalDomainModeMixed
ms:assetid: a6affcfe-7264-455b-8e5c-683fa87383f1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.localdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50491342
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 活动目录域处于混合 mode\_LocalDomainModeMixed

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

由于现有的 Active Directory 域未设置为 Microsoft Windows® 2000 Server 纯模式或更佳模式，因此 Microsoft® Exchange Server 2007 安装程序无法继续。

Exchange 2007 安装程序将创建通用安全组，这些组只能在使用 Windows 2000 Server 纯模式或更佳模式的域中存在。

若要解决此问题，请遵循下列步骤，至少将域功能级别提升到 Windows 2000 Server 纯模式级别，然后重新运行 Exchange 2007 安装程序。

提升域功能级别

1.  打开\&quot;Active Directory 域和信任\&quot;。

2.  在控制台树中，用鼠标右键单击要提升其功能的域，然后单击\&quot;提升域功能级别\&quot;。

3.  在\&quot;选择可用的域功能级别\&quot;中，使用下列步骤之一：
    
      - 若要将域功能级别提升到 Windows 2000 Server 纯模式，请单击\&quot;Windows 2000 纯模式\&quot;，然后单击\&quot;提升\&quot;。
    
      - 若要将域功能级别提升到 Windows Server® 2003，请单击\&quot;Windows Server 2003\&quot;，然后单击\&quot;提升\&quot;。

> [!CAUTION]  
> 如果您有或将有运行 Windows NT® 4.0 的域控制器并更早版本，不会引发对 Windows 2000 Server 本机域功能级别。域功能级别设置为 Windows 2000 Server 本机后，就无法更改回混合的 Windows 2000 服务器中。
> 如果已拥有或将会拥有任何运行 Windows NT 4.0 和更早版本或运行 Windows 2000 Server 的域控制器，请不要将域功能级别提升到 Windows Server 2003。将域功能级别设置为 Windows Server 2003 后，无法将其更改回到 Windows 2000 Server 混合模式或 Windows 2000 Server 纯模式。

