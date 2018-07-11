---
title: '为 Exchange 管理中心找到内部和外部 URL: Exchange 2013 Help'
TOCTitle: 为 Exchange 管理中心找到内部和外部 URL
ms:assetid: 3ddb30ff-a405-4b9d-8d77-2d7a3a5ab8fa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ680108(v=EXCHG.150)
ms:contentKeyID: 50490413
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 Exchange 管理中心找到内部和外部 URL

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-04_

因为 Exchange 管理中心 (EAC) 是 Exchange Server 2013 中提供的一个基于 Web 的管理控制台，因此您可以在 Web 浏览器中使用 ECP 虚拟目录的 URL 访问它。本主题将演示如何查找 ECP 虚拟目录的 URL。

> [!NOTE]  
> ECP 是为 Exchange Server 2010 开发的基于 Web 的用户界面。虚拟目录的 EAC cmdlet 仍然使用“ECP”这个名称，并且这些 cmdlet 可用于管理 Exchange 2010 和 Exchange 2013 ECP 虚拟目录。


有关 EAC 的详细信息，请参阅 [Exchange 2013 中的 Exchange 管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 无法使用 EAC 执行此过程。必须使用命令行管理程序。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“Exchange 管理中心连接”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序查找 ECP 虚拟目录的内部和外部 URL

本示例将以格式化列表的形式返回 ECP 虚拟目录的名称、内部 URL 和外部 URL。

    Get-ECPVirtualDirectory | Format-List Name,InternalURL,ExternalURL

命令完成后，在 Web 浏览器中使用 *InternalURL* 或 *ExternalURL* 值启动 EAC。

有关语法和参数的详细信息，请参阅 [Get-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd351058\(v=exchg.150\))。

