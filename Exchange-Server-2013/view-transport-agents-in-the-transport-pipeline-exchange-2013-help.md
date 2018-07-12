---
title: '查看传输管道中的传输代理: Exchange 2013 Help'
TOCTitle: 查看传输管道中的传输代理
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51408272
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看传输管道中的传输代理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

您可以使用 Exchange 命令行管理程序在 Microsoft Exchange Server 2013 邮箱服务器和客户端访问服务器上查看传输管道中的传输代理列表。具体来说，**Get-TransportPipeline** cmdlet 可以显示有关传输管道中下列传输代理类型的信息：

  - 邮箱服务器上的传输服务中基于 **SmtpReceiveAgent**、**RoutingAgent**、**DeliveryAgent** 和 **StorageAgent** 类的代理。

  - 邮箱服务器上的邮箱传递服务中基于 **SmtpReceiveAgentClass** 的代理。

  - 客户端访问服务器上的前端传输服务中基于 **SmtpReceiveAgentClass** 的代理。

您可以查看在传输管道中遇到邮件的所有已启用传输代理的列表，以及注册这些传输代理的 SMTP 事件。有关传输代理的详细信息，请参阅[传输代理](transport-agents-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输代理”条目。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序查看传输管道中传输代理的列表

若要使用命令行管理程序在 Exchange 服务器上查看传输管道中的传输代理列表，可以运行以下命令：

    Get-TransportPipeline | Format-List

若要将结果导出至名为 C:\\My Documents\\Transport Agents.txt 的文本文件，可以运行以下命令：

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## 您如何知道操作成功？

只有在启动传输服务与运行 **Get-TransportPipeline** cmdlet 之间这段时间内，在传输管道中遇到邮件的传输代理才会由该 cmdlet 显示。在传输管道中没有遇到邮件的传输代理不会出现在由 **Get-TransportPipeline** cmdlet 显示的结果中，即使已启用该传输代理也是如此。

