---
title: 'Exchange 2013 电话顾问: Exchange Online Help'
TOCTitle: Exchange 2013 电话顾问
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50556693
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 电话顾问

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-07-25_

统一消息 (UM) 要求将 Microsoft Exchange 与组织的现有电话系统集成起来。要成功进行部署，您需要仔细分析现有电话基础结构，并执行正确的计划步骤来部署统一消息。

对于很少或没有电话网络经验的 Exchange 管理员来说，计划阶段可能是一项重大的挑战。为了帮助应对这一挑战，请参阅本主题下文中的Resources to Help with Your UM Deployment。

若要查看统一消息支持的 VoIP 网关，以及确定特定 VoIP 网关型号或制造商是否支持您的 PBX，或者直接 SIP 连接是否支持您的 IP PBX，或者查看 Exchange Online UM 支持的会话边界控制器 (SBC)，请单击以下链接之一：

  - Supported VoIP gateways

  - Supported PBXs when using an AudioCodes VoIP gateway

  - Supported PBXs when using a dialogic VoIP gateway
    
      - PBXs supported when using a DMG1000 series Media Gateway
    
      - PBXs supported when using a DMG 2000 series Media Gateway
    
      - PBXs supported when using a DMG3000 series Media Gateway

  - Supported IP PBXs

  - Supported IP PBXs when using SIP media gateways

  - Exchange Unified Messaging, Office Communications Server 2007 R2, and Microsoft Lync Server

## 有助于 UM 部署的资源

创建电话网络部署准则非常有挑战性。由于电话网络可以包括具有不同配置设置、固件和要求的 VoIP 网关、IP PBX 和 PBX，因此各个电话网络之间差异很大。不过，有几项资源可以帮助您成功部署统一消息：

  - **统一消息专家**   UM 专家是一些系统集成人员，他们接受过由 Exchange 工程团队实施的 Exchange 统一消息技术培训。为确保从旧式语音邮件系统平滑过渡到统一消息，Microsoft 建议所有客户都要与 UM 专家接洽。有关联系信息，请访问 [Microsoft Exchange Server 2013 统一消息 (UM) 专家](https://go.microsoft.com/fwlink/p/?linkid=262708)或者[面向统一消息的 Microsoft Pinpoint](https://go.microsoft.com/fwlink/p/?linkid=261951)。

  - **支持的 VoIP 网关、IP PBX 和 PBX 的配置说明**   这些配置说明包含的设置和其他信息在配置 VoIP 网关、IP PBX 和 PBX 以与网络上的统一消息服务器通信时很有用。有关详细信息，请参阅[支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)。

  - **支持的会话边界控制器的配置说明**   这些配置说明包含的设置和其他信息在配置会话边界控制器(SBCs) 以与混合部署和 Exchange Online UM 部署的统一消息服务器通信时很有用。有关详细信息，请参阅[受支持的会话边界控制器的配置说明](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)。
    
    > [!NOTE]  
    > Exchange 联机 UM 支持第三方 PBX 系统，通过直接连接从客户操作 SBCs 将在 7 月 2018年结束。 请 Exchange 团队博客<a href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">终止的会话边框中的控制器联机 Exchange 支持统一消息</a>的详细信息，参阅。


在接洽统一消息专家之前，您应当能够回答他们将询问您的一些关键问题。知晓以下问题的答案有助于让您和 UM 专家之间的会话更有效率：

  - 在您的组织中现在有多少使用电话或语音邮件（或二者都使用）的用户？

  - 您计划向多少用户提供统一消息？

  - 您打算使用哪个或哪些 PBX 实现与统一消息集成？

  - 您的组织有多少 PBX？说出供应商、类型（基于电路或 IP）、型号和固件版本。

  - PBX 网络是否联网，它们是集中的，还是位于多个位置？

  - 您的组织当前使用什么语音邮件系统？说出供应商、类型、型号和固件版本。

  - 语音邮件系统是如何集成到您的 PBX 中的（模拟、T1/E1、PRI、数字组仿真、VoIP、其他）？

  - 您当前正在使用语音网络吗？

  - 您的组织使用什么类型的传真系统，传真系统是否支持路由到 Exchange 的入站传真？

  - 您的组织是否使用自动助理？

  - 您是否需要为仅使用电话的用户（即不能访问电子邮件的用户）提供支持？

## 支持的 VoIP 网关

将统一消息与 PBX 集成需要使用一个或多个 VoIP 网关，以便将基于 TDM 的 PBX 所使用的电路交换协议转换成统一消息所使用的基于 IP 的数据包交换协议。VoIP 网关供应商提供的几种型号的 VoIP 网关和媒体网关已通过测试，支持统一消息。

如今，统一消息与 VoIP 网关、IP PBX 和 SBC 的互操作性测试已与 Microsoft 统一通信开放式互操作性计划集成。有关详细信息，请参阅 [Microsoft 统一通信开放式互操作性计划](http://go.microsoft.com/fwlink/p/?linkid=140722)。

[Microsoft 统一通信开放式互操作性计划](http://go.microsoft.com/fwlink/p/?linkid=140722)资格计划针对 VoIP 网关、IP PBX 和高级 VoIP 网关，可以确保客户在将合格的电话 VoIP 网关和 IP PBX 与 Microsoft 统一通信软件一起使用时，拥有无缝的安装和支持体验。只有满足一系列苛刻测试要求、且符合规范和测试计划的产品才具备资格。

关于配置支持的 VoIP 网关、IP PBX、PBX 和 SBC 的详细信息，请参阅下列资源之一：

  - [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [受支持的会话边界控制器的配置说明](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

以下 VoIP 网关供应商经过了互操作性验证：

  - AudioCodes

  - Dialogic

  - 下表列出了 VoIP 网关供应商、VoIP 网关型号和每种型号所支持的协议。

### 支持的统一消息 VoIP 网关

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>供应商</th>
<th>型号</th>
<th>受支持的协议</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>与带内 DTMF 模拟</p></li>
<li><p>与 SMDI 模拟</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>与带内 DTMF 模拟</p></li>
<li><p>与 SMDI 模拟</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP 到 IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP 到 IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>数字组仿真</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>与带内 DTMF 模拟</p></li>
<li><p>与 SMDI 模拟</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CAS</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 或更高版本</p></td>
<td><ul>
<li><p>TDM 信号 (ISDN)：AT&amp;T 4ESS/5ESS、Nortel DMS- 100、Euro ISDN (ETSI 300-102)、QSIG、NTT InsNet（日本）、ANSI National ISDN-2 (NI-2)</p></li>
<li><p>TDM 信号 (CAS)：T1 CAS（E&amp;M，循环开始）；E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Tenor DX 系列</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 使用 AudioCodes VoIP 网关时支持的 PBX

下表列出了使用 AudioCodes VoIP 网关（包括 MediaPack-114 FXO、MediaPack-118 FXO 和 Mediant 2000）时所支持的 PBX。

### AudioCodes VoIP 网关支持的 PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>AudioCodes 型号 &quot;x&quot; - 需要替换为 4 或 8 &quot;y&quot; - 需要替换为 1、2、4、8 或 16</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000/IP 到 IP</p></li>
<li><p>Mediant2000/IP 到 IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra Elite</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Communication Server-1000M、1000S、1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 11c、51c、61c、81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824、KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30、KX-TDA100、KX-TDA200、KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP 电话系统</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran Telecom</p></td>
<td><p>Coral Flexicom、Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 使用 Dialogic VoIP 网关时支持的 PBX

每个 Dialogic VoIP 网关模型支持不同的 PBX。下表显示了 PBX 制造商和型号，以及可以使用的 Dialogic VoIP 网关。每个 VoIP 网关使用不同的信号方法、密度和协议。

## 使用 DMG1000 系列媒体网关时支持的 PBX

下表显示了使用低密度对话媒体网关 (DMG1000) 时所支持的 PBX。但是，使用模拟 DMG1000 时，必须使用补充信号（RS232 SMDI、MD110、MCI 协议或带内 DTMF 信号）。

### 使用低密度对话 DMG1000 系列 VoIP 网关时支持的 PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>DMG 型号和附加信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110（以前为 Ericsson MD110）</p></td>
<td><p>DMG1008LSW</p>
<p>使用 MD110 RS232 协议的模拟连接</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100、S8300、S8700 和 S8710（Communications Mgr SW V2.0 或更高版本）</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>使用 SMDI 串行协议的模拟连接</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200D、X-200 Light、SX-2000 Light、SX-2000 S、SX-2000 VS、SX-200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - 选项 11、21、21A、51、61、71 和 81</p>
<p>Meridian SL1 - 常规 X11，15 版或更高版本</p>
<p>Nortel Communication Server - 带 V3.0 或更高版本的 1000M、1000S、1000E</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>使用 SMDI 串行协议的模拟连接</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E（欧洲）</p></td>
<td><p>DMG1008LSW</p>
<p>使用带内 DTMF 信号的模拟连接</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000（SW 80003 版或更高版本）<br />
9000（所有版本）</p>
<p>9751（SW 发布版 9005 的所有版本）</p>
<p>9751（SW 9006.4 版或更高版本）</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX（SW 版本 AR1ME021.00）</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>其他</p></td>
<td><p>各种</p></td>
<td><p>DMG1008LSW</p>
<p>使用带内 DTMF 或 SMDI 的模拟连接</p></td>
</tr>
</tbody>
</table>


## 使用 DMG 2000 系列媒体网关时支持的 PBX

下表显示了 T1/E1 Dialogic 媒体网关 (DMG2000) 所支持的 PBX。DMG2000 网关，它提供单跨段 (DMG2030DTIQ)、双跨段 (DMG2060DTIQ) 或四跨段 (DMG2120DTIQ) 密度，支持以下协议：

  - T1 CAS

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

如果使用通道关联信号 (CAS) 信号方式，则补充信号（RS232 SMDI、MD110、MCI 协议或带内 DTMF 信号）是必需的。如果使用 Q.SIG 信号，则 PBX 必须支持与呼叫和被呼叫方信息关联的补充服务，并且支持统一消息需要的呼叫转移能力。

### 使用 DMG2000 媒体网关时所支持的 PBX

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>所需的软件版本</th>
<th>协议和附加信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>Omni PCX 4400</p></td>
<td><p>版本 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>版本 3 或更高版本</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW V2.0 或更高版本</p></td>
<td><p>T1 CAS</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Release MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercom</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS（w/SMDI 串行协议）</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>5200 Dec. 92 1b 版或更高版本</p></td>
<td><p>CAS（w/MCI 串行协议）</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 发布版 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridian 1 - 选项 11</p></td>
<td><p>15 版或更高版本，需要选项 19 和 46</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Communication Server 1000</p></td>
<td><p>版本 2121，发布版 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>发布版 9006.4 或更高版本（注意：仅北美软件负载）</p></td>
<td><p>T1 CAS</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX-2000 S、SX-2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>5.1.4.8 版</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## 使用 DMG4008BRI 系列媒体网关时支持的 PBX

随 DMG4000 系列媒体网关一起提供了一些 TDM 界面选项。DMG4008BRI 支持 4 端口/8 通道密度，并支持以下协议：

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3（比利时）

  - VN3（法国）

  - 1TR6（德国）

  - INS-64（日本）

  - 5ESS 自定义（北美 - AT\&T）

  - National ISDN（NI1 - 北美）

下表显示了使用 Dialogic 4000 媒体网关系列 (DMG4008) 时所支持的 PBX。

### 使用 DMG4008BRI 媒体网关支持的 PBX

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>所需的软件版本</th>
<th>协议和附加信号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q.SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## 受支持的 IP PBX

统一消息还支持 IP PBX。下表显示了使用与统一消息的直接 SIP 连接时所支持的 IP PBX。

### 使用直接 SIP 连接时支持的 IP PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>所需的软件版本</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX-ONE</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>带 Service Pack 5 (SP5) 的 5.2.1</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Communication Server 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Call Manager、Unified Communications Manager</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## 使用 SIP 媒体网关时支持的 IP PBX

统一消息也支持使用 SIP 媒体网关的 IP PBX。下表显示了使用 SIP 媒体网关的 IP 到 IP 功能连接到统一消息所支持的 IP PBX。

### 使用 SIP 媒体网关时支持的 IP PBX

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 制造商</th>
<th>PBX 型号/类型</th>
<th>SIP 网关型号</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Call Manager 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000（已启用 IP 到 IP 协议）</p></td>
</tr>
</tbody>
</table>


## Exchange 统一消息、Office Communications Server 2007 R2 和 Microsoft Lync Server

对于内部部署和混合部署，可以将 Exchange 统一消息与 Microsoft Office Communications Server 2007 R2 以及 Microsoft Lync Server 2010 或 Lync Server 2013 部署到一起，从而为组织中的用户提供语音邮件、即时消息 (IM)、增强的用户在线状态、音频视频会议以及集成的电子邮件和邮件体验。有关详细信息，请参阅：

  - [部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

若要了解适用于企业电话基础结构的 Microsoft 统一通信开放式互操作性计划的更多信息，包括了解合格的 SIP PSTN 网关和 IP PBX 以及电话基础结构供应商加入此计划的流程，请参阅 [Microsoft 统一通信开放式互操作性计划](https://go.microsoft.com/fwlink/p/?linkid=132071)。

