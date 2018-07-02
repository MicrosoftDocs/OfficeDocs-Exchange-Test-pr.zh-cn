---
title: '当前帐户未登录到 Active Directory: Exchange 2013 Help'
TOCTitle: 当前帐户未登录到 Active Directory
ms:assetid: 0e229d10-605a-420f-bf8b-58a7fcb5b259
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.loggedontodomain(v=EXCHG.150)
ms:contentKeyID: 50490002
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 当前帐户未登录到 Active Directory

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2014-12-02_

因检测到当前帐户未登录到 Active Directory 域，Microsoft Exchange Server 2013 安装程序无法继续。必须使用具有 Exchange Server 2013 安装权限的 Active Directory 帐户进行登录。

安装程序要求安装 Exchange 2013 时登录的用户具有在 Active Directory 中创建和修改对象的权限。如果是首次在组织中运行 Exchange 2013 安装程序，则使用的帐户必须是 Schema Admins 组和 Enterprise Admins 组的成员。之所以需要这些权限，是因为首次运行安装程序时，Active Directory 是针对 Exchange 2013 做准备的。在准备好 Active Directory 之后，用户安装其他 Exchange 2013 服务器的帐户必须是组织管理角色组的成员。

若要解决此问题，请向登录的用户授予相应的权限，或者使用拥有这些权限的帐户登录并重新运行 Exchange 2013 安装程序。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不支持跨林安装 Exchange 2013。使用属于要在其中安装 Exchange 2013 的 Active Directory 林的成员的帐户。</td>
</tr>
</tbody>
</table>


遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

