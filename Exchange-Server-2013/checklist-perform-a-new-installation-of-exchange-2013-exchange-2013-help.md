---
title: '检查表：执行 Exchange 2013 的新安装: Exchange 2013 Help'
TOCTitle: 检查表：执行 Exchange 2013 的新安装
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50491964
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 检查表：执行 Exchange 2013 的新安装

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

使用此检查表部署 Microsoft Exchange Server 2013。在开始使用此检查表之前，请确保您熟悉以下内容中介绍的概念：

  - [规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [部署安全性核对清单](deployment-security-checklist-exchange-2013-help.md)

该检查表提供了针对典型情况的指导，因此是一个通用的检查表。

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


## Exchange 2013 的新安装检查表


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
<td><p>1. 阅读发行说明。</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 发行说明</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. 验证系统要求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. 确认先决条件步骤已完成。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. 配置非连续命名空间。</p>
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
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">非连续命名空间应用场景</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. 安装邮箱服务器角色。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. 安装客户端访问服务器角色。</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. 安装边缘传输服务器角色。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此为可选步骤。只有当您想安装边缘传输服务器时，才是必需步骤。有关详细信息，请参阅<a href="edge-transport-servers-exchange-2013-help.md">边缘传输服务器</a>。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013 边缘传输角色</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. 创建 EdgeSync 订阅。</p>
<p>此为可选步骤。只有当您已安装边缘传输服务器且想在边缘传输服务器和集线器传输服务器之间配置 EdgeSync 订阅时，才是必需步骤。有关详细信息，请参阅<a href="edge-subscriptions-exchange-2013-help.md">边缘订阅</a>。</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">配置通过所订阅的边缘传输服务器的 Internet 邮件流</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 配置传输。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 添加其他接受域。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 配置电子邮件地址策略。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. 在虚拟目录上配置设置，包括脱机通讯簿、Exchange Web 服务、Exchange 管理中心 (EAC)、Outlook Web App 和 Exchange ActiveSync 虚拟目录。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要使用 Exchange Web 服务、Outlook Anywhere 或脱机通讯簿，此步骤是必需的。如果需要更改 EAC、Outlook Web App 或 Exchange ActiveSync 的任何默认设置，可能也需要此步骤。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. 在客户端访问服务器上添加数字证书。</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. 配置统一消息。</p>
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
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">部署语音邮件和 UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 配置其他统一消息和 Lync Server 设置。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此步骤是可选的。只有当已经在组织中配置了统一消息，且希望将其与 Lync Server 集成时，才需要此步骤。</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">部署 Exchange 2013 UM 和 Lync Server 概述</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. 安装后任务。</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 安装后任务</a></p></td>
</tr>
</tbody>
</table>

