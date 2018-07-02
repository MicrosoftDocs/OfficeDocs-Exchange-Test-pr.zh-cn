---
title: '从 Exchange 2007 升级到 Exchange 2013: Exchange 2013 Help'
TOCTitle: 从 Exchange 2007 升级到 Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51408252
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 从 Exchange 2007 升级到 Exchange 2013

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

Microsoft Exchange Server 2010 和 Exchange Server 2007 有多个服务器角色：客户端访问、邮箱、集线器传输、统一消息和边缘传输。使用 Exchange Server 2013，我们将服务器角色的数量从五个减少到了三个：客户端访问、邮箱和边缘传输。统一消息现在被认为是 Exchange 2013 中提供的语音相关功能的组件或子功能。（有关该更改的详细信息，请参阅[Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)中的“Exchange 2013 体系结构”。）

将现有 Exchange 2007 组织升级至 Exchange 2013 时，会有一段时间，Exchange 2007 和 Exchange 2013 在组织中共存。您可以无限期地维护此模式，也可以通过将所有资源从 Exchange 2013 移动到 Exchange 2007，然后停止使用 Exchange 2013 服务器，立即完成到 Exchange 2007 的升级。如果符合下列条件，则有共存方案：

  - 在现有 Exchange 2013 组织中部署 Exchange。

  - 有多个 Microsoft Exchange 版本为组织提供邮件服务。

您无法将现有的 Exchange 2003 组织直接升级到 Exchange 2013。必须先将 Exchange 2003 组织升级到 Exchange 2007 或 Exchange 2010 组织，然后再将 Exchange 2007 或 Exchange 2010 组织升级到 Exchange 2013。建议您将组织从 Exchange 2003 升级到 Exchange 2010，然后从 Exchange 2010 升级到 Exchange 2013。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在升级到 Exchange 2013 之前，需要从组织中删除 Exchange 2003 的所有实例。</td>
</tr>
</tbody>
</table>


可以将你的所有 Exchange 2003 邮箱都迁移到 Exchange Online。有关此方法的详细信息，请参阅[将多个电子邮件帐户迁移到 Office 365 的方法](https://go.microsoft.com/fwlink/p/?linkid=524030)。

下表列出了一些支持 Exchange 2013 与早期版本的 Exchange 共存的方案。

### Exchange 2013 和早期版本的 Exchange Server 共存

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 版本</th>
<th>Exchange 组织共存</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 和更早版本</p></td>
<td><p>不支持</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>1组织中所有 Exchange 2007 服务器（包括边缘传输服务器）上的 Exchange 2007 Service Pack 3 (SP3) 更新汇总 10。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 累计更新 2 (CU2) 或更高版本。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>2组织中所有 Exchange 2010 服务器（包括边缘传输服务器）上的 Exchange 2010 SP3。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 CU2 或更高版本。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2010 和 Exchange 2007 的混合组织</p></td>
<td><p>支持以下最低 Exchange 版本：</p>
<ul>
<li><p>1组织中所有 Exchange 2007 服务器（包括边缘传输服务器）上的 Exchange 2007 SP3 更新汇总 10。</p></li>
<li><p>2组织中所有 Exchange 2010 服务器（包括边缘传输服务器）上的 Exchange 2010 SP3。</p></li>
<li><p>组织中所有 Exchange 2013 服务器上的 Exchange 2013 CU2 或更高版本。</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   如果您想要在 Exchange 2007 集线器传输服务器和 Exchange2013 SP1 边缘传输服务器之间创建 EdgeSync 订阅，您需要在 Exchange 2007 集线器传输服务器上安装 Exchange 2007 SP3 更新汇总 13 或更高版本。

2   如果您想要在 Exchange 2010 集线器传输服务器和 Exchange 2013 SP1 边缘传输服务器之间创建 EdgeSync 订阅，您需要在 Exchange 2010 集线器传输服务器上安装 Exchange 2010 SP3 更新汇总 5 或更高版本。

## Exchange 2013 和 Exchange 2007 与 Exchange 2010 的混合模式共存

如果您已在 Active Directory 站点中安装 Exchange 2010 和 Exchange 2007，请按照 Exchange 2010 与 Exchange 2007 的升级说明执行操作，并执行这二者所需的升级步骤。

## 升级过程概述

为了帮助您大致了解从 Exchange 2007 到 Exchange 2013 的升级过程，我们在下表中收集了与各项关键任务相关的资源。有关特定分步指导，请参阅[检查表：从 Exchange 2007 升级](checklist-upgrade-from-exchange-2007-exchange-2013-help.md)。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>任务</th>
<th>主题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>了解 Exchange 2013 角色和组件</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的新增功能</a></p>
<p><a href="client-access-server-exchange-2013-help.md">客户端访问服务器</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">邮箱服务器</a></p>
<p><a href="mail-flow-exchange-2013-help.md">邮件流</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">统一消息</a></p></td>
</tr>
<tr class="even">
<td><p>安装 Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013 边缘传输角色</a>（可选）</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">验证 Exchange 2013 安装</a></p></td>
</tr>
<tr class="odd">
<td><p>在客户端访问服务器上添加数字证书</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 客户端访问服务器配置</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">数字证书和 SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">创建数字证书请求</a></p></td>
</tr>
<tr class="even">
<td><p>配置 Exchange 相关虚拟目录</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Exchange 虚拟目录的默认设置</a></p></td>
</tr>
<tr class="odd">
<td><p>从 Exchange 2010 中移动邮箱</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的邮箱移动</a></p></td>
</tr>
<tr class="even">
<td><p>配置传输组件</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>（仅当安装了边缘传输服务器时才需执行此步骤）</p>
<p><a href="mail-routing-exchange-2013-help.md">邮件路由</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">卷影冗余</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">管理员的送达报告</a></p></td>
</tr>
<tr class="odd">
<td><p>配置并部署 UM</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">统一消息规划</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">部署语音邮件和 UM</a></p></td>
</tr>
</tbody>
</table>

