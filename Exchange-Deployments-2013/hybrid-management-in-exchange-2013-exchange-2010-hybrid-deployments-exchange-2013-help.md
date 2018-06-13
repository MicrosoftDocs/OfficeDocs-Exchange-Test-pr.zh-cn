---
title: 'Exchange 2013/Exchange 2010 混合部署中的混合管理: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 混合部署中的混合管理
ms:assetid: 613ad2c2-bb7a-4810-b572-71945bd103f1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn393961(v=EXCHG.150)
ms:contentKeyID: 59636466
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 混合部署中的混合管理

本主题正在进行。  

_**适用于：**Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

在 Exchange 2010 内部部署组织中安装运行 Microsoft Exchange Server 2013 的服务器时，会自动在服务器上安装 Exchange 2013 管理工具。您将使用以下工具来配置和管理内部部署 Exchange 和 Exchange Online 组织的混合功能：

  - **Exchange 管理中心**   EAC 是基于 Web 的管理控制台，包含在 Exchange 2013 中，使用简单，并针对内部部署、在线或混合 Exchange 部署进行了优化。EAC 补充了用于管理 Exchange Server 2010 的 Exchange 管理控制台 (EMC) 和 Exchange 控制面板 (ECP) 界面。

  - **Exchange 命令行管理程序**Exchange 命令行管理程序是基于 Windows PowerShell 的命令行界面。

## Exchange 管理中心

EAC 允许您同时在内部部署 Exchange 服务器和 Exchange Online 组织上执行许多部署任务和最常见的日常管理任务。默认情况下，它将在每个 Exchange 2013 服务器上安装。此外，由于它是基于 Web 的管理控制台，您还可以使用网络中的其他计算机的 Web 浏览器或通过使用 ECP 虚拟目录 URL 访问它。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果想要使用邮箱位于 Exchange 2010 邮箱服务器中的帐户（例如域管理员帐户）访问 EAC，则必须在浏览器中使用以下地址访问 EAC：<br />
https://<em>&lt;FQDN of Exchange 2013 Client Access server&gt;</em>/ECP? ExchClientVer=15</td>
</tr>
</tbody>
</table>


您可以通过选择 Office 365 跨界导航选项卡来访问 EAC 中的 Exchange Online 组织。跨界导航允许您在 Exchange Online 和内部部署 Exchange 组织之间轻松切换。如果您已经配置混合部署，选择 Office 365 选项卡将允许您管理 Exchange Online 组织和收件人对象。如果您没有 Exchange Online 组织，选择 Office 365 链接会将您转到 Office 365 注册页面。

有关 EAC 的详细信息，请参阅 [Exchange 2013 中的 Exchange 管理中心](https://technet.microsoft.com/zh-cn/library/jj150562\(v=exchg.150\))。

## Exchange 命令行管理程序

Exchange 命令行管理程序可以执行 EAC 执行的任何任务，以及只能在Exchange 命令行管理程序中执行的某些其他任务。Exchange 命令行管理程序是安装 Exchange 2013 管理工具时安装在计算机上的 Windows PowerShell 脚本和 cmdlet 的集合。只有在使用Exchange 命令行管理程序图标打开Exchange 命令行管理程序时，才会加载这些脚本和 cmdlet。如果你直接打开 Windows PowerShell，则不会加载 Exchange 脚本和 cmdlet，并且你将无法管理内部部署组织。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>你可以创建到本地内部部署组织的手动 Windows PowerShell 连接，方式与手动连接到以下 Exchange Online 组织类似。但是，强烈建议你使用Exchange 命令行管理程序图标来打开Exchange 命令行管理程序，以管理内部部署Exchange服务器。</td>
</tr>
</tbody>
</table>


当你在安装了管理工具的计算机上使用Exchange 命令行管理程序图标打开Exchange 命令行管理程序时，可以管理内部部署组织。但是，在使用此图标打开Exchange 命令行管理程序时不能管理 Exchange Online 组织。这是因为使用Exchange 命令行管理程序图标打开Exchange 命令行管理程序会自动连接到本地 Exchange 服务器。

如果要使用 Windows PowerShell 管理 Exchange Online 组织，必须直接打开 Windows PowerShell，而不要通过Exchange 命令行管理程序图标打开。打开 Windows PowerShell 后，你便可以手动指定要连接的位置。当你创建手动连接时，可在 Office 365 租户组织中指定一个管理员帐户，然后运行命令以创建连接。建立该连接后，你即可使用有权运行的 Exchange cmdlet。有关更多信息，请参阅[使用 Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660)。

如果你不熟悉Exchange 命令行管理程序，请查看 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))，以了解有关Exchange 命令行管理程序的工作方式的基本信息、命令语法及更多内容。

