---
title: '将 Exchange 2013 升级到最新累积更新或 Service Pack: Exchange 2013 Help'
TOCTitle: 将 Exchange 2013 升级到最新累积更新或 Service Pack
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52061534
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将 Exchange 2013 升级到最新累积更新或 Service Pack

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2015-09-04_

如果安装了 Microsoft Exchange Server 2013，您可以将其升级到最新的 Exchange 2013 累积更新或 Service Pack。可以使用 Exchange 2013 设置向导升级当前版本的 Exchange 2013。有关最新 Exchange 2013 累积更新或 Service Pack 的详细信息，请参阅 [Exchange 2013 更新](updates-for-exchange-2013-exchange-2013-help.md)。有关 Exchange 2013 的详细信息，请参阅[Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

> [!WARNING]  
> 将 Exchange 2013 升级到较新的累积更新或 Service Pack 后，不能卸载新版本以还原到之前的版本。如果卸载新版本，将从服务器中删除 Exchange。


## 在开始之前，您需要知道什么？

  - 估计完成时间：60 分钟

  - 确保在安装 Exchange 2013 之前阅读发行说明。有关详细信息，请参阅[Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 确保您计划在其中安装累积更新或 Service Pack 的所有服务器都满足系统要求和先决条件。有关详细信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md) 和 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。
    
    > [!WARNING]  
    > 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。


  - 安装累积更新或 Service Pack 后，必须重新启动计算机，以便能够对注册表和操作系统做出更改。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 安装 Exchange 2013 累积更新或 Service Pack

您可以使用设置向导或通过无人值守模式为 Exchange 2013 安装累积更新或 Service Pack。有关具体说明，请参阅下列主题：

  - [使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [使用无人参与的模式安装 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

如果您安装了 Service Pack 或累积更新的计算机是某个数据库可用性组 (DAG) 的成员，请按照[管理数据库可用性组](managing-database-availability-groups-exchange-2013-help.md)主题的[为 DAG 成员执行维护](managing-database-availability-groups-exchange-2013-help.md)部分中的步骤操作。

