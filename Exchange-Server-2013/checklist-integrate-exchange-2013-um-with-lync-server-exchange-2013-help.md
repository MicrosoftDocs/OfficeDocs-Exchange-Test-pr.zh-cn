---
title: '检查表：将 Exchange 2013 UM 与 Lync Server 集成: Exchange 2013 Help'
TOCTitle: 检查表：将 Exchange 2013 UM 与 Lync Server 集成
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52061499
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 检查表：将 Exchange 2013 UM 与 Lync Server 集成

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

使用此检查表安装和部署统一消息 (UM) 和 Microsoft Lync Server 2013。在此主题中，“Lync Server”也指 Lync Server 2010。但是，Microsoft Office Communications Server 2007 R2 也能与统一消息一起部署。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td></td>
</tr>
</tbody>
</table>


开始使用此检查表之前，请务必熟悉以下章节中的概念：

  - [部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [与 Office Communications Server 2007 R2 和 Lync Server 共存](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

有关如何执行 Lync Server 必须完成的任务的详细信息，请参阅 [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752)。

## 部署 Microsoft Lync Server 和统一消息的检查表


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
<td><p>在安装 Exchange Server 2013 之前，请查看系统要求。</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>验证是否符合安装的先决条件。</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>查看将 Microsoft Lync Server 2013 和 Microsoft Exchange Server 2013 集成的先决条件。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">集成 Microsoft Lync Server 2013 和 Microsoft Exchange Server 2013 的先决条件</a></p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013、Lync Server 2010 和 2013 需要 Unified Communications Managed API (UCMA) 4.0 Runtime，在安装期间也会安装它。若要下载和查看关于 UCMA 4.0 的信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</a></td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>安装所需的客户端访问服务器和邮箱服务器。</p></td>
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
<td><p>创建组织所需的 SIP URI 拨号计划数。</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">创建 UM 拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>配置拨号计划安全设置。</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">配置 VoIP 安全设置</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>配置邮箱服务器上的并发呼叫数。</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">在邮箱服务器上配置拨入呼叫的数</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>配置 Outlook Voice Access 号码和其他设置。</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">管理 UM 拨号计划</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>将所有客户端访问服务器和邮箱服务器添加到每个 SIP URI 拨号计划。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>为统一消息配置出站拨号。允许 SIP URI 拨号计划和与拨号计划相关的 UM 邮箱策略上的任何呼叫。</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">拨号计划中授权用户的呼叫</a></p>
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
<td><p> </p></td>
<td><p>为 UM 创建、导入和启用新的 Exchange 证书，或启用相互信任的第三方证书。</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">将邮箱服务器和客户端访问服务器添加到 SIP URI 的拨号计划</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>将每个客户端访问服务器和邮箱服务器的 UM 启动模式配置为双协议模式或 TLS。</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">在邮箱服务器上配置的启动模式</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">在客户端访问服务器上配置的启动模式</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>重新启动所有 Exchange 服务器上的 Microsoft Exchange 统一消息服务和统一消息呼叫路由器服务，以加载所需的证书。</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">停止的 Microsoft Exchange 统一消息服务</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">启动 Microsoft Exchange 统一消息服务</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">停止的 Microsoft Exchange 统一消息呼叫路由器服务</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">启动 Microsoft Exchange 统一消息呼叫路由器服务</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>创建 UM 邮箱策略或配置默认 UM 邮箱策略。</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">创建 UM 邮箱策略</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">管理 UM 邮箱策略</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>为具有 SIP 地址的统一消息启用用户，并关联到 SIP URI 拨号计划。</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">为用户启用语音邮件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>检查 Lync Server 2013 计划文档。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">规划</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>安装并部署 Lync Server 2013。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">部署 Lync Server 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>导入互信内部 PKI 或在 Exchange UM 服务器上导入的第三方证书。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">为服务器配置证书</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">在运行 Microsoft Exchange Server 统一消息的服务器上配置证书</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>如有需要，启动服务器上的 Lync 服务，以下载证书。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">启动服务器上的服务</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>打开 Exchange 命令行管理程序，运行 %Program Files%\Microsoft\Exchange Server\V15\Scripts 文件夹中的 exchucutil.ps1 脚本。</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">将 UM 配置为与 Lync Server 配合使用</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>查看企业语音的要求。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">企业语音的软件先决条件</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">企业语音的安全和配置先决条件</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>部署和配置媒体网关或中介服务器，并定义同级。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">部署中介服务器并定义同级</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>在中介服务器和一个或多个同级之间配置 Trunk，以提供公共交换电话网络 (PSTN) 连接。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">配置 Trunk</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>创建和配置 Lync 拨号计划，并创建、定义和关联规范化规则。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">配置 Trunk</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>配置语音策略并定义电话用法和出站呼叫路由。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">配置语音策略、PSTN 使用记录和语音路由</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>运行 Exchange 集成实用程序 (ocsumutil.exe)，为 Outlook Voice Access 和自动助理创建联系人对象。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">在 Microsoft Exchange Server 上将 Lync Server 2013 配置为与统一信息一起使用</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>定义、部署和配置任何所需的高级企业语音功能。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">部署高级企业语音功能</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>为用户启用企业语音。输入线路 URI，分配语音策略和 Lync 拨号计划。</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">为用户启用企业语音</a></p></td>
</tr>
</tbody>
</table>

