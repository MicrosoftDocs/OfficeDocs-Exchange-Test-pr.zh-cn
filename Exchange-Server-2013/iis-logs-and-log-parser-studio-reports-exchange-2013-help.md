---
title: 'IIS 日志和 Log Parser Studio 报告: Exchange 2013 Help'
TOCTitle: IIS 日志和 Log Parser Studio 报告
ms:assetid: 01fa67d4-dc02-4c5f-93af-6da7b97d282f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn904092(v=EXCHG.150)
ms:contentKeyID: 63910927
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# IIS 日志和 Log Parser Studio 报告

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

## 分析 Log Parser Studio 报表

Log Parser Studio 是一个实用工具，可用于在多种类型的日志文件中执行搜索操作并创建报表，其中包括那些用于 Internet 信息服务 (IIS) 的日志文件。该工具基于 Log Parser 2.2 构建，其完整的用户界面简化了相关 SQL 查询的创建和管理。

[下载 Log Parser Studio](https://go.microsoft.com/fwlink/p/?linkid=524244) 并阅读博客文章 [Log Parser Studio 入门](https://go.microsoft.com/fwlink/p/?linkid=524243)。

请记住，在 Exchange 2013 中，所有通信都必须通过 IIS。这意味着，若要全面了解访问服务器的连接数、有关这些连接的协议专用信息以及对性能影响最大的用户，最好的办法是分析 IIS 日志。目前已针对 Log Parser Studio 开发出了二十余种新报表，以解决 Exchange 2013 的性能问题。

## Log Parser Studio 针对 Exchange 2013 性能问题的报表

若要全面了解您的 Exchange 2013 环境的总负载，请使用以下报表并针对每个服务器进行数值比较。

.zip 文件中包含了此处列出的 Log Parser Studio 报表以及与故障排除相关的其他报表，您可[从此处下载](https://go.microsoft.com/fwlink/p/?linkid=524245)。

  - **IIS:Requests Per Hour**。IIS 日志中来自默认网站（W3SVC1 目录）或后端网站（W3SVC2 目录）的馈送，但是二者无法同时进行。

  - **ACTIVESYNC\_WP:Clients by percent**。计算所有被用户代理中断的 ActiveSync 请求以及每个客户端占请求总数的百分比。

  - **ACTIVESYNC\_WP:Requests per hour (CSV)**。列出每小时的 ActiveSync 请求并将结果发送到 CSV 文件。

  - **ACTIVESYNC\_WP:Requests per user (CSV)**。列出每个用户的 ActiveSync 请求并将结果发送到 CSV 文件。

  - **ACTIVESYNC\_WP:Requests per user (Top 10k)**。针对前 10,000 名用户列出每个用户的 ActiveSync 请求。

  - **ACTIVESYNC\_WP:Top Talkers (CSV)**。从最高到最低请求计数列出排名居前的 ActiveSync 客户端，并将结果发送到 CSV 文件。

  - **EWS\_WP:Clients by percent**。计算所有被用户代理中断的 EWS 请求以及每个客户端占请求总数的百分比。

  - **EWS\_WP:Requests per hour (CSV)**。列出每小时的 EWS 请求总数。

  - **EWS\_WP:Requests per user (CSV)**。列出每个用户的 EWS 请求并将结果发送到 CSV 文件。

  - **EWS\_WP:Requests per user (Top 10k)**。针对前 10,000 名用户列出每个用户的 EWS 请求。

  - **EWS\_WP:Top Talkers (CSV)**。从最高到最低请求计数列出排名居前的 EWS 客户端。

  - **OLA\_WP:Errors, per user, per hour, per day**。按请求数量显示 Outlook 无处不在 用户。

  - **OLA\_WP:Requests per hour**。列出每小时的 Outlook 无处不在 请求。

  - **OLA\_WP:Requests per hour, per user**。列出每小时、每个用户的 Outlook 无处不在 请求。

  - **OLA\_WP:Requests per user (CSV)**。列出每个用户的 Outlook 无处不在 请求。

  - **OLA\_WP:Requests per user (Top 10k)**。针对前 10,000 名用户列出每个用户的 Outlook 无处不在 请求。

  - **OLA\_WP:Top Talkers**。从最高到最低请求计数列出排名居前的 Outlook 无处不在 客户端。

  - **OWA\_WP:Clients by percent**。计算所有被用户代理中断的 OWA 请求以及每个客户端占请求总数的百分比。

  - **OWA\_WP:Requests per hour (CSV)**。列出每小时的 OWA 请求并将结果发送到 CSV 文件。

  - **OWA\_WP:Requests per user (CSV)**。列出每个用户的 OWA 请求并将结果发送到 CSV 文件。

  - **OWA\_WP:Requests per user (Top 10k)**。针对前 10,000 名用户列出每个用户的 OWA 请求。

  - **OWA\_WP:Top Talkers (CSV)**。从最高到最低请求计数列出排名居前的 OWA 客户端，并将结果发送到 CSV 文件。

