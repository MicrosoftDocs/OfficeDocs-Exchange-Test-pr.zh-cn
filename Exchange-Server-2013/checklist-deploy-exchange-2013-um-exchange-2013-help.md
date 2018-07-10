---
title: '检查表：部署 Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 检查表：部署 Exchange 2013 UM
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52061501
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 检查表：部署 Exchange 2013 UM

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

使用检查列表可帮助您在组织中安装和部署统一消息 (UM)。

开始使用此检查表之前，请务必熟悉以下章节中的概念：

  - [统一消息](unified-messaging-exchange-2013-help.md)

  - [新的语音邮件功能](new-voice-mail-features-exchange-2013-help.md)

  - [统一消息规划](planning-for-unified-messaging-exchange-2013-help.md)

有关如何部署 UM 和 Microsoft Lync Server 的分布指导，请参阅[检查表：将 Exchange 2013 UM 与 Lync Server 集成](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)。

## 用于部署统一消息的检查表


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>完成？</th>
<th>任务</th>
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
<td><p> </p></td>
<td><p>验证是否符合安装的先决条件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>安装所需的客户端访问服务器和邮箱服务器。</p>

> [!warning]
> 在配置 VoIP 网关或 IP PBX 以将 UM SIP 和 RTP 通信发送到 Exchange 2013 客户端访问服务器之前，您应在您的组织内部署至少一个 Exchange 2013 邮箱服务器。

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">使用安装向导安装 Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>验证安装并查看服务器安装日志。</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">验证 Exchange 2013 安装</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>如有需要，安装所需的 UM 语言包。</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">安装 UM 语言包</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>为组织创建所需数量的拨号计划。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">创建 UM 拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>配置拨号计划安全设置。</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">配置 VoIP 安全设置</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>为每个客户端访问服务器和邮箱服务器配置 UM 启动模式。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">在邮箱服务器上配置的启动模式</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">在客户端访问服务器上配置的启动模式</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>配置邮箱服务器上的并发呼叫数。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">在邮箱服务器上配置拨入呼叫的数</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>配置 Outlook Voice Access 号码和其他设置。</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>为统一消息配置出站拨号。</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">使用拨号规则授权通话</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">拨号计划中授权用户的呼叫</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">授权一组用户的呼叫</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>创建所需数量的自动助理。</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">创建 UM 自动助理</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>设置并配置每个 UM 自动助理。</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">设置 UM 自动助理</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>为 UM 创建、导入和启用新的 Exchange 证书，或启用相互信任的第三方证书。此外，导入所有 VoIP 网关、IP PBX 以及 SBC 上的证书。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>重新启动所有 Exchange 服务器上的 Microsoft Exchange 统一消息服务和统一消息呼叫路由器服务，以加载所需的证书。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">停止的 Microsoft Exchange 统一消息服务</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">启动 Microsoft Exchange 统一消息服务</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">停止的 Microsoft Exchange 统一消息呼叫路由器服务</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">启动 Microsoft Exchange 统一消息呼叫路由器服务</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>创建 UM 邮箱策略或配置默认 UM 邮箱策略。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">创建 UM 邮箱策略</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 邮箱策略</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>如果需要，可通过分机号码和 E.164 号码为用户启用统一消息。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">为用户启用语音邮件</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>启用传入传真（可选）。</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">为语音邮件用户启用接收传真功能</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>设置受保护的语音邮件（可选）。</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">保护语音邮件</a></p></td>
</tr>
</tbody>
</table>


返回顶部

