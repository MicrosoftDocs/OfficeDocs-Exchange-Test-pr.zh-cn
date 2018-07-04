---
title: '创建 Outlook Web App 邮箱策略: Exchange 2013 Help'
TOCTitle: 创建 Outlook Web App 邮箱策略
ms:assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335191(v=EXCHG.150)
ms:contentKeyID: 50490184
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建 Outlook Web App 邮箱策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2013-05-30_

您可以创建 Outlook Web App 邮箱策略来应用一组公用的策略设置。Outlook Web App 邮箱策略用于应用和标准化特定用户组的设置，例如附件设置。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能运行此 cmdlet。虽然此主题中列出了该 cmdlet 的所有参数，但如果这些参数未包含在分配给您的权限中，则您无法使用这些参数。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Outlook Web App 邮箱策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 创建 Outlook Web App 邮箱策略

1.  在 EAC 中，单击“权限” \> “Outlook Web 应用程序策略”。

2.  单击“新建”按钮。

3.  
    
    输入策略名称。

4.  
    
    使用复选框来启用或禁用功能。默认情况下，显示最常用的功能。要查看可以启用或禁用的所有功能，可单击“更多选项”。
    
    > [!NOTE]
    > Outlook Web App 邮箱策略的功能设置将覆盖 Outlook Web App 虚拟目录设置。您可以在命令行管理程序中使用 <strong>Set-CASMailbox</strong> cmdlet 更改单个用户的分段设置。


5.  单击“保存”保存此策略。

## 使用命令行管理程序创建 Outlook Web App 邮箱策略

本示例将创建一个名为 `Policy1` 的 Outlook Web App 邮箱策略。

  - 在此命令行管理程序中，运行以下命令。
    
        New-OwaMailboxPolicy -Name Policy1

有关语法和参数的详细信息，请参阅 [New-OwaMailboxPolicy](https://technet.microsoft.com/zh-cn/library/dd351067\(v=exchg.150\))。有关使用命令行管理程序配置 Outlook Web App 邮箱策略的信息，请参阅 [Set-OwaMailboxPolicy](https://technet.microsoft.com/zh-cn/library/dd297989\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否成功创建 Outlook Web App 邮箱策略：

  - 在 EAC 中，单击“权限”\>“Outlook Web App 策略”，然后查找您新建的邮箱策略。

