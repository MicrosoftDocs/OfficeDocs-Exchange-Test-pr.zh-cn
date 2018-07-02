---
title: '邮件签名和加密的 S/MIME: Exchange 2013 Help'
TOCTitle: 邮件签名和加密的 S/MIME
ms:assetid: 887c710b-0ec6-4ff0-8065-5f05f74afef3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn626158(v=EXCHG.150)
ms:contentKeyID: 61212707
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮件签名和加密的 S/MIME

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

S/MIME（安全/多用途 Internet 邮件扩展）是被广泛接受的用于发送数字签名和加密邮件的方法，或者更确切地说是一种协议。S/MIME 允许您加密电子邮件，并对它们进行数字签名。当您在电子邮件中使用 S/MIME 时，可帮助接收邮件的用户确信他们在收件箱中看到的邮件就是发件人发出的邮件。它还能帮助接收邮件的用户确信邮件来自特定的发件人，而不是冒充此发件人的人。为此，S/MIME 提供了加密安全服务，例如身份验证、邮件完整性和防发送方抵赖（使用数字签名）。它还有助于增强电子邮件的隐私和数据安全（使用加密）。有关电子邮件环境下 S/MIME 的历史记录和体系结构的完整背景，请参阅[了解 S/MIME](https://go.microsoft.com/fwlink/?linkid=393948)。

作为管理员，如果您具有 Exchange 2013 SP1 或 Exchange Online（属于 Office 365 的一部分）邮箱，您可以为组织启用基于 S/MIME 的安全。使用此处链接的主题中的指南以及 Exchange 命令行管理程序来设置 S/MIME。若要将支持的 Outlook 或 ActiveSync 版本中的 S/MIME 与 Exchange 2013 SP1 或 Exchange Online 一起使用，您组织中的用户必须拥有为签名和加密目的而颁发的证书和发布到本地 Active Directory (AD DS) 域服务的数据。您的 AD DS 必须在位于由您控制的物理位置的计算机上，而不是 Internet 上其他位置的远程设施或基于云的服务。有关 AD DS 的详细信息，请参阅 [Active Directory 域服务](https://go.microsoft.com/fwlink/?linkid=394064)。

## 支持的场景和技术考虑因素

如果您的组织使用 Exchange 2013 SP1 或 Exchange Online，您可以将 S/MIME 设置为用于以下任一终结点：

  - Outlook 2010

  - Outlook 2013

  - Outlook Web App

  - Exchange ActiveSync (EAS)

根据您选择的终结点，为这些终结点设置 S/MIME 时需遵循的步骤可能略有不同。通常情况下，您需要完成以下步骤：

  - 安装基于 WIndows 的证书颁发机构，并设置公钥基础结构以颁发 S/MIME 证书。还支持第三方证书提供商颁发的证书。有关详细信息，请参阅 [Active Directory 证书服务概述](https://technet.microsoft.com/library/hh831740.aspx)。

  - 在内部部署 AD DS 帐户的 UserSMIMECertificate 和/或 UserCertificate 属性中发布用户证书。

  - 对于 Exchange Online 组织，使用 DirSync 的相应版本将用户证书从 AD DS 同步到 Azure Active Directory。这些证书将从 Azure Active Directory 同步到 Exchange Online 目录，并将用于加密给收件人的邮件。

  - 设置虚拟证书集合以验证 S/MIME。此信息供 OWA 用于验证电子邮件的前面并确保它是由可信证书签名的。

  - 将 Outlook 或 EAS 终结点设置为使用 S/MIME。

## 将 S/MIME 设置为用于 Outlook Web App

要将 Exchange 2013 SP1 或 Exchange Online 的 S/MIME 设置为用于 Outlook Web App，需执行以下步骤：

1.  [配置 Outlook Web App 的 S/MIME 设置](configure-s-mime-settings-for-outlook-web-app-exchange-2013-help.md)

2.  [设置虚拟证书集合以验证 S/MIME](set-up-virtual-certificate-collection-to-validate-s-mime-exchange-2013-help.md)

3.  [出于 S/MIME 目的将用户证书同步到 Office 365](https://technet.microsoft.com/zh-cn/library/dn626159\(v=exchg.150\)) 此步骤仅适用于 Exchange Online。

## 相关邮件加密技术

随着邮件安全变得越来越重要，管理员需要理解安全邮件的原则和概念。由于保护相关技术（例如 S/MIME）的不断推陈出新，这种理解变得尤为重要。要了解关于 S/MIME 的详细信息以及它在电子邮件环境下如何运作，请参阅[了解 S/MIME](https://go.microsoft.com/fwlink/?linkid=393948)。各种加密技术配合使用，为处于静止和传送状态的邮件提供保护。S/MIME 可与以下技术一起运作，但并不依赖于这些技术：

  -  
    **传输层安全 (TLS)** 对电子邮件服务器之间的隧道或路由进行加密，以帮助阻止窥探和窃听。

  -  
    **安全套接字层 (SSL)** 对电子邮件客户端和 Office 365 服务器之间的连接进行加密。

  -  
    **BitLocker** 对数据中心中硬盘驱动器上的数据进行加密，以使进行未授权访问的人员无法读取数据。

## S/MIME 与 Office 365 邮件加密对比

S/MIME 需要证书和发布基础结构，通常用于企业到企业和企业到消费者的情况。用户控制 S/MIME 中的加密密钥，并且可以选择是否为他们发送的每封邮件使用密钥。Outlook 等电子邮件程序搜索可信根证书颁发机构位置，以执行数字签名和签名验证。Office 365 邮件加密是一种基于策略的加密服务，可以由管理员（而不是单个用户）配置，以便对发送给组织内部或外部用户的邮件进行加密。它是基于 Azure 权限管理 (RMS)，而不依赖于公钥基础结构的联机服务。Office 365 邮件加密还提供其他功能，例如使用组织品牌自定义邮件的功能。有关 Office 365 邮件加密的详细信息，请参阅 [Office 365 邮件加密](https://go.microsoft.com/fwlink/?linkid=392525)。

## 详细信息

[Outlook Web App](outlook-web-app-exchange-2013-help.md)

[安全邮件 (2000)](https://technet.microsoft.com/zh-cn/library/cc962043.aspx)

