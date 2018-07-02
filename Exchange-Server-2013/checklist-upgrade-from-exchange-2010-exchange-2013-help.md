﻿---
title: '检查表：从 Exchange 2010 升级: Exchange 2013 Help'
TOCTitle: 检查表：从 Exchange 2010 升级
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51408190
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 检查表：从 Exchange 2010 升级

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

使用此检查列表可从 Microsoft Exchange 2010 升级到 Exchange 2013。在开始使用此检查表之前，请确保您熟悉以下内容中介绍的概念：

  - [规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)

该检查表提供了针对典型升级情况的指导，因此是一个通用的检查表。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange Server 部署助理将为您提供有关如何部署 Exchange Server 的自定义分步指导。部署助理可帮助您部署 Exchange Server 2013 的全新安装，将早期版本升级到 Exchange 2013，或配置 Exchange 2013 和 Exchange Online 的混合部署。若要了解详细信息，请参阅 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。</td>
</tr>
</tbody>
</table>


## 从 Exchange 2010 升级到 Exchange 2013 的检查表


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>完成？</p></td>
<td><p>任务</p></td>
<td><p>主题</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. 阅读发行说明</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 发行说明</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. 验证系统要求</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. 确认先决条件步骤是否已完成</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">部署安全性核对清单</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. 配置脱节命名空间</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步骤是可选的。仅当组织运行脱节命名空间时，才需执行此步骤。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">为非连续命名空间配置 DNS 后缀搜索列表</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. 为所有 Exchange 2010 邮箱数据库选择脱机通讯簿</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> in<a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">管理 Exchange 2013 中的邮箱数据库</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. 安装 Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013 边缘传输角色</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">验证 Exchange 2013 安装</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. 创建 Exchange 2013 邮箱</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">创建用户邮箱</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. 配置 Exchange 相关虚拟目录</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要使用 Exchange Web 服务、Outlook Anywhere 或脱机通讯簿，此步骤是必需的。当您需要更改 Exchange 控制面板、Microsoft OfficeOutlook Web App 或 Exchange ActiveSync 的任何默认设置时，也可能需要此步骤。<br />
</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 客户端访问服务器配置</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 在客户端访问服务器上添加数字证书</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">数字证书和 SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 移动仲裁邮箱</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">将 Exchange 2010 系统邮箱移到 Exchange 2013 中</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 配置统一消息</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步骤是可选的。仅当要在组织中使用统一消息时，才需执行此步骤。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">将 Exchange 2010 UM 升级到 Exchange 2013 UM</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. 配置边缘传输服务器</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步骤是可选的。只有当组织使用的是边缘传输服务器时，才有必要。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">配置通过所订阅的边缘传输服务器的 Internet 邮件流</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. 启用和配置 Outlook Anywhere</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook 无处不在</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. 配置服务连接点</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 客户端访问服务器配置</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 配置 DNS 记录</p></td>
<td><p><a href="https://technet.microsoft.com/zh-cn/library/dn307232(v=exchg.150)">配置 Exchange 2010 多个服务器安装的 DNS 记录</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. 将邮箱从 Exchange 2010 移动到 Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的邮箱移动</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. 将公用文件夹数据从 Exchange 2013 移动到 Exchange 2013</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">公用文件夹</a></p>
<p><a href="https://technet.microsoft.com/zh-cn/library/jj150486(v=exchg.150)">使用串行迁移将公用文件夹从以前版本迁移到 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. 安装后任务</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 安装后任务</a></p></td>
</tr>
</tbody>
</table>

