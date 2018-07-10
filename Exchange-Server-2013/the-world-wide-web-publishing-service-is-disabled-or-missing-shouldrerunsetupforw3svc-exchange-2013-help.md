---
title: '万维网发布服务被禁用或 missing_ShouldReRunSetupForW3SVC: Exchange 2013 Help'
TOCTitle: 万维网发布服务被禁用或 missing_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 50491968
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 万维网发布服务被禁用或 missing\_ShouldReRunSetupForW3SVC

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft® Exchange Server 2007 安装程序无法继续，原因是它在安装邮箱服务器或客户端访问角色时发现该计算机已禁用或未安装万维网发布服务。

Exchange 2007 安装程序要求安装 Microsoft Exchange 的计算机装有万维网发布服务，同时被设置为禁用之外的其他设置。

要解决此问题，请验证本地计算机上是否安装了万维网发布服务，并且未被禁用，然后重新运行 Microsoft Exchange 安装程序。

验证是否安装了万维网发布服务且未被禁用

1.  在桌面上右键单击\&quot;我的电脑\&quot;，然后单击\&quot;管理\&quot;。

2.  展开\&quot;服务和应用程序\&quot;节点，再单击\&quot;服务\&quot;节点。

3.  在右窗格中，找到\&quot;World Wide Web 发布服务\&quot;。
    
    如果\&quot;万维网发布服务\&quot;没有显示在已安装的服务列表中，请按照下列步骤进行安装。

4.  如果显示了\&quot;万维网发布服务\&quot;，但状态不是\&quot;已启动\&quot;，请继续执行下列步骤启动该服务。

5.  右键单击\&quot;World Wide Web 发布服务\&quot;，然后单击\&quot;属性\&quot;。

6.  验证\&quot;启动类型\&quot;是否为\&quot;自动\&quot;，\&quot;服务状态\&quot;是否设置为\&quot;已启动\&quot;。

7.  依次单击\&quot;应用\&quot;和\&quot;确定\&quot;。

安装万维网发布服务

1.  在\&quot;开始\&quot;菜单上，依次选择\&quot;设置\&quot;、\&quot;控制面板\&quot;，然后单击\&quot;添加或删除程序\&quot;。

2.  单击\&quot;添加/删除 Windows 组件\&quot;。

3.  在\&quot;组件\&quot;列表中，选中\&quot;应用程序服务器\&quot;复选框，然后单击\&quot;详细信息\&quot;。

4.  选择\&quot;Internet Information Services 管理器\&quot;，然后单击\&quot;详细信息\&quot;。

5.  选择\&quot;万维网服务\&quot;，然后选中该复选框。

6.  单击\&quot;确定\&quot;两次以返回到\&quot;组件\&quot;列表，然后单击\&quot;下一步\&quot;。

7.  安装了 IIS 服务后，单击\&quot;完成\&quot;。

