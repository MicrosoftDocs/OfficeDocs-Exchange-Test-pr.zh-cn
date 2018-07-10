---
title: '配置 Exchange Online 公用文件夹以实现混合部署: Exchange 2013 Help'
TOCTitle: 配置 Exchange Online 公用文件夹以实现混合部署
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768737
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 Exchange Online 公用文件夹以实现混合部署

 

_<strong>适用于：</strong>Exchange Server 2013_

_<strong>上一次修改主题：</strong>2016-12-15_


**摘要：**  有关允许本地 Exchange 2013 用户访问 Exchange Online 中的公用文件夹的说明。

在混合部署中，您的用户可以位于 Exchange Online 中，或内部部署内，或同时位于两者中，并且您的公用文件夹位于 Exchange Online 中或内部部署内。有时，您的联机用户可能需要访问 Exchange Server 2013 内部部署环境中的公用文件夹。同样，Exchange 2013 用户可能需要访问 Office 365 或 Exchange Online 中的公用文件夹。

本文介绍了如何允许 Exchange 2013 本地环境中的用户访问 Exchange Online/Office 365 公用文件夹。若要允许 Exchange Online/Office 365 用户访问本地 Exchange 2013 公用文件夹，请参阅[针对混合部署配置 Exchange 2013 公用文件夹](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)。

> [!NOTE]
> 如果您有 Exchange 2010 或 Exchange 2007 公用文件夹，请参阅<a href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">针对混合部署配置旧版本地公用文件夹</a>。


## 在开始之前，您需要知道什么？

1.  这些说明假定您已经使用混合配置向导对您的内部部署和 Exchange Online 环境进行配置和同步，并且假定用于多数用户的自动发现的 DNS 记录可以引用一个内部部署终结点。有关详细信息，请参阅[“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  这些说明假定 Outlook 无处不在已启用，并且在内部部署 Exchange Server 上正常运行。有关如何启用 Outlook 无处不在的信息，请参阅 [Outlook 无处不在](https://technet.microsoft.com/zh-cn/library/bb123741\(v=exchg.150\))。

3.  对 Exchange 与 Office 365 的混合部署实施公用文件夹共存可能需要在导入过程中解决冲突。冲突可能是由于分配给启用邮件的公用文件夹的不可路由电子邮件地址，或者与 Office 365 中的其他用户和组冲突及其他属性所致。

4.  为了能够跨界访问公用文件夹，用户必须将其 Outlook 客户端升级至 2012 年 11 月的 Outlook 公共更新或更高版本。
    
    1.  若要下载 2012 年 11 月发布的适用于 Outlook 2010 的 Outlook 更新程序，请参阅 [Microsoft Outlook 2010 更新 (KB2687623) 32 位版本](https://www.microsoft.com/zh-cn/download/details.aspx?id=35702)。
    
    2.  若要下载 2012 年 11 月发布的适用于 Outlook 2007 的 Outlook 更新程序，请参阅 [Microsoft Office Outlook 2007 更新 (KB2687404)](https://www.microsoft.com/zh-cn/download/details.aspx?id=35718)。

5.  Outlook 2011 for Mac 和 Outlook for Mac for Office 365 不受跨界公用文件夹的支持。用户必须与公用文件夹位于相同位置，才能通过 Outlook 2011 for Mac 或 Outlook for Mac for Office 365 访问这些公用文件夹。此外，使用 Exchange Online 邮箱的用户将无法使用 Outlook Web App 访问内部部署公用文件夹。
    
    > [!NOTE]
    > Outlook 2016 for Mac 支持跨界部署公用文件夹。如果组织中的客户使用 Outlook 2016 for Mac，请确保他们安装了 2016 年 4 月发布的更新程序。否则，这些用户将无法访问共存或混合拓扑中的公用文件夹。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/mt788631(v=exchg.150)">通过 Outlook 2016 for Mac 访问公用文件夹</a>。


## 步骤 1：下载脚本

1.  从 [Mail-enabled Public Folders - directory sync from EXO to On-prem script](https://go.microsoft.com/fwlink/p/?linkid=797795)（启用邮件的公用文件夹 - 将目录从 EXO 同步到本地的脚本）下载以下文件。
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  将这些文件保存到将要运行 PowerShell 的本地计算机中。例如，C:\\PFScripts。

## 步骤 2：配置目录同步

运行脚本 `Sync-MailPublicFoldersCloudToOnprem.ps1` 会在 Exchange Online 和 Exchange 2013 本地环境之间同步启用邮件的公用文件夹。必须在云中重新创建分配给启用邮件的公用文件夹的特殊权限，因为混合部署方案不支持跨界部署权限。有关详细信息，请参阅 [Exchange Server 2013 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

> [!NOTE]
> 已同步的启用邮件的公用文件夹将显示为邮件联系人对象，用于处理邮件流，并且不会在 Exchange 管理员中心中显示。请参阅 Get-MailPublicFolder 命令。要重新创建云中的 SendAs 权限，请使用 Add-RecipientPermission 命令。


1.  在 Exchange 2013 服务器上，运行以下命令，将启用邮件的公用文件夹从 Exchange Online/Office 365 同步到本地 Active Directory。
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    其中，`Credential` 是你的 Office 365 用户名和密码。

> [!NOTE]
> 我们建议每天运行一次这段脚本，以同步启用邮件的公用文件夹。


## 第 3 步：将本地用户配置为访问 Exchange Online 公用文件夹

此过程的最后一步是将 Exchange 2013 本地组织配置为允许访问 Exchange Online 公用文件夹。

运行脚本 `Import-PublicFolderMailboxes.ps1` 会以启用邮件的用户身份将公用文件夹邮箱对象从云中导入本地环境。此脚本还会将导入的对象配置为远程公用文件夹邮箱。

1.  在 Exchange 2013 服务器上，运行以下命令，将公用文件夹邮箱对象从云中导入本地 Active Directory。
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    其中，`Credential` 是你的 Office 365 用户名和密码。
    
    > [!NOTE]
    > 我们建议每天运行一次这段脚本，以导入公用文件夹邮箱对象，因为只要公用文件夹邮箱达到阈值容量，就会自动拆分为多个新邮箱。因此，你总是要确保从云中导入的是最新公用文件夹邮箱。


2.  允许 Exchange 2013 本地组织访问 Exchange Online 公用文件夹。
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

> [!NOTE]
> 您必须等待 ActiveDirectory 同步完成才能查看更改。此过程可能需要 3 个小时才能完成。如果您不想等待每隔三小时进行一次定期同步，可以随时强制执行目录同步。有关强制执行目录同步的详细步骤，请参阅<a href="http://technet.microsoft.com/zh-cn/library/jj151771.aspx">强制执行目录同步</a>。


## 我如何知道这有效？

1.  登录到位于 Exchange Online 内的用户的 Outlook，并执行以下公用文件夹测试：
    
      - 查看层次结构。
    
      - 检查权限
    
      - 创建和删除公用文件夹。
    
      - 发布内容到公用文件夹并从公用文件夹删除内容。

