---
title: 'Exchange ActiveSync 虚拟目录管理任务: Exchange 2013 Help'
TOCTitle: Exchange ActiveSync 虚拟目录管理任务
ms:assetid: f0b339b7-e184-4392-a133-20523183459d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125170(v=EXCHG.150)
ms:contentKeyID: 50491949
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange ActiveSync 虚拟目录管理任务

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-05_

您可以通过 Exchange ActiveSync 虚拟目录来管理 Exchange Server 2013 中的多个 Exchange ActiveSync 应用程序设置。 虚拟目录由 Internet Information Services (IIS) 使用，允许访问 Web 应用程序，例如 Exchange ActiveSync。 您可以为 Exchange ActiveSync 进行管理的一些虚拟目录设置包括认证、安全和报告。

## Exchange ActiveSync 虚拟目录设置

您可以在 Exchange ActiveSync 虚拟目录上修改以下属性和设置：

  - **InternalURL** InternalURL 是内部客户用于访问虚拟目录的 URL。它通常的格式为 https://servername/Microsoft-Server-ActiveSync。 例如，如果服务器的 NetBIOS 名是 Sequoia，那么 InternalURL 则是 https://sequoia/Microsoft-Server-ActiveSync。

  - **ExternalURL** ExternalURL 是外部客户用于访问虚拟目录的 URL。此 URL 应该可以从您的内部网络外进行访问。例如，您的 ExternalURL 可能是 https://www.contoso.com/。

  - **身份验证设置** 您可以对 Exchange ActiveSync 虚拟目录进行配置的两种验证方法是基本身份验证和客户证书验证。

