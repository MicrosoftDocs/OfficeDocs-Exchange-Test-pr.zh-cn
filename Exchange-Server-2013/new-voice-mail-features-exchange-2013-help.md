---
title: '新的语音邮件功能: Exchange 2013 Help'
TOCTitle: 新的语音邮件功能
ms:assetid: 89faaa97-3485-4704-a56c-d13632f01e2a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ649002(v=EXCHG.150)
ms:contentKeyID: 50491125
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 新的语音邮件功能

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

统一消息 (UM) 在 Microsoft Exchange Server 2013包括相同的功能集为Exchange 2010和Exchange 2007，一些增强功能和体系结构的更改。但是，统一消息不再是一个单独的服务器角色。它现在是在Exchange 2013中提供的与语音相关的功能组件。

## 语音体系结构中的更改

在Exchange 2013的语音体系结构是不同的比它在Exchange 2010和Exchange 2007。在早期版本的 Exchange UM，统一消息的所有组件都包括在已安装 UM 服务器角色的服务器上。在Exchange 2013，统一消息组件运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器和邮箱服务器运行 Microsoft Exchange 统一消息服务之间拆分。大部分的功能，包括服务和工作流程，统一消息，位于每个邮箱服务器上。运行 Microsoft Exchange 统一消息呼叫路由器服务、 代理到邮箱服务器的传入呼叫的客户端访问服务器。有关详细信息，请参阅[语音体系结构更改](voice-architecture-changes-exchange-2013-help.md)。

## 支持 IPv6

Internet 协议版本 6 (IPv6) 是最新版本的网际协议 (IP)。IPv6 旨在解决 IPv4，这是以前版本的 IP 的缺点很多。就像Exchange 2010一样， Exchange 2013客户端访问和邮箱服务器完全支持 IPv6 网络。有关详细信息，请参阅[统一消息中的 IPv6 支持](ipv6-support-in-unified-messaging-exchange-2013-help.md)。

## 支持 UCMA 4.0 API

由于Exchange 2010 Service Pack 1 (SP1)，统一消息角色依靠统一通信管理 API 2.0 版 (UCMA) 信号和媒体。因此，UCMA 2.0 的Exchange 2010 UM 设置的先决条件。UCMA 2.0 是单独下载并运行Exchange 2010 SP1 或更高版本的 UM 服务器上的管理员手动部署。

但是，UCMA 2.0 有一些限制。许多这些缺点纠正由 UCMA 4.0，这是Exchange 2013的要求。现在，UM 服务器不再是单独的服务器角色，则需要 UCMA 4.0 的客户端访问和邮箱服务器。

UCMA 4.0 如文字语音转换 (TTS) 和自动语音识别 (ASR) 使用相同版本的语音引擎支持统一消息中的新功能。用于Exchange 2013，.NET 4.0 的平台包括一个单一的安装程序文件，并使与Exchange 2010和Exchange 2007 UM 服务器的向后兼容性。

在Exchange 2010 SP2 和 SP1 中，UCMA 2.0 系统不需要在安装统一消息服务器上的服务包之前安装。

使用 UCMA 4.0 提供了多种好处︰

  - 它包含的修复程序和修补程序。

  - 它支持 IPv6。

  - 已自动化并简化部署的 UCMA 4.0。

  - UCMA 4.0 安装程序包括 Exchange 2013 的所有先决条件。

  - UCMA 4.0 提供更准确的语音引擎翻译和更具可扩展性的语音平台支持跨多个产品。

> [!NOTE]  
> 当您正在安装Exchange 2013安装 UCMA 4.0。有关 UCMA 4.0 和安装要求的详细信息，请参阅<a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。要升级到最新的 UCMA 版本，必须先卸载以前的版本 UCMA，使用添加/删除程序安装。


## 语音邮件预览改进

与语音相关的服务的一些增强功能包括在Exchange Server 2013 UM 通过语音引擎 11.0 和 UCMA 4.0。在语法生成、 核心语音服务和多种语言的支持有了改进。Exchange Server 2013嗯还包括几个抄写服务交付给最终用户和增强的信心的增强功能和语音邮件预览的准确性。有关详细信息，请参阅[语音邮件预览增强功能](voice-mail-preview-enhancements-exchange-2013-help.md)。

## 增强的呼叫者 ID 支持

在以前版本的 Exchange 统一消息，UM 服务器接收到调用用于呼叫方 ID 查找可能的调用方的标识。此搜索跨Active Directory和 UM 扩展其邮箱中存储用户的个人联系人。

过去，用户有时被对语音邮件系统无法识别 Exchange 或个人联系人从其调用 id。到目前为止，只有默认联系人文件夹用户的 Exchange 邮箱中已用于此搜索。但Exchange Server 2013用户很容易有聚合来自外部的社会网络或他们添加到唯一文件夹组织联系人时的联系人的联系人。在Exchange 2013，UM 扩展搜索范围以包括用户范围的其他 Exchange 和手动创建的个人联系人文件夹。Exchange 2013还支持从外部社会网络联系人聚合、 提供情报指同一个人的多个联系人链接和使用该数据来呈现视图以用户为中心 （而不是联系中心）。这意味着从外部社会网络聚合的联系人可以位于联系人文件夹存储在用户的邮箱中 Microsoft Outlook Web App和Outlook。这些联系人现在还可以添加到任何其他的联系人文件夹的用户创建。

呼叫方 ID 查找集成具有联系的聚合，以便它在外部联系人搜索。**PersonID**属性中，在其中显示和值设置为非空值，改善了用户体验呼叫者 ID 解析为通过抑制重复匹配值与同一个人相关联的联系人。过程属性相当于在这两个结果，因为 UM 将这视为匹配到一个联系人。

## 语音平台和语音识别的增强

Exchange Server 2013 UM 引入了一些针对语音平台和语音识别的增强功能，包括以下这些：

  - 针对语音邮件预览的增强功能和更高准确性。

  - [Microsoft 语音平台--运行时 （11.0 版）](https://go.microsoft.com/fwlink/p/?linkid=253196)的支持。

  - 将系统邮箱用于组织的语音语法生成。

Exchange 统一消息使用静态和动态语音语法无法识别的命令、 全局地址列表 (GAL) 中的联系人的名字和用户的邮箱中的个人联系人的名字。今天， Exchange Server 2013，在运行 Microsoft Exchange 统一消息服务的每个邮箱服务器生成安装在其上的所有 UM 语言的语法，并将它们存储在目录中。每个邮箱服务器存储每个可能的语法，它生成基于拨号计划、 自动助理和已安装 UM 语言的数量。

UM 使用语法文件允许调用方使用语音来查找您的组织中的用户。通过邮箱助理每 24 小时更新的文件。在Exchange 2007和Exchange 2010的 GGG.exe 命令进行手动更新而无需等待计划更新的语法文件。在Exchange Server 2013，来解决 ASR 语法生成可扩展性颁发为 UM，语音 GAL 语法生成不再发生在服务器安装了统一消息服务器角色。相反，它发生定期使用邮箱助理邮箱运行的服务器上承载的组织仲裁邮箱的 Microsoft Exchange 统一消息服务。GAL 语音语法文件是存储在组织的仲裁邮箱，以后下载到 Exchange 组织中的所有邮箱服务器。默认情况下，邮箱助理每 24 小时运行。您可以通过使用**Set-MailboxServer** cmdlet 调整频率。

## Cmdlet 更新

对于Exchange 2013，许多 UM cmdlet 已带来了从Exchange 2010。但是，在一些这些 cmdlet，已更改和新 cmdlet 添加了新功能。有关详细信息，请参阅[统一消息 cmdlet 更新](unified-messaging-cmdlet-updates-exchange-2013-help.md)。

