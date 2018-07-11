---
title: '查看或配置 Outlook Web 应用程序邮箱策略属性: Exchange 2013 Help'
TOCTitle: 查看或配置 Outlook Web 应用程序邮箱策略属性
ms:assetid: be012ffe-8fdb-4fb7-aebd-78b3a55593fa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351097(v=EXCHG.150)
ms:contentKeyID: 50491440
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看或配置 Outlook Web 应用程序邮箱策略属性

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-04-13_

在创建 Outlook Web App 邮箱策略后，您可以配置多种选项以控制对 Outlook Web App 中用户可用的功能。例如，您可以启用或禁用收件箱规则或创建允许的附件文件类型列表。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“Outlook Web App 邮箱策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 查看或配置 Outlook Web App 邮箱策略

1.  在 EAC 中，单击“权限” \> “Outlook Web 应用程序策略”。

2.  在结果窗格中，单击以选择要查看或配置的邮箱策略。

3.  单击“编辑”按钮。

4.  
    
    在“常规”选项卡上，您可以查看并编辑策略的名称。

5.  
    
    在“功能”选项卡上，使用复选框可启用或禁用功能。默认情况下，显示最常用的功能。要查看可以启用或禁用的所有功能，可单击“更多选项”。
    
    > [!NOTE]
    > Outlook Web App 邮箱策略的功能设置将覆盖 Outlook Web App 虚拟目录设置。您可以在命令行管理程序中使用 <strong>Set-CASMailbox</strong> cmdlet 更改单个用户的分段设置。


6.  
    
    在“文件访问”选项卡上，使用“直接文件访问”复选框配置用户的文件访问和查看选项。文件访问使用户可以打开或查看附加到电子邮件的文件的内容。
    
    可根据用户是否已经登录公共或私人计算机来控制文件访问。用户选择私人计算机访问或公共计算机访问的选项只有在您使用基于表单式身份验证时才可用。所有其他形式的身份验证默认设置为私人计算机访问。

7.  在“脱机访问”选项卡中，使用选项按钮配置脱机访问的可用性。

8.  单击“保存”更新策略。

## 使用命令行管理程序配置 Outlook Web App 邮箱策略

此示例在默认邮箱策略中启用日历访问。

    Set-OwaMailboxPolicy -Identity Default -CalendarEnabled $true

有关语法和参数的详细信息，请参阅 [Set-OwaMailboxPolicy](https://technet.microsoft.com/zh-cn/library/dd297989\(v=exchg.150\))。

## 使用命令行管理程序查看 Outlook Web App 邮箱策略

本示例将检索组织 `Executives` 中 Outlook Web App 邮箱策略 `Fabrikam` 的属性。

    Get-OwaMailboxPolicy -Identity Fabrikam\Executives

有关语法和参数的详细信息，请参阅 [Get-OwaMailboxPolicy](https://technet.microsoft.com/zh-cn/library/dd351095\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功编辑 Outlook Web App 邮箱策略：

1.  在 EAC 中，单击“权限”\>“Outlook Web App 策略”，然后选择特定 Outlook Web App 邮箱策略。

2.  单击“编辑”按钮查看邮箱策略的属性。

3.  单击“保存”或“取消”关闭属性页面。

