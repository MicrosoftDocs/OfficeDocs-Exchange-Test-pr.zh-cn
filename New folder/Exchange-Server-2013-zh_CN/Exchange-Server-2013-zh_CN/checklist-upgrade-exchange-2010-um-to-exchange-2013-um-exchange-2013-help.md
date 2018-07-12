---
title: '检查表：将 Exchange 2010 UM 升级到 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 检查表：将 Exchange 2010 UM 升级到 Exchange 2013 UM
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54652280
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 检查表：将 Exchange 2010 UM 升级到 Exchange 2013 UM

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

使用此检查表可帮助将 Exchange 2010 统一消息 (UM) 升级到 Exchange 2013 UM。请确保在将 Exchange 2010 组织和 UM 部署升级到 Exchange 2013 时参考此信息。有关升级到 Exchange 2013 UM 的分步说明，请参阅[将 Exchange 2010 UM 升级到 Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)。

开始使用此检查表之前，请务必熟悉以下章节中的概念：

  - [统一消息规划](planning-for-unified-messaging-exchange-2013-help.md)

  - [与 UM 电话系统集成](telephone-system-integration-with-um-exchange-2013-help.md)

  - [连接到电话网络的语音邮件系统](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)

有关如何从 Exchange 2007 UM 升级到 Exchange 2013 UM 的分步指南，请参阅[升级到 Exchange 2013 UM 的 Exchange 2007 UM](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md)。

## 将 Exchange 2010 UM 升级到 Exchange 2013 UM 的检查表


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成？</th>
<th>Tasks</th>
<th>主题</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>部署和配置电话组件。</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">将 UM 连接到电话系统</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>在安装 Exchange 2013 之前，检查系统要求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>验证是否符合安装的先决条件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>安装所需的客户端访问服务器和邮箱服务器。</p>

> [!warning]
> 在配置 VoIP 网关或 IP PBX 以将 UM SIP 和 RTP 通信发送到 Exchange 2013 客户端访问服务器之前，您应在组织内部署至少一个 Exchange 2013 邮箱服务器。

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>验证安装并查看服务器安装日志。</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">验证 Exchange 2013 安装</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>如有需要，安装所需的 UM 语言包。</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">安装 UM 语言包</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>将用于 UM 自定义提示的 Exchange 2010 系统邮箱移动到 Exchange 2013。</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的邮箱移动</a></p>

> [!NOTE]
> 如果系统邮箱已移动，您仍可使用<a href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">导入和导出自定义问候语、通知、菜单和提示</a>从 Exchange 2010 手动导入/导出自定义提示。

</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>导出和导入证书。</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">为 UM 部署证书</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在所有 Exchange 2013 客户端访问服务器上配置 UM 启动模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">在客户端访问服务器上配置的启动模式</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>在所有 Exchange 2013 邮箱服务器上配置 UM 启动模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">在邮箱服务器上配置的启动模式</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>创建或配置现有 UM 拨号计划。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">创建 UM 拨号计划</a></p>
<p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>创建或配置现有 UM IP 网关。</p></td>
<td><p><a href="create-a-um-ip-gateway-exchange-2013-help.md">创建 UM IP 网关</a></p>
<p><a href="manage-a-um-ip-gateway-exchange-2013-help.md">管理 UM IP 网关</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>创建 UM 智能寻线。</p></td>
<td><p><a href="create-a-um-hunt-group-exchange-2013-help.md">创建 UM 智能寻线</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>创建或配置 UM 自动助理。</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">创建 UM 自动助理</a></p>
<p><a href="manage-a-um-auto-attendant-exchange-2013-help.md">管理 UM 自动助理</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>创建或配置 UM 邮箱策略。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">创建 UM 邮箱策略</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 邮箱策略</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>将启用 UM 的现有邮箱移动到 Exchange 2013。</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 中的邮箱移动</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>为新用户启用 UM 或为启用 UM 的现有用户配置设置。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">为用户启用语音邮件</a></p>
<p><a href="manage-voice-mail-settings-for-a-user-exchange-2013-help.md">管理用户的语音邮件设置</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>配置 VoIP 网关、IP PBX 和启用 SIP 的 PBX 以便将所有传入呼叫发送到 Exchange 2013 客户端访问服务器。</p></td>
<td><p><a href="configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md">支持的 VoIP 网关、IP PBX 和 PBX 的配置说明</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">将 VoIP 网关、IP PBX 或会话边界控制器与 UM 连接</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在 Exchange 2010 UM 服务器上禁用呼叫应答。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">禁用统一邮件在 Exchange 2010</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>删除拨号计划中的 Exchange 2010 UM 服务器。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">删除 UM 服务器从拨号计划</a></p></td>
</tr>
</tbody>
</table>

