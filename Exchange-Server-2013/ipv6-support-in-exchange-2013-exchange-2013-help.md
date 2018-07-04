---
title: 'Exchange 2013 中的 IPv6 支持: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的 IPv6 支持
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 50490174
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的 IPv6 支持

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

Internet 协议版本 6 (IPv6) 是 Internet 协议 (IP) 的最新版本。IPv6 旨在修正上一版本 IP 协议 IPv4 中的许多不足之处。

在 Microsoft Exchange Server 2013 中，仅在也安装和启用 IPv4 时才支持 IPv6。如果在此配置中已部署 Exchange 2013，并且网络支持 IPv4 和 IPv6，则所有 Exchange 服务器均可在使用 IPv6 地址的设备、服务器和客户端中发送和接收数据。

本主题讨论 Exchange 2013 中的 IPv6 寻址。有关 IPv6 的其他背景信息，请参阅 [IPv6](https://go.microsoft.com/fwlink/p/?linkid=92582)。

**目录**

Exchange 2013 组件中的 IPv6 支持

启用或禁用操作系统中的协议

IPv6 地址基础知识

## Exchange 2013 组件中的 IPv6 支持

下表介绍了 Exchange 2013 中受 IPv6 影响的组件。

### Exchange 2013 的功能和 IPv6

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>功能</th>
<th>支持 IPv6</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>连接筛选代理中的 IP 允许列表和 IP 阻止列表</p></td>
<td><p>是</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>连接筛选代理中的 IP 允许列表提供程序和 IP 阻止列表提供程序</p></td>
<td><p>否</p></td>
<td><p>目前，还没有广为接受的用于查找 IPv6 地址的行业标准协议。大多数 IP 阻止列表提供程序不支持 IPv6 地址。如果在接收连接器上允许来自未知 IPv6 地址的匿名连接，就会提高垃圾邮件发送者绕过 IP 阻止列表提供程序而将垃圾邮件成功传入组织的风险。</p></td>
</tr>
<tr class="odd">
<td><p>协议分析代理中的发件人信誉</p></td>
<td><p>否</p></td>
<td><p>协议分析代理对于来自 IPv6 发件人的邮件不计算发件人信誉级别 (SRL)。有关发件人信誉的详细信息，请参阅<a href="sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md">发件人信誉和协议分析代理</a>。</p></td>
</tr>
<tr class="even">
<td><p>发件人 ID</p></td>
<td><p>是</p></td>
<td><p>有关详细信息，请参阅<a href="sender-id-exchange-2013-help.md">发件人 ID</a>。</p></td>
</tr>
<tr class="odd">
<td><p>接收连接器</p></td>
<td><p>是</p></td>
<td><p>下列组件接受 IPv6 地址：</p>
<ul>
<li><p>本地 IP 地址绑定</p></li>
<li><p>远程 IP 地址</p></li>
<li><p>IP 地址范围</p></li>
</ul>
<p>我们强烈建议不要将接收连接器配置为接受来自未知 IPv6 地址的匿名连接。如果您的组织必须接收来自使用 IPv6 地址的发件人的邮件，应创建一个专用的接收连接器，用于将远程 IP 地址限制在这些发件人使用的特定 IPv6 地址。</p>
<p>有关详细信息，请参阅<a href="receive-connectors-exchange-2013-help.md">接收连接器</a>。</p></td>
</tr>
<tr class="even">
<td><p>发送连接器</p></td>
<td><p>是</p></td>
<td><p>下列组件接受 IPv6 地址：</p>
<ul>
<li><p>智能主机 IP 地址</p></li>
<li><p>边缘传输服务器上配置的发送连接器的 <em>SourceIPAddress</em> 参数</p></li>
</ul>

> [!NOTE]
> 如果要为 <em>SourceIPAddress</em> 参数指定 IPv6 地址，请确保正确配置了相应的 DNS AAAA 和邮件交换 (MX) 记录。如果远程邮件传送服务器对指定的 IPv6 地址尝试进行任何种类的反向查找测试，则这样可帮助确保邮件妥投。

<p>有关详细信息，请参阅<a href="send-connectors-exchange-2013-help.md">发送连接器</a>。</p></td>
</tr>
<tr class="odd">
<td><p>传入邮件速率限制</p></td>
<td><p>部分</p></td>
<td><p>可对接收连接器设置的传入邮件速率限制（如 <em>MaxInboundConnectionPercentagePerSource</em> 参数、<em>MaxInboundConnectionPerSource</em> 参数和 <em>TarpitInterval</em> 参数）仅适用于全局 IPv6 地址。任何指定的传入邮件速率限制都不影响链接本地 IPv6 地址和站点本地 IPv6 地址。</p></td>
</tr>
<tr class="even">
<td><p>统一消息</p></td>
<td><p>是</p></td>
<td><p>有关详细信息，请参阅<a href="ipv6-support-in-unified-messaging-exchange-2013-help.md">统一消息中的 IPv6 支持</a>。</p></td>
</tr>
<tr class="odd">
<td><p>数据库可用性组 (DAG) 成员</p></td>
<td><p>是</p></td>
<td><p>Windows Server 和群集服务支持静态 IPv6 地址。但是，使用静态 IPv6 地址与最佳实践相悖。Exchange 2013 不支持在安装过程中静态 IPv6 地址的配置。</p>
<p>故障转移群集支持站内自动隧道寻址协议 (ISATAP)。这些群集仅支持可以在 DNS 中进行动态注册的 IPv6 地址。不能在群集中使用链接本地地址。</p>
<p>有关 DAG 网络要求的详细信息，请参阅<a href="planning-for-high-availability-and-site-resilience-exchange-2013-help.md">对高可用性和站点恢复的规划</a>中的“网络要求”部分。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 启用或禁用操作系统中的协议

Exchange 2013 服务器完全支持 IPv6 网络。因此，即使您不使用 IPv6，也无需在 Exchange 服务器上禁用 IPv6。

Exchange 2013 中对 IPv6 的支持要求在所有 Exchange 2013 服务器上安装和启用 IPv4。不支持从 Exchange 2013 服务器上卸载 IPv4。

若要了解有关 Microsoft Windows 中的 IPv6 支持的详细信息，请参阅[用于 Microsoft Windows 的 IPv6：常见问题](https://go.microsoft.com/fwlink/p/?linkid=147465)。

返回顶部

## IPv6 地址基础知识

IPv6 地址的长度为 128 位。使用冒号十六进制表示法描述此类地址。冒号十六进制表示法使用以冒号 (:) 分隔的八个 16 位（即 4 位十六进制）数字描述 128 位地址。例如，2001:0DB8:0000:0000:02AA:00FF:C0A8:640A 便是以冒号十六进制表示法表示的 IPv6 地址 。

可使用下列方法表示 IPv6 地址：

  - **禁止以零开头**   在 IPv6 地址中，可省略任何 8 个 4 位十六进制数字中开头的零。

  - **双冒号压缩** 可使用两个冒号 (::) 表示全部由零组成的连续 16 位十六进制数字。这些全部由零组成的数字可出现在 IPv6 地址的开始、中间或结束部分。仅可在 IPv6 地址中使用一次双冒号压缩。

  - **尾部点分十进制表示法** 可通过以句点 (.) 分隔 8 位数字，用点分十进制表示法表示 IPv6 地址尾部的最后 32 位。IPv4 兼容地址经常使用尾部点分十进制表示法。

下表提供了 IPv6 地址表示法和等效 IPv6 地址语法的示例。

### IPv6 地址表示法和语法

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>IPv6 地址表示法</th>
<th>IPv6 地址语法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>完整 IPv6 地址</p></td>
<td><p>2001:0DB8:0000:0000:02AA:00FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>不以零开头的 IPv6 地址</p></td>
<td><p>2001:DB8:0:0:2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="odd">
<td><p>使用双冒号压缩的 IPv6 地址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>使用尾部点分十进制表示法的 IPv6 地址</p></td>
<td><p>2001:DB8::2AA:FF:192.168.100.10</p></td>
</tr>
</tbody>
</table>


IPv6 地址可分为以下几种类型：

  - **单播地址**   数据包发送到一个接口。

  - **多播地址**   数据包发送到多个接口。

  - **任播地址**   数据包发送到多个接口中最近的接口。根据路由开销定义接口之间的距离。

IPv6 单播地址的范围可以如下：

  - **链接本地** IPv6 地址的范围为本地子网。IPv6 链接本地地址类似于自动专用 IP 地址 (APIPA) 中使用的 IPv4 链接本地地址。

  - **站点本地** IPv6 地址的范围为本地组织。RFC 3879 不推荐使用站点本地地址，根据 RFC 4193 中的定义，用唯一本地地址代替站点本地地址。IPv6 站点本地地址和 IPv6 唯一本地地址类似于 IPv4 专用 IP 地址。

  - **全局** IPv6 地址的范围为全局。IPv6 全局地址与 IPv4 公用 IP 地址类似。

下表对 IPv4 元素和 IPv6 元素进行了比较。

### IPv4 与 IPv6 元素

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>项目</th>
<th>IPv4</th>
<th>IPv6</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>专用 IP 地址</p></td>
<td><p>10.0.0.0/8</p>
<p>172.16.0.0/12</p>
<p>192.168.0.0/16</p></td>
<td><p>FD00::/8</p></td>
</tr>
<tr class="even">
<td><p>链接本地地址</p></td>
<td><p>169.254.0.0/16</p></td>
<td><p>FE80::/64</p></td>
</tr>
<tr class="odd">
<td><p>环回地址</p></td>
<td><p>127.0.0.1</p></td>
<td><p>::1</p></td>
</tr>
<tr class="even">
<td><p>未指定的地址</p></td>
<td><p>0.0.0.0</p></td>
<td><p>::</p></td>
</tr>
<tr class="odd">
<td><p>地址解析</p></td>
<td><p>地址解析协议 (ARP)</p></td>
<td><p>邻居发现 (ND)</p></td>
</tr>
<tr class="even">
<td><p>域名系统 (DNS) 主机名解析</p></td>
<td><p>地址记录（A 记录）</p></td>
<td><p>AAAA 记录或 A6 记录</p></td>
</tr>
</tbody>
</table>


有关 IPv6 寻址的详细信息，请参阅 [IPv6 地址类型](https://go.microsoft.com/fwlink/p/?linkid=98357)。

## 支持的 IPv6 地址输入格式

Exchange 2013 中支持以下几种类型的 IPv6 地址输入格式：

  - 单一 IPv6 地址

  - IPv6 地址范围

  - 带有子网掩码的 IPv6 地址

  - IPv6 地址，带有使用无类别域际路由选择 (CIDR) 表示法的子网掩码

下表提供了 Exchange 2013 中可接受的 IPv6 地址输入格式的示例。

### IPv6 地址示例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>IPv6 地址的示例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>单一地址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A</p></td>
</tr>
<tr class="even">
<td><p>地址范围</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414</p></td>
</tr>
<tr class="odd">
<td><p>带有子网掩码的地址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)</p></td>
</tr>
<tr class="even">
<td><p>带有使用 CIDR 表示法的子网掩码的地址</p></td>
<td><p>2001:DB8::2AA:FF:C0A8:640A/64</p></td>
</tr>
</tbody>
</table>


在 Exchange 2013 中，支持以下输入格式：

  - 禁止以零开头

  - 双冒号压缩

  - 尾部点分十进制表示法

返回顶部

