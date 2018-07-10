---
title: '针对混合部署配置 Exchange 2013 公用文件夹: Exchange 2013 Help'
TOCTitle: 针对混合部署配置 Exchange 2013 公用文件夹
ms:assetid: b828520f-022c-4fcb-ab68-e1c330e87c33
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn986544(v=EXCHG.150)
ms:contentKeyID: 65330366
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 针对混合部署配置 Exchange 2013 公用文件夹

 


_<strong>适用于：</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_

**摘要：**  允许 Exchange Online 用户访问 Exchange 2013 环境中的本地公用文件夹的说明。

在混合部署中，您的用户可以位于 Exchange Online 中，或内部部署内，或同时位于两者中，并且您的公用文件夹位于 Exchange Online 中或内部部署内。有时，您的联机用户可能需要访问 Exchange Server 2013 内部部署环境中的公用文件夹。同样，Exchange 2013 用户可能需要访问 Office 365 或 Exchange Online 中的公用文件夹。

> [!NOTE]
> 如果您有 Exchange 2010 或 Exchange 2007 公用文件夹，请参阅<a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">针对混合部署配置旧版本地公用文件夹</a>。


本文介绍如何允许 Exchange Online/Office 365 用户访问 Exchange 2013 中的公用文件夹。若要允许本地 Exchange 2013 用户访问 Exchange Online 中的公用文件夹，请参阅[配置 Exchange Online 公用文件夹以实现混合部署](configure-exchange-online-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)。

必须由 Exchange 本地环境中的 MailUser 对象来表示 Exchange Online/Office 365 用户，才能访问 Exchange 2013 公用文件夹。此 MailUser 对象还必须是目标 Exchange 2013 公用文件夹层次结构的本地对象。如果你的 Office 365 用户目前不是由 MailUser 对象进行本地表示，请参阅 Microsoft 知识库文章 3106618[“Exchange Online 用户无法访问旧的本地公用文件夹”](https://go.microsoft.com/fwlink/p/?linkid=699451)来创建匹配的本地实体。

## 在开始之前，您需要知道什么？

1.  这些说明假定您已经使用混合配置向导对您的内部部署和 Exchange Online 环境进行配置和同步，并且假定用于多数用户的自动发现的 DNS 记录可以引用一个内部部署终结点。有关详细信息，请参阅[“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  这些说明假定 Outlook 无处不在已启用，并且在内部部署 Exchange Server 上正常运行。有关如何启用 Outlook 无处不在的信息，请参阅 [Outlook 无处不在](https://technet.microsoft.com/zh-cn/library/bb123741\(v=exchg.150\))。

3.  对 Exchange 与 Office 365 的混合部署实施公用文件夹共存可能需要在导入过程中解决冲突。冲突可能是由于分配给启用邮件的公用文件夹的不可路由电子邮件地址，或者与 Office 365 中的其他用户和组冲突及其他属性所致。

4.  为了能够跨界访问公用文件夹，用户必须将其 Outlook 客户端升级至 2012 年 11 月的 Outlook 公共更新或更高版本。
    
    1.  若要下载 2012 年 11 月发布的适用于 Outlook 2010 的 Outlook 更新程序，请参阅 [Microsoft Outlook 2010 更新 (KB2687623) 32 位版本](https://www.microsoft.com/zh-cn/download/details.aspx?id=35702)。
    
    2.  若要下载 2012 年 11 月发布的适用于 Outlook 2007 的 Outlook 更新程序，请参阅 [Microsoft Office Outlook 2007 更新 (KB2687404)](https://www.microsoft.com/zh-cn/download/details.aspx?id=35718)。

5.  Outlook 2011 for Mac 和 Outlook for Mac for Office 365 不受跨界公用文件夹的支持。用户必须与公用文件夹位于相同位置，才能通过 Outlook 2011 for Mac 或 Outlook for Mac for Office 365 访问这些公用文件夹。此外，使用 Exchange Online 邮箱的用户将无法使用 Outlook Web App 访问本地公用文件夹。
    
    > [!NOTE]
    > Outlook 2016 for Mac 支持跨界部署公用文件夹。如果组织中的客户使用 Outlook 2016 for Mac，请确保他们安装了 2016 年 4 月发布的更新程序。否则，这些用户将无法访问混合拓扑中的公用文件夹。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/mt788631(v=exchg.150)">通过 Outlook 2016 for Mac 访问公用文件夹</a>。


## 步骤 1：下载脚本

1.  从[启用邮件的公用文件夹 - 目录同步脚本](https://www.microsoft.com/en-us/download/details.aspx?id=46381)中下载以下文件：
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  将这些文件保存到将要运行 PowerShell 的本地计算机中。例如，C:\\PFScripts。

## 步骤 2：配置目录同步

目录同步服务不对启用邮件的公用文件夹进行同步。运行以下两个脚本可以对已启用邮件的跨界和 Office 365 公用文件夹进行同步。分配给已启用邮件的公用文件夹的特殊权限将需要在云中重新创建，因为跨界权限在混合部署方案中不受支持。有关详细信息，请参阅 [Exchange Server 2013 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

> [!NOTE]
> 已同步的启用邮件的公用文件夹将显示为邮件联系人对象，用于处理邮件流，并且不会在 EExchange 管理中心 中显示。请参阅 Get-MailPublicFolder 命令。要重新创建云中的 SendAs 权限，请使用 Add-RecipientPermission 命令。


1.  在 Exchange 2013 服务器上，运行以下命令将启用邮件的公用文件夹从内部部署 Active Directory 同步到 O365 中。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    其中 `Credential` 是您的 Office 365 用户名和密码，`CsvSummaryFile` 是您要以 .csv 格式记录同步操作和错误的文件路径。

> [!NOTE]
> 在运行此脚本之前，我们建议您先模拟此脚本将在环境中执行的操作，方法是使用 <code>-WhatIf</code> 参数按照如上所述运行此脚本。<br />
我们还建议您每天都运行此脚本以同步启用邮件的公用文件夹。


## 步骤 3：配置 Exchange Online 用户以访问 Exchange 2013 本地公用文件夹

该程序的最后一步是配置 Exchange Online 组织并允许访问 Exchange 2013 公用文件夹。

允许 Exchange Online 组织访问本地公用文件夹。您将指向所有本地公用文件夹邮箱。

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

> [!NOTE]
> 您必须等待 ActiveDirectory 同步完成才能查看更改。此过程可能需要 3 个小时才能完成。如果您不想等待每隔三小时进行一次定期同步，可以随时强制执行目录同步。有关强制执行目录同步的详细步骤，请参阅<a href="http://technet.microsoft.com/zh-cn/library/jj151771.aspx">强制执行目录同步</a>。


## 我如何知道这有效？

1.  登录到位于 Exchange Online 内的用户的 Outlook，并执行以下公用文件夹测试：
    
      - 查看层次结构。
    
      - 检查权限
    
      - 创建和删除公用文件夹。
    
      - 发布内容到公用文件夹并从公用文件夹删除内容。

