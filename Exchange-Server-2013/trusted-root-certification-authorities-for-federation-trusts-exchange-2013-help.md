---
title: '联合身份验证信任的受信任根证书颁发机构: Exchange 2013 Help'
TOCTitle: 联合身份验证信任的受信任根证书颁发机构
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50491613
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 联合身份验证信任的受信任根证书颁发机构

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2017-07-26_

要建立联合身份验证信任关系 Microsoft Exchange Server 2013组织和[Azure Active Directory 验证系统](https://go.microsoft.com/fwlink/p/?linkid=135986)，您需要用来创建信任的Exchange服务器上安装数字证书。我们强烈建议使用自签名的证书。创建并使用Exchange 管理中心 (EAC) 中**启用联合身份验证信任**向导时自动安装一个自签名的证书。

如果不想使用推荐的自签名证书，则应从 Microsoft 信任的证书颁发机构 (CA) 请求并安装 X.509 安全套接字层 (SSL) 证书。虽然也可以使用其他 CA 颁发的证书建立与 Azure AD 身份验证系统的联合身份验证信任，但它们迄今尚未得到 Microsoft 的认证。

下表列出了当前受 Microsoft 信任的 CA。这些 CA 已经过 Exchange 2013 使用测试。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>CA 友好名称</th>
<th>颁发者</th>
<th>预期目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Comodo 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>Baltimore CyberTrust 根证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Digicert 全局根证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>Digicert 高保证 EV</p></td>
<td><p>Digicert 全局根证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net 安全服务器证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>Entrust (2048)</p></td>
<td><p>Entrust.net 安全服务器证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax 安全证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>GlobalSign 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>Network Solutions 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Comodo 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>SECOM Trust Systems 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Comodo 证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Class 3 主要公用证书颁发机构</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign 信任网络</p></td>
<td><p>服务器身份验证，客户端身份验证</p></td>
</tr>
</tbody>
</table>


有关联合身份验证信任证书要求的详细信息，请参阅[联盟](federation-exchange-2013-help.md)。

