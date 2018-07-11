---
title: '配置邮箱数据库副本的激活策略: Exchange 2013 Help'
TOCTitle: 配置邮箱数据库副本的激活策略
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50490769
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮箱数据库副本的激活策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-02_

激活是将邮箱数据库副本从被动副本更改为主动副本的过程。 激活可以作为数据库或服务器故障转移操作的一部分由系统自动进行，也可以作为数据库或服务器切换操作的一部分由管理员手动执行。 阻止数据库激活将阻止数据库在数据库或服务器故障转移期间成为主动副本。

若要了解与邮箱数据库副本相关的其他管理任务， 请查看[管理邮箱数据库副本](managing-mailbox-database-copies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间： 1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[高可用性和站点恢复权限](high-availability-and-site-resilience-permissions-exchange-2013-help.md)主题中的“邮箱数据库副本”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为邮箱数据库副本配置激活策略

1.  
    
    在 EAC 中，转到“服务器”\>“数据库”。

2.  选择要配置的数据库。

3.  
    
    在“详细信息”窗格中的“数据库副本”下，找到要配置的数据库副本并单击“挂起”。

4.  可以选择添加注释并选中“此副本只能通过手动干预激活”复选框。

5.  单击“保存”可保存邮箱数据库副本的配置更改。

## 使用命令行管理程序挂起或恢复数据库副本激活

本示例将阻止服务器 MBX2 上数据库 DB1 的副本激活。

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly

本示例将恢复服务器 MBX2 上数据库 DB1 的副本激活。

    Resume-MailboxDatabaseCopy -Identity DB1\MBX2

有关语法和参数的详细信息，请参阅 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\)) 和 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335220\(v=exchg.150\))。

## 使用命令行管理程序为服务器配置激活策略

本示例将服务器 MBX2 上的数据库副本配置为阻止激活。

    Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked

本示例将服务器 MBX3 上的数据库副本配置为阻止站点外激活。

    Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly

本示例将服务器 MBX4 上的数据库副本配置为取消阻止激活。

    Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted

有关语法和参数的详细信息，请参阅 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd351074\(v=exchg.150\))、[Resume-MailboxDatabaseCopy](https://technet.microsoft.com/zh-cn/library/dd335220\(v=exchg.150\)) 或 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功配置了激活策略，请执行以下操作之一：

  - 在命令行管理程序中，运行以下命令来验证数据库副本的激活设置。
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended

  - 在命令行管理程序中，运行以下命令来验证 DAG 成员的激活设置。
    
        Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy

