---
title: '边缘传输服务器规划: Exchange 2013 Help'
TOCTitle: 边缘传输服务器规划
ms:assetid: 3d34de82-58a5-4b30-9978-7d330102eb92
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn641596(v=EXCHG.150)
ms:contentKeyID: 61545098
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 边缘传输服务器规划

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

Exchange Service Pack 1 中重新引入了边缘传输服务器角色。边缘传输为 Exchange 组织增强了反垃圾邮件保护。边缘传输服务器还会对在组织之间传输的邮件应用策略。此服务器角色部署在外围网络中和 Active Directory 林之外。边缘传输服务器无法按客户端访问服务器或邮箱服务器所采用的方式直接访问 Active Directory，以获取配置和收件人信息。边缘传输服务器使用 Active Directory 轻型目录服务 (AD LDS) 来在本地存储配置和收件人信息。

您可以向现有 Exchange 2013 组织添加边缘传输服务器。在安装边缘传输服务器时，不必执行任何其他 Active Directory 准备步骤。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要向现有 Exchange 2010 或 Exchange 2007 组织添加边缘传输，将需要在旧版服务器上安装特定汇总更新，然后再安装 Exchange 2013 边缘传输。有关详细信息，请参阅 <a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 系统要求</a>。</td>
</tr>
</tbody>
</table>


规划部署边缘传输服务器时，应当考虑以下问题：

  - **服务器容量**   规划服务器容量包括规划边缘传输服务器的性能监视。性能监视将帮助您了解服务器的工作状态。此信息将确定当前硬件配置的容量。

  - **传输功能**   边缘传输服务器可以在网络边缘处提供反垃圾邮件的保护。作为整个规划过程的一部分，应当确定要在边缘传输服务器上启用的反垃圾邮件功能以及如何配置这些功能。

  - **安全性**   边缘传输服务器角色能够将受攻击的可能性降到最低。因此，恰当地保护和管理对服务器的物理访问及网络访问十分重要。对安全性进行规划有助于确保仅启用来自已授权服务器和已授权用户的 IP 连接。有关详细信息，请参阅[部署安全性核对清单](deployment-security-checklist-exchange-2013-help.md)。
    
    建议做法是将边缘传输服务器放在外围网络中。若要确保服务器可以发送和接收电子邮件并可以接收来自 Microsoft Exchange EdgeSync 服务的收件人和配置数据更新，必须允许通过下表中列出的端口进行通信。
    
    ### 边缘传输服务器的通信端口设置
    
    <table>
    <colgroup>
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    <col style="width: 25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>网络接口</th>
    <th>打开的端口</th>
    <th>协议</th>
    <th>注意</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>进入和流出 Internet</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>发往和来自 Internet 的邮件流需要此端口。</p></td>
    </tr>
    <tr class="even">
    <td><p>进入和流出内部网络</p></td>
    <td><p>25/TCP</p></td>
    <td><p>SMTP</p></td>
    <td><p>发往和来自 Exchange 组织的邮件流需要此端口。</p></td>
    </tr>
    <tr class="odd">
    <td><p>仅限本地</p></td>
    <td><p>50389/TCP</p></td>
    <td><p>LDAP</p></td>
    <td><p>此端口用于建立 AD LDS 本地连接。</p></td>
    </tr>
    <tr class="even">
    <td><p>流出内部网络</p></td>
    <td><p>50636/TCP</p></td>
    <td><p>保护 LDAP 安全</p></td>
    <td><p>EdgeSync 同步需要此端口。</p></td>
    </tr>
    <tr class="odd">
    <td><p>流出内部网络</p></td>
    <td><p>3389/TCP</p></td>
    <td><p>RDP</p></td>
    <td><p>可以选择打开此端口。它允许使用远程桌面连接来管理边缘传输服务器，从而使用户可以更加灵活地在内部网络中管理边缘传输服务器。</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>边缘传输服务器角色使用非标准 LDAP 端口。本主题中指定的端口是在安装边缘传输服务器角色时配置的 LDAP 通信端口。</td>
    </tr>
    </tbody>
    </table>


  - **EdgeSync**   推荐的部署过程是创建一个边缘订阅，从而将边缘传输服务器订阅到 Exchange 组织。创建边缘订阅时，会将收件人和配置数据从 Active Directory 复制到 AD LDS。将边缘传输服务器订阅到 Active Directory 站点。然后，该站点的邮箱服务器上运行的 MicrosoftExchange EdgeSync 服务将通过同步 Active Directory 中的数据来定期更新 AD LDS。边缘订阅过程自动提供启用从 Exchange 组织到 Internet 的邮件流（通过边缘传输服务器）所需的发送连接器。如果在边缘传输服务器上使用查找收件人或安全列表聚合功能，则必须将边缘传输服务器订阅到组织。

## 配置边缘传输服务器角色的 DNS 设置

边缘传输服务器在 Exchange 组织外部部署为外围网络中的独立服务器，或外围网络 Active Directory 域的成员。安装 Exchange 2013 之前，需要为边缘传输服务器角色手动配置正确的 DNS 后缀。如果未配置 DNS 后缀，则安装将会失败。

由于边缘传输服务器部署在外围网络中，因此它具有连接到多个网段的网络接口。其中的每个网段都具有唯一的 IP 配置。连接到外部网段（或称公共网段）的网络接口应该配置为使用公用 DNS 服务器进行名称解析。这使服务器能够将 SMTP 域名解析为 MX 资源记录并将邮件路由到 Internet。

连接到内部或专用网段的网络接口应配置为使用 DNS 服务器（可以解析组织中的邮箱服务器的名称），或者应具有可用的 Hosts 文件。边缘传输服务器和邮箱服务器必须能够使用 DNS 主机解析来相互进行查找。

若要通过边缘传输服务器启用邮箱服务器的名称解析，请使用下列方法之一：

  - 在边缘传输服务器的内部网络适配器上配置的 DNS 服务器的正向查找区域中手动创建邮箱服务器的资源记录。

  - 编辑边缘传输服务器上的 Hosts 文件，以便包括邮箱服务器的主机记录。Hosts 文件是与 4.3 Berkeley Software Distribution (BSD) UNIX/etc/hosts 文件格式相同的本地文本文件。此文件将主机名映射到 IP 地址，并将此文件存储在 \\%Systemroot%\\System32\\Drivers\\Etc 文件夹中。

若要通过邮箱服务器启用边缘传输服务器的名称解析，请使用下列方法之一：

  - 在邮箱服务器上配置的 DNS 服务器的正向查找区域中手动创建边缘传输服务器的资源记录。

  - 若要添加边缘传输服务器的主机记录，请编辑位于已订阅的 Active Directory 站点中的邮箱服务器上的 Hosts 文件。

请按照下列步骤配置边缘传输服务器的 DNS 设置：

1.  验证每个网络接口的 DNS 服务器设置对于网段是否正确。

2.  可使用下列步骤为边缘传输服务器名称配置 DNS 后缀：
    
    1.  打开“控制面版”，然后选择“系统属性”。
    
    2.  选择“计算机名称”选项卡。
    
    3.  选择“更改”。
    
    4.  在“计算机名称更改”页上，单击“更多”。
    
    5.  在“此计算机的主 DNS 后缀”字段中，键入边缘传输服务器的 DNS 域名和后缀。
    
    安装了边缘传输服务器角色之后，不能更改此名称。

## 覆盖 DNS 设置

您可能需要覆盖 Exchange 服务器上的默认 DNS 设置，以便正确路由和传递邮件。为此，需要修改传输服务器的属性的“内部 DNS 查找”和“外部 DNS 查找”设置。这些设置将覆盖网络适配器上的设置以路由电子邮件。

