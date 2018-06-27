---
title: '允许或阻止客户端访问服务器上的电话应答: Exchange 2013 Help'
TOCTitle: 允许或阻止客户端访问服务器上的电话应答
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50556606
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 允许或阻止客户端访问服务器上的电话应答

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-18_

可以允许客户端访问服务器上的 Microsoft Exchange 统一消息呼叫路由器服务应答新的呼叫，也可以阻止其这样做。默认情况下，客户端访问服务器在安装后就处于启用状态。在设置客户端访问服务器以接受传入的语音、传真、自动助理和 Outlook Voice Access 呼叫时，可使用 **Set-ServerComponentState** cmdlet。

通过配置客户端访问服务器的维护模式，可以让服务器退出服务。对于客户端访问服务器，退出服务意味着该服务器将不接受来自 VoIP 网关、IP PBX、支持 SIP 的 PBX 或者会话边界控制器 (SBC) 的任何传入呼叫。

在 Exchange 2007 和 Exchange 2010 中，有一个状态参数可用于控制统一消息服务器的运行状态。在 Exchange 2013 中，没有可用于在客户端访问服务器上的 **Set-UMCallRouterSettings** cmdlet 上实现该目的状态参数。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>除非要将 UM 与 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 集成，否则不需要将客户端访问服务器和邮箱服务器添加到 UM 拨号计划上就能处理统一消息的呼叫。默认情况下，组织中的所有客户端访问服务器和邮箱服务器都可用于应答传入呼叫。</td>
</tr>
</tbody>
</table>


有关与客户端访问服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“Exchange Server 配置设置”条目。

  - 验证客户端访问服务器是安装在与邮箱服务器相同的计算机上还是安装在单独的计算机上。

  - 如果要将客户端访问服务器置于维护模式，请验证客户端访问阵列中是否有足够的正常容量使服务器能够退出服务。

  - 在将服务器退出维护模式之前，请验证服务器的运行状况并确保其已准备好进入服务。

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


## 使用命令行管理程序可允许或阻止客户端访问服务器上的呼叫应答

此示例使客户端访问服务器 `UMCallRouter-05x.contoso.com` 能够应答从 VoIP 网关、IP PBX、支持 SIP 的 PBX 和 SBC 传入的语音、传真、自动助理和 Outlook Voice Access 呼叫，并将更改写入 UMCallRouter-05x 服务器上的注册表。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

此示例阻止客户端访问服务器 `UMCallRouter-05x.contoso.com` 应答从 VoIP 网关、IP PBX、支持 SIP 的 PBX 和 SBC 传入的语音、传真、自动助理和 Outlook Voice Access 呼叫，并仅将更改写入 Active Directory。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

