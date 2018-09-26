---
title: '在 Exchange 组织之间配置联合共享: Exchange 2013 Help'
TOCTitle: 在 Exchange 组织之间配置联合共享
ms:assetid: 94e31454-b027-4757-b52f-d3c2ead6d916
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657473(v=EXCHG.150)
ms:contentKeyID: 50491056
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Exchange 组织之间配置联合共享

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

使用联合共享，您的内部部署 Exchange 组织中的用户可以与同样配置了联合共享的其他 Exchange 组织中的收件人共享忙/闲日历信息。忙/闲共享可以在两个运行 Exchange 2013 的组织之间以及采用混合 Exchange 部署的组织之间实现。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

此主题概括介绍了要在不同类型的以下常见 Exchange 部署间启用忙/闲共享所必须满足的要求和完成的配置步骤：

  - 两个 Exchange 2013 组织。

  - 一个 Exchange 2013 组织以及一个 Exchange 2010 SP2 组织。

  - 一个 Exchange 2007 组织（或混合的 Exchange 2007 和 Exchange 2010 SP2 组织）以及一个 Exchange 2013 组织。

  - 一个 Exchange 2003 组织（或混合的 Exchange 2003 和 Exchange 2010 SP2 组织）以及一个 Exchange 2013 组织。

关于混合共享的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：2 小时。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 在执行本主题中的步骤之前，请确保您了解 Exchange 组织间共享忙/闲信息相关的限制。有关详细信息，请参阅[Limitations of free/busy sharing](sharing-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 配置 Exchange 2013 组织之间的忙/闲共享

同时为两个组织完成[配置联合共享](configure-federated-sharing-exchange-2013-help.md)中的步骤。

## 配置 Exchange 2013 和 Exchange 2010 SP2 组织之间的忙/闲共享

  - 配置 Exchange 2013 组织的联合共享。完成 [配置联合共享](configure-federated-sharing-exchange-2013-help.md) 中的步骤。

  - 为 Exchange 2010 SP2 组织配置联合委派（联合共享的前称）。完成[配置联合委派](https://go.microsoft.com/fwlink/p/?linkid=268410)中的步骤。

## 配置 Exchange 2013 和 Exchange 2007 组织之间的忙/闲共享

  - 配置 Exchange 2013 组织的联合共享。完成 [配置联合共享](configure-federated-sharing-exchange-2013-help.md) 中的步骤。

  - 完成 Exchange 2007 组织中的下列步骤：
    
    1.  **添加 Exchange 2010 SP2 服务器**
        
        具有客户端访问服务器角色的 Exchange 2010 SP2 服务器必须安装在 Exchange 2007 组织中。如果当前存在 Exchange 2010 服务器，这些服务器还应更新到 Exchange 2010 SP2。有关在 Exchange 2007 组织中安装 Exchange 2010 的信息，请参阅 [Exchange 2007 - 规划升级和共存路线图](https://go.microsoft.com/fwlink/p/?linkid=268411)。
    
    2.  **配置联合委派**
        
        配置 Exchange 2007 组织的联合代理。在 Exchange 2007 组织中的 Exchange 2010 SP2 服务器上，完成[配置联合代理](https://go.microsoft.com/fwlink/p/?linkid=268410)中的步骤。
    
    3.  **配置 Active Directory 同步**
        
        必须为需要在组织之间共享忙/闲信息的所有用户配置 Active Directory 同步。可以手动配置 Active Directory 同步，也可以使用自动的 Active Directory 同步服务。若要配置 Active Directory 同步，请参见下面的步骤：
        
          - **先决条件**   确保您的组织满足安装 Active Directory 同步的先决条件。
            
            要了解更多信息，请参阅[为 Active Directory 同步做准备](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **计划**   了解 Microsoft Online Services 目录同步工具和安装路线图。
            
            要了解更多信息，请参阅 [Active Directory 同步：路线图](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **安装和配置**   配置您的内部部署组织与 Office 365 租户服务组织之间的 Active Directory 同步。
            
            要了解更多信息，请参阅[安装和升级 Microsoft Online Services 目录同步工具](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **创建一个可用性地址空间**
        
        为远程 Exchange 2013 组织创建一个可用性地址空间，用于将 Exchange 2007 邮箱用户的可用性请求发往 Exchange 2007 组织中的 Exchange 2010 SP2 客户端访问服务器。通过此设置，Exchange 2007 用户对远程 Exchange 2013 组织中用户的用户可用性请求可以通过 Exchange 2007 组织中的 Exchange 2010 客户端访问服务器进行代理。Exchange 2007 组织中的 Exchange 2010 客户端访问服务器使用联合信任和组织关系将可用性请求发送给远程 Exchange 2013 组织林可用性终结点。
        
        若要配置可用性地址空间，请在 Exchange 2007 组织中的 Exchange 2010 客户端访问服务器的 Exchange 命令行管理程序中运行以下命令：
        
          ```powershell
            Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl https://<Exchange 2010 CAS server name>/ews/exchange.asmx -ForestName <SMTP domain of the remote Exchange organization> -UseServiceAccount $True
          ```

        有关语法和参数的详细信息，请参阅 [Add-AvailabilityAddressSpace](https://go.microsoft.com/fwlink/p/?linkid=268413)

## 配置 Exchange 2013 组织与 Exchange 2003 组织之间的忙/闲共享

  - 配置 Exchange 2013 组织的联合共享。完成 [配置联合共享](configure-federated-sharing-exchange-2013-help.md) 中的步骤。

  - 完成 Exchange 2003 组织中的下列步骤：
    
    1.  **添加 Exchange 2010 SP2 服务器**。
        
        具有客户端访问服务器角色的 Exchange 2010 SP2 服务器必须安装在 Exchange 2003 组织中。如果当前存在 Exchange 2010 服务器，这些服务器还应更新到 Exchange 2010 SP2。有关在 Exchange 2003 组织中安装 Exchange 2010 的信息，请参阅 [Exchange 2003 - 规划升级和共存路线图](https://go.microsoft.com/fwlink/?linkid=268414)。
        
        > [!WARNING]  
        > 为确保 Exchange 2013 和 Exchange 2003 组织之间的忙/闲共享正常工作，<strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 公用文件夹必须位于公用文件夹层次结构中。仅当在 Exchange 2010 安装期间选择创建公用文件夹作为配置 Outlook 2003 支持的客户端设置选项时，才会在 Exchange 2003 组织的 Exchange 2010 邮箱服务器上自动创建此文件夹。此外，仅当 Exchange 2010 邮箱服务器是组织中安装的第一个邮箱服务器时，才会在安装过程中提供此选项。如果未在安装过程中创建 <strong>OU=EXTERNAL (FYDIBOHF25SPDLT)</strong> 公用文件夹，则必须手动创建该文件夹。有关如何创建此公用文件夹的详细信息，请参阅<a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=2555008">在 Microsoft Office 365 企业版环境中使用 Exchange 联合身份验证时如何解决忙/闲问题</a>。
    
    2.  **配置联合委派**。
        
        配置 Exchange 2003 组织的联合代理。在 Exchange 2003 组织中的 Exchange 2010 SP2 服务器上，完成[配置联合代理](https://go.microsoft.com/fwlink/p/?linkid=268410)中的步骤。
    
    3.  **配置 Active Directory 同步**。
        
        必须为需要在组织之间共享忙/闲信息的所有用户配置 Active Directory 同步。可以手动配置 Active Directory 同步，也可以使用自动的 Active Directory 同步服务。若要了解有关 Active Directory 同步的详细信息，请参阅 [Forefront 身份管理](https://go.microsoft.com/fwlink/?linkid=294645)。
        
          - **先决条件**   确保您的组织满足安装 Active Directory 同步的先决条件。
            
            要了解更多信息，请参阅[为 Active Directory 同步做准备](https://go.microsoft.com/fwlink/p/?linkid=247302)
        
          - **计划**   了解 Microsoft Online Services 目录同步工具和安装路线图。
            
            要了解更多信息，请参阅 [Active Directory 同步：路线图](http://go.microsoft.com/fwlink/p/?linkid=203007)
        
          - **安装和配置**   配置您的内部部署组织与 Office 365 租户服务组织之间的 Active Directory 同步。
            
            要了解更多信息，请参阅[安装和升级 Microsoft Online Services 目录同步工具](https://go.microsoft.com/fwlink/p/?linkid=247303)
    
    4.  **配置 Exchange 2003 组织中的忙/闲共享公用文件夹。**
        
        在 Exchange 2003 服务器上完成下列步骤：
        
          - 在 Exchange 系统管理器的控制台树中，导航到“管理组”\>“第一个管理组”\>“服务器”。
        
          - 选择您的 Exchange 2003 服务器，然后导航到“第一个存储组”\>“公用文件夹存储”\>“公用文件夹”\>“Schedule+ 忙/闲”。
        
          - 在操作窗格中，为“第一个管理组”选择 **OU=EXTERNAL (FYDIBOHF25SPDLT)**。
        
          - 右键单击 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 文件夹，然后单击“属性”。
        
          - 在“OU=EXTERNAL (FYDIBOHF25SPDLT) 属性”中，选择“复制”选项卡。
        
          - 若要将 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 文件夹复制到 Exchange 2010 客户端访问/邮箱服务器，请单击“添加”。
        
          - 在“选择公用文件夹存储”中，选择 Exchange 2010 客户端访问/邮箱服务器的“公用文件夹数据库”，然后单击“确定”。
            
            > [!NOTE]  
            > 默认情况下，Exchange 使用在公用文件夹数据库中设置的复制日程安排。
        
          - 单击“确定”关闭“OU=EXTERNAL (FYDIBOHF25SPDLT) 属性”并保存所做的更改。
        
          - 对 **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 文件夹完成上述相同步骤。
            
            > [!WARNING]  
            > 根据公用文件夹的大小，可能需要数小时才能完成该复制过程。
        
          - 将 **OU=EXTERNAL (FYDIBOHF25SPDLT)** 和 **OU=Exchange Administrative Group (FYDIBOHF23SPDLT)** 公用文件夹复制到 Exchange 2010 客户端访问/邮箱服务器后，必须在 Exchange 2003 服务器上删除这些公用文件夹的副本。
    
    5.  **修改 LegacyExchangeDN 参数**
        
        在引用远程 Exchange 2013 组织的 Exchange 2003 组织中，修改所有已启用邮件的对象的 *LegacyExchangeDN* 参数。将已启用邮件的对象的现有组织单位 (OU) 值修改为 **External (FYDIBOHF25SPDLT)**。例如，**LegacyExchangeDN=/o=First Organization/ou=External (FYDIBOHF25SPDLT)/cn=Recipients/cn=User Name**。
        
        要在 Exchange 2003 组织中修改启用邮箱的对象，可以使用 [Active Directory 服务界面编辑器（ADSI 编辑）工具](http://go.microsoft.com/fwlink/?linkid=294644)或 [Microsoft Exchange Server LegacyDN 实用程序](https://go.microsoft.com/fwlink/?linkid=294643)。

