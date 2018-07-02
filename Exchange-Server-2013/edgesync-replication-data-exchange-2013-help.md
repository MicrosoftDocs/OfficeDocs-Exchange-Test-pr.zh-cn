---
title: 'EdgeSync 复制数据: Exchange 2013 Help'
TOCTitle: EdgeSync 复制数据
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61183398
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# EdgeSync 复制数据

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

部署边缘传输服务器时，它无法访问 Active Directory。若要执行收件人查找和安全列表聚合任务，以及使用相互传输层安全性 (MTLS) 身份验证实现域安全性，边缘传输服务器需要 Active Directory 中的数据。这些数据通过 EdgeSync 复制到边缘传输服务器，边缘传输服务器将所有复制的信息存储在 Active Directory 轻型目录服务 (AD LDS) 中。

本主题重点介绍从 Active Directory 复制到订阅到 Active Directory 站点的边缘传输服务器的数据。有关 EdgeSync 和边缘订阅的详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

有四种类型的数据被复制到 AD LDS 并为边缘传输服务器所用：

边缘订阅信息

配置信息

收件人信息

拓扑信息

## 边缘订阅信息

Exchange 2013 扩展 Active Directory 和 AD LDS 架构，以提供 **ms-Exch-ExchangeServer** 对象的属性，从而提供控制 EdgeSync 同步所需的数据。这些属性为 EdgeSync 提供三项功能：

  - 自动设置和维护用于帮助保护邮箱服务器和订阅的边缘传输服务器之间的 LDAP 连接的凭证。

  - 仲裁同步锁定和租用进程，以确保一次只有一个服务器尝试与单个边缘传输服务器进行同步。有关锁定进程和租用进程的详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

  - 优化 EdgeSync 同步，以维护当前同步状态的记录。轻松查看同步状态可帮助避免过多的手动同步。

下表中的架构扩展特定于边缘订阅。分配给这些属性的值由边缘订阅和 EdgeSync 进行维护，不可手动编辑。

### 边缘订阅的架构扩展

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>服务器所使用的证书的当前公钥。边缘传输服务器和邮箱服务器均存储此值。在 LDAP 和 SMTP 通信期间，公钥用于对用来验证服务器身份的凭据进行加密。</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>EdgeSync 用于与 AD LDS 建立经过身份验证的 LDAP 会话的凭据列表。在邮箱服务器上，此属性只包含邮箱服务器用于对订阅的边缘传输服务器进行身份验证的凭据。在边缘传输服务器上，此属性包含订阅的 Active Directory 站点中参与 EdgeSync 同步的每个邮箱服务器的凭据。该属性只存在于运行 EdgeSync 同步的邮箱服务器以及订阅的边缘传输服务器上。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>如果多个邮箱服务器尝试向同一个边缘传输服务器复制数据，则使用此属性在邮箱服务器之间进行仲裁。</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>仅存在于边缘传输服务器对象的 AD LDS 中。此属性跟踪向 AD LDS 实例复制数据的状态，并包含有关复制的信息。</p></td>
</tr>
</tbody>
</table>


返回顶部

## 配置信息

将边缘传输服务器订阅到组织时，可以从组织内部管理边缘传输服务器和 Exchange 组织中常见的配置对象。然后，使用 EdgeSync 将这些更改复制到边缘传输服务器。此进程有助于使参与邮件处理的所有服务器上的配置保持一致。

必须还要在边缘传输服务器上维护 Exchange 组织的配置数据的一个子集。在 EdgeSync 同步期间，边缘传输服务器所需的配置数据将被写入 AD LDS 的配置分区。写入 AD LDS 的配置数据包括：

  - **邮箱服务器**   订阅的 Active Directory 站点中每个邮箱服务器的完全限定的域名 (FQDN) 可供边缘传输服务器上的本地 AD LDS 存储使用。使用此信息派生入站发送连接器的智能主机服务器列表。

  - **接受域**   为 Exchange 组织配置的所有权威域、内部中继域和外部中继域均将写入 AD LDS。接受域可供边缘传输服务器使用后，Exchange 组织可以尽早地执行域筛选并拒绝无效的 SMTP 通信传入组织。有关接受域的详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

  - **邮件分类**   如果可以在边缘传输服务器上进行邮件分类，那么传输代理和内容转换就可以作用于外围网络中的邮件分类。例如，附件筛选器代理可以在删除附件时应用“附件已删除”分类，同时向 Microsoft Outlook 用户或 Outlook Web App 发送信息性文本，告诉收件人所发生的情况。为第三方应用程序开发的代理可以通过类似的方式使用邮件分类。

  - **远程域**   为 Exchange 组织配置的所有远程域条目都将被写入 AD LDS。远程域条目控制远程域的“外出”邮件设置以及邮件格式设置。有关远程域的详细信息，请参阅[远程域](remote-domains-exchange-2013-help.md)。

  - **发送连接器**   默认情况下，创建边缘订阅会自动创建发送连接器，这些发送连接器是订阅边缘传输服务器时在 Exchange 组织和 Internet 之间实现端到端邮件流所必需的。边缘传输服务器上所有现有的发送连接器均将被删除。如果希望配置其他发送连接器，则在 Exchange 组织内部配置发送连接器，然后选择边缘订阅作为连接器的源服务器。有关详细信息，请参阅[边缘订阅](edge-subscriptions-exchange-2013-help.md)。

  - **内部 SMTP 服务器** *InternalSMTPServers* 属性的值存储在 Exchange 组织和本地边缘传输服务器的 **TransportConfig** 对象上。在 EdgeSync 同步期间，存储在本地边缘传输服务器对象上的值将被 Exchange 组织的此对象上存储的值覆盖。此属性指定发件人 ID 筛选和连接筛选应忽略的内部 SMTP 服务器 IP 地址或 IP 地址范围的列表。

  - **域安全列表** *TLSReceiveDomainSecureList* 和 *TLSSendDomainSecureList* 属性存储在 Exchange 组织和本地边缘传输服务器的 **TransportConfig** 对象上。在 EdgeSync 同步期间，存储在本地边缘传输服务器对象上的值将被 Exchange 组织的此对象上存储的值覆盖。这些属性指定为相互 TLS 身份验证配置的远程域列表。

返回顶部

## 收件人信息

复制到 AD LDS 的收件人信息只包括收件人属性的子集。只复制了边缘传输服务器执行某些反垃圾邮件任务所需的数据。复制到 AD LDS 的收件人信息包括：

  - **收件人**Exchange 组织中的收件人列表将复制到 AD LDS。每个收件人由分配的 Active Directory GUID 进行标识。如果将某个收件人的帐户配置为拒绝接收来自组织外部的邮件，则该收件人不会被复制到 AD LDS。如果禁用或删除某个收件人的邮箱，则该邮箱不会再被复制到 AD LDS。

  - **代理地址**   为每个收件人分配的所有代理地址均将以哈希数据的形式复制到 AD LDS。此哈希数据是使用安全哈希算法 (SHA)-256 的单向哈希数据。SHA-256 为原始邮件生成一个 256 位的邮件摘要。通过将代理地址存储为哈希数据的形式，可以在边缘传输服务器或 AD LDS 存在安全风险时帮助保护这些信息。边缘传输服务器执行收件人查找反垃圾邮件任务时引用代理地址。

  - **安全发件人列表、阻止发件人列表和安全收件人列表**   在每个收件人的 Outlook 实例中定义的安全发件人列表、阻止发件人列表和安全收件人列表聚合在一起并复制到 AD LDS。这些设置存储在收件人邮箱所在的邮箱数据库中。Outlook 用户的安全列表集合是来自用户的安全发件人列表、安全收件人列表、阻止发件人列表和外部联系人的组合数据。通过使安全列表集合数据可以在 AD LDS 中使用，边缘传输服务器可以正确地屏蔽发件人，从而减少与筛选邮件有关的操作开销。这些信息以哈希数据的形式发送。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>尽管安全收件人数据存储在 Outlook 中，并且可以聚合到边缘传输服务器的 AD LDS 实例上的安全列表集合中，但内容筛选功能对安全收件人数据不起作用。</td>
    </tr>
    </tbody>
    </table>


  - **每个收件人的反垃圾邮件设置**   使用 **Set-Mailbox** cmdlet 可以为每个收件人分配反垃圾邮件阈值设置（与组织范围的反垃圾邮件设置不同）。如果配置了每个收件人的反垃圾邮件设置，这些设置将覆盖组织范围的设置。通过将每个收件人的设置复制到 AD LDS，可以在将邮件中继到 Exchange 组织之前考虑每一收件人设置。这些信息以哈希数据的形式发送。

返回顶部

## 拓扑信息

拓扑信息包括新订阅了站点的边缘传输服务器或已删除的边缘订阅的通知。这些数据每隔五分钟刷新一次。

返回顶部

