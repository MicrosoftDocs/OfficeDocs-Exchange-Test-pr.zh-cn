---
title: '本地计算机负责扩展组成员身份_ServerIsGroupExpansionServer: Exchange 2013 Help'
TOCTitle: 本地计算机负责扩展组成员身份_ServerIsGroupExpansionServer
ms:assetid: 52872561-60e6-4f3d-bbc6-6de0edf74b09
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.serverisgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50490567
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 本地计算机负责扩展组成员身份\_ServerIsGroupExpansionServer

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为尝试卸载负责扩展组成员身份的集线器传输角色失败，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求在卸载集线器传输角色之前，应从当前桥头服务器删除通讯列表展开。

通讯组列表扩展启用属于要标识的通讯组列表的各个收件人的标识，或启用用于扩展的其他通讯组列表的标识。展开的通讯组列表可以返回任何所需的传递状态通知 (DSN) 的路径。DSN 将特定电子邮件状态通知给 Microsoft Exchange 管理员或电子邮件发件人。此外，通讯组列表扩展确定是否应将\&quot;外出\&quot;回复邮件或自动生成的回复邮件发送到原始邮件的发件人。

要解决此问题，请将通讯组扩展移到另一台服务器并重新运行 Microsoft Exchange 安装程序。

为通讯组或动态通讯组更改扩展服务器

1.  打开 Exchange 管理控制台。

2.  在控制台树中，展开\&quot;收件人配置\&quot;。

3.  在控制台树中，单击\&quot;通讯组\&quot;。

4.  创建筛选器来查看将当前桥头服务器用作扩展服务器的所有通讯组以及动态通讯组。
    
    1.  在操作窗格中，单击\&quot;创建筛选器\&quot;。
    
    2.  在属性下拉列表中，单击\&quot;扩展服务器\&quot;。
    
    3.  在运算符下拉列表中，单击\&quot;等于\&quot;。
    
    4.  在值框中，单击\&quot;浏览\&quot;按钮来选择当前充当扩展服务器的桥头服务器。

> [!NOTE]
> 以下步骤是可选的。


1.  单击\&quot;添加表达式\&quot;指定其他筛选条件。仅显示满足所有筛选条件的邮件。

2.  单击\&quot;应用筛选器\&quot;。此时将显示符合筛选器标准的结果。

<!-- end list -->

1.  在结果窗格中，单击要为其更改扩展服务器的通讯组，然后在操作窗格中单击\&quot;属性\&quot;。

2.  在\&quot;属性\&quot;中，单击\&quot;高级\&quot;选项卡。

3.  在扩展服务器下拉列表中，从列表中选择一台特定的服务器或选择\&quot;组织中的任意服务器\&quot;。

4.  对将桥头服务器用作其扩展服务器的所有通讯组或动态通讯组重复步骤 5 到 7。

