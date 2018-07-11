---
title: '部署 Exchange 2013 UM 和 Lync Server 概述: Exchange 2013 Help'
TOCTitle: 部署 Exchange 2013 UM 和 Lync Server 概述
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50491089
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 部署 Exchange 2013 UM 和 Lync Server 概述

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

可以将统一消息 (UM) 和 Microsoft Lync Server 一起部署，为组织中的用户提供语音邮件、即时消息、增强的用户在线状态、音频/视频会议以及集成的电子邮件和消息体验。统一消息用于提供语音邮件呼叫应答、Outlook 语音访问和自动助理服务。Microsoft Lync Server 在 Enterprise Voice 中提供更多高级功能，例如即时消息 (IM)、会议和入站或出站呼叫。本主题介绍如何配置统一消息和 Microsoft Lync Server 以支持上述功能。

> [!tip]
> Microsoft Office Communications Server 2007 R2 也可以与统一消息一起部署。在本主题中，“Microsoft Lync Server”指 Microsoft Lync Server 2010 或 Microsoft Lync Server 2013。


若要了解有关 Microsoft Lync Server 的详细信息，请参阅 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

**目录**

部署 Exchange UM 和 Lync Server 概述

证书配置的建议

部署步骤

详细信息

## 部署 Exchange UM 和 Lync Server 概述

统一消息将多个语音和电子邮件组合成单个邮件基础结构。Microsoft Lync Server Enterprise Voice 利用 UM 基础结构提供语音邮件、Outlook Voice Access、来电通知和自动助理。

下表显示简单的 UM 和 Lync Server 部署步骤。在本主题后面包含有关每个步骤的详细信息。

1.  在安装运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器以及运行 Microsoft Exchange 统一消息服务的邮箱服务器的同一拓扑中安装 Microsoft Lync Server。确认已创建至少一个 Lync 池。

2.  安装由私有或公有证书颁发机构 (CA) 签发且 Lync Server 可信任的有效证书。

3.  安装客户端访问服务器和邮箱服务器。验证安装。

4.  安装由与 Lync Server 上安装的证书相同的证书颁发机构 (CA) 签发的有效证书。

5.  创建和配置会话初始协议 (SIP) URI 拨号计划。

6.  将所有客户端访问和邮箱服务器添加到 SIP URI 拨号计划。但是，如果有多个 SIP URI 拨号计划，则必须将所有客户端访问和邮箱服务器添加到所有 SIP URl 拨号计划。

7.  从邮箱服务器上的 \<Exchange 安装文件夹\>\\Exchange Server\\Script 文件夹运行 ExchUcUtil.ps1 脚本。
    
    > [!important]
    > ExchUcUtil.ps1 脚本会为 Lync 集成创建一个或多个 UM IP 网关。除该脚本创建的一个网关外，必须禁用所有 UM IP 网关上的传出呼叫。这包括禁用在运行该脚本之前创建的 UM IP 网关上的传出呼叫。若要禁用 UM IP 网关上的传出呼叫，请参阅<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">禁用 UM IP 网关的传出呼叫</a>。


8.  从 Lync Server 上的 %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support 文件夹运行 **OcsUmUtil.exe**。

9.  部署中介服务器和媒体网关。

10. 在中介服务器上安装由与 Lync Server 上安装的证书相同的证书颁发机构 (CA) 签发的有效证书。

11. 为用户启用 UM 和 Enterprise Voice。

## 证书配置的建议

必须拥有运行 Exchange 的计算机和运行 Lync Server 的计算机都信任的证书。在装有 Lync Server 和统一通信的环境中，使用下列指南部署受信任证书：

  - 在 Lync Server、客户端访问服务器、邮箱服务器、中介服务器和媒体网关上，导入由私有或公有证书颁发机构 (CA) 签发的有效证书。这可以是受信任的第三方商业证书或公钥基础结构 (PKI) 证书。

  - 如果将相同的第三方商业证书或 PKI 证书导入到各个 Exchange 服务器会简单得多。同时，将此受信任的证书安装到运行 Microsoft Lync Server 和中介服务器的各个计算机中。这将简化证书部署，同时降低与部署证书有关的管理费用。但是，您必须获取一个支持主题备用名称 (SAN) 的受信任证书。
    
    当您使用 UM 部署传输层安全性 (TLS) 时，客户端访问服务器和邮箱服务器上使用的证书必须同时在证书的主题名称中包含本地计算机的完全限定域名 (FQDN)。若要解决这一问题，请使用公有证书并导入所有客户端访问和邮箱服务器、任何 VoIP 网关、IP PBX 以及所有 Lync Server 上使用的证书。
    
    如果部署包括 VoIP 网关或 IP PBX，并且使用 SIP 安全或安全拨号计划，则客户端访问和邮箱服务器以及 VoIP 网关或 IP PBX 之间需要受信任证书。如果使用直接的会话初始协议 (SIP) 连接，则同样需要受信任的证书。如果使用 SIP 安全或安全拨号计划，则可以在 Lync 和 Exchange 服务器上使用与 VoIP 网关或 IP PBX 上相同的受信任证书。

  - 将 Exchange 客户端访问和邮箱服务器连接到 Microsoft Lync Server 或第三方 SIP 网关或专用交换机 (PBX) 电话设备时，为建立受保护的会话，必须使用内部或公共的第三方证书颁发机构 (CA) 签名的有效证书。只要证书的 SAN 列表中拥有所有客户端访问和邮箱服务器的 FQDN，您就可以在所有客户端访问和邮箱服务器上使用单个证书。或者，您可以为每台客户端访问和邮箱服务器生成不同的证书，同时证书的主题公用名称或 SAN 列表中包含本地计算机的 FQDN。Exchange UM 不支持 Microsoft Lync Server 使用通配符证书。
    
    Lync Server 和 Exchange 需要非通配符主题名称才能一起工作。UM 和 Lync Server 使用主题名称来表明其是受信任 SIP 对等项。Lync Server 还需要在某些呼叫路由方案中使用非通配符主题名称。必须使用 FQDN 作为“颁发给”值。
    
    对于 Exchange UM，不支持在证书名称中放置通配符。但是，您可以在 SAN 中放置通配符。

下表显示安装和配置 Exchange UM 证书的证书要求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>拓扑</th>
<th>证书配置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>同一服务器上的客户端访问和邮箱（不带 Lync 2010 或 2013；非 SIP 拨号计划）</p></td>
<td><p>客户端访问和邮箱服务器之间需要证书。这是客户端访问和邮箱服务器以及 VoIP 网关、IP PBX 或 SBC 之间使用的相同证书。</p></td>
</tr>
<tr class="even">
<td><p>不同服务器上的客户端访问和邮箱（不带 Lync 2010 或 2013；非 SIP 拨号计划）</p></td>
<td><p>必须有证书。客户端访问和邮箱服务器上的证书必须匹配。客户端访问和邮箱服务器以及 VoIP 网关、IP PBX 或 SBC 之间也需要证书。此证书与客户端访问和邮箱服务器上使用的证书可以相同，也可以不同。对于客户端访问和邮箱服务器，可以从任一服务器运行 <strong>Create-ExchangeCertificate</strong> cmdlet。</p></td>
</tr>
<tr class="odd">
<td><p>同一服务器上的客户端访问和邮箱（带 Lync 2010 或 2013；SIP 拨号计划）</p></td>
<td><p>必须有证书。客户端访问以及邮箱服务器必须有和 Lync 2010 或 2013 服务器一样的根证书。</p></td>
</tr>
<tr class="even">
<td><p>不同服务器上的客户端访问和邮箱（带 Lync 2010 或 2013；SIP 拨号计划）</p></td>
<td><p>必须有证书。客户端访问以及邮箱服务器必须有和 Lync 2010 或 2013 服务器一样的根证书。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 部署步骤

在组织中安装所需的服务器后，必须在 Exchange 统一消息和 Lync Server 部署中按照建议的顺序执行相关步骤，才能为用户正确部署 Enterprise Voice。

有关 Microsoft Lync Server 的详细信息，请参阅 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

必须完成下列步骤，以将统一消息配置为使用 Lync Server 中的 Enterprise Voice 功能：

1.  创建一个或多个统一消息 SIP URI 拨号计划，并且每个拨号计划都映射到相应的 Lync Server 位置配置文件。必须为每个 Exchange UM 拨号计划创建 Enterprise Voice 位置配置文件。可以使用 **Get-UMDialPlan** cmdlet 获取 SIP URI 拨号计划的 FQDN。有关如何创建 SIP URI 拨号计划的详细信息，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。
    
    > [!important]
    > 当您将 Exchange UM 和 Lync Server 集成后，可能会发现在 Exchange UM 中将无需配置拨号规则或拨号规则组。Lync Server 用于执行组织中用户的呼叫路由和号码转换，此外，在统一消息代表用户进行呼叫时也会执行此操作。


2.  在客户端访问和邮箱服务器上安装由私有或公有证书颁发机构 (CA) 签发的有效证书。此证书的 CA 与 Lync Server 上使用的相同。

3.  通过将 SIP URI 拨号计划配置为 SIP 安全或安全，加密 IP 语音 (VoIP) 通信。
    
    > [!CAUTION]
    > 如果将安装设置设置为 SIP 安全以仅对 SIP 通信进行加密，则当配置要求加密的前端池（这意味着池需要同时对 SIP 和 RTP 通信进行加密）时，为拨号计划进行此设置是无法满足其要求的。当拨号计划和池安全设置不兼容时，前端池向 Exchange UM 发出的所有呼叫将失败，并出现一个错误，指明您进行了“不兼容的安全设置”。
    
    尽管可以将 UM 拨号计划配置为 SIP 安全或安全，但建议您将拨号计划配置为安全，以使 Lync Phone Edition 设备能够正常工作。因为这是 Lync Server 中配置的默认加密级别设置，建议您使用此设置。仅当加密设置配置如下表所示时，Lync Phone Edition 设备才会正常工作。此表给出了 Lync Server 和 UM 拨号计划的加密设置之间的关系。
    
    **Lync Phone Edition 的加密设置**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>UM 拨号计划</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>要求加密（默认）</p></td>
    <td><p>安全</p></td>
    </tr>
    <tr class="even">
    <td><p>加密可选</p></td>
    <td><p>SIP 安全/安全</p></td>
    </tr>
    <tr class="odd">
    <td><p>无加密</p></td>
    <td><p>SIP 安全</p></td>
    </tr>
    </tbody>
    </table>


4.  将所有客户端访问和邮箱服务器添加到 SIP 拨号计划。为使服务器应答传入呼叫，并且希望 Exchange 服务器应答来自 Lync Server 的呼叫，必须将所有 Exchange 服务器添加到拨号计划中。

5.  在添加到 SIP URI 拨号计划的客户端访问和邮箱服务器上将启动模式设置为“双模式”并设置 TLS 侦听端口，然后重新启动每台邮箱服务器上的 MicrosoftExchange 统一消息服务以及每台客户端访问服务器上的 MicrosoftExchange 统一消息呼叫路由器服务。

6.  创建和配置 UM 自动助理。有关详细信息，请参阅[设置 UM 自动助理](set-up-a-um-auto-attendant-exchange-2013-help.md)。

7.  为用户启用语音邮件功能时，为使用 Enterprise Voice 的用户创建一个 SIP 地址。在大多数情况下，此 SIP 地址将与为用户启用 Enterprise Voice 时使用的 SIP 地址相同。有关详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。
    
    > [!important]
    > 与 SIP URI 拨号计划关联的用户无法收到传入的传真。这是因为传入的语音和传真呼叫通过中介服务器进行路由，但使用中介服务器时不支持传真。


8.  打开 Exchange 命令行管理程序，运行 %Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts 文件夹中的 exchucutil.ps1 脚本。Exchucutil.ps1 脚本会执行下列操作：
    
      - 授予 Lync Server 权限，以读取 Exchange UM Active Directory 组件，特别是以前任务中创建的 SIP URI 拨号计划。有关如何配置 Active Directory 中的权限的详细信息，请参阅[如何使用 ADSI 编辑应用权限](https://go.microsoft.com/fwlink/p/?linkid=82751)。
    
      - 为每个 Lync Server 池或每台运行 Lync Server Standard Edition 并承载将启用 Enterprise Voice 的用户的服务器创建一个 UM IP 网关。有关详细信息，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。
    
      - 为每个 UM IP 网关创建一个 Exchange UM 智能寻线。智能寻线引导号码将是与相应的 UM IP 网关关联的拨号计划的名称。智能寻线必须指定 UM IP 网关使用的 UM SIP 拨号计划。

9.  为用户启用语音邮件。启用后，必须为用户输入有效的 SIP 地址并将其链接到 SIP 拨号计划。有关详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

还必须完成以下任务，才能将 Lync Server 配置为与 Exchange UM 一起使用：

  - 创建位置配置文件或 Lync 拨号计划。位置配置文件名称不必与相应 UM 拨号计划的 FQDN 相匹配。

  - 将位置配置文件分配给 Lync Server 池。

  - 部署和配置媒体网关或中介服务器。还必须导入与客户端访问和邮箱服务器以及 Lync Server 上使用的证书相同的受信任 CA 签发的证书。

  - 定义电话用法、创建和分配语音策略及出站呼叫路由。

  - 为用户配置 Enterprise Voice 并添加 TEL URI 和 SIP 标识符。

  - 运行 **ocsumutil.exe** 命令，为 Outlook Voice Access 和自动助理创建联系人对象。
    
    > [!NOTE]
    > 在安装 Lync Server 时，<strong>msRTC-SIPLine</strong> 属性将添加到 Active Directory 中。如果尚未在环境中安装 Lync Server，则该属性不会添加到 Active Directory 中，除非为未启用 UM 的用户配置统一消息代理地址，否则，单个林或跨林方案中拨号计划间的呼叫者 ID 名称解析将无法正常进行。


配置 Lync Server 和统一消息服务器之后，必须让用户能够使用 Lync Server，并在用户的客户端计算机上安装 Lync Server。

> [!important]
> 在集成统一消息和 Lync Server 时，邮箱位于 Exchange 2007 或 Exchange 2010 邮箱服务器上的用户不可使用未接呼叫通知。如果用户在呼叫发送至邮箱服务器之前断开连接，则会生成未接呼叫通知。


返回顶部

## 详细信息

有关如何执行 Microsoft Lync Server 必须完成的任务的详细信息，请参阅 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)。

