---
title: '受支持的会话边界控制器的配置说明: Exchange Online Help'
TOCTitle: 受支持的会话边界控制器的配置说明
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50556677
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 受支持的会话边界控制器的配置说明

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2017-07-25_

会话边界控制器 (SBC) 可用于通过专用公共 WAN 连接将内部部署电话网络连接到 Microsoft 数据中心。SBC 位于内部部署 IP 网络的边缘，并与 Microsoft 数据中心中的另一个 SBC 连接。

SBC 需要使用数字证书对内部部署组织和 Microsoft 数据中心之间的所有通信进行加密。必须获取用于与 Exchange 混合和联机部署通信的网络边界元素（如会话边界控制器）的数字证书。数字证书将在内部部署组织和 Microsoft 数据中心之间建立信任关系，并保证相互传输层安全性（相互 TLS）。建立此信任关系后，内部部署组织和 Microsoft 数据中心的网络边界元素会交换会话密钥，然后使用这些密钥对后续数据通信进行加密。

在混合或联机部署中，一个 UM IP 网关代表一个 SBC。证书中的使用者公用名称必须与您创建的 UM IP 网关\&quot;地址\&quot;框中的完全限定域名 (FQDN) 值匹配。例如，如果在 UM IP 网关上指定了 FQDN 地址 sbcexternal.contoso.com，则应确保证书中的使用者名称和使用者备用名称包含相同的值：sbcexternal.contoso.com。使用的名称区分大小写，因此请确保证书和 UM IP 网关上的大小写相同。如果使用 Acme Packet SBC 并且公用名称与 UM IP 网关的 FQDN 不匹配，则会拒绝呼叫，并出现 403 错误。

> [!NOTE]
> 因为 SBC 设计为处于网络边缘，所以也将它们当作防火墙使用。如果您在组织的防火墙之后设置 SBC，则可能会导致配置问题并且不支持连接到 Office 365。


## 支持的会话边界控制器

已成功测试以下 SBC 与 Exchange 混合和联机部署的互操作性。请注意，SBC 的功能和兼容性可能有所差异，并且它们的设置方式可能因网络上的其他设备而异。请咨询 SBC 制造商以了解是否存在针对混合或联机部署中的统一消息的特定配置说明。

> [!NOTE]
> Exchange 联机 UM 支持第三方 PBX 系统，通过直接连接从客户操作 SBCs 将在 7 月 2018年结束。 请 Exchange 团队博客<a href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">终止的会话边框中的控制器联机 Exchange 支持统一消息</a>的详细信息，参阅。



<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>供应商</strong></p></td>
<td><p><strong>型号</strong></p></td>
<td><p><strong>配置说明</strong></p></td>
<td><p><strong>注释</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 或 4500</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>专用 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>专用 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>SBC 和 IP 网关</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> 必须已安装 IOS 15.4(3)S3 或更高版本。

</td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>专用 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>专用 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 &amp; VX1800</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>用于 VoIP 网关产品的 SBC 选项</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 或更高版本</p></td>
<td><p><strong>有关如何设置设备的最新说明，请与硬件供应商联系。</strong></p></td>
<td><p>专用 SBC</p></td>
</tr>
</tbody>
</table>

