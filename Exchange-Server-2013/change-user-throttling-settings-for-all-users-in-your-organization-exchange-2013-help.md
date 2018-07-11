---
title: '更改组织中所有用户的用户限制设置: Exchange 2013 Help'
TOCTitle: 更改组织中所有用户的用户限制设置
ms:assetid: c45cacfc-768d-4605-9bb0-53e30273fe4d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863578(v=EXCHG.150)
ms:contentKeyID: 50556669
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改组织中所有用户的用户限制设置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-08-05_

通过更改默认限制设置，可以控制 Exchange 组织中单个用户的资源使用情况。

在 Exchange Server 2010 中可以控制各个用户使用资源的方式，该功能已针对 Exchange Server 2013 进行扩展。除非您自定义了限制策略，否则策略 GlobalThrottlingPolicy 将定义组织中每个新用户和现有用户的默认限制设置。在许多典型的 Exchange 部署方案中，策略 GlobalThrottlingPolicy 足以管理用户。

要自定义应用于组织中所有用户的限制设置，请创建一个作用域分配为“组织”的新限制策略。只能使用命令行管理程序更改默认限制设置。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[服务器运行状况和性能权限](server-health-and-performance-permissions-exchange-2013-help.md)主题中的“用户限制”条目。

  - 在新的“组织”作用域策略中，仅应设置不同于策略 GlobalThrottlingPolicy 及任何其他组织策略中的限制设置的设置。这样一来，策略 GlobalThrottlingPolicy 中的其余策略设置将被继承，就像在将来的 Exchange 更新中加入对限制策略的任何更新一样。在执行此过程之前，建议阅读主题 [Exchange 工作负载管理](exchange-workload-management-exchange-2013-help.md)中的“使用作用域管理限制策略”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序更改整个组织中的所有用户的资源使用方式

此示例创建了一个应用于组织中所有用户的限制策略。省略的任何参数都将继承默认限制策略 GlobalThrottlingPolicy 的值。

    New-ThrottlingPolicy -Name AllUsersEWSPolicy EwsMaxConcurrency 4 -ThrottlingPolicyScope Organization

有关语法和参数的详细信息，请参阅 [New-ThrottlingPolicy](https://technet.microsoft.com/zh-cn/library/dd351045\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功创建了“组织”限制策略，请执行以下操作：

1.  运行以下命令。
    
        Get-ThrottlingPolicy | Format-List

2.  验证在显示 GlobalThrottlingPolicy 对象的列中是否列出了刚创建的组织限制策略。

3.  运行以下命令。
    
        Get-ThrottlingPolicy | Format-List

4.  验证新组织策略的属性是否与配置的值匹配。

