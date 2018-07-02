---
title: 'Exchange 2013 中统一消息的最近更新: Exchange 2013 Help'
TOCTitle: Exchange 2013 中统一消息的最近更新
ms:assetid: a444ef2d-d893-408e-adf9-c9d8a8b07593
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150545(v=EXCHG.150)
ms:contentKeyID: 50491254
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中统一消息的最近更新

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

在 Microsoft Exchange Server 2013 中，我们正在通过引入新的功能和体系结构更改来增强早期版本的 Exchange。Exchange 2013 中的统一消息 (UM) 包含与 Exchange 2010 和 Exchange 2007 相同的功能集，但是统一消息不再是单独的服务器角色。它现在是 Exchange 2013 中提供的语音相关功能的组件。

## 语音体系结构中的更改

Exchange 2013 体系结构与 Exchange 2010 和 Exchange 2007 中的体系结构不同。在之前的 Exchange UM 版本中，统一消息的所有组件包含在安装了 UM 服务器角色的服务器上。在 Exchange 2013 中，所有统一消息组件都可分为两种：运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和运行 Microsoft Exchange 统一消息服务的邮箱服务器。所有功能（包括统一消息服务和工作进程）都位于每个邮箱服务器上，但运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器除外，它代理邮箱服务器的传入呼叫。有关详细信息，请参阅[语音体系结构更改](voice-architecture-changes-exchange-2013-help.md)。

## 支持 IPv6

Internet 协议版本 6 (IPv6) 是 Internet 协议的最新版本。IPv6 旨在修正上一版本 IP 协议 IPv4 中的许多不足之处。和在 Exchange 2010 中一样，Exchange 2013 客户端访问和邮箱服务器完全支持 IPv6 网络。有关详细信息，请参阅[统一消息中的 IPv6 支持](ipv6-support-in-unified-messaging-exchange-2013-help.md)。

## 支持 UCMA 4.0 API

自 Exchange 2010 Service Pack 1 以来，统一消息角色便一直依赖于用于信号发送和媒体的统一通信托管 API 2.0 版本 (UCMA)。因此，UCMA 2.0 是 Exchange 2010 UM 安装的先决条件。UCMA 2.0 可单独下载并由管理员手动部署在运行 Exchange 2010 SP1 或更高版本的统一消息服务器上。对于 Exchange 2013，UCMA 4.0 是必需项。但是，UM 服务器现在已经不再是 Exchange 2013 中单独的服务器角色，而是需要 UCMA 4.0 的客户端访问和邮箱服务器。

UCMA 4.0 支持统一消息中的新功能，如将相同版本的语音引擎同时用于文字转语音 (TTS) 和自动语音识别 (ASR)。用于 Exchange 2013 的平台 .NET 4.0 包含一个安装程序文件，并实现与 Exchange 2010 和 Exchange 2007 UM 服务器的向后兼容。

在 Exchange 2010 SP2 和 SP1 中，在统一消息服务器上安装 Service Pack 前，需要安装 UCMA 2.0。不过，UCMA 2.0 具有一些限制。UCMA 4.0 更正了许多缺点。在 Exchange Server 2013 中，UM 将继续使用 UCMA。但是，转移到 UCMA 的最新版本具有以下优点：

  - UCMA 的最新版本包含修补和补丁程序。

  - UCMA 需要 .NET 4.0，这是 Exchange Server 2013 使用的平台。（UCMA 2.0 不支持 .NET 4.0。）

  - UCMA 4.0 支持 IPv6。

  - UCMA 4.0 的简化和自动部署。Exchange 2013 安装程序可对 UCMA 4.0 执行单个检查。

  - UCMA 4.0 安装程序包括 Exchange 2013 的所有先决条件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UCMA 4.0 会在安装 Exchange 2013 时安装。有关 UCMA 4.0 和安装要求的详细信息，请参阅 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。若要升级到 UCMA 的最新版本，必须先使用“添加/删除程序”卸载任何已安装的以前版本的 UCMA。</td>
</tr>
</tbody>
</table>


## 语音邮件预览改进

通过 Speech Engine 11.0 和 UCMA 4.0 为 Exchange Server 2013 UM 提供了一些语音相关服务的增强功能。包括语法生成和语言方面的改进。此外，Exchange Server 2013 UM 还包含几个用户界面增强功能以及用于提高语音邮件预览可信度和准确性的改进。有关详细信息，请参阅[语音邮件预览增强功能](voice-mail-preview-enhancements-exchange-2013-help.md)。

## 增强的呼叫者 ID 支持

在以前版本的 Exchange 统一消息中，进行呼叫的 UM 服务器尝试使用呼叫者 ID 查找呼叫者的标识。此搜索可扩展到 Active Directory 及 UM 用户邮箱中存储的用户个人联系人。

Exchange 用户常常会由于无法通过呼叫者 ID 识别 Exchange 或个人联系人而感到苦恼。到现在为止，只有 Exchange UM 中默认的联系人文件夹用于进行过此类搜索。但是，Exchange Server 2013 用户很可能拥有从外部社交网络聚合的联系人或用户手动创建的独有文件夹中的联系人。Exchange 2013 支持从外部社交网络聚合联系人，提供相关智能来链接指的是同一人的多个联系人，并使用该数据来展示以人为中心（而不是以联系人为中心）的视图。从外部社交网络聚合的联系人放置在联系人文件夹以及用户创建的任何其他联系人文件夹中。Exchange 2013 UM 中的功能扩展了搜索范围以包含用户手动创建的其他 Exchange 及个人联系人文件夹。

呼叫者 ID 查找与联系人聚合集成，从而可跨外部联系人进行搜索。展示的 PersonID 属性（具有非 null 值）会通过禁止显示与同一人关联的联系人的重复匹配项，来提升呼叫者 ID 解析的用户体验。因为 PersonID 属性在两个结果中相同，所以 UM 会将此视为单个联系人的匹配项。

## 语音平台和语音识别的增强

Exchange Server 2013 UM 引入了一些针对语音平台和语音识别的增强功能，包括以下这些：

  - 针对语音邮件预览的增强功能和更高准确性。

  - 对 [Microsoft 语音平台 – 运行时（版本 11.0）](https://go.microsoft.com/fwlink/p/?linkid=253196)的支持。

  - 将系统邮箱用于组织的语音语法生成。

Exchange 统一消息使用静态和动态语音语法来识别命令、全局地址列表中的联系人的姓名、用户邮箱中的个人联系人的姓名。如今在 Exchange Server 2013 中，每个运行 Microsoft Exchange 统一消息服务的邮箱服务器对安装在其上的所有语言生成语法并在目录中存储它们。每个邮箱服务器会存储每个可能的语法（基于拨号计划数、自动助理和安装的 UM 语言来生成）。

语法文件用作语音识别过程的输入，并定期生成。Exchange 2007 和 Exchange 2010 中的 GGG.exe 命令使你可以手动更新语法文件，而无需等待进行安排的更新。在 Exchange Server 2013 中，为了解决 UM 的 ASR 语法生成可伸缩性问题，不再在安装有统一消息服务器角色的服务器上进行语音 GAL 语法生成，而是在托管组织仲裁邮箱并运行 Microsoft Exchange 统一消息服务的邮箱服务器上，使用邮箱助理定期进行。GAL 语音语法文件存储在 Exchange 组织的仲裁邮箱上，然后在以后下载到该组织中的所有邮箱服务器上。默认情况下，邮箱助理每 24 小时运行一次。可以使用 **Set-MailboxServer** cmdlet 来调整频率。

## Cmdlet 更新

对于 Exchange 2013，许多 UM cmdlet 来自 Exchange 2010，但是其中一些 cmdlet 进行了更改，并添加了一些新 cmdlet 以实现新功能。有关详细信息，请参阅 [统一消息 cmdlet 更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)。

