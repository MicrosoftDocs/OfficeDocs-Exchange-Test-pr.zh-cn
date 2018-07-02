---
title: 'Passwords and Security in Outlook for iOS and Android for Exchange Server: Exchange 2013 Help'
TOCTitle: Passwords and Security in Outlook for iOS and Android for Exchange Server
ms:assetid: e5565beb-7ef3-47c4-8daf-6d8f1d22dceb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt465750(v=EXCHG.150)
ms:contentKeyID: 70086931
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Passwords and Security in Outlook for iOS and Android for Exchange Server

 

_**适用于：**Exchange Server 2010, Exchange Server 2013_

_**上一次修改主题：**2018-04-01_

**摘要：**本文介绍了密码和安全功能通过 Exchange Server 在 Outlook for iOS 和 Outlook for Android 中的工作原理。

适用于 iOS 和 Android 的 Outlook 应用程序首次在 Exchange 本地环境中运行时，Outlook 生成随机的 AES-128 密钥。此密钥称为*设备密钥*，仅存储在用户的设备上。

## 创建帐户并保护密码

用户登录到 Exchange 时，用户名、密码和唯一的 AES-128 设备密钥通过 TLS 连接从用户设备发送到 Outlook 服务，其中设备密钥保存在运行时计算内存中。通过 Exchange 服务器验证密码后，Outlook 服务使用设备密钥加密密码，然后，加密的密码存储在服务中。同时，设备密钥从内存中擦除，从不存储在 Outlook 服务中（该密钥仅存储在用户的设备上）。

接下来，用户尝试连接到 Exchange 以检索邮箱数据时，该设备密钥再次通过 TLS 安全连接从该设备传递到 Outlook 服务，其中设备密钥用于解密运行时计算内存中的密码。一旦解密，密码就不会存储在服务中或写入本地存储磁盘，并且设备密钥再次从存储器擦除。

Outlook 服务在运行时解密密码后，该服务可以连接到 Exchange 服务器以同步邮件、日历和其他邮箱数据。只要用户继续打开并定期使用 Outlook，Outlook 服务将在内存中保留用户解密密码的副本，以便与 Exchange 服务器的连接保持活动状态。

## 帐户非活动并从内存刷新密码

在三天的非活动期后，Outlook 服务将从内存刷新解密的密码。刷新解密的密码后，Outlook 服务无法访问用户邮箱。加密的密码仍存储在 Outlook 服务中，但如果没有设备密钥（只能从用户设备获取），则无法对其再次解密。

用户帐户可以通过三种方式变为非活动状态：

  - Outlook for iOS 和 Outlook for Android 已由用户卸载。

  - 在\&quot;设置\&quot;选项中禁用后台应用刷新，然后对 Outlook 应用强制退出。

  - 设备上没有可用的 Internet 连接，导致 Outlook 无法与 Exchange 同步。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook 不会仅仅因为用户在一段时间内没有打开应用（例如周末或休假期间）而变为非活动状态。只要启用后台应用刷新（这是 Outlook for iOS 和 Outlook for Android 的默认设置），推送通知和电子邮件后台同步等功能将被视为处于活动状态。</td>
</tr>
</tbody>
</table>


**从硬盘刷新加密密码和邮件缓存**

Outlook 服务每周安排刷新或删除非活动帐户。用户帐户变为非活动状态后，Outlook 服务将刷新加密密码和用户缓存的该服务的所有邮箱内容。

**设备和服务安全组合**

每个用户的唯一设备密钥永远不会存储在 Outlook 服务中，并且用户的 Exchange 密码永远不会存储在该设备上。这种体系结构意味着，恶意方要获取对用户密码的访问权限，他们将需要对 Outlook 服务的未经授权访问权限和对该用户设备的物理访问权限。

通过在你的组织的设备上强制实施 PIN 策略和加密，恶意方还必须获取设备的加密才能访问设备密钥。这些操作均必须在用户注意到设备受到威胁之前发生，并可以请求设备的远程擦除。

## 密码安全常见问题解答

以下是有关 Outlook for iOS 和 Outlook for Android 的安全设计和设置的常见问题解答。

## 如果我阻止 Outlook 访问我的 Exchange Server，用户凭据是否存储在 Outlook 服务中？

如果你选择阻止 Outlook for iOS 和 Outlook for Android 访问你的本地 Exchange 服务器，Exchange 将拒绝初始连接。Outlook 服务不会存储用户凭据，并且会立即从内存刷新失败的连接尝试中存在的凭据。

## 唯一设备密钥和加密的用户密码如何传输到 Outlook 服务？

Outlook 应用和 Outlook 服务之间的所有通信均通过加密 TLS 连接进行。Outlook for iOS 和 Outlook for Android 仅能与 Outlook 服务连接。

## 如何从 Outlook 服务中删除用户凭据和邮箱信息？

有三种方法可以从 Outlook 服务中删除信息：

  - 选项 1：对使用该应用连接到 Exchange 的每个用户启动远程擦除。

  - 选项 2：让所有用户删除 Outlook for iOS 和 Outlook for Android。所有数据将在大约 3-7 天内从 Outlook 服务中删除。

  - 选项 3：让用户从 Outlook 应用中删除其帐户，然后从其设备中删除该应用。在应用中，让用户转到\&quot;**设置**\&quot;，然后依次点击\&quot;**帐户设置**\&quot;、\&quot;**选择帐户**\&quot;、\&quot;**删除帐户**\&quot;。

## 该应用已关闭或已卸载，但我发现它仍连接到我的 Exchange 服务器。为何出现这种情况？

Outlook 服务会解密运行时计算内存中的用户密码，然后使用解密的密码连接到 Exchange。由于 Outlook 服务代表设备连接到 Exchange，以便提取和缓存邮箱数据，因此它可以持续较短的一段时间，直到该服务检测到 Outlook 不再请求数据。

如果用户在不首先使用\&quot;**删除帐户**\&quot;选项的情况下从其设备中卸载该应用，则在帐户变为非活动状态前，Outlook 服务将持续连接到 Exchange 服务器，如之前在\&quot;帐户非活动和从内存刷新密码\&quot;中所述。若要停止此活动，只需按照上述常见问题解答中的选项 1 或选项 3 操作即可，或阻止应用，如[阻止 Outlook for iOS 和 Outlook for Android](https://technet.microsoft.com/zh-cn/library/mt759239\(v=exchg.150\)) 中所述。

## 与使用其他 Exchange ActiveSync 客户端相比，Outlook for iOS 和 Outlook for Android 中的用户密码安全性更低吗？

不。EAS 客户端通常在用户设备上本地保存用户凭据。这意味着设备被盗或受到威胁可能导致恶意方获取用户密码访问权限。通过 Outlook for iOS 和 Outlook for Android 的安全设计，恶意方需要对 Outlook 云服务的未经授权访问权限**和**对用户设备的物理访问权限。

## 在用户数据已从 Outlook 服务中删除后，如果用户尝试使用 Outlook for iOS 和 Outlook for Android 会怎样？

如果用户帐户变为处于非活动状态（如通过禁用设备上的后台应用刷新或将其设备与 Internet 断开一段时间），Outlook 应用会在下次启动应用时重新连接至 Outlook 服务，并将重新启动密码加密和电子邮件缓存进程。这对于用户而言是透明的。

## 在 Outlook 服务中进行存储时，临时缓存的邮箱数据如何受到保护？

您可以阅读有关如何在[Azure 信任中心](https://azure.microsoft.com/support/trust-center/)当前保护我们的数据。如先前所述，我们正转向从 Azure Office 365。在[Office 365 信任中心](https://go.microsoft.com/fwlink/p/?linkid=525776)介绍了这些服务的安全。

