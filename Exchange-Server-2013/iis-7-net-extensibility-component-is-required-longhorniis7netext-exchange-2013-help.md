---
title: '需要 IIS 7 .NET 可扩展性组件_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: 需要 IIS 7 .NET 可扩展性组件_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50491136
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 需要 IIS 7 .NET 可扩展性组件\_LonghornIIS7NetExt

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2012-06-05_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

Microsoft®Exchange Server 2010 安装程序无法继续，因为目标服务器中未安装所需的 Internet 信息服务 (IIS) 7 .NET 扩展性组件。

必须先在目标服务器中安装 IIS 7 .NET 扩展性组件，Exchange 2010 才可使用 Windows PowerShell Remoting。

要解决此错误，请使用服务器管理器在此服务器中安装 IIS 7 .NET 扩展性组件，然后重新运行 Exchange 2010 安装程序。

使用服务器管理器工具，在 Windows Server 2008 R2 或 Windows Server 中安装 IIS 7 .NET 可扩展性组件。

1.  依次单击\&quot;开始\&quot;、\&quot;管理工具\&quot;和\&quot;服务器管理器\&quot;。

2.  在左侧导航窗格中，展开\&quot;角色\&quot;，再右键单击\&quot;Web 服务器 (IIS)\&quot;并选择\&quot;添加角色服务\&quot;。

3.  在\&quot;选择角色服务\&quot;窗格上，向下滚动到\&quot;应用程序开发\&quot;。

4.  选中\&quot;.NET 扩展性\&quot;下的复选框。

5.  单击\&quot;选择角色服务\&quot;窗格中的\&quot;下一步\&quot;，然后单击\&quot;确认安装选择\&quot;窗格中的\&quot;安装\&quot;。

6.  单击\&quot;关闭\&quot;退出\&quot;添加角色服务\&quot;向导。

