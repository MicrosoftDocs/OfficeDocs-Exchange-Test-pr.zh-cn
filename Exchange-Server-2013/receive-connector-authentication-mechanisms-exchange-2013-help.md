---
title: '接收连接器身份验证机制: Exchange 2013 Help'
TOCTitle: 接收连接器身份验证机制
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50491176
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 接收连接器身份验证机制

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_


接收连接器的身份验证机制如下所示：


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>身份验证机制</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>无</p></td>
<td><p>无需身份验证。</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>公布 STARTTLS。要求提供服务器证书以提供 TLS。</p></td>
</tr>
<tr class="odd">
<td><p>集成</p></td>
<td><p>NTLM 和 Kerberos（集成的 Windows 身份验证）。</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>基本身份验证。需要在登录时进行身份验证。</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>基于 TLS 的基本身份验证。需要服务器证书。</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange Server 身份验证（通用安全服务应用程序编程接口 (GSSAPI） 和相互 GSSAPI）。</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>该连接因使用 Exchange 外部安全机制而被视为外部安全连接。该连接可能是 Internet 协议安全性 (IPsec) 关联或虚拟专用网络 (VPN)。或者，服务器可能驻留在受信任的物理控制网络中。<code>ExternalAuthoritative</code> 身份验证方法需要 <code>ExchangeServers</code> 权限组。这种将身份验证方法与安全组结合使用的做法，允许对通过该连接器接收的邮件的匿名发件人电子邮件地址进行解析。</p></td>
</tr>
</tbody>
</table>


有关接收连接器身份验证机制的详细信息，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

