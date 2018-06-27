---
title: '手动配置边缘传输服务器邮件流: Exchange 2013 Help'
TOCTitle: 手动配置边缘传输服务器邮件流
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61183397
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 手动配置边缘传输服务器邮件流

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-02-21_

本主题介绍对边缘传输服务器管理邮件流的方式进行手动配置更改的步骤。这些步骤只针对特定方案；除非您的组织有进行手动配置更改的特殊需求，否则在订阅边缘传输服务器时将首选默认配置。

**目录**

手动配置发送连接器

组织内部发送连接器

订阅边缘后，创建其他发送连接器

禁止自动创建发送连接器的原因

划分邮件流

将出站电子邮件路由到智能主机

为外部中继域配置发送连接器

## 手动配置发送连接器

您可以手动修改发送连接器的配置。例如，如果需要通过智能主机对出站电子邮件进行路由，则可以禁止发送连接器的自动创建，并手动将发送连接器配置为 Internet。

## 组织内部发送连接器

组织内部发送连接器是隐式且隐藏的发送连接器，该连接器由 Exchange 自动计算，使同一个组织中的邮箱服务器上的传输服务不必使用显式发送连接器即可相互中继邮件。由于边缘订阅的 Active Directory 中存在具有 Active Directory 站点关联的配置对象，所以，也可以使用组织内部发送连接器将邮件中继到该边缘传输服务器。

只有位于订阅的 Active Directory 站点中的邮箱服务器可以直接将电子邮件传输到订阅的边缘传输服务器或传输来自订阅的边缘传输服务器的电子邮件。如果有多站点 Active Directory 林，并且在多个站点上部署了 Exchange，非订阅站点中的邮箱服务器会将出站电子邮件路由到订阅的站点。订阅的站点中的邮箱服务器会将出站电子邮件路由到边缘传输服务器。

## 订阅边缘后，创建其他发送连接器

将边缘传输服务器订阅到 Active Directory 站点后，将禁用用于在边缘传输服务器上创建和修改发送连接器的 cmdlet。如果希望创建的发送连接器将边缘传输服务器作为源服务器，请在 Exchange 组织内部创建发送连接器。可以指定一个或多个边缘订阅作为发送连接器的源服务器。无法同时指定邮箱服务器和边缘订阅作为同一个发送连接器的源服务器。下次 EdgeSync 同步配置数据时，发送连接器将被复制到配置为源服务器的边缘传输服务器上的 AD LDS 实例。如果多个边缘订阅作为源服务器列出，将在订阅的边缘传输服务器之间对指向该发送连接器的连接进行负载平衡。但是，必须将边缘传输服务器订阅到同一个 Active Directory 站点，才能进行负载平衡。如果不同 Active Directory 站点中的边缘订阅被配置为同一个发送连接器上的源服务器，边缘传输服务器只会路由到最接近的源服务器。

在以下情况下，需要手动创建发送连接器：

  - 已禁止自动创建 Internet 发送连接器或入站发送连接器。

  - 已接受组织中被配置为外部中继域的域。

## 禁止自动创建发送连接器的原因

根据 Exchange 组织的拓扑，您可能会决定禁止自动创建发送连接器。以下示例介绍了需要您禁止自动创建发送连接器的方案。

## 划分邮件流

如果决定对两个边缘传输服务器之间的入站和出站邮件处理进行划分，那么一个边缘传输服务器负责处理出站邮件流，另一个边缘传输服务器负责处理入站邮件流。为此，需要对边缘订阅进行如下配置：

  - 对于出站边缘传输服务器，在邮箱服务器上运行以下命令：
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - 对于入站边缘传输服务器，在邮箱服务器上运行以下命令：
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## 将出站电子邮件路由到智能主机

如果 Exchange 组织的所有出站电子邮件都通过智能主机路由，自动创建的发送连接器的配置将不正确。

在邮箱服务器上运行以下命令，以禁止自动创建 Internet 发送连接器。

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

完成边缘订阅进程后，手动创建 Internet 发送连接器。在 Exchange 组织内部创建发送连接器，并选择边缘订阅作为连接器的源服务器。选择 `Custom` 使用类型并配置一个或多个智能主机。下次 EdgeSync 同步配置数据时，此新发送连接器将被复制到边缘传输服务器上的 AD LDS 实例。通过在邮箱服务器上运行 **Start-EdgeSynchronization** cmdlet 可以强制执行即时 EdgeSync 同步。

示例：使用命令行管理程序为订阅的边缘传输服务器配置发送连接器，以便通过智能主机路由所有 Internet 地址空间的邮件。在 Exchange 组织内的邮箱服务器（而非边缘传输服务器）上运行此项任务。

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>此示例未指定任何智能主机身份验证机制。在您自己的 Exchange 组织中创建智能主机连接器时，确保配置了正确的身份验证机制并提供了所有必要的凭据。</td>
</tr>
</tbody>
</table>


## 为外部中继域配置发送连接器

如果已接受 Exchange 组织中配置为外部中继域的域，则必须手动为这些地址空间创建发送连接器。传递到外部中继域的邮件将通过边缘传输服务器进行中继。边缘订阅进程不会自动为外部中继域创建并配置发送连接器。因此，必须为这些域配置发送连接器，并将一个或多个边缘订阅指定为这些发送连接器的源服务器。

外部中继域的 DNS MX 资源记录解析到您的边缘传输服务器。您可以配置一个将电子邮件中继到外部中继域的发送连接器，以使用智能主机进行路由。将外部中继域的发送连接器配置为使用 DNS 路由会导致发生路由循环。有关外部中继域的详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

返回顶部

