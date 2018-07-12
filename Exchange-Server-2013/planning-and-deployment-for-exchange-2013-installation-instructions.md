---
title: '规划和部署: Exchange 2013 Help'
TOCTitle: 规划和部署
ms:assetid: 692c59e3-f0b0-4cef-a66e-751aa740abae
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998636(v=EXCHG.150)
ms:contentKeyID: 50490750
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 规划和部署

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

是否需要获取 Exchange 安装指导？本文提供了有关规划 Microsoft Exchange Server 2013 开发的指导，以及你在开发过程中需要查看的文章链接。

以下各节包含有关规划然后部署 Microsoft Exchange Server 2013 的信息的链接。

> [!IMPORTANT]  
> 确保在开始部署之前阅读 <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 发行说明</a>主题。发行说明包含有关在部署期间和之后可能遇到的问题的重要信息。


**目录**

规划 Exchange 2013

部署 Exchange 2013 的安装

了解 Exchange 2013 安装

详细信息

## 规划 Exchange 2013

使用以下链接可访问有助于您规划组织内 Exchange Server 2013 部署的信息。

> [!IMPORTANT]  
> 请参阅本主题后面部分中有关在测试环境中安装 Exchange 2013 的建立测试环境。


  - [邮箱和客户端访问服务器](mailbox-and-client-access-servers-exchange-2013-help.md)  
    了解 Exchange 2013 中包含的邮箱和客户端访问服务器角色。

<!-- end list -->

  - [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)  
    了解在安装 Exchange 2013 之前需要在组织中满足的系统要求。

<!-- end list -->

  - [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)  
    了解为执行 Exchange 2013 的成功安装而需要安装的 Windows Server 2008 R2 Service Pack 1 (SP1) 或 Windows Server 2012 功能及其他软件。

<!-- end list -->

  - [Exchange Server 部署助理](exchange-server-deployment-assistant-exchange-2013-help.md)  
    使用此工具可生成一个自定义检查表，用于规划、安装或升级到 Exchange 2013。指南适用于多个场景，包括内部部署、混合部署或云部署。

<!-- end list -->

  - [Active Directory](active-directory-exchange-2013-help.md)  
    阅读本主题可了解 Exchange 2013 如何使用 Active Directory 以及 Active Directory 部署如何影响 Exchange 部署。

<!-- end list -->

  - [反恶意软件保护](anti-malware-protection-exchange-2013-help.md)  
    阅读本主题可了解 Exchange 2013 的反恶意软件保护选项。

<!-- end list -->

  - [Exchange Server 混合部署](https://technet.microsoft.com/zh-cn/library/jj200581\(v=exchg.150\))  
    阅读本主题可帮助规划包含 Microsoft Office 365 和内部部署 Exchange 2013 组织的混合部署。

<!-- end list -->

  - [对高可用性和站点恢复的规划](planning-for-high-availability-and-site-resilience-exchange-2013-help.md)  
    阅读本主题可帮助您规划实现高可用性和业务连续性要求。

<!-- end list -->

  - [与 SharePoint 和 Lync 的集成](integration-with-sharepoint-and-lync-exchange-2013-help.md)  
    阅读本主题可了解集成 Exchange 2013、Microsoft SharePoint 2013 和 Microsoft Lync 2013 以启用跨产品存档、保留和电子数据展示；站点邮箱；身份验证；Lync 状态等的相关信息。

<!-- end list -->

  - [统一消息规划](planning-for-unified-messaging-exchange-2013-help.md)  
    阅读本主题可了解更多有关规划 Exchange 2013 统一消息的信息。

<!-- end list -->

  - [Exchange 2013 存储配置选项](exchange-2013-storage-configuration-options-exchange-2013-help.md)  
    阅读本主题可了解 Exchange 2013 邮箱服务器角色支持的存储体系结构、磁盘类型和存储配置。

<!-- end list -->

  - [Exchange 2013 虚拟化](exchange-2013-virtualization-exchange-2013-help.md)  
    阅读本主题可了解有关如何在虚拟化环境中部署 Exchange 2013 的详细信息。

<!-- end list -->

  - [Exchange 2013 中的多租户](multi-tenancy-in-exchange-2013-exchange-2013-help.md)  
    阅读本主题可了解如何配置 Exchange 2013 以对通常情况下不共享电子邮件、数据、用户、全局地址列表 (GAL) 或其他常用 Exchange 对象的多个分散组织或业务单元进行托管的详细信息。

<!-- end list -->

  - [Exchange Development Technologies](https://go.microsoft.com/fwlink/p/?linkid=268448)（Exchange 开发技术）  
    本主题包含有关向使用 Exchange 2013 的应用程序提供的应用程序编程接口 (API) 的重要信息。

## 建立测试环境

首次安装 Exchange 2013 之前，建议在隔离的测试环境中安装。此方法可降低最终用户发生故障的风险以及对生产环境的负面影响。

在部署到生产环境中之前，测试环境将充当新 Exchange 2013 设计的“概念证明”，并可以推进或回滚任何实现。采用专门的测试环境进行验证和测试，可针对未来的生产环境进行安装前的检查。通过首先在测试环境中安装，我们相信贵组织更加能够在完全生产实施中获得成功。

对于很多组织，由于需要复制生产环境，因此建立测试实验室的成本可能很高。若要降低原型实验室的相关硬件成本，建议通过 Windows Server 2008 R2 或 Windows Server 2012 Hyper-V 技术采用虚拟化。Hyper-V 实现了服务器虚拟化，从而使多个虚拟操作系统可运行于一台物理计算机上。

如需了解 Hyper-V 的更多详情，请参阅 [Server Virtualization](https://go.microsoft.com/fwlink/p/?linkid=117704)（服务器虚拟化）。有关 Microsoft 支持 Exchange 2013 在硬件虚拟化软件上进行生产的信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)中的“硬件虚拟化”。

## 部署 Exchange 2013 的安装

部署阶段是指将 Exchange 2013 安装到组织中的阶段。在开始部署阶段之前，应当先规划 Exchange 组织。有关详细信息，请参阅本主题前面的规划 Exchange 2013一节。

通过以下链接可获取有助于部署 Exchange 2013 的信息。

  - [准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)  
    了解为 Exchange 2013 准备 Active Directory 林而需要执行的步骤以及 Exchange 对林进行的更改。

<!-- end list -->

  - [使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)  
    按照本主题中的步骤使用 Exchange 2013 安装向导将 Exchange 2013 安装到新的 Exchange 组织中。

<!-- end list -->

  - [使用无人参与的模式安装 Exchange 2013](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)  
    按照本主题中的步骤使用 Exchange 2013 无人参与安装将 Exchange 2013 安装到新的 Exchange 组织中。

<!-- end list -->

  - [使用安装向导安装 Exchange 2013 边缘传输角色](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)  
    按照本主题中的步骤使用 Exchange 2013 安装向导将 Exchange 2013 边缘传输角色安装到外围网络中。

<!-- end list -->

  - [将 Exchange 2013 升级到最新累积更新或 Service Pack](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md)  
    按照本主题中的步骤对组织中的 Exchange 2013 服务器应用最新累积更新或 Service Pack。

<!-- end list -->

  - [从 Exchange 2010 升级至 Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md)  
    按照本主题中的步骤将 Exchange 2013 安装到现有的 Exchange 2010 组织中。

<!-- end list -->

  - [从 Exchange 2007 升级到 Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)  
    按照本主题中的步骤将 Exchange 2013 安装到现有的 Exchange 2007 组织中。

<!-- end list -->

  - [部署 Exchange 2013 多林拓扑](deploy-multiple-forest-topologies-for-exchange-2013-exchange-2013-help.md)  
    阅读本主题，以获取有助于在包含多个 Active Directory 林的组织中部署 Exchange 2013 的信息。

<!-- end list -->

  - [部署语音邮件和 UM](deploying-voice-mail-and-um-exchange-2013-help.md)  
    阅读本主题以获取帮助您了解部署 Exchange 2013 统一消息（无论是新的部署还是升级）的信息。

<!-- end list -->

  - [混合部署过程](https://technet.microsoft.com/zh-cn/library/jj200788\(v=exchg.150\))  
    阅读本主题以获取帮助您在现有混合部署中部署 Exchange 2013 的信息。

<!-- end list -->

  - [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md)  
    了解用于完成 Exchange 2013 安装的安装后任务。

## 了解 Exchange 2013 安装

您可以使用 Exchange 2013 安装程序的不同类型和模式来安装并维护各种版次和版本的 Exchange 2013。

## Exchange 版次和版本

Exchange 2013 有两种服务器版本：Standard Edition 和 Enterprise Edition。这是由产品密钥定义的两种授权版本。有关详细信息，请参阅 [Exchange Server Licensing](https://go.microsoft.com/fwlink/p/?linkid=237292)（Exchange Server 授权）。

## Exchange 安装程序的类型

有下列 Exchange 2013 安装程序的选项供您选择：

  - **Exchange 安装程序 UI**   在不使用任何命令行开关的情况下运行 Setup.exe 可提供交互式体验，由 Exchange 2013 安装向导提供指导。

  - **Exchange 无人参与安装** 在使用命令行开关的情况下运行 Setup.exe 使您可以从交互式命令行或通过脚本来安装 Exchange。

可以通过 Exchange 2013 DVD 或下载的源文件获得 Setup.exe。

## Exchange 安装程序的模式

Exchange 2013 的安装程序包括以下几种安装模式：

  - **安装** 当您正在安装新的服务器角色，或将服务器角色添加到现有的安装（维护模式）时，使用此模式。可以通过 Exchange 安装向导和无人值守安装使用此模式。

  - **卸载**   当您从计算机删除 Exchange 安装时，使用此模式。可以通过 Exchange 安装向导和无人值守安装使用此模式。

  - **更新**   当您已安装了 Exchange 并要安装累积更新或 Service Pack 时，选择使用此模式。可以通过 Exchange 安装向导和无人值守安装使用此模式。
    
    > [!NOTE]  
    > Exchange 2013 不支持从以前版本的 Exchange 进行就地升级。此模式仅用于安装累积更新或 Service Pack。


  - **RecoverServer**   在服务器发生灾难性故障，您需要恢复数据时使用此模式。必须使用与出现故障的服务器相同的完全限定域名 (FQDN) 来安装服务器，然后使用 **/m:RecoverServer** 开关运行安装程序。不要指定要还原的角色。安装程序在 Active Directory 中检测 Exchange Server 对象，并自动安装相应的文件和配置。恢复服务器后，可以还原数据库并重新配置其他所有设置。若要在 **RecoverServer** 模式下运行，则服务器上不能安装 Exchange。Exchange 服务器对象必须位于 Active Directory 中。只能在无人值守安装过程中使用此模式。

> [!NOTE]  
> 您必须完成一种模式的安装后才能使用另一种模式。


## 详细信息

[Exchange 2013 中的 IPv6 支持](ipv6-support-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 中的 Exchange 管理中心](exchange-admin-center-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013 语言支持](exchange-2013-language-support-exchange-2013-help.md)

[Exchange 2013 准备情况检查](exchange-2013-readiness-checks-exchange-2013-help.md)

