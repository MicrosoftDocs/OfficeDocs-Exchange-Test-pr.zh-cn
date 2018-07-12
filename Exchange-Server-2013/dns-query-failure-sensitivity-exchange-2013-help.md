---
title: 'DNS 查询失败敏感度: Exchange 2013 Help'
TOCTitle: DNS 查询失败敏感度
ms:assetid: a3c3980c-20ca-4b54-a2e6-76d49af620b4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb676467(v=EXCHG.150)
ms:contentKeyID: 52061543
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DNS 查询失败敏感度

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-02_

在 Microsoft Exchange Server 2013 中，可以为目标域调整 DNS 查询敏感度，以便遇到 DNS 错误时能更快地进行邮件传递。但是，在某些情况下该调整可能导致传递失败，具体取决于 DNS 错误。

## DNS 查询和远程邮件传递

负责向外部收件人传递邮件的 Exchange 服务器必须能找到为外部收件人接收邮件的目标邮件服务器。根据目标，邮件在等待传递到远程收件人的过程中将放入一个或多个远程传递队列中。有关传递队列的详细信息，请参阅[队列](queues-exchange-2013-help.md)。

Exchange 服务器查询配置的 DNS 服务器，以查找传递邮件所需的 DNS 记录。DNS 服务器将按所列顺序进行查询。如果某一 DNS 服务器不可用，则查询会转到列表上的下一 DNS 服务器。对 DNS 服务器查询下列信息：

  - **外部收件人域部分的邮件交换 (MX) 记录**   MX 记录包含负责为该域接收邮件的消息服务器的完全限定域名 (FQDN)，以及该消息服务器的首选项值。较低的首选项值表示首选消息服务器。如果域有多个 MX 记录，则首选项值非常重要。为了优化容错能力，大多数组织都使用多个消息服务器和具有不同首选项值的多个 MX 记录。

  - **目标消息服务器的地址 (A) 记录**   MX 记录中使用的每个消息服务器都应具有一个对应的 A 记录。该 A 记录用于查找目标消息服务器的 IP 地址。订阅的边缘传输服务器使用该 IP 地址来打开与目标消息服务器的 SMTP 连接。尽管从技术上来说，可以在 MX 记录中使用规范名称 (CNAME) 记录的 FQDN，但此做法违反了 RFC 974、RFC 1034、RFC 1912 和 RFC 2181，因此不为多数消息服务器所支持。
    
    将以根 DNS 服务器开始的迭代 DNS 查询和递归 DNS 查询根据需要组合起来，使用这种组合将 MX 记录中发现的消息服务器的 FQDN 解析为 IP 地址。

在 Exchange 2013 中，每个 DNS 服务器的 DNS 查询限制为 5 秒（不可配置），整个 DNS 查询限制为 1 分钟。

## 潜在的 DNS 问题

即使正确配置了 Exchange 服务器上的 DNS 设置，特定域的 DNS 记录或用于查找特定域权威 DNS 服务器的任何 DNS 服务器仍可能发生问题。通常，这些问题会超出您的控制范围，需要那些 DNS 服务器的所有方来解决。这些与 DNS 有关的错误可能是由下列一个或多个条件引起的：

  - 无效的目标域 DNS 记录

  - DNS 服务器使用方面的问题

  - DNS 服务器复制方面的问题

在 Exchange 2013 中，如果 DNS 查询导致错误，则只有在该 DNS 服务器没有对当前查询返回错误时，才会继续查询下一个 DNS 服务器。

您可以通过修改 `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML 应用程序配置文件来控制 DNS 查询失败敏感度。此文件与 Microsoft Exchange 传输服务相关联。重新启动 Microsoft Exchange 传输服务后，将应用保存到此文件中的更改。重新启动此服务时，会临时中断服务器上的邮件流。DNS 查询失败敏感度由 EdgeTransport.exe.config 文件中的 *DnsFaultTolerance* 键控制。此键使用下列值：

  - **Lenient**   当 DNS 查询遇到有效 MX 记录和无效 MX 记录组合时，DNS 查询将继续进行，直到达到 1 分钟的 DNS 查询超时值为止。丢弃无效的 MX 记录，同时使用首选项值最低的有效 MX 记录将邮件传递到目标消息服务器。此值为默认值。

  - **Normal**   当 DNS 查询首先遇到无效 MX 记录时，立即丢弃其首选项值大于或等于无效 MX 记录的任何已解析 MX 记录。使用具有最低首选项值的剩余 MX 记录不需等待至整个 DNS 查询超时即可将邮件传递到目标消息服务器。尽管这种行为可以更快地进行邮件传递，但此行为的潜在缺点是，如果下列条件为真，则 DNS 查询可能没有有效的 MX 记录。
    
      - 无效 MX 记录是目标域的第一个 MX 记录。
    
      - 有效 MX 记录具有与无效 MX 记录相同的优先级值。

在 `Normal` 模式和 `Lenient` 模式下，从不缓存无效 MX 记录的 DNS 查询结果。下一次执行 DNS 查询时，会尝试解析目标域的 MX 记录。

> [!NOTE]  
> 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

