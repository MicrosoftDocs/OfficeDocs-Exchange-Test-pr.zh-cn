---
title: '未检测到 Exchange 2010 或 Exchange 2007 服务器: Exchange 2013 Help'
TOCTitle: 未检测到 Exchange 2010 或 Exchange 2007 服务器
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50490953
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 未检测到 Exchange 2010 或 Exchange 2007 服务器

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2012-11-08_

Microsoft Exchange Server 2013 安装程序显示了此警告，因为组织中不存在任何 Exchange Server 2010 或 Exchange Server 2007 服务器角色。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您继续执行 Exchange Server 2013 安装，以后会无法将 Exchange 2010 或 Exchange 2007 服务器添加到组织中。</td>
</tr>
</tbody>
</table>


在部署 Exchange 2013 之前，请考虑以下因素，可能需要您在部署 Exchange 2013 之前首先部署 Exchange 2010 或 Exchange 2007 服务器：

  - **第三方或内部开发的应用程序**   为较早版本的 Exchange 开发的应用程序可能与 Exchange 2013 不兼容。您可能需要维护 Exchange 2010 或 Exchange 2007 服务器才能支持这些应用。

  - **共存或迁移要求**   如果计划将邮箱迁移到组织中，部分解决方案可能要求使用 Exchange 2010 或 Exchange 2007 服务器。

如果确定需要部署 Exchange 2010 或 Exchange 2007 服务器，就必须在部署 Exchange 2013 之前执行此操作。必须按以下顺序为每个 Exchange 版本准备 Active Directory：

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

