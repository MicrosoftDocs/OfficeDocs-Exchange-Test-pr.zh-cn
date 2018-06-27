---
title: '配置一个完全限定的域名称: Exchange Online Help'
TOCTitle: 配置一个完全限定的域名称
ms:assetid: af093f87-59b7-44a8-a9a2-8f17f0cc7db8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423553(v=EXCHG.150)
ms:contentKeyID: 50491301
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置一个完全限定的域名称

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-09_

您可以配置统一邮件 (UM) IP 网关的 IP 地址或完全合格的域名称 (FQDN)。创建 UM IP 网关时，您必须定义的 IP 地址或配置上的 VoIP 网关，IP PBX 或会话边框控制器 (SBC) 所使用的 FQDN。创建 UM IP 网关之后，可以更改的 IP 地址或 FQDN。

如果您创建使用 FQDN 的 UM IP 网关，必须在您的 DNS 正向查找区域中创建相应的主机 (A) 记录。如果您创建 UM IP 网关使用 FQDN，并更改 DNS 配置 UM IP 网关，您必须禁用然后再启用 UM IP 网关，以确保其配置信息已正确更新。

如果您想要使用相互 UM IP 网关和拨号计划中任何一种操作系统之间的传输层安全性 (相互 TLS) SIP 安全或安全模式下，您必须使用 FQDN 配置的 UM IP 网关。您还必须配置侦听端口 5061 并验证 VoIP 网关，IP PBX 或 SBC 也配置为侦听端口 5061 上相互 TLS 请求。要配置的 UM IP 网关，请运行下面的命令 ︰ `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

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


## 您想执行什么操作？

## 使用 EAC 配置 FQDN

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，选择要修改的 UM IP 网关，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM IP 网关\&quot;页面的\&quot;地址\&quot;中，为 VoIP 网关、为 SIP 启用的 PBX、IP PBX 或 SBC 输入 FQDN。

3.  单击\&quot;保存\&quot;。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果在 UM IP 网关上使用 FQDN（而不是 IP 地址），请验证是否已创建正确的 DNS 记录。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序配置 FQDN

本示例为名为 `MyUMIPGateway` 的 UM IP 网关配置了名为 voipgateway.contoso.com 的 FQDN。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com

本示例为名为 `MySBC` 的 UM IP 的网关配置了 sbc.contoso.com 的 FQDN，并在 TCP 端口 5061 上侦听 SIP 请求。

    Set-UMIPGateway -Identity MySBC -Address sbc.contoso.com -Port 5061

