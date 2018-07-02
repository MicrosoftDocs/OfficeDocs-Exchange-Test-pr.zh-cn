---
title: '允许邮件等待指示器: Exchange 2013 Help'
TOCTitle: 允许邮件等待指示器
ms:assetid: 57fb439e-8208-499f-a20b-814677843a8c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298001(v=EXCHG.150)
ms:contentKeyID: 54652282
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许邮件等待指示器

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-03-09_

邮件等待指示器 (MWI) 这一功能可以在大多数旧版语音邮件系统中找到。它会提醒客户新的或未听取的语音邮件。此功能最常见的形式是点亮用户电话上的指示灯，以表示存在新的或未听取的语音邮件。

**目录**

概述

The Mailbox server's role in MWI

MWI SIP NOTIFY messages

MWI resilience

MWI administration

Text message (SMS) notifications for voice mail messages and missed calls

## 概述

MWI 通知可以包括任何指示存在新的或未听取的语音邮件的机制。邮件可以是新的电子邮件，也可以是被标记为未听取的邮件。MWI 通知可能采用以下任何形式：

  - 从 Microsoft Outlook 或 Outlook Web App 查看的新语音邮件。

  - 发送到配置为接收短信的移动电话的文本或短消息服务 (SMS) 消息。

  - 从 Exchange 统一消息 (UM) 发出的出站呼叫。

  - 电话上的灯。

  - 特殊拨号音。

  - 电话显示屏幕上的图标或按钮。

  - 软件应用程序中突出显示的通知。

在统一消息中，用户的语音邮件存储在他们的邮箱中。可以从使用 Outlook Voice Access 的电话、从使用 Outlook 或 Outlook Web App 的台式或便携计算机以及从移动电话客户端访问该邮箱。当用户接收到一封新语音邮件时，该邮件会出现在用户的\&quot;语音邮件\&quot;搜索文件夹中。如果使用 Outlook 或 Outlook Web App 访问该语音邮件，则会在该语音邮件中包含一封电子邮件。

在组织中部署之前版本的 UM 时，通过使用第三方解决方案或应用程序来支持传统 VoIP 网关环境或 IP PBX 环境中的 MWI，或者将其包含在 Exchange UM 中，作为它的一部分。在 Exchange 2010 或更高版本中，当 UM 和 Microsoft Lync Server 一起部署时，也支持 MWI。Lync Server 使用的 MWI 通知机制取决于由启用了 Enterprise Voice 和 UM 的用户所使用的基于 VoIP 的电话类型，并且可以位于以下任何一项中：

  - 电话

  - 电话显示屏幕

  - 拨号盘按钮

默认情况下，会为所有启用 UM 的用户打开 MWI。它通过 UM 邮箱策略中的设置或已创建并链接到 UM 拨号计划的 UM IP 网关中的设置进行控制。MWI 还适用于受保护的语音邮件。

为了在包含 VoIP 网关、IP PBX 或启用 SIP 的 PBX 的传统电话环境中实现 MWI，运行 Microsoft Exchange 统一消息服务的邮箱服务器会向 *SIP 对等方*发送 MWI 会话初始协议 (SIP) 通知消息，该对等放可以是 IP PBX、与旧版 PBX 一起使用的 VoIP 网关、启用 SIP 的 PBX，或者如果您已部署 Lync Server，Lync 服务器也会被认为是 SIP 对等方。IP PBX 或 PBX 会点亮桌面电话上的灯以通知用户有新的或未听取的语音邮件。

呼叫者可以通过两种方式留下语音邮件：使用呼叫应答和 Outlook Voice Access。使用呼叫应答，邮箱服务器会答复传入呼叫并允许呼叫者为用户留下语音邮件。使用 Outlook Voice Access，如果呼叫者呼叫 Outlook Voice Access 号码，则可以使用菜单系统为启用 UM 的用户留下语音邮件。

返回顶部

## MWI 中的邮箱服务器角色

当呼叫者呼叫启用 UM 的用户但该用户没有答复电话时，邮箱服务器上的 Microsoft Exchange 统一消息服务会接收 MWI 状态更改信息并使用 SIP 通知消息将通知更改请求发送到 VoIP 网关、IP PBX 或启用 SIP 的 PBX。通知更改包括以下信息：

  - 邮件等待指示器已启用（是或否）。

  - 新语音邮件或标记为未听取的语音邮件数。

  - 旧语音邮件或标记为已听取的语音邮件数。

  - 新紧急语音邮件或标记为未听取的紧急语音邮件数。

  - 旧紧急语音邮件或标记为已听取的紧急语音邮件数。

  - 主 UM 拨号计划中的主分机号码。

  - 要用于 SIP 通知消息的 SIP 对等方的 IP 地址或完全限定域名 (FQDN)。

  - UM 拨号计划的安全类型（不安全、SIP 安全或安全）。将使用这些信息确定与 VoIP 网关或 IP PBX 的连接必须为 TCP 上的 SIP 还是 TLS 上的 SIP。MWI SIP 通知支持传输层安全性 (TLS)。

邮箱服务器使用传入呼叫标头中的转换信息确定启用 UM 的用户的分机号码或电话号码。分机号码或电话号码确定后，邮箱服务器会向 SIP 对等方发送请求。然后，SIP 对等方会更改 MWI 状态并在用户的电话上打开通知。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管 PBX 中断应该十分少见，但是 UM 会至少每 12 个小时自动刷新一次每个邮箱的 MWI 状态。无法强制进行刷新，但是如果 PBX 或 IP PBX 断开电源且所有 MWI 指示灯熄灭，则所有指示灯会在 6 小时内还原为正确状态。</td>
</tr>
</tbody>
</table>


返回顶部

## MWI SIP 通知消息

MWI 通知使用 SIP 通知消息与 SIP 对等方通信。MWI 状态更改信息包括在 SIP 通知消息中，指示 MWI 通知是否会发送给用户。只要 MWI 状态更改，邮箱助理就会将此信息发送给在邮箱服务器上运行的 Microsoft Exchange 统一消息服务。在统一消息服务接收到此信息之后，它会分析消息以获取目标 SIP 对等方以及 MWI 状态更改信息。它随后会形成 SIP 通知消息并在消息正文中包含 MWI 状态更改信息，然后将这些信息发送给 SIP 对等方。

MWI 基于 RFC 3842。RFC 3842 声明必须将 SIP 事件通知用于邮件等待通知。MWI 基于 SIP 模型，由统一消息系统中的终结点驱动。获取 MWI 信息的 SIP 终结点（也称为 SIP 对等方）必须将 SIP 订阅消息发送给统一消息服务。服务使用通知消息进行答复，指示已接受订阅。所有 MWI 状态更改信息都会使用嵌入在之前创建的订阅中的通知消息，从统一消息系统传达到 SIP 终结点。发送到 SIP 对等方的 SIP 通知消息的确切语法基于 RFC 3842 中说明的格式。

当邮箱服务器上的统一消息服务向 SIP 对等方发送 MWI 通知消息时，事件标头设置为\&quot;消息汇总\&quot;，指示这是与 MWI 相关的通知消息。\&quot;收件人\&quot;标头字段指示必须为其提供 MWI 服务的 SIP 终结点。订阅状态标头必须设置为\&quot;已终止\&quot;而不是\&quot;活动\&quot;。执行以下操作以响应 SIP 通知消息：

1.  SIP 对等方使用电路交换协议（如 SMDI）将这些信息传达给 PBX。

2.  PBX 通过电路交换协议发送成功消息。

3.  SIP 对等方可以使用以下任一消息进行响应：200 正常（成功）或 480（暂时不可用）。邮箱服务器可以处理这两种响应和其他失败响应。

## 传统电话环境中的 MWI

在传统电话环境中，传入呼叫由 PBX 接收，随后发送给 VoIP 网关，或者由 IP PBX 或启用 SIP 的 PBX 接收。邮箱服务器和邮箱助理用于确定启用 UM 的用户的 MWI 状态。它们负责将 SIP 通知传递回 VoIP 网关和旧版 PBX、IP PBX 或启用 SIP 的 PBX。

在传统电话环境中，呼叫流和 MWI 通知如下所示：

1.  传入呼叫由旧版 PBX 接收，转发到 VoIP 网关，或转发到 IP PBX 或启用 SIP 的 PBX，然后转发到启用 UM 的用户的分机号码。用户未应答，系统提示呼叫者留下语音邮件。

2.  VoIP 网关或 IP PBX 将呼叫提交给运行 Microsoft Exchange 统一消息服务的邮箱服务器。

3.  邮箱服务器执行 LDAP 查询以查找启用 UM 的用户的信息，如用户的分机号码和个人问候语。启用 UM 的用户的问候语会进行播放。

4.  由统一消息服务创建的语音邮件被提交到同一邮箱服务器上的 Microsoft Exchange 传输服务。

5.  邮箱服务器上的传输服务将语音邮件提交到包含用户邮箱的邮箱服务器。邮箱助理接收到有关新语音邮件的 MAPI 事件。

6.  邮箱助理会读取 UM 拨号计划和 UM 邮箱策略，以确定是否应将 MWI 通知发送给启用 UM 的用户。邮箱助理会查询与启用 UM 的用户的 UM 拨号计划关联的所有邮箱服务器。邮箱助理尝试将 RPC 事件发送给返回的第一个邮箱服务器。如果失败，则它会尝试下一个邮箱服务器。它会不断重试五分钟，或直至尝试了所有邮箱服务器。如果所有 RPC 呼叫都失败，则邮箱助理会将错误记录在事件查看器中。邮箱服务器会查询与启用 UM 的用户邮箱的 UM 拨号计划关联的所有 UM IP 网关。

7.  UM 将 SIP 通知消息发送给从查询返回的第一个 VoIP 网关或 IP PBX。如果失败，则邮箱服务器会选择下一个 VoIP 网关或 IP PBX。邮箱服务器会不断尝试 VoIP 网关或 IP PBX 达五分钟。如果查找 VoIP 网关或 IP PBX 的所有尝试都失败，则邮箱服务器会记录一个错误。如果成功找到某个 VoIP 网关或 IP PBX，则该 VoIP 网关会将通知发送给 PBX，而 PBX 进而将 MWI 事件的通知发送给用户的电话，以点亮电话指示灯。如果使用 IP PBX，MWI 通知将由 IP PBX 处理，稍后将点亮用户电话的指示灯。概述部分列出了其他 MWI 通知机制。通知的类型取决于 PBX 或 IP PBX 硬件供应商以及是否正在使用 Lync Server。还取决于正在使用的电话类型（模拟、数字或 VoIP）。

返回顶部

## Lync Server 环境中的 MWI

在包含 Lync Server 的电话环境中，传入呼叫可以从外部电话发送给中介服务器、从 Lync 客户端发送或从统一通信 (UC) 或基于其他 VoIP 的电话发送。在接收到呼叫后，呼叫会发送给 Lync Server 前端服务器池。邮箱服务器和邮箱助理用于确定启用 UM 的用户的 MWI 状态，并将此通知传递给 Lync 客户端、模拟、数字、UC 或基于 VoIP 的电话。

在包含 Lync Server 的电话环境中，呼叫流和 MWI 通知如下所示：

1.  呼叫从以下对象之一发送：
    
      - 组织外部的电话（发送给中介服务器）
    
      - 基于 Lync 的客户端
    
      - UC 或基于其他 VoIP 的电话

2.  传入呼叫由 Lync Server 前端服务器池接收，并发送给启用 UM 的用户的电话或 SIP 终结点。用户未应答，系统提示呼叫者留下语音邮件。

3.  Lync Server 前端服务器池将呼叫提交到内部部署网络中的邮箱服务器，并找到用户的邮箱。

4.  邮箱服务器执行 LDAP 查询以查找启用 UM 的用户的信息，如其分机号码和问候语。播放问候语，系统提示呼叫者留下语音邮件。

5.  由统一消息服务创建的语音邮件被提交到同一站点中同一邮箱服务器中的传输服务。

6.  传输服务将语音邮件提交到包含用户邮箱的邮箱服务器。邮箱助理接收到有关新语音邮件的 MAPI 事件。

7.  邮箱助理会读取 UM 拨号计划和 UM 邮箱策略，以确定是否应将 MWI 通知发送给用户。邮箱助理会查询与用户的 UM 拨号计划关联的所有邮箱服务器。邮箱助理尝试将 RPC 事件发送给返回的第一个邮箱服务器。如果此尝试失败，则邮箱助理会尝试下一个邮箱服务器。它会不断尝试查找某个邮箱服务器五分钟，或直至尝试了所有服务器。如果所有 RPC 呼叫都失败，则邮箱助理会将错误记录在事件查看器中。邮箱服务器会查询与启用 UM 的用户的 UM 拨号计划关联的所有 UM IP 网关的 Active Directory。

8.  UM 将 SIP 通知消息发送给从查询返回的第一个 VoIP 网关或 IP PBX。如果失败，则邮箱服务器会选择下一个 VoIP 网关或 IP PBX。邮箱服务器会不断尝试查找 VoIP 网关或 IP PBX 达五分钟。如果联系 VoIP 网关或 IP PBX 的所有尝试都失败，则邮箱服务器会记录一个错误。如果成功，则 VoIP 网关或 IP PBX 会将通知发送给 Lync Server 前端服务器池，该服务器池进而将 MWI 事件的通知发送给用户使用的 SIP 终结点、用户的电话或 Lync 客户端。

返回顶部

## MWI 恢复

在部署邮箱和客户端访问服务器、UM 拨号计划和 UM IP 网关并将 MWI 用于启用 UM 的用户时，最好部署多个邮箱和客户端访问服务器以及多个 VoIP 网关和 IP PBX 以形成容错和恢复能力。这样做也可形成 MWI 恢复能力，因为提供了多种发送 MWI 通知的方式，如前面部分所述。

若要在统一消息中为 MWI 实现容错功能，必须创建和配置以下一项或多项：

  - 与将接收 MWI 通知的启用 UM 的用户链接的 UM 拨号计划。

  - 与将接收 MWI 通知的启用 UM 的用户链接的 UM 邮箱策略。

  - 与 UM 拨号计划（与将接收 MWI 通知的启用 UM 的用户链接）链接的 UM IP 网关。

  - 如果使用 Lync Server，所有客户端访问和邮箱服务器都必须添加到与将接收 MWI 通知的启用 UM 的用户链接的 UM SIP URI 拨号计划。

## MWI 管理

可以通过配置以下两个 UM 组件中的设置来管理 MWI：UM 邮箱策略和 UM IP 网关。对于这两个 UM 组件，可以使用 Exchange 命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet 或 **Set-UMIPgateway** cmdlet 来启用或禁用 MWI 通知。也可以使用 Exchange 管理中心 (EAC) 配置设置。可以使用命令行管理程序中的 **Get-UMMailboxPolicy** cmdlet 和 **Get-UMIPgateway** cmdlet 来查看 MWI 通知的状态，也可以通过在 EMC 中查看设置来查看 MWI 通知的状态。

## UM 邮箱策略和 MWI

可以创建 UM 邮箱策略，以将一组通用的 UM 策略设置应用于启用 UM 的邮箱集合。例如，可以使用 UM 邮箱策略应用 PIN 策略设置、拨号限制和 MWI 通知设置。如果您对某个 UM 邮箱策略启用或禁用 MWI，则会为与该 UM 邮箱策略链接的所有启用 UM 的用户都启用或禁用 MWI。MWI 设置也可以应用于与 UM 拨号计划链接的一部分用户。若要了解有关 UM 邮箱策略的详细信息（包括如何为一组启用 UM 的用户启用或禁用 MWI），请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

可以使用 EAC 或命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet 配置 MWI 设置，如下表所示。

### UM 邮箱策略的邮件等待指示器设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令行管理程序参数</th>
<th>是否为 EAC 中的可用设置？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowMessageWaitingIndicator</em></p></td>
<td><p>是</p></td>
<td><p><em>AllowMessageWaitingIndicator</em> 参数指定与 UM 邮箱策略链接的用户是否可以在接收到新语音邮件时接收 MWI 通知。默认值为 <code>$true</code>。</p>
<p>启用此设置时，会针对 UM IP 网关接收的呼叫，向与单个 UM 邮箱策略链接的用户发送 MWI 通知。此设置允许 UM IP 网关接收 SIP NOTIFY 邮件并向启用 UM 的用户电话或 SIP 终结点发送此邮件。</p>
<p></p></td>
</tr>
</tbody>
</table>


有关如何管理 UM 邮箱策略中的 MWI 设置的详细信息，请参阅下列主题：

  - [管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [为用户启用消息等待指示符 (MWI)](enable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [为用户禁用消息等待指示符 (MWI)](disable-message-waiting-indicator-mwi-for-users-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-cn/library/bb124903\(v=exchg.150\))

## UM IP 网关和 MWI

如果对某个 UM IP 网关禁用 MWI，则会为连接到由该 UM IP 网关表示的 VoIP 网关或 IP PBX 的所有用户都禁用 MWI 通知。禁用与 UM 拨号计划链接的单个 UM IP 网关中的 MWI 会为与单个或多个 UM 拨号计划或者单个或多个 UM 邮箱策略相关联的所有启用 UM 的用户都禁用 MWI 通知。若要了解有关 UM 邮箱策略的详细信息（包括如何为一组启用 UM 的用户启用或禁用 MWI），请参阅[管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)。

可以使用 EAC 或命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet 配置 MWI 设置，如下表所示。

### UM IP 网关的邮件等待指示器设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令行管理程序参数</th>
<th>是否为 EAC 中的可用设置？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>MessageWaitingIndicatorAllowed</em></p></td>
<td><p>是</p></td>
<td><p><em>MessageWaitingIndicatorAllowed</em> 参数指定是否可让 UM IP 网关允许向与 UM 拨号计划关联的用户发送 SIP NOTIFY 通知消息。默认值为 <code>$true</code>。</p>
<p>当启用了此设置时，可以针对 UM IP 网关接收的呼叫，向用户发送语音邮件通知。此设置允许 UM IP 网关向启用 UM 的用户发送邮件等待通知。</p></td>
</tr>
</tbody>
</table>


有关如何管理 MWI 设置的详细信息，请参阅下列主题：

  - [管理 UM IP 网关](manage-a-um-ip-gateway-exchange-2013-help.md)

  - [在 UM IP 网关允许消息等待指示符 (MWI)](allow-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [消息等待指示符 (MWI) 如果不在 UM IP 网关](prevent-message-waiting-indicator-mwi-on-a-um-ip-gateway-exchange-2013-help.md)

  - [Set-UMIPGateway](https://technet.microsoft.com/zh-cn/library/aa996577\(v=exchg.150\))

返回顶部

## 语音邮件和未接来电的短信 (SMS) 通知

前面已提到，MWI 通知是任何表示存在新语音邮件的机制。除了上述机制外，也可以通过短信（也称为 SMS（短消息服务）消息）通知用户存在待收听的语音邮件。这是一种有别于传统亮灯或其他机制的新语音邮件 MWI 通知类型。

当呼叫者留下新语音邮件时，会向用户的移动电话发送短信。当用户有未接来电且没有语音邮件时，他们也会收到短信通知。未接来电通知短信可能会和新语音邮件通知一起发送给用户。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>发送给用户的短信包括语音邮件预览。</td>
</tr>
</tbody>
</table>


与 UM IP 网关或 UM 邮箱策略中的 MWI 设置相比，短信通知使用不同的设置。新语音邮件和未接来电的短信通知在 UM 邮箱策略和 UM 邮箱中进行配置。可以使用命令行管理程序中的 **Set-UMMailboxPolicy** cmdlet 和 **Set-UMMailbox** cmdlet 启用或禁用短信通知。可以使用 **Get-UMMailboxPolicy** cmdlet 和 **Get-UMMailbox** cmdlet 查看短信通知的状态。无法在 EAC 中配置短信通知。

以下表格显示了 UM 邮箱中必须为用户进行配置以接收语音邮件和未接来电通知短信的参数：

### 用户邮箱中的短信通知设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>UMSMSNotificationOption</em></p></td>
<td><p>否</p></td>
<td><p><em>UMSMSNotificationOption</em> 参数指定启用 UM 的用户是只能接收语音邮件的短信通知，可以接收语音邮件和未接来电的短信通知，还是不允许接收通知。此参数的值为：<code>VoiceMail</code>、<code>VoiceMailAndMissedCalls</code> 和 <code>None</code>。默认值为 <code>None</code>。</p>
<p></p></td>
</tr>
</tbody>
</table>


有关如何管理用户邮箱中的短信通知设置的详细信息，请参阅下列主题：

  - [管理用户的语音邮件设置](manage-voice-mail-settings-for-a-user-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/zh-cn/library/bb124893\(v=exchg.150\))

以下表格显示了 UM 邮箱策略中必须为用户进行配置以接收语音邮件和未接来电通知短信的参数：

### UM 邮箱策略中的短信和未接来电通知设置

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>命令行管理程序参数</th>
<th>是否为 EAC 中的可用设置？</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AllowSMSNotification</em></p></td>
<td><p>否</p></td>
<td><p><em>AllowSMSNotification</em> 参数指定是否允许其邮箱与 UM 邮箱策略关联的启用 UM 的用户在移动电话上接收短信通知。如果此参数设置为 <code>$true</code>，则还必须使用 <strong>Set-UMMailbox</strong> cmdlet，并针对启用 UM 的用户将 <em>UMSMSNotificationOption</em> 参数设置为 <code>voicemail</code> 或 <code>VoiceMailAndMissedCalls</code>。默认值为 <code>$true</code>。</p>
<p></p></td>
</tr>
</tbody>
</table>


有关如何管理短信通知设置的详细信息，请参阅下列主题：

  - [管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailboxPolicy](https://technet.microsoft.com/zh-cn/library/bb124903\(v=exchg.150\))

为了使语音邮件和未接来电的短信通知能够正常工作，必须执行以下任务：

1.  使用 EAC 或命令行管理程序为用户启用 UM 并将他们链接到正确的 UM 邮箱策略。

2.  在链接到用户的 UM 邮箱策略中，验证 *AllowSMSNotification* 参数已设置为 `$true`。若要将参数设置为 `$true`，请运行以下命令：`Set-UMMailboxPolicy -id MyUMMailboxPolicy - AllowSMSNotification $true`.

3.  在用户邮箱中，通过将 *UMSMSNotificationOption* 参数设置为 `VoiceMailAndMissedCalls` 或 `VoiceMail` 来启用短信通知。

4.  由于默认设置为 `None`，因此您必须从命令行管理程序运行以下命令，并将短信通知选项设置为 `VoiceMailAndMissedCalls` 或 `VoiceMail`。例如：`Set-UMMailbox- -id MyUMMailbox -UMSMSNotificationOption VoiceMailAndMissedCalls`.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>UM 邮箱策略中的 <em>AllowSMSNotification</em> 参数和用户邮箱中的 <em>UMSMSNotificationOption</em> 参数必须都设置为 <code>$true</code>，以便 SMS 通知能够正常工作。</td>
    </tr>
    </tbody>
    </table>


除了将 UM 邮箱策略和用户的邮箱配置为启用新语音邮件和未接来电的短信通知外，用户在登录到 Outlook Web App 时还必须启用和配置短信通知。若要设置和配置短信通知，用户必须：

1.  登录到 Outlook Web App 并转到\&quot;选项\&quot;\>\&quot;电话\&quot;\>\&quot;语音邮件\&quot;。

2.  在\&quot;语音邮件\&quot;页上，在\&quot;通知\&quot;下单击\&quot;设置通知\&quot;。

3.  在\&quot;短信\&quot;页上单击\&quot;打开通知\&quot;按钮。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不要单击&amp;quot;语音邮件通知&amp;quot;，否则将会返回&amp;quot;语音邮件&amp;quot;页面。</td>
    </tr>
    </tbody>
    </table>


4.  在\&quot;短信\&quot;页上，在\&quot;区域设置\&quot;下，使用下拉列表选择短信移动运营商的区域设置或位置。

5.  在\&quot;短信\&quot;页上，在\&quot;移动运营商\&quot;下，使用下拉列表选择短信移动运营商，然后单击\&quot;下一步\&quot;。

6.  在\&quot;短信\&quot;页上，在\&quot;输入您的电话号码并单击下一步\&quot;框中，输入用于接收短信通知的移动电话号码然后单击\&quot;下一步\&quot;。将会向该移动电话发送一个六位数字的密码。如果未收到密码，单击\&quot;我没有收到密码，需要再次发送\&quot;。

7.  在\&quot;密码\&quot;框中输入密码，然后单击\&quot;完成\&quot;。

8.  用户启用短信通知后，可以在\&quot;短信\&quot;页上单击\&quot;设置语言邮件通知\&quot;。将会返回语音邮件页，在那里可以向下滚动到\&quot;通知\&quot;部分并为未接来电和语音邮件设置短信通知选项。

返回顶部

