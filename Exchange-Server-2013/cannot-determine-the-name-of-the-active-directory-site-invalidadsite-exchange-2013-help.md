---
title: '无法确定 Active Directory 站点的名称_InvalidADSite: Exchange 2013 Help'
TOCTitle: 无法确定 Active Directory 站点的名称_InvalidADSite
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50491922
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 无法确定 Active Directory 站点的名称\_InvalidADSite

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为该服务器似乎不属于一个有效的 Active Directory® 目录服务站点，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Microsoft Exchange 安装程序要求用于安装 Exchange 2007 的服务器必须属于一个有效的 Active Directory 站点。

要解决此问题，请验证本地服务器是否是有效的 Active Directory 站点的成员，并重新运行 Exchange Server 2007 安装程序。

可以使用 Nltest.exe 命令行工具的 **/DsGetSite** 选项来验证并显示站点的成员身份。有关详细信息，请参阅*Windows Server 2003 技术参考*([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)) 的“工具与设置集合”中的“Nltest.exe: NLTest 概述”。

有关 Active Directory 疑难解答的详细信息，请参阅“Windows Server 2003: *操作* (<https://go.microsoft.com/fwlink/?linkid=68099>)。

