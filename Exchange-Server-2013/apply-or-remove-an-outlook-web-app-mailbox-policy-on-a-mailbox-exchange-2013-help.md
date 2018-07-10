---
title: '向邮箱应用或删除 Outlook Web App 邮箱策略: Exchange 2013 Help'
TOCTitle: 向邮箱应用或删除 Outlook Web App 邮箱策略
ms:assetid: 51d8e269-b0d5-4bc7-9b3d-0460871e54fa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876884(v=EXCHG.150)
ms:contentKeyID: 50490548
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 向邮箱应用或删除 Outlook Web App 邮箱策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-12_

可以使用 EAC 或命令行管理程序向一个或多个邮箱应用 Outlook Web App 邮箱策略或者删除一个策略。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Outlook Web App 邮箱策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 应用 Outlook Web App 邮箱策略

## 使用 EAC 应用 Outlook Web App 邮箱策略

1.  在 EAC 中，单击“收件人”\>“邮箱”。

2.  在工作窗格中，单击以选择要向其应用 Outlook Web App 邮箱策略的邮箱。也可以选择多个邮箱。

3.  **如果选择了一个邮箱：** 
    
    1.  在详细信息窗格中向下滚动到“电子邮件连接”并单击“查看详细信息”。
    
    2.  单击“浏览”查看和选择可用的邮箱策略。
    
    3.  单击“保存”以将所选策略分配给所选邮箱。
    
    **如果选择了多个邮箱：** 
    
    1.  在详细信息窗格中向下滚动到“Outlook Web App”并单击“分配策略”。
    
    2.  单击“浏览”查看和选择可用的邮箱策略。
    
    3.  单击“保存”以将所选策略分配给所选邮箱。

## 使用命令行管理程序向现有邮箱应用 Outlook Web App 邮箱策略

此示例将向用户邮箱 tony@contoso.com 应用名为“日历”的 Outlook Web App 邮箱策略。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:Calendar

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

## 删除 Outlook Web App 邮箱策略

## 使用 EAC 删除 Outlook Web App 邮箱策略

1.  在 EAC 中，单击“收件人”\>“邮箱”。

2.  在工作窗格中，单击以选择要从中删除 Outlook Web App 邮箱策略的邮箱。

3.  在详细信息窗格中向下滚动到“电子邮件连接”并单击“查看详细信息”。
    
    如果分配了邮箱策略，请单击“清除”以从邮箱中删除它。

4.  单击“保存”保存更改。

## 使用命令行管理程序从现有邮箱删除 Outlook Web App 邮箱策略。

此示例将从用户邮箱 tony@contoso.com 中删除 Outlook Web App 邮箱策略。

    Set-CASMailbox -Identity tony@contoso.com -OwaMailboxPolicy:$null

有关语法和参数的详细信息，请参阅 [Set-CASMailbox](https://technet.microsoft.com/zh-cn/library/bb125264\(v=exchg.150\))。

