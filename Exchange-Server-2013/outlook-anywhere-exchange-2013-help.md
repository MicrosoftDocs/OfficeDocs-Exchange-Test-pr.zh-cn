---
title: 'Outlook 无处不在: Exchange 2013 Help'
TOCTitle: Outlook 无处不在
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50491024
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook 无处不在

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

在 Microsoft Exchange Server 2013 中，Outlook Anywhere 功能（以前称为 HTTP 上的 RPC）让使用 MicrosoftOutlook 2013、Outlook 2010 或 Outlook 2007 的客户端可以通过支持 HTTP 上的 RPC 功能的 Windows 网络组件，从公司网络外部或通过 Internet 连接到各自的 Exchange 服务器。本主题介绍 Outlook 无处不在功能并列出了使用 Outlook 无处不在的益处。

**目录**

Outlook 无处不在 and Exchange 2013

Benefits of using Outlook 无处不在

Deploying Outlook 无处不在

Managing Outlook 无处不在

Outlook 无处不在 coexistence

Testing Outlook 无处不在 connectivity

## Outlook 无处不在 和 Exchange 2013

Windows RPC over HTTP Proxy 组件（Outlook Anywhere 客户端使用它进行连接）用一个 HTTP 层封装远程过程调用 (RPC)。这样不必打开 RPC 端口即可让通信穿越网络防火墙。在 Exchange 2013 中，默认情况下此功能处于启用状态，这是因为 Exchange 2013 不允许直接 RPC 连接。

## 使用 Outlook 无处不在 的益处

Outlook Anywhere 向使用 Outlook 2013、Outlook 2010 或 Outlook 2007 访问 Exchange 邮件基础结构的客户端提供以下益处：

  - 用户可通过 Internet 远程访问 Exchange 服务器。

  - 可以使用 Outlook Web App 和 Microsoft Exchange ActiveSync 所用的相同 URL 和命名空间。

  - 可以使用 Outlook Web App 和 Exchange ActiveSync 所用的相同的安全套接字层 (SSL) 服务器证书。

  - 未通过身份验证的 Outlook 请求无法访问 Exchange 服务器。

  - 无需使用虚拟专用网络 (VPN) 即可通过 Internet 访问 Exchange 服务器。

  - 如果已经通过 SSL 使用 Outlook Web App 或 Exchange ActiveSync，则无需从 Internet 打开任何其他端口。

  - 通过使用 **Test-OutlookConnectivity** cmdlet，可以测试 Outlook Anywhere 的端到端客户端连接和基于 TCP 的连接。

## 部署 Outlook 无处不在

在 Exchange 2013 中，默认会启用 Outlook 无处不在，因为所有 Outlook 连接都通过 Outlook 无处不在 进行。要成功使用 Outlook 无处不在，唯一必须执行的部署后任务是：在客户端访问服务器上安装有效的 SSL 证书。组织中的邮箱服务器只需要默认的自签名 SSL 证书。

## 管理 Outlook 无处不在

可以使用 Exchange 管理中心或 Exchange 命令行管理程序来管理 Outlook Anywhere。

## Outlook 无处不在 共存

如果打算在与 Exchange Server 以前版本共存的方案中安装 Exchange 2013，则可能仍需要在组织中保留 Outlook 2003 客户端。Outlook 2003 不是 Exchange 2013 支持的客户端。

在将命名空间移动到 Exchange 2013 之前，需要确保所有 Outlook 客户端已升级到支持的最低版本。Outlook 无处不在 与 Exchange 2013 的连接需要使用 Outlook 2007 或更高版本，即使目标邮箱仍位于 Exchange 2007 或 Exchange 2010 上也是如此。

如果当前正在 Exchange 2007 或 2010 环境中使用 Outlook 无处不在，若要允许 Exchange 2013 客户端访问服务器将连接代理到 Exchange 2007/2010 服务器，必须在组织内的所有 Exchange 2007/2010 CAS 上启用并配置 Outlook 无处不在。但是，如果当前并未在 Exchange 2007/2010 环境中使用 Outlook 无处不在，并且不希望开始使用它，那么你不需要启用旧版环境中的 Outlook 无处不在。有关如何在运行于 Exchange Server 2007 的客户端访问服务器上启用 Outlook 无处不在 的说明，请参阅[如何启用 Outlook 无处不在](https://go.microsoft.com/fwlink/p/?linkid=510497)。有关如何在运行于 Exchange Server 2010 的客户端访问服务器上启用 Outlook 无处不在 的说明，请参阅[启用 Outlook 无处不在](https://go.microsoft.com/fwlink/p/?linkid=510502)。

请确保在客户端访问服务器上启用 Outlook 无处不在 时，为 IIS 身份验证选择 NTLM。

最后，配置 Outlook 无处不在 外部主机名称以指向 Exchange 2013Outlook 无处不在 主机名称。有关 Exchange Server 2007 的说明，请参阅[如何配置 Outlook 无处不在 的外部主机名称](https://go.microsoft.com/fwlink/p/?linkid=510530)。有关 Exchange Server 2010 的说明，请参阅[配置 Outlook 无处不在 的外部主机名称](https://go.microsoft.com/fwlink/p/?linkid=510531)。

## 测试 Outlook 无处不在 连接

您可以执行以下任一操作来测试端到端 Outlook 连接：

  - 运行 **Test-OutlookConnectivity** cmdlet。该 cmdlet 将测试 Outlook 无处不在（HTTP 上的 RPC）连接。如果此 cmdlet 测试失败，则输出中会标明失败的步骤。有关语法和参数的详细信息，请参阅[Test-OutlookConnectivity](https://technet.microsoft.com/zh-cn/library/dd638082\(v=exchg.150\))。

  - 使用 Outlook 远程连接分析器 (ExRCA) 运行 Exchange Anywhere 连接测试。运行此测试时，会向您显示详细的摘要，其中说明测试失败之处以及为修复问题所需采取的步骤。有关详细信息，请参阅 [Exchange 远程连接分析器](exchange-remote-connectivity-analyzer-exchange-2013-help.md)。

两项测试都在从自动发现服务获得服务器设置之后尝试通过 Outlook Anywhere 进行登录。端到端验证包括下列内容：

  - 测试自动发现连接

  - 验证 DNS

  - 验证证书（证书名称是否与网站匹配，证书是否过期，证书是否受信任）

  - 检查是否已正确设置防火墙（ExRCA 检查总体防火墙设置。cmdlet 将测试 Windows 防火墙配置。）

  - 通过登录到用户邮箱来确认客户端连接

