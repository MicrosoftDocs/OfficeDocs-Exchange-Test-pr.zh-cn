---
title: '支持的 VoIP 网关、IP PBX 和 PBX 的配置说明: Exchange 2013 Help'
TOCTitle: 支持的 VoIP 网关、IP PBX 和 PBX 的配置说明
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50556530
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 支持的 VoIP 网关、IP PBX 和 PBX 的配置说明

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

此页面提供已经由 Microsoft 或 VoIP 网关合作伙伴创建和测试的配置说明的链接。Microsoft 或合作伙伴使用新的 VoIP 网关和 PBX 或 IP PBX 配置部署统一消息时，将记录先决条件和配置设置。该信息用于创建配置说明。

每个 PBX 配置说明都包含有关如何部署具有特定电话配置（包括 VoIP 网关、IP PBX 或 PBX 的制造商、型号和固件版本）的统一消息的信息。此外，每个 PBX 配置说明还包括其他信息，如：

  - 编写配置说明的作者。

  - 详细的先决条件，包括：
    
      - 必须在 PBX 上启用或禁用的功能。
    
      - 必须安装的特殊硬件。
    
      - 是否需要 VoIP 网关。
    
      - VoIP 网关上必须具有的功能（如果需要）。
    
      - IP 网关和 PBX 之间的特定线缆要求。
    
      - 在使用给定电话配置时可能不可用的统一消息功能的列表。

若要详细了解适用于企业电话服务基础结构的 Microsoft 统一通信开放式互操作性计划，包括了解合格的 SIP PSTN 网关和 IP PBX，以及电话服务基础结构供应商可用于加入此计划的流程，请参阅 [Microsoft Unified Communications Open Interoperability Program](https://go.microsoft.com/fwlink/p/?linkid=132071)（Microsoft 统一通信开放式互操作性计划）。

## VoIP 网关、IP PBX 和 PBX 配置说明

Microsoft 正在与 VoIP 网关合作伙伴 AudioCodes 和 Dialogic 合作，以添加到经过测试的 PBX 列表。因为我们当前正在测试电话组件的很多组合，所以本主题会频繁更新。如果无法找到针对您的部署的合适配置说明，请以后再访问本网页。

已有下列配置说明：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Inter-Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110（以前为 Ericsson MD110）</p></td>
<td><p>MX1 TSW R2A (aka BC13)</p></td>
<td><p>模拟 – 串行 MD110</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110（以前为 Ericsson MD110）</p></td>
<td><p>MX1 TSW R2A (aka BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX-ONE</p></td>
<td><p>4.0</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">下载</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aura</p></td>
<td><p>带 SP 5 的通信管理器 5.2.1</p>
<p>会话管理器 5.2。</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">下载</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>数字组仿真 (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Merlin Magix</p></td>
<td><p>版本 1.5 v.6.0</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>G3xV11 Communication Manager 1.3</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 CAS – 带内 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Communication Manager 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco Call Manager 4.x</p></td>
<td><p>4.x</p></td>
<td><p>IP 到 IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Call Manager 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 6.0 和 6.1</p></td>
<td><p>6.x</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Unified Communications Manager 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>直接 SIP 连接</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">下载</a></p></td>
</tr>
</tbody>
</table>


## Inter-Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>Inter-Tel 5000 v2.1</p></td>
<td><p>T1 CAS – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 CAS – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS - SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>数字组仿真 (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra Elite 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>版本 7400</p></td>
<td><p>T1 CAS - 串行 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>版本 7400</p></td>
<td><p>数字组仿真 (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.R18.06.24.000</p></td>
<td><p>T1 CAS – 串行 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.R18.06.24.000</p></td>
<td><p>模拟 – 串行 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG – 串行 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>S</p></td>
<td><p>RMS1 版本 R1.3 E1TA</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 &amp; 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Meridian 81C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridian 81C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>发布版 25</p></td>
<td><p>数字组仿真 (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>发布版 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>发布版 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>CS-1000M（连续）</p></td>
<td><p>发布版 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX-TDA200</p></td>
<td><p>001-001</p></td>
<td><p>模拟 - 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>KX-TDA200</p></td>
<td><p>3</p></td>
<td><p>模拟 - 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>KX-TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>模拟 - 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>数字组仿真 (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP 电话系统</p></td>
<td><p>6.1</p></td>
<td><p>模拟 – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>IP 电话系统</p></td>
<td><p>7.5</p></td>
<td><p>模拟 – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>Rel.2.2</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>数字组仿真 (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS - 带内 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>Rel.3</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>版本 3.0 SMR5 SMP4</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>版本 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>版本 2.0 SMR9 SMP0</p></td>
<td><p>模拟 - 带内 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>版本 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
</tbody>
</table>


## Sonus


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>VoIP 网关模型</th>
<th>VoIP 网关软件版本</th>
<th>受支持的协议</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 或更高版本</p></td>
<td><ul>
<li><p>TDM 信号 (ISDN)：AT&amp;T 4ESS/5ESS、Nortel DMS- 100、Euro ISDN (ETSI 300-102)、QSIG、NTT InsNet（日本）、ANSI National ISDN-2 (NI-2)</p></li>
<li><p>TDM 信号 (CAS)：T1 CAS（E&amp;M，循环开始）；E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">下载</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS - 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP-11x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – 带内 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">下载</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 型号</th>
<th>PBX 软件版本</th>
<th>协议</th>
<th>网关供应商</th>
<th>网关型号</th>
<th>配置作者</th>
<th>配置文件下载</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>模拟 – SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>模拟 – 带内 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">下载</a></p></td>
</tr>
</tbody>
</table>

