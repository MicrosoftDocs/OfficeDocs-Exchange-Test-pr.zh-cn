---
title: 'Windows Process Activation Service - 需要过程模型组件'
TOCTitle: Windows Process Activation Service - 需要过程模型组件_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 50491138
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Windows Process Activation Service - 需要过程模型组件\_LonghornWASProcessModelInstalled

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2015-04-07_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Exchange Server 2010 设置无法继续安装在基于 Windows Server 2008 或基于 Windows Server 2008 R2 的计算机中，因为该服务器中未安装 Windows Process Activation Service - 进程模型功能。

Windows Process Activation Service 整合了 Internet 信息服务 (IIS) 进程模型，取消了对 HTTP 的依赖。通过使用非 HTTP 协议，所有以前仅可用于 HTTP 应用程序的 IIS 功能如今均可用于托管 Windows Communication Foundation (WCF) 服务的应用程序。此外，IIS 7.0 还使用 Windows Process Activation Service 用于通过 HTTP 的基于邮件的激活。

进程模型承载 Web 和 WCF 服务。如 IIS 6.0 中所介绍，进程模型是一个新的体系结构，可提供快速的故障保护、运行状况监控以及重复利用。

若要解决此问题，请在此服务器上安装 Windows Process Activation Service - 进程模型功能，然后重新运行 Exchange 2010 设置。

使用服务器管理器工具安装 Windows Process Activation Service - 进程模型功能

1.  依次单击\&quot;开始\&quot;、\&quot;管理工具\&quot;和\&quot;服务器管理器\&quot;。

2.  在左侧导航窗格中，右键单击\&quot;功能\&quot;，然后单击\&quot;添加功能\&quot;。

3.  在\&quot;选择功能\&quot;窗格中，向下滚动到\&quot;Windows Process Activation Service\&quot;。

4.  选中\&quot;进程模型\&quot;复选框。

5.  单击\&quot;选择功能\&quot;窗格中的\&quot;下一步\&quot;，然后单击\&quot;确认安装选择\&quot;窗格中的\&quot;安装\&quot;。

6.  单击\&quot;关闭\&quot;退出\&quot;添加角色服务\&quot;向导。

