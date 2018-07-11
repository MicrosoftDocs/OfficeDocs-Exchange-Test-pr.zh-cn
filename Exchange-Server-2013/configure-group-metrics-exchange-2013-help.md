---
title: '配置组指标: Exchange 2013 Help'
TOCTitle: 配置组指标
ms:assetid: 76ccd6a7-e2ec-42f4-9ab3-e8cc257ac896
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ649327(v=EXCHG.150)
ms:contentKeyID: 50490859
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置组指标

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

提供有关通讯组及动态通讯组大小的信息的邮件提示依赖于组指标数据。在指定的邮箱服务器上生成组指标数据。有关组指标的详细信息，请参阅[组的指标和邮件提醒](group-metrics-and-mailtips-exchange-2013-help.md)。

可以在邮箱服务器上启用或禁用组指标生成。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;组指标\&quot;条目。

  - 组指标数据仅用于邮件提示。请确保在您的组织中已启用组指标邮件提示。有关详细步骤，请参阅[针对组织关系管理邮件提示](manage-mailtips-for-organization-relationships-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序启用或禁用组指标生成

> [!NOTE]  
> 默认情况下，在负责生成脱机通讯簿 (OAB) 的任何服务器上都会生成组指标数据。这些示例仅是不使用 OAB 的组织所需的。


要在邮箱服务器上启用或禁用组指标生成，请运行以下命令：

    Set-MailboxServer <ServerIdentity> -ForceGroupMetricsGeneration <$true | $false>

此示例在名为 MBX1 的邮箱服务器上启用组指标生成。

    Set-MailboxServer MBX1 -ForceGroupMetricsGeneration $true

## 您如何知道这有效？

要验证是否成功在不使用 OAB 的组织中启用或禁用了组指标生成，请执行以下操作：

1.  运行以下命令：
    
        Get-MailboxServer <ServerIdentity> | Format-List ForceGroupMetricsGeneration

2.  验证显示的设置是否为您配置的设置。

