---
title: 'TLS 功能及相关术语: Exchange 2013 Help'
TOCTitle: TLS 功能及相关术语
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52061491
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# TLS 功能及相关术语

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-06-18_

Microsoft Exchange Server 2013 提供管理功能和其他增强功能，可改善对传输层安全性 (TLS) 的总体管理。使用这项功能时，您需要了解一些与 TLS 有关的功能。某些术语和概念适用于多项与 TLS 有关的功能。本主题提供了每项功能的简要介绍，目的是帮助您了解与 TLS 和域安全性功能集有关的一些差异和常用术语：

  - **传输层安全性** TLS 是一种标准协议，用于在 Internet 或 Intranet 上提供安全的 Web 通信。它可以使客户端对服务器进行身份验证，也可以使服务器对客户端进行身份验证。它还通过对通信进行加密来提供安全通道。TLS 是安全套接字层 (SSL) 协议的最新版本。

  - **相互 TLS** 相互 TLS 身份验证与通常部署的 TLS 不同。通常，部署 TLS 只是用于以加密的形式提供机密性。发送方和接收方之间不进行任何身份验证。此外，有时，TLS 部署只对接收服务器进行身份验证。这种 TLS 部署是 TLS 的 HTTP 实现方式的典型部署。此实现方式是 SSL，只对接收服务器进行身份验证。
    
    使用相互 TLS 身份验证，每台服务器通过验证另一台服务器提供的证书来验证这台服务器的身份。在这种情况下，如果在 Exchange 2013 环境中通过已验证的连接从外部域中接收邮件，则 Microsoft Outlook 将显示“域安全”图标。

  - **域安全性**   域安全性是使相互 TLS 成为有用并且容易管理的技术的功能集，例如证书管理、连接器功能和 Outlook 客户端行为。通过 Exchange 2013 客户端访问服务器路由出站电子邮件时，不支持域安全性。

  - **机会型 TLS**   在 Exchange 2013 中，安装程序会创建一个自签名证书。默认情况下启用 TLS。这样，任何发送系统都能够对到 Exchange 的入站 SMTP 会话进行加密。默认情况下，Exchange 2013 还对所有远程连接尝试实现 TLS。

  - **直接信任**   默认情况下，边缘传输服务器与邮箱服务器之间的所有通信均进行身份验证并加密。身份验证和加密的基础机制仍是相互 TLS。Exchange 2013 使用直接信任（而不是使用 X.509 验证）来验证证书。直接信任意味着 Active Directory 或 Active Directory 轻型目录服务 (AD LDS) 中存在证书即证明证书有效。Active Directory 被认为是受信任的存储机制。使用直接信任时，证书是自签名还是由证书颁发机构签名并不重要。将边缘传输服务器订阅到 Exchange 组织后，边缘订阅将在 Active Directory 中发布边缘传输服务器证书，以便邮箱服务器进行验证。Microsoft Exchange EdgeSync 服务会使用边缘传输服务器要验证的邮箱服务器证书集来更新 AD LDS。

