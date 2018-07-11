---
title: '边缘订阅凭据: Exchange 2013 Help'
TOCTitle: 边缘订阅凭据
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61183386
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘订阅凭据

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

本主题介绍边缘订阅进程如何设置用于保护 EdgeSync 订阅进程的凭据，以及 EdgeSync 如何使用这些凭据在 Exchange 2013 邮箱服务器和边缘传输服务器之间建立安全 LDAP 连接。有关边缘订阅进程的详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

**目录**

边缘订阅进程

EdgeSync 复制帐户

验证初始复制

验证计划的同步会话

续订 EdgeSync 复制帐户

## 边缘订阅进程

为边缘传输服务器订阅 Active Directory 站点，以便在 Active Directory 站点中的邮箱服务器与订阅的边缘传输服务器之间建立同步关系。在边缘订阅进程中设置的凭据可以帮助保护邮箱服务器与外围网络中的边缘传输服务器之间的 LDAP 连接。

在边缘传输服务器上运行 **New-EdgeSubscription** cmdlet 时，将在本地服务器的 Active Directory 轻型目录服务 (AD LDS) 目录中创建 EdgeSync bootstrap 复制帐户 (ESBRA) 凭据，并将其写入边缘订阅文件。这些凭据只用于建立初始同步，将在创建边缘订阅文件后 24 小时过期。如果边缘订阅进程未在 24 小时内完成，您将需要再次运行 **New-EdgeSubscription** cmdlet 创建新的边缘订阅文件。边缘订阅 XML 文件存储用于边缘订阅的配置数据。

边缘订阅 XML 文件包含下表所示的数据。

### 边缘订阅文件的内容

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>订阅数据</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>边缘传输服务器的 NetBIOS 名称。边缘订阅的 Active Directory 名称将与此名称匹配。</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>边缘传输服务器的完全限定的域名 (FQDN)。订阅的 Active Directory 站点中的邮箱服务器必须可以使用 DNS 解析 FQDN，以找到边缘传输服务器。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>边缘传输服务器的自签名证书的公钥。</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>为 ESBRA 指定的名称。ESBRA 帐户有以下格式：ESRA.<em>边缘传输服务器名称</em>。ESRA 表示 EdgeSync 复制帐户；请注意 ESBRA（初始 bootstrap 复制帐户）和 ESRA 之间的区别。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>为 ESBRA 指定的密码。密码使用随机数字生成器生成并以明文形式存储在边缘订阅文件中。</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>边缘订阅文件的创建日期。</p></td>
</tr>
<tr class="odd">
<td><p><strong>持续时间</strong></p></td>
<td><p>这些凭据在过期之前的有效时间长度。ESBRA 帐户的有效期只有 24 个小时。</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>将 Active Directory 中的数据同步到 AD LDS 中时绑定到的安全 LDAP 端口 EdgeSync。默认情况下，此端口是 TCP 端口 50636。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>边缘传输服务器的许可信息。在创建边缘订阅之前，您需要许可边缘传输服务器。</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>边缘订阅文件的版本号。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>边缘传输服务器的 Exchange 版本。</p></td>
</tr>
</tbody>
</table>


> [!IMPORTANT]  
> ESBRA 凭据以明文形式写入边缘订阅文件。必须在整个订阅进程中保护此文件。将边缘订阅文件导入 Exchange 组织后，应该立即将边缘订阅文件从边缘传输服务器、用于将文件导入 Exchange 组织的网络共享以及任何可移动媒体中删除。


返回顶部

## EdgeSync 复制帐户

EdgeSync 复制帐户 (ESRA) 是 EdgeSync 安全性的重要组成部分。ESRA 的身份验证和授权机制可以帮助保护边缘传输服务器与邮箱服务器之间的连接。

边缘订阅文件中包含的 ESBRA 用于在初始同步期间建立安全 LDAP 连接。将边缘订阅文件导入要为边缘传输服务器订阅的 Active Directory 站点中的邮箱服务器之后，在 Active Directory 中为每个边缘传输服务器/邮箱服务器对创建其他 ESRA 帐户。在初次同步期间，新建的 ESRA 凭据会复制到 AD LDS。这些 ESRA 凭据可以帮助保护以后的同步会话。

为每个 EdgeSync 复制帐户指定下表中所示的属性。

### Ms-Exch-EdgeSyncCredential 属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>字符串</p></td>
<td><p>接受这些凭据的边缘传输服务器。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>字符串</p></td>
<td><p>提供这些凭据的邮箱服务器。如果凭据是 bootstrap 凭据，则此值为空。</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>日期时间 (UTC)</p></td>
<td><p>此凭据的生效时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>日期时间 (UTC)</p></td>
<td><p>此凭据的过期时间。</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>字符串</p></td>
<td><p>用于进行身份验证的用户名。</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>字节</p></td>
<td><p>用于进行身份验证的密码。该密码使用 <strong>ms-Exch-EdgeSync-Certificate</strong> 进行加密。</p></td>
</tr>
</tbody>
</table>


下列各节介绍如何在 EdgeSync 同步进程中设置和使用 ESRA 凭据。

## 设置 EdgeSync bootstrap 复制帐户

在边缘传输服务器上运行 **New-EdgeSubscription** cmdlet 时，ESBRA 的设置如下所述：

  - 在边缘传输服务器上创建一个自签名证书 (Edge-Cert)。私钥存储在本地计算机存储中，公钥被写入边缘订阅文件。

  - 在 AD LDS 中创建 ESBRA 帐户，凭据被写入边缘订阅文件。

  - 将边缘订阅文件复制到可移动媒体将其导出（因为边缘服务器不在 Active Directory 中，因此您无法使用共享文件夹导出文件）。现在，该文件可以导入邮箱服务器。

## 在 Active Directory 中设置 EdgeSync 复制帐户

在邮箱服务器上导入边缘订阅文件时，会通过下列步骤在 Active Directory 中建立边缘订阅记录并提供其他 ESRA 凭据：

1.  在 Active Directory 中创建一个边缘传输服务器配置对象。Edge-Cert 证书被作为属性写入此对象。

2.  订阅的 Active Directory 站点中的每个邮箱服务器都会收到一条 Active Directory 通知，表明新边缘订阅已注册。每个邮箱服务器在收到通知后，会立即检索 ESRA.edge 帐户并使用 Edge-Cert 公钥为该帐户加密。加密后的 ESRA.edge 帐户将被写入边缘传输服务器配置对象。

3.  每个邮箱服务器都会创建自签名证书 (TransportService-Cert)。私钥存储在本地计算机存储中，公钥存储在 Active Directory 的邮箱服务器配置对象中。

4.  每个邮箱服务器使用自己的 TransportService 证书的公钥为 ESRA.edge 帐户加密，然后将其存储在自己的配置对象中。

5.  每个邮箱服务器为 Active Directory 中的每个现有边缘传输服务器配置对象生成 ESRA (ESRA.edge. *Mailboxname.\#*)。
    
    示例：ESRA.edge.Example.0
    
    ESRA.edge 的密码通过随机数字生成器生成，并使用 TransportService-Cert 证书的公钥进行加密。生成的密码为 Windows Server 允许的最大长度。

6.  每个 ESRA.edge. *Mailboxname.\#* 帐户使用 Edge-Cert 证书的公钥进行加密，并存储在 Active Directory 的边缘传输服务器配置对象中。

以下各节说明在 EdgeSync 同步过程中如何使用这些帐户。

返回顶部

## 验证初始复制

初始 ESBRA 帐户仅在建立初始同步时使用。在初始 EdgeSync 同步期间，其他 ESRA 帐户 ESRA.edge.*Mailboxname.\#* 将被复制到 AD LDS。这些帐户用于对以后的 EdgeSync 同步会话进行身份验证。

执行初始复制的邮箱服务器是随机确定的。Active Directory 站点中第一个执行拓扑扫描并发现新边缘订阅的邮箱服务器将执行初始复制。由于此发现基于拓扑扫描的时间设置，因此该站点中的任何邮箱服务器都可能会执行初始复制。

EdgeSync 启动从邮箱服务器到边缘传输服务器的安全 LDAP 会话。边缘传输服务器提供其自签名证书，邮箱服务器验证该证书与 Active Directory 的边缘传输服务器配置对象中存储的证书是否匹配。验证了边缘传输服务器的身份之后，邮箱服务器向边缘传输服务器提供 ESRA.edge.*Mailboxname.\#* 帐户的凭据。边缘传输服务器根据 AD LDS 中存储的帐户来验证凭据。

然后，邮箱服务器上的 EdgeSync 服务将拓扑、配置和收件人数据从 Active Directory 推送到 AD LDS。对 Active Directory 中的边缘传输服务器配置对象所做的更改将被复制到 AD LDS。AD LDS 接收新添加的 ESRA.edge.*Mailboxname.\#* 条目，而 Microsoft Exchange 凭据服务创建相应的 AD LDS 帐户。现在，可以使用这些帐户对以后计划的 EdgeSync 同步会话进行身份验证。

## Microsoft Exchange 凭据服务

Microsoft Exchange 凭据服务是边缘订阅进程的一部分。凭据服务仅在边缘传输服务器上运行。此服务在 AD LDS 中创建互补的 ESRA 帐户，使邮箱服务器可以对边缘传输服务器进行身份验证，以便执行 EdgeSync 同步。EdgeSync 不会直接与 Microsoft Exchange 凭据服务进行通信。Microsoft Exchange 凭据服务与 AD LDS 进行通信，并且只要邮箱服务器更新了 ESRA 凭据，就立即进行安装。

返回顶部

## 验证计划的同步会话

初始 EdgeSync 同步完成后，将制订 EdgeSync 同步计划，在 AD LDS 中定期更新已更改的任何 Active Directory 数据。邮箱服务器与边缘传输服务器上的 AD LDS 实例建立安全 LDAP 会话。AD LDS 通过提供其自签名证书，向该邮箱服务器证明其身份。邮箱服务器将其 ESRA.edge 凭据提供给 AD LDS。ESRA.edge 密码使用邮箱服务器的自签名证书的公钥进行加密。仅该特定的邮箱服务器才能使用这些凭据向 AD LDS 进行身份验证。

返回顶部

## 续订 EdgeSync 复制帐户

ESRA 帐户的密码必须符合本地服务器的密码策略。为了避免密码续订进程造成暂时的身份验证失败，请在第一个 ESRA.edge 帐户过期前七天创建另一个 ESRA.edge 帐户，其生效时间在第一个 ESRA 过期时间之前的三天。只要第二个 ESRA.edge 帐户生效，EdgeSync 就会停止使用第一个帐户，并开始使用第二个帐户。到达第一个帐户的过期时间时，将删除这些 ESRA 凭据。此续订进程将继续进行，直到删除了边缘订阅。

返回顶部

