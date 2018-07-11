---
title: '创建脱机通讯簿虚拟目录: Exchange 2013 Help'
TOCTitle: 创建脱机通讯簿虚拟目录
ms:assetid: 2c70e21f-2b12-414a-9e8c-65634a767c72
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996917(v=EXCHG.150)
ms:contentKeyID: 50490126
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建脱机通讯簿虚拟目录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-16_

OAB 虚拟目录是 OAB 的分发。默认情况下，安装 Microsoft Exchange Server 2013 时，将在 Internet 信息服务 (IIS) 的默认内部网站中创建一个名为 OAB 的新虚拟目录。如果有从组织防火墙外部连接到 Microsoft Outlook 的客户端用户，则可以添加外部网站。另外，在命令行管理程序中运行 **New-OABVirtualDirectory** cmdlet 时，将在本地 Exchange 服务器的默认 IIS 网站中创建一个名为 OAB 的新虚拟目录。

创建 OAB 虚拟目录不是一项常见任务。Exchange 允许使用一个名为 OAB 的 OAB 虚拟目录，只有当现有 OAB 虚拟目录出现问题并且以前的 OAB 虚拟目录被删除后，才应创建 OAB 虚拟目录。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

> [!IMPORTANT]  
> 创建 OAB 虚拟目录之前，请确保用户了解所做的更改。此步骤会中断用户的 OAB 下载进程。


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“脱机通讯簿”条目。

  - 本地 Exchange 服务器必须安装了客户端访问服务器角色。

  - 默认 IIS 网站必须存在（例如 /w3svc/1/root）。

  - 尚不存在名为 OAB 的虚拟目录。

  - 虽然默认情况下会启用基于 Web 的分发并且不需要进一步的配置，但还是建议为 OAB 分发点启用安全套接字层 (SSL)。

  - 不能使用 Exchange 管理中心 (EAC) 执行此过程。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序创建 OAB 虚拟目录

若要创建带有所有默认值的 OAB 虚拟目录，可以运行不带任何参数的 **New-OABVirtualDirectory** cmdlet。使用以下步骤创建具有自定义设置的 OAB 虚拟目录。

> [!NOTE]  
> 创建 OAB 虚拟目录时，推荐启用 SSL。


此示例将在启用 SSL 且具有外部 URL 的 CASServer01 客户端访问服务器上创建 OAB 虚拟目录。

    New-OABVirtualDirectory -Server CASServer01 -RequireSSL $true -ExternalURL "https://www.contoso.com/OAB"

新建 OAB 虚拟目录后，必须编辑使用基于 Web 分发的每个 OAB 的设置，以重新连接到 OAB 虚拟目录。有关详细信息，请参阅[更改脱机通讯簿生成日程安排](change-the-offline-address-book-generation-schedule-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [New-OabVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123735\(v=exchg.150\))。

