---
title: '卸载统一消息语言包_AdditionalUMLangPackExists: Exchange 2013 Help'
TOCTitle: 卸载统一消息语言包_AdditionalUMLangPackExists
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 50490332
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 卸载统一消息语言包\_AdditionalUMLangPackExists

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为统一消息服务器角色升级失败，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 安装程序要求先卸载所有的统一消息服务器角色语言包（美国英语语言包除外），统一消息服务器角色升级才能继续进行。

Exchange 2007 附带的统一消息 (UM) 语言包包含给定语言的预录制提示、语音合成 (TTS) 转换支持。

通过 Exchange 2007 UM 语言包，呼叫者和 Outlook Voice Access 用户可以用多种语言与统一消息系统进行交互。

需要卸载现有的非美国英语语言包，才能安装新语言包。

若要解决此问题，请卸载所有的统一消息服务器角色语言包（美国英语语言包除外），再重新运行 Exchange 2007 安装程序。

有关卸载统一消息服务器角色语言包的详细信息，请参阅 Exchange 2007 产品文档中的[统一消息语言包从统一消息服务器中删除方法](https://go.microsoft.com/fwlink/?linkid=85973) 。

