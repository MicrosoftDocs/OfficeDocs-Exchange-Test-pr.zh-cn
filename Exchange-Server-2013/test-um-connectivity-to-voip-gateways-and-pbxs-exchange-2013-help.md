---
title: '测试 VoIP 网关和 PBX 的 UM 连接性: Exchange 2013 Help'
TOCTitle: 测试 VoIP 网关和 PBX 的 UM 连接性
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56271411
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 测试 VoIP 网关和 PBX 的 UM 连接性

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2014-09-17_

您可以测试统一消息 (UM) 及连接的相关电话设备的运行情况。执行下列步骤时，客户端访问服务器和邮箱服务器会测试语音邮件系统的完全端到端运行情况。这包括连接到客户端访问和邮箱服务器的电话组件，包括 VoIP 网关、专用交换机 (PBX)、IP PBX 和电缆。

有关与故障排除 UM 相关的其他管理任务，请参阅[UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;邮箱服务器（UM 服务）\&quot;和\&quot;客户端访问服务器（UM 呼叫路由器服务）\&quot;条目。

  - 若要执行以下过程，必须使用作为本地管理员组成员的帐户登录邮箱服务器。

  - 验证邮箱服务器是安装在与客户端访问服务器相同的计算机中，还是安装在单独的计算机中。

  - 验证客户端访问服务器是安装在与邮箱服务器相同的计算机上，还是安装在单独的计算机中。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序测试统一消息和电话组件的运行情况

此示例将测试 UM IP 网关在 TCP 端口 5060 上侦听传入 SIP 请求的能力。

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

本示例测试本地邮箱服务器是否可以使用不安全的 TCP 连接（而不是安全的相互 TLS 连接），使用电话号码 56780 通过名为 `MyUMIPGateway` 的 UM IP 网关发出呼叫。

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

本示例使用 SIP URI 测试拨号计划上的 Outlook Voice Access 号码。本示例可用于包括 Lync Server 在内的环境中。

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以将 <code>-Timeout</code> 参数设置为小于 5 秒的值。但是，建议始终将此参数的值配置为大于或等于 5 秒。如果在命令行语法中指定了 <code>­UMIPGateway</code> 参数，那么请使用模式 2。</td>
</tr>
</tbody>
</table>

