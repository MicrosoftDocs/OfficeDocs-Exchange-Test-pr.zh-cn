---
title: '允许或禁止呼叫应答在邮箱服务器上: Exchange 2013 Help'
TOCTitle: 允许或禁止呼叫应答在邮箱服务器上
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50556562
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许或禁止呼叫应答在邮箱服务器上

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-18_

以回答新的呼叫或禁止它这样做的邮箱服务器上，您可以允许 Microsoft Exchange 统一消息服务。默认情况下，邮箱服务器处于启用状态安装后。在设置邮箱服务器接受传入的语音、 传真、 自动助理和 Outlook Voice Access 调用时，您可以使用**Set-ServerComponentState** cmdlet。

为邮箱服务器配置维护模式，可以使服务器停止服务。邮箱服务器，出服务意味着服务器不承载任何活动的数据库，所有传输队列都是空的并且服务器将不接受任何来电从客户端访问服务器、 VoIP 网关，IP Pbx、 SIP 启用 Pbx 或会话边框控制器 (SBCs)。

在Exchange 2007和Exchange 2010中，没有一个状态参数，可用于控制统一消息服务器的运行状态。在Exchange 2013，无状态参数是可为该目的**Set-UMService** cmdlet 的邮箱服务器上。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它不被必需之前他们可以处理调用为统一消息，除在集成 UM 和 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 时，客户端访问和邮箱服务器将添加到 UM 拨号计划。默认情况下，组织中的所有客户端访问和邮箱服务器都可以应答传入呼叫。</td>
</tr>
</tbody>
</table>


有关与邮箱服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;Exchange Server 配置设置\&quot;条目。

  - 验证邮箱服务器是安装在与客户端访问服务器相同的计算机中，还是安装在单独的计算机中。

  - 如果将邮箱服务器置于维护模式，请验证所有数据库副本是否具有足够的冗余允许服务器停止工作。

  - 将服务器退出维护模式之前，请验证服务器的运行状况，并确保它已准备就绪，可以投入正常工作。

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


## 使用命令行管理程序允许或阻止邮箱服务器中的呼叫应答

本示例允许邮箱服务器 `UMMBXr-05x.contoso.com` 应答来自 VoIP 网关、IP PBX、启用了 SIP 的 PBX 和 SBC 的传入语音、传真、自动助理和 Outlook Voice Access 呼叫，允许将所做的更改写入 UMMBX-05x 服务器的注册表中。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

本示例阻止邮箱服务器 `UMMBX-05x.contoso.com` 应答来自 VoIP 网关、IP PBX、启用了 SIP 的 PBX 和 SBC 的传入语音、传真、自动助理和 Outlook Voice Access 呼叫，并且仅将所做的更改写入 Active Directory 中。

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

