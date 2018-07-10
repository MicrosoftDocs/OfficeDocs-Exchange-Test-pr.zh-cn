---
title: '无法在包含 Exchange 2000 或 Exchange 2003 服务器的林中安装 Exchange 2013。: Exchange 2013 Help'
TOCTitle: 无法在包含 Exchange 2000 或 Exchange 2003 服务器的林中安装 Exchange 2013。
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50491237
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 无法在包含 Exchange 2000 或 Exchange 2003 服务器的林中安装 Exchange 2013。

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

Microsoft Exchange Server 2013 无法继续，因为 Active Directory 林中有一台或多台计算机在运行 Exchange 2000 Server 或 Exchange Server 2003。必须将所有的 Exchange 2000 和 Exchange 2003 服务器从林中删除，然后才能安装 Exchange 2013。邮箱、公用文件夹以及其他所有 Exchange 对象或组件都必须升级为 Exchange Server 2007 或 Exchange Server 2010。你不能从 Exchange 2000 或 Exchange 2003 直接升级到 Exchange 2013。

你在组织中安装 Exchange 2013 时需要遵循的路径取决于你当前在林中安装的 Exchange 版本。有关详细信息，请参阅下表。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>如果您已将以下内容安装到组织中</th>
<th>您必须将此路径升级为 Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>将 Exchange 2007 安装到您的 Exchange 2000 组织中。</p></li>
<li><p>配置 Exchange 2007 和 Exchange 2000 共存。</p></li>
<li><p>将 Exchange 2000 邮箱、公用文件夹以及其他组件迁移到 Exchange 2007。</p></li>
<li><p>停用并删除所有的 Exchange 2000 服务器。</p></li>
<li><p>将 Exchange 2013 安装到您的 Exchange 2007 组织中。</p></li>
<li><p>配置 Exchange 2013 和 Exchange 2007 共存。</p></li>
<li><p>将 Exchange 2007 邮箱、公用文件夹以及其他组件迁移到 Exchange 2013。</p></li>
<li><p>停用并删除所有的 Exchange 2007 服务器。</p></li>
</ol>
<p>有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=103281">升级到 Exchange 2007</a> 和<a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">从 Exchange 2007 升级到 Exchange 2013</a>。</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>将 Exchange 2010 安装到您的 Exchange 2003 组织中。</p></li>
<li><p>配置 Exchange 2010 和 Exchange 2003 共存。</p></li>
<li><p>将 Exchange 2003 邮箱、公用文件夹以及其他组件迁移到 Exchange 2010。</p></li>
<li><p>停用并删除所有的 Exchange 2003 服务器。</p></li>
<li><p>将 Exchange 2013 安装到您的 Exchange 2010 组织中。</p></li>
<li><p>配置 Exchange 2013 和 Exchange 2010 共存。</p></li>
<li><p>将 Exchange 2010 邮箱、公用文件夹以及其他组件迁移到 Exchange 2013。</p></li>
<li><p>停用并删除所有的 Exchange 2010 服务器。</p></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003 - 规划升级和共存的路线图</a>和<a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">从 Exchange 2010 升级至 Exchange 2013</a>。</p></td>
</tr>
</tbody>
</table>


升级到 Exchange 2010 或 Exchange 2013 后，你就可以使用 Exchange 部署助理来帮助完成部署。有关详细信息，请参阅以下链接：

  - [Exchange 2010 部署助理](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Exchange 2013 部署助理](https://go.microsoft.com/fwlink/p/?linkid=277105)

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

