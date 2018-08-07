---
title: 'Active Directory 中存在重复的 Exchange 系统对象容器'
TOCTitle: Active Directory 中存在重复的 Microsoft Exchange System Objects 容器
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 50491561
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Active Directory 中存在重复的 Microsoft Exchange System Objects 容器

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2013-02-18_

Microsoft Exchange Server 2013 安装程序无法继续，因为它在 Active Directory 域命名上下文中发现一个重复的 Microsoft Exchange System Objects 容器。当安装程序发现重复的 Microsoft Exchange System Objects 容器时，您必须删除此重复容器，安装程序才能继续运行。如果存在重复的 Microsoft Exchange System Objects 容器，再次运行 **DomainPrep** 不能解决问题。必须标识并删除重复的 Microsoft Exchange System Objects 容器。

要解决此问题，请执行下列步骤：

1.  使用管理凭据登录到域控制器。

2.  在“管理工具”中，单击“Active Directory 用户和计算机”。

3.  在“Active Directory 用户和计算机”管理控制台窗格中，单击工具栏菜单中的“查看”，然后选择“高级功能”。

4.  找到重复的 Microsoft Exchange System Object 容器。

5.  确认重复的 Microsoft Exchange System Objects 容器不包含有效的 Active Directory 对象。

6.  右键单击重复的 Microsoft Exchange System Objects 容器，再单击“删除”。

7.  在 Active Directory 对话框中单击“是”来确认删除。

> [!NOTE]  
> 如果要立即复制更改，必须手动启动域控制器之间的复制。


遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

