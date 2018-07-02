---
title: '已在注册表中设置域控制器重写_ConfigDCHostNameMismatch: Exchange 2013 Help'
TOCTitle: 已在注册表中设置域控制器重写_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 50490337
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 已在注册表中设置域控制器重写\_ConfigDCHostNameMismatch

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-15_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft Exchange Server 2007 安装程序因其使用指定域控制器的尝试失败，而无法继续运行。域控制器已在注册表中静态映射。

Exchange 2007 安装程序要求在 setup 命令中指定的域控制器与使用注册表覆盖静态映射的域控制器匹配。

若要解决此问题，请再次运行安装程序，同时为 **/DomainController: \<***FQDN of thestatically mapped domain controller***\>** 参数指定静态映射的域控制器。

关于 DSAccess 和目录服务检测，请参阅 Microsoft 知识库文章 250570，"目录服务服务器检测并 DSAccess 使用情况"([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=250570)) 的详细信息。

