---
title: 'IIS 为 32 位兼容模式_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS 为 32 位兼容模式_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50490917
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 为 32 位兼容模式\_IIS32BitMode

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

由于 Microsoft Internet 信息服务 (IIS) 在此 64 位计算机上以 32 位模式运行，因此 Microsoft® Exchange Server 2007 安装程序无法继续。

Exchange 2007 要求 IIS 在 64 位计算机上运行时，必须完全处于 64 位模式。

若要解决此问题，请将 IIS 切换到 64 位模式，然后重新运行 Microsoft Exchange 安装程序。

将 IIS 切换到 64 位模式

1.  打开命令提示符。

2.  键入以下命令：
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  按 Enter

