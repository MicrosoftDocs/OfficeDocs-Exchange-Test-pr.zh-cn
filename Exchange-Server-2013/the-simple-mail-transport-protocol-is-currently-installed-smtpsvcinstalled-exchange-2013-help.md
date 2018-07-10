---
title: '目前 installed_SMTPSvcInstalled 简单邮件传输协议。: Exchange 2013 Help'
TOCTitle: 目前 installed_SMTPSvcInstalled 简单邮件传输协议。
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 50492011
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 目前 installed\_SMTPSvcInstalled 简单邮件传输协议。

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为该计算机上安装了 Microsoft Windows Server™ 2003 简单邮件传输协议 (SMTP) 服务，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Microsoft Exchange 安装程序要求 SMTP 服务不能安装在用于 Exchange 2007 的服务器上。

若要解决此问题，请卸载 SMTP 服务并重新运行 Microsoft Exchange 安装程序。

通过使用控制面板中的\&quot;添加/删除 Windows 组件\&quot;来卸载 SMTP 服务

1.  在\&quot;开始\&quot;菜单上，单击\&quot;控制面板\&quot;。

2.  双击\&quot;添加或删除程序\&quot;。

3.  单击\&quot;添加/删除 Windows 组件\&quot;。

4.  在\&quot;组件\&quot;列表中，选中\&quot;应用程序服务器\&quot;复选框，然后单击\&quot;详细信息\&quot;。

5.  选择\&quot;Internet 信息服务管理器\&quot;，然后单击\&quot;详细信息\&quot;。

6.  选择\&quot;SMTP 服务\&quot;，然后单击以清除此复选框。

7.  单击\&quot;确定\&quot;两次以返回到\&quot;组件\&quot;列表，然后单击\&quot;下一步\&quot;。

8.  卸载 SMTP 服务后，单击\&quot;完成\&quot;。

