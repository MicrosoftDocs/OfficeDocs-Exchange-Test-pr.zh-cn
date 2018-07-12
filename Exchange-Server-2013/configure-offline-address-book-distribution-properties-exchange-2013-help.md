---
title: '配置脱机通讯簿分发属性: Exchange 2013 Help'
TOCTitle: 配置脱机通讯簿分发属性
ms:assetid: 8df985e9-75ba-47ea-9cc3-aa98a5d8acf4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123710(v=EXCHG.150)
ms:contentKeyID: 50491009
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.ClientAccess.OabDistributionGeneralPage
ms.translationtype: HT
---

# 配置脱机通讯簿分发属性

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-14_

对于 Exchange 中的每个脱机通讯簿 (OAB) 分发点，您可以配置两个 URL — 一个只可从公司内部网络访问的内部 URL 和一个可从 Internet 访问的外部 URL。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“脱机通讯簿”条目。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序配置 OAB 分发属性

此示例将 OAB 虚拟目录 OAB（默认网站）上 OAB 分发的轮询间隔设置为六个小时。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -PollInterval 360

此示例将默认 OAB 虚拟目录 OAB（默认网站）的外部分发点设置为 https://contoso.com/OAB。

    Set-OABVirtualDirectory "OAB (Default Web Site)" -ExternalUrl https://contoso.com/OAB

有关语法和参数的详细信息，请参阅 [Set-OabVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb124707\(v=exchg.150\))。

## 详细信息

[脱机通讯簿](offline-address-books-exchange-2013-help.md)

