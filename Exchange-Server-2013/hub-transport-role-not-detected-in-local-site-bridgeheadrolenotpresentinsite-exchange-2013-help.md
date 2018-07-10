---
title: '未检测到本地 site_BridgeheadRoleNotPresentInSite 中的集线器传输角色: Exchange 2013 Help'
TOCTitle: 未检测到本地 site_BridgeheadRoleNotPresentInSite 中的集线器传输角色
ms:assetid: f318c947-81a8-4c18-975a-0f1e7868042a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.bridgeheadrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50491930
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 未检测到本地 site\_BridgeheadRoleNotPresentInSite 中的集线器传输角色

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

如果没有在本地 Active Directory® 目录服务站点中检测到现有集线器传输服务器角色，Microsoft® Exchange Server 2007 安装程序就会显示此警告。

在 Active Directory 站点安装集线器传输角色实例以前，应已经选择了安装邮箱服务器角色。

在您的组织的 Active Directory 部署 Exchange 2007 集线器传输服务。在组织内部的所有邮件都流的集线器传输服务句柄应用组织邮件都流路由规则，并负责邮件传递到收件人的邮箱。

用户可以登录到其邮箱，但是在安装集线器传输角色以前，该邮箱服务器无法发送或接收邮件。

