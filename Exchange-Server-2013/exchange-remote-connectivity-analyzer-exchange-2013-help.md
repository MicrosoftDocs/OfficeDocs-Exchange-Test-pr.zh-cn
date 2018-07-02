---
title: 'Exchange 远程连接分析器: Exchange 2013 Help'
TOCTitle: Exchange 远程连接分析器
ms:assetid: dd26698e-d00c-47f5-a7aa-c3894fe86c75
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff701693(v=EXCHG.150)
ms:contentKeyID: 50491788
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 远程连接分析器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-09-22_

MicrosoftExchange 远程连接分析器 (ExRCA) 可帮助您确保正确设置 Exchange 服务器的连接。如果您遇到问题，它还可以帮助您查找并修复这些问题。ExRCA 网站可以运行测试以检查 MicrosoftExchange ActiveSync、Exchange Web 服务、MicrosoftOutlook 和 Internet 电子邮件连接。

## 远程连接分析器测试

您可以使用 ExRCA 执行几个测试。以下测试可在 Exchange 2007 和更高版本上进行：

  - Exchange ActiveSync

  - Exchange Web 服务

  - Outlook

  - Internet 电子邮件

## Exchange ActiveSync 测试

您可以针对 Exchange ActiveSync 运行以下测试：

  - **“Exchange ActiveSync：”** 此测试将模拟移动设备使用 Exchange ActiveSync 连接 Exchange 服务器所采用的步骤。

  - **Exchange ActiveSync 自动发现**：此测试将完成 Exchange ActiveSync 设备用来从自动发现服务中获取设置的所有步骤。

## Exchange Web 服务连接测试

Exchange Web 服务测试检查多个 Exchange Web 服务的设置。您可以针对 Exchange Web 服务运行以下测试：

  - **同步、通知、可用性和自动回复**：这些测试将完成用于确认 Exchange Web 服务是否正在运行的许多基本的 Exchange Web 服务任务。这对想要使用 Entourage EWS 或其他 Web 服务客户端解决外部访问问题的 IT 管理员很有用。

  - **服务帐户访问(开发人员)** ：此测试将验证服务帐户访问指定邮箱、在该邮箱中创建和删除项目以及通过 Exchange 模拟访问该邮箱的能力。此测试主要由应用程序开发人员用于测试使用其他凭据访问邮箱的能力。

## Microsoft Office Outlook 连接测试

您可以针对 Outlook 连接运行以下测试：

  - **Outlook 无处不在 (HTTP 上的 RPC)**：此测试将完成 Outlook 通过 Outlook 无处不在 (HTTP 上的 RPC) 进行连接所采用的步骤。

  - **Outlook 自动发现**：此测试将完成 Outlook 用于从自动发现服务中获取设置的步骤。此测试不会实际连接到邮箱。

## Internet 电子邮件测试

您可以针对 Internet 电子邮件运行以下测试：

  - **入站 SMTP** **电子邮件**：此测试将完成 Internet 电子邮件服务器用来将入站 SMTP 电子邮件发送到您的域的步骤。

  - **出站 SMTP 电子邮件**：此测试将根据特定要求检查您的出站 IP 地址。这包括反向 DNS、发件人 ID 和 RBL 检查。

  - **POP 电子邮件** ：此测试将完成电子邮件客户端通过 POP3 连接邮箱所采用的步骤。

  - **IMAP 电子邮件** ：此测试将完成电子邮件客户端通过 IMAP 连接邮箱所采用的步骤。

