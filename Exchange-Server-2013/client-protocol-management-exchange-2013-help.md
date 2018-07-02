---
title: '客户端协议管理: Exchange 2013 Help'
TOCTitle: 客户端协议管理
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50491121
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 客户端协议管理

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

Exchange ActiveSync、Outlook Web App、POP3、IMAP4、自动发现服务、Exchange Web 服务和可用性服务的客户端协议管理任务在三个不同的区域进行：Exchange 管理中心 (EAC)、Exchange 命令行管理程序和 Internet 信息服务 (IIS) 管理器。每个位置所管理的设置因客户端协议而异。

## 管理 Outlook Web App 设置

大多数会对用户可用的 Outlook Web App 功能产生影响的设置都可以在 Outlook Web App 虚拟目录中设定，也可以在 Outlook Web App 邮箱策略中进行配置。使用 Outlook Web App 邮箱策略，可以定义单个用户可用的各项功能。邮箱策略设置将覆盖虚拟目录设置。有关管理 Outlook Web App 的详细信息，请参阅 [Outlook Web App](outlook-web-app-exchange-2013-help.md)。

## 管理 Exchange ActiveSync 设置

在 Exchange 2010 中，所有客户端访问协议都在单个服务器角色（即客户端访问服务器角色）上实现和管理。协议管理任务在单个 IIS 实例上进行，每个客户端协议在 Active Directory 中都有一个单一的虚拟目录对象，以及单一的一套 cmdlet 用于配置虚拟目录。

在 Exchange 2013 中，Exchange ActiveSync 的客户端协议管理在客户端访问服务器与邮箱服务器上分开进行。由于体系结构上的这种变化，您可以同时在客户端访问服务器和邮箱服务器上运行不同的虚拟目录管理任务。如果这两个服务器不安装在同一物理服务器上，则用于虚拟目录 cmdlet 的参数将根据运行它们的服务器角色而发生改变。

有关 Exchange 2013 中体系结构变化的详细信息，请参阅 [Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

下列两类设置可应用于 Exchange ActiveSync 虚拟目录：

  - 适用于邮箱会话的设置

  - 适用于服务器和虚拟目录的设置

适用于邮箱会话的设置是用户会话设置。当某用户连接到一台客户端访问服务器时，该连接将通过代理转至包含该用户邮箱的邮箱服务器。通过代理转接的请求中将包含虚拟目录的唯一标识符。邮箱服务器随后从 Active Directory 中检索虚拟目录设置，并将其应用到会话。虚拟目录设置缓存在邮箱服务器上，以提升性能。

如果连接通过代理转至其他 Active Directory 站点，虚拟目录设置将从与邮箱服务器位于同一站点的客户端访问服务器加载，而不是从发起该连接的客户端访问服务器加载。

下列各表中列出了可在各个服务器上管理的各项虚拟目录设置。如果您试图在不适用某个设置的服务器上管理该设置，将收到一条错误消息，提示所操作的服务器只能对要设置的属性进行只读访问。

**客户端访问服务器上的 Exchange ActiveSync 虚拟目录设置**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>客户端访问</p></td>
</tr>
</tbody>
</table>


**客户端访问服务器和邮箱服务器上的 Exchange ActiveSync 虚拟目录设置**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>Name</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>Path</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
</tbody>
</table>


## 管理 POP3 和 IMAP4 设置

在 Exchange 2013 中，POP3 和 IMAP4 协议的实现同样在客户端访问服务器角色与邮箱服务器角色之间进行了划分。由于这一新的实现方式，POP3 和 IMAP4 连接性分别通过客户端访问服务器和邮箱服务器上的相应服务进行管理。客户端访问服务器上运行的服务的名称与 Exchange 2010 中的服务名称相同：Microsoft Exchange IMAP4 服务和 Microsoft Exchange POP3 服务。邮箱服务器上运行的两项新服务的名称分别为：Microsoft Exchange IMAP4 后端服务和 Microsoft Exchange POP3 后端服务。

在管理组织中的 POP3 和 IMAP4 连接性时，请考虑以下内容：

  - 如果在同一台计算机上运行客户端访问服务器角色和邮箱服务器角色，则对 POP3 或 IMAP4 设置所做的任何更改都将自动应用于正确的 POP3 和 IMAP4 服务。

  - 如果在不同计算机上运行客户端访问服务器角色和邮箱服务器角色，则需要在用于管理要更改的设置的计算机上管理需要的设置。

使用下列各表确定适用于各个服务器角色的 POP/IMAP 设置。

**客户端访问服务器上的 POP3 和 IMAP4 设置**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>Banner</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>客户端访问</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>客户端访问</p></td>
</tr>
</tbody>
</table>


**邮箱服务器上的 POP3 和 IMAP4 设置**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>邮箱</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>邮箱</p></td>
</tr>
</tbody>
</table>


**客户端访问服务器和邮箱服务器上的 POP3 和 IMAP4 设置**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>设置</th>
<th>服务器</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="even">
<td><p>Server</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>客户端访问和邮箱</p></td>
</tr>
</tbody>
</table>

