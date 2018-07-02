---
title: 'Active Directory 不存在或无法通信: Exchange 2013 Help'
TOCTitle: Active Directory 不存在或无法通信
ms:assetid: 56adb6fe-ecb8-4a7f-b440-89aa401c28b7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.cannotaccessad(v=EXCHG.150)
ms:contentKeyID: 50490619
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 不存在或无法通信

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

Microsoft Exchange Server 2013 安装程序无法继续，因为无法与有效的 Active Directory 目录服务站点通信。安装程序要求要在其上安装 Exchange 的服务器可以在 Active Directory 中查找配置命名上下文。

若要解决此问题，请验证运行 Exchange 安装程序的用户帐户是否为 Active Directory 用户，然后重新运行安装程序。如果这样做没有解决问题，请按照下面主题中有关使用 dcdiag.exe 和 repadmin.exe 支持工具的指导，进一步诊断问题。

有关针对 Exchange 的 Active Directory 疑难解答和配置的详细信息，请参阅下列主题：

  - [准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)

  - [Active Directory 域服务疑难解答](https://go.microsoft.com/fwlink/p/?linkid=272144)

  - [计算机疑难解答配置](https://go.microsoft.com/fwlink/p/?linkid=272141)

  - [解决 Active Directory 复制问题](https://go.microsoft.com/fwlink/p/?linkid=272142)

  - [使用 Repadmin 监视和解决 Active Directory 复制问题](https://go.microsoft.com/fwlink/p/?linkid=272143)

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

