---
title: '边缘订阅: Exchange 2013 Help'
TOCTitle: 边缘订阅
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61183389
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘订阅

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

边缘传输服务器通过处理所有面向 Internet 的邮件流，并为您的 Exchange 组织提供 SMTP 中继和智能主机服务，从而最大限度地缩小了攻击面。在您组织外围网络中的边缘传输服务器上运行的一系列代理提供了额外的邮件保护和安全层。这些代理支持可抵御病毒和垃圾邮件危害的功能，并应用传输规则来控制消息流。

边缘订阅可使用 Active Directory 数据填充边缘传输服务器上的 Active Directory 轻型目录服务 (AD LDS) 实例。虽然可以视需要选择创建边缘订阅，但如果将边缘传输服务器订阅到 Exchange 组织，则可以带来更简单的管理体验，并能改进反垃圾邮件功能。如果您计划使用收件人查找或安全列表聚合，或计划使用相互传输层安全性 (MTLS) 帮助保护与合作伙伴域的 SMTP 通信，则需要创建边缘订阅。

**目录**

边缘订阅进程

Microsoft Exchange EdgeSync 服务

管理边缘订阅

## 边缘订阅进程

边缘传输服务器并不拥有对 Active Directory 的直接访问权限。边缘传输服务器用来处理邮件的配置和收件人信息均存储在本地 AD LDS 中。创建边缘订阅后，可以自动将信息从 Active Directory 安全地复制到 AD LDS。边缘订阅进程会设置凭据，用于在 Exchange 2013 邮箱服务器和订阅的边缘传输服务器之间建立安全的 LDAP 连接。邮箱服务器上运行的 Microsoft Exchange EdgeSync 服务 (EdgeSync) 会定期运行单向同步，将最新的数据传输到 AD LDS。这样就可以通过允许您配置邮箱服务器并将信息同步到边缘传输服务器，减少您在外围网络中执行的管理任务。

将边缘传输服务器订阅到包含负责以下工作的邮箱服务器的 Active Directory 站点：传输传入或传出边缘传输服务器的邮件。边缘订阅过程会为边缘传输服务器创建 Active Directory 站点成员资格关联。通过站点关联，Exchange 组织中的邮箱服务器可以将邮件中继到边缘传输服务器，以传递到 Internet，而不必配置显式发送连接器。

可以将一个或多个边缘传输服务器订阅到一个 Active Directory 站点，但不能将一个边缘传输服务器订阅到多个 Active Directory 站点。如果您已部署多个边缘传输服务器，则可以将每个服务器订阅到不同的 Active Directory 站点。每个边缘传输服务器需要各自的边缘订阅。

若要部署边缘传输服务器并将其订阅到 Active Directory 站点，请按照下列步骤操作：

1.  安装边缘传输服务器角色。

2.  验证邮箱服务器和边缘传输服务器能否使用 DNS 名称解析找到对方。

3.  在邮箱服务器上，配置要复制到边缘传输服务器的对象和设置。

4.  在边缘传输服务器上，创建并导出边缘订阅文件。

5.  将边缘订阅文件复制到邮箱服务器，或复制到可从包含邮箱服务器的 Active Directory 站点进行访问的文件共享。

6.  将边缘订阅文件导入 Active Directory 站点。

## 新建边缘订阅后会出现什么情况

通过在边缘传输服务器上运行 **New-EdgeSubscription** cmdlet 创建边缘订阅文件时，会触发下列操作：

  - 创建名为 EdgeSync 启动加载程序复制帐户 (ESBRA) 的 AD LDS 帐户。此类 ESBRA 凭据用于验证与边缘传输服务器的初次 EdgeSync 连接。此帐户配置为在创建 24 小时后过期。因此，您需要在 24 小时内完成上述部分中介绍的 6 步订阅过程。如果 ESBRA 在边缘订阅过程完成之前过期，则您需要再次运行 **New-EdgeSubscription** cmdlet，以新建一个边缘订阅文件。

  - 从 AD LDS 检索 ESBRA 凭据并写入边缘订阅文件。边缘传输服务器的自签名证书的公钥也会导出到边缘订阅文件。写入边缘订阅文件的凭据是导出该文件的服务器的专用凭据。

  - 之前在边缘传输服务器上创建、现在将从 Active Directory 复制到 AD LDS 的任何配置对象都会从 AD LDS 中删除，并且用于配置这些对象的 Exchange 命令行管理程序 cmdlet 也会禁用。不过，您仍然可以使用 **Get-\*** cmdlet 来查看这些对象。运行 **New-EdgeSubscription** cmdlet 会在边缘传输服务器上禁用下列 cmdlet：
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

通过在邮箱服务器上运行 **New-EdgeSubscription** cmdlet 在邮箱服务器上导入边缘订阅文件后：

  - 创建边缘订阅，从而将边缘传输服务器加入到 Exchange 组织中。EdgeSync 会将配置数据传播到此边缘传输服务器，从而在 Active Directory 中创建一个边缘配置对象。

  - Active Directory 站点中的每个邮箱服务器会从 Active Directory 收到有关已订阅新的边缘传输服务器的通知。邮箱服务器从边缘订阅文件中检索 ESBRA。然后，邮箱服务器使用边缘传输服务器的自签名证书的公钥对 ESBRA 进行加密。加密后的凭据将写入边缘配置对象。

  - 每个邮箱服务器还使用自己的公钥对 ESBRA 进行加密，然后将凭据存储在自己的配置对象中。

  - 在 Active Directory 中为每个边缘传输邮箱服务器对创建 EdgeSync 复制帐户 (ESRA)。每个邮箱服务器将其 ESRA 凭据存储为邮箱服务器配置对象的属性。

  - 自动创建发送连接器，以便将出站邮件从边缘传输服务器中继到 Internet，并将入站邮件从边缘传输服务器中继到 Exchange 组织。

  - 邮箱服务器上运行的 Microsoft Exchange EdgeSync 服务使用 ESBRA 凭据在邮箱服务器与边缘传输服务器之间建立安全的 LDAP 连接，并执行初始数据复制。下列数据将被复制到 AD LDS：
    
      - 拓扑数据
    
      - 配置数据
    
      - 收件人数据
    
      - ESRA 凭据

  - 边缘传输服务器上运行的 Microsoft Exchange 凭据服务安装 ESRA 凭据。这些凭据用于验证并保护以后的同步连接。

  - 制订 EdgeSync 同步计划。

然后，在已订阅的 Active Directory 站点中的邮箱服务器上运行的 Microsoft Exchange EdgeSync 服务会定期将数据从 Active Directory 单向复制到 AD LDS。您还可以使用 **Start-EdgeSynchronization** cmdlet 替代 EdgeSync 同步计划并立即开始同步。

若要详细了解 ESRA 帐户以及如何使用这些帐户帮助保护 EdgeSync 同步进程，请参阅[边缘订阅凭据](edge-subscription-credentials-exchange-2013-help.md)。

本示例将边缘传输服务器订阅到指定站点，并自动创建 Internet 发送连接器以及从该边缘传输服务器连接到邮箱服务器的发送连接器。

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 

> [!NOTE]  
> <em>CreateInternetSendConnector</em> 和 <em>CreateInboundSendConnector</em> 参数的默认值均为 <code>$true</code>（仅供演示）。


本示例导出边缘订阅文件。

```powershell
New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"
```

> [!NOTE]  
> 在边缘传输服务器上运行 <strong>New-EdgeSubscription</strong> cmdlet 时，系统会提示您确认将禁用的命令以及边缘传输服务器上将覆盖的配置。若要绕过此确认，则必须使用 <em>Force</em> 参数。如果使用 <strong>New-EdgeSubscription</strong> cmdlet，则会发现此参数很有用。<em>Force</em> 参数还用于覆盖与您在重新订阅边缘传输服务器时要创建的文件同名的现有文件。


有关语法和参数的详细信息，请参阅 [New-EdgeSubscription](https://technet.microsoft.com/zh-cn/library/bb123800\(v=exchg.150\))。

## 发送在边缘订阅过程中创建的连接器

默认情况下，当您通过将边缘订阅文件导入邮箱服务器完成推荐的边缘订阅过程时，启用 Internet 与 Exchange 组织之间的端到端邮件流所需的发送连接器会自动创建，并且边缘传输服务器上的任何现有发送连接器都会删除。在某些情况下，您可以选择取消自动创建发送连接器，然后手动配置发送连接器。有关手动配置发送连接器的详细信息，请参阅[手动配置边缘传输服务器邮件流](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md)和[不使用 EdgeSync 的情况下通过边缘传输服务器配置 Internet 邮件流](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)。

边缘订阅进程设置下列发送连接器：

  - 配置为从 Exchange 组织向 Internet 中继电子邮件的发送连接器。

  - 配置为从边缘传输服务器向 Exchange 组织中继电子邮件的发送连接器。

此外，将边缘传输服务器订阅到 Exchange 组织还允许已订阅的 Active Directory 站点中的邮箱服务器使用组织间发送连接器将邮件中继到边缘传输服务器。

## 自动创建从 Internet 接收邮件的入站发送连接器

默认情况下，当您在邮箱服务器上运行 **New-EdgeSubscription** cmdlet 时，入站发送连接器参数 *CreateInboundSendConnector* 的值会设置为 `$true`。这就创建了向 Exchange 组织发送邮件所需的发送连接器。下表介绍了此发送连接器的配置。

### 入站发送连接器的自动配置

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Inbound to &lt;<em>站点名</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>地址空间中的 <code>--</code> 值代表 Exchange 组织的所有权威和内部中继接受的域。边缘传输服务器针对这些接受的域收到的所有邮件都会路由至此发送连接器并中继到智能主机。</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>边缘订阅名称</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>智能主机列表中的 <code>--</code> 值代表已订阅的 Active Directory 站点中的所有邮箱服务器。您在建立边缘订阅后向已订阅的 Active Directory 站点添加的任何邮箱服务器均不参与 EdgeSync 同步过程。不过，这些邮箱服务器会自动添加到自动创建的入站发送连接器的智能主机列表中。如果多个邮箱服务器位于已订阅的 Active Directory 站点中，则入站连接会在智能主机之间平衡负载。</p></td>
</tr>
</tbody>
</table>


无法在创建时修改自动创建的入站发送连接器的地址空间或智能主机列表。不过，您可以在创建边缘订阅时将 *CreateInboundSendConnector* 参数的值设置为 `$false`。这样，您便可以手动配置从边缘传输服务器连接到 Exchange 组织的发送连接器。

## 自动创建向 Internet 发送邮件的出站发送连接器

默认情况下，当您在邮箱服务器上运行 **New-EdgeSubscription** cmdlet 时，出站发送连接器参数 *CreateInternetSendConnector* 的值会设置为 `$true`。这就创建了向 Internet 发送邮件所需的发送连接器。下表显示此发送连接器的默认配置。

### Internet 发送连接器的自动配置

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>站点名</em>&gt; to Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>边缘订阅名称</em>&gt;</p>

> [!NOTE]  
> 边缘订阅的名称与订阅的边缘传输服务器的名称相同。

</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


如果将多个边缘传输服务器订阅到同一个 Active Directory 站点，则不会创建连接到 Internet 的其他任何发送连接器。相反，所有边缘订阅会作为源服务器添加到同一发送连接器。到 Internet 的出站连接会在各个已订阅的边缘传输服务器之间平衡此负载。

出站发送连接器配置为使用将域名解析为 MX 资源记录的 DNS 路由，从 Exchange 组织向所有远程 SMTP 域发送电子邮件。有关手动配置连接器配置的详细信息，请参阅[手动配置边缘传输服务器邮件流](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md)。

## Microsoft Exchange EdgeSync 服务

在您将边缘传输服务器订阅到 Active Directory 站点之后，EdgeSync 会将配置和收件人数据复制到边缘传输服务器。该服务将下列数据从 Active Directory 复制到 AD LDS：

  - 发送连接器配置

  - 接受域

  - 远程域

  - 邮件分类

  - 安全发件人列表

  - 阻止发件人列表

  - 收件人

  - 用于与伙伴的域安全通信的发送和接收域列表

  - 列为组织传输配置内部的 SMTP 服务器列表

  - 已订阅的 Active Directory 站点中的邮箱服务器的列表

若要详细了解复制到 AD LDS 的数据及其使用方式，请参阅 [EdgeSync 复制数据](edgesync-replication-data-exchange-2013-help.md)。

EdgeSync 使用相互进行身份验证和授权的安全 LDAP 通道将数据从邮箱服务器传输到边缘传输服务器。

为了将数据复制到 AD LDS，邮箱服务器绑定到全局编录服务器以检索更新的数据。EdgeSync 在邮箱服务器和已订阅的边缘传输服务器之间启动通过非标准 TCP 端口 50636 的安全 LDAP 会话。

当您首次将边缘传输服务器订阅到 Active Directory 站点时，使用来自 Active Directory 的数据填充 AD LDS 的初始复制可能需要 5 分钟或更长的时间才能完成，具体取决于目录服务中的数据量。初始复制后，EdgeSync 只同步新的和已更改的对象，并删除任何已删除的对象。

## 同步计划

不同类型的数据按照不同的计划进行同步。EdgeSync 同步计划指定两次 EdgeSync 同步之间的最长时间间隔。按下列间隔进行 EdgeSync 同步：

  - 配置数据：3 分钟。

  - 收件人数据：5 分钟。

  - 拓扑数据：5 分钟。

如果您想更改这些时间间隔，请使用 **Set-EdgeSyncServiceConfig** cmdlet。在邮箱服务器上运行 **Start-EdgeSynchronization** cmdlet 可以强制边缘订阅同步替代下一个计划 EdgeSync 同步的计时器，并立即启动 EdgeSync。

## 选择邮箱服务器

每一个已订阅的边缘传输服务器均与特定的 Active Directory 站点相关联。如果站点中存在多个邮箱服务器，则任何一个邮箱服务器都可以将数据复制到已订阅的边缘传输服务器。为了避免同步时邮箱服务器之间发生争用，首选邮箱服务器的选择如下所示：

1.  Active Directory 站点中第一个执行拓扑扫描并发现新边缘订阅的邮箱服务器执行初始复制。由于此发现基于拓扑扫描的时间安排，因此该站点中的任何邮箱服务器都可以执行初始复制。

2.  执行初始复制的邮箱服务器设立 EdgeSync 租用选项并为边缘订阅设置锁定。租用选项将该特定邮箱服务器设立为向相应的边缘传输服务器提供同步服务的首选服务器。该锁定可以防止在其他邮箱服务器上运行的 EdgeSync 接管租用选项。

3.  EdgeSync 租用选项持续有效一个小时。在这一个小时内，其他任何 EdgeSync 服务都不能接管该选项，除非在时间结束之前启动了手动同步。如果首选邮箱服务器在手动同步启动时无法提供 EdgeSync 服务，则等待 5 分钟，之后该锁定会解除，其他 EdgeSync 服务可以接管租用选项并执行同步。

4.  除非启动手动同步，否则同步按照 EdgeSync 同步计划执行。如果首选服务器在计划同步执行时不可用，则等待 5 分钟，之后该锁定会解除，其他 EdgeSync 服务可以接管租用选项并执行同步。

这种锁定和租用方法可以避免多个 EdgeSync 实例同时将数据推送到同一个边缘传输服务器。

> [!NOTE]  
> 如果已订阅的 Active Directory 站点中还有 Exchange 2010 或 Exchange 2007 邮箱服务器，那么 Exchange 2013 邮箱服务器将始终获得优先权并执行复制。


> [!NOTE]  
> 当您将边缘传输服务器订阅到 Active Directory 站点时，Active Directory 站点中安装的所有邮箱服务器均可以参与 EdgeSync 同步过程。如果删除其中一个服务器，则剩余邮箱服务器上运行的 EdgeSync 服务将继续执行数据同步过程。不过，如果您在 Active Directory 站点中安装新的邮箱服务器，则它们不会自动参与 EdgeSync 同步。如果要启用这些新邮箱服务器，使其能够参与 EdgeSync 同步，您需要重新订阅边缘传输服务器。


下表列出了与锁定和租用相关的 EdgeSync 属性。使用 **Set-EdgeSyncServiceConfig** cmdlet 可配置这些属性。

### EdgeSync 租用属性

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>默认值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code>（5 分钟）</p></td>
<td><p>此设置确定特定 EdgeSync 服务获取锁定的时间。如果保持此锁定的邮箱服务器上的 EdgeSync 服务没有响应，那么在 5 分钟后另一个邮箱服务器上的 EdgeSync 服务将接管租用选项。强制即时 EdgeSync 同步不替代此设置。</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code>（1 小时）</p></td>
<td><p>此设置确定 EdgeSync 服务可以在边缘传输服务器上声明租用选项的时间。如果接管租用选项的 EdgeSync 服务不可用，并且在此选项的期限内没有重启，那么其他任何 Exchange EdgeSync 服务都不会接管该租用选项，除非您强制进行 EdgeSync 同步。</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code>（1 分钟）</p></td>
<td><p>此设置确定在 EdgeSync 服务已获取对边缘传输服务器的锁定后锁定字段的更新频率。</p></td>
</tr>
</tbody>
</table>


## 准备运行 EdgeSync 服务

您必须确保基础结构和邮箱服务器已为运行 EdgeSync 服务做好准备，然后才能将边缘传输服务器订阅到 Exchange 组织。若要为 EdgeSync 同步做好准备，您需要执行以下操作：

  - 验证将边缘传输服务器与 Exchange 组织隔离的外围网络防火墙是否配置为通过正确的端口进行通信。边缘传输服务器将使用非标准 LDAP 端口。如果您的环境需要特定的端口，您可以使用同 Exchange 一起提供的 ConfigureAdam.ps1 脚本修改 AD LDS 使用的端口。有关详细信息，请参阅[修改 AD LDS 配置](modify-ad-lds-configuration-exchange-2013-help.md)。在创建边缘订阅之前修改端口。如果在创建边缘订阅后修改端口，则需要删除边缘订阅并创建新的边缘订阅。默认情况下，使用下列 LDAP 端口访问 AD LDS：
    
      - **LDAP**   在本地使用端口 50389/TCP 绑定到 AD LDS 实例。不必在外围网络防火墙上打开此端口。
    
      - **安全 LDAP**   使用端口 50636/TCP 从邮箱服务器向 AD LDS 同步目录。若要成功地进行 EdgeSync 同步，此端口必须在防火墙上处于打开状态。

  - 验证从边缘传输服务器到邮箱服务器以及从邮箱服务器到边缘传输服务器的 DNS 主机名解析是否成功。

  - 认证边缘传输服务器。在边缘订阅创建后，边缘传输服务器的许可信息将会得到捕获。在许可证密钥在边缘传输服务器上应用之后，您需要将已订阅的边缘传输服务器订阅到 Exchange 组织。如果您在执行边缘订阅过程后在边缘传输服务器上应用许可证密钥，则 Exchange 组织中的许可信息不会更新，您需要重新订阅边缘传输服务器。

  - 配置下列传输设置，以向边缘传输服务器进行传播：
    
      - **内部 SMTP 服务器**   使用 **Set-TransportConfig** cmdlet 上的 *InternalSMTPServers* 参数指定边缘传输服务器上的发件人 ID 和连接筛选代理要忽略的内部 SMTP 服务器的 IP 地址或 IP 地址范围的列表。
    
      - **接受域**   配置所有权威域、内部中继域和外部中继域。
    
      - **远程域**   配置远程域设置。

返回顶部

## 管理边缘订阅

有关边缘订阅管理任务的分步说明，请参阅[管理边缘订阅](manage-edge-subscriptions-exchange-2013-help.md)。

