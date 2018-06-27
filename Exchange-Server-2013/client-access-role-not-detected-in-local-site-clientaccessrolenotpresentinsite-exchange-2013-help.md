---
title: '未检测到本地 site_ClientAccessRoleNotPresentInSite 的客户端访问角色: Exchange 2013 Help'
TOCTitle: 未检测到本地 site_ClientAccessRoleNotPresentInSite 的客户端访问角色
ms:assetid: b5bfc6af-9c55-46c0-a293-6078b64e87dd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.clientaccessrolenotpresentinsite(v=EXCHG.150)
ms:contentKeyID: 50491470
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 未检测到本地 site\_ClientAccessRoleNotPresentInSite 的客户端访问角色

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

如果没有在本地 Active Directory® 目录服务站点中检测到现有客户端访问角色，Microsoft® Exchange Server 2007 安装程序就会显示此警告。

在 Active Directory 站点安装客户端访问角色实例以前，应已选择安装邮箱服务器角色。

客户端访问服务器角色从各种不同的客户端与您的 Exchange 2007 服务器接受连接。例如，Microsoft Outlook Express 和 Eudora 的软件客户端使用 POP3 或 IMAP4 连接与 Exchange 服务器通信。硬件的客户端，如移动设备，使用 ActiveSync、 POP3 或 IMAP4 与 Exchange 服务器通信。

如果用户使用 Microsoft Office Outlook® 以外的任何客户端访问其收件箱，则您必须在您的 Exchange 组织中安装客户端访问服务器角色。

虽然用户可以使用 Outlook 登录其邮箱，但是在客户端访问角色存在于本地 Active Directory 站点中之前，用户不能对同一邮箱使用 Outlook Web Access 或移动设备。

