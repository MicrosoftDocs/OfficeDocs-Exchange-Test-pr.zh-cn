---
title: '针对混合部署配置旧版本地公用文件夹: Exchange Online Help'
TOCTitle: 针对混合部署配置旧版本地公用文件夹
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54913580
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 针对混合部署配置旧版本地公用文件夹

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2018-05-22_


**摘要：**  使用本文中的步骤同步 Office 365 与 Exchange 2007 本地部署或 Exchange 2010 本地部署之间的公用文件夹。

在混合部署中，您的用户可以位于 Exchange Online 中或本地内，或同时位于两者中，并且您的公用文件夹位于 Exchange Online 中或本地内。公用文件夹只能驻留在一个位置，因此您必须决定是将其放在 Exchange Online 中还是本地内。他们无法同时位于两者中。目录同步服务可以将公用文件夹邮箱同步至 Exchange Online 上。但是，已启用邮件的公用文件夹无法跨界同步。

本主题介绍在您的用户位于 Office 365 中且 Exchange 2010 SP3 或 Exchange 2007 SP3 RU10 公用文件夹位于本地时，如何对已启用邮件的公用文件夹进行同步。但是，不是由 MailUser 本地对象代表的 Office 365 用户（对目标公用文件夹层次结构是本地的）不能访问旧版或 Exchange 2013 本地公用文件夹。

> [!NOTE]  
> 本主题将 Exchange 2010 SP3 和 Exchange 2007 SP3 RU10 服务器称为<em>旧版 Exchange 服务器</em>。


您可以使用下列脚本同步已启用邮件的公用文件夹，这些脚本由在内部部署环境内运行的 Windows 任务启动。

1.  `Sync-MailPublicFolders.ps1`   此脚本在您的本地 Exchange 本地部署和 Office 365 之间同步已启用邮件的公用文件夹对象。该脚本将本地 Exchange 本地部署用作主机来确定需要应用于 O365 的更改。该脚本将基于本地 Exchange 部署中存在的内容创建、更新或删除 O365 Active Directory 中已启用邮件的公用文件夹对象。

2.  `SyncMailPublicFolders.strings.psd1`   这是由上述同步脚本使用的支持文件，并且应当将其复制到与上述脚本相同的位置。

当您完成此过程时，您的本地和 Office 365 用户将可以访问相同的本地公用文件夹基础结构。

## Exchange 的哪个混合版本可以和公用文件夹一起使用？

下表介绍了用户邮箱和受支持的公用文件夹的版本和位置组合。“混合不适用”仍然是一个受支持的方案，但是由于公用文件夹和用户驻留在相同位置，因此它不再被认为是一个混合方案。


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>内部部署 Exchange 2007 或 Exchange 2010 用户邮箱</th>
<th>内部部署 Exchange 2013 用户邮箱</th>
<th>Exchange Online 用户邮箱</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>内部部署 Exchange 2007 或 Exchange 2010 公用文件夹</p></td>
<td><p>混合不适用</p></td>
<td><p>混合不适用</p></td>
<td><p>支持</p></td>
</tr>
<tr class="even">
<td><p>内部部署 Exchange 2013 公用文件夹</p></td>
<td><p>混合不适用</p></td>
<td><p>混合不适用</p></td>
<td><p>支持</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Online 公用文件夹</p></td>
<td><p>不支持</p></td>
<td><p>支持</p></td>
<td><p>混合不适用</p></td>
</tr>
</tbody>
</table>


不支持包含 Exchange 2003 公用文件夹的混合配制。如果您的组织运行的是 Exchange 2003，则必须将所有公用文件夹数据库和副本移动至 Exchange 2007 SP3 RU10 或更高版本。Exchange 2003 中不能保留公用文件夹副本。

> [!NOTE]
> Outlook 2016 不支持访问 Exchange 2007 旧版公用文件夹。如果有使用 Outlook 2016 的用户，则需要将公用文件夹移动到 Exchange 的最新版本。可在<a href="https://go.microsoft.com/fwlink/p/?linkid=849053">本文</a>找到有关 Outlook 2016 和 Office 2016 与 Exchange 2007 及更早版本兼容性的详细信息。


## 步骤 1：在开始之前，您需要知道什么？

1.  这些说明假定您已经使用混合配置向导对您的内部部署和 Exchange Online 环境进行配置和同步，并且假定用于多数用户的自动发现的 DNS 记录可以引用一个内部部署终结点。有关详细信息，请参阅[“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md)。

2.  这些说明假定 Outlook 无处不在 已启用，并且在内部部署旧版 Exchange Server 上正常运行。有关如何启用 Outlook 无处不在 的信息，请参阅 [Outlook 无处不在](https://technet.microsoft.com/zh-cn/library/bb123741\(v=exchg.150\))。

3.  对 Exchange 与 Office 365 的混合部署实施旧公用文件夹共存可能需要在导入过程中解决冲突。冲突可能是由于分配给启用邮件的公用文件夹的不可路由电子邮件地址，或者与 Office 365 中的其他用户和组冲突及其他属性所致。

4.  这些说明假定您的 Exchange Online 组织已升级至支持公用文件夹的版本。

5.  在 Exchange Online 中，您必须是“组织管理”角色组的成员。该角色组与订阅 Exchange Online 时分配给您的权限不同。有关如何启用“组织管理”角色组的详细信息，请参阅[管理角色组](https://technet.microsoft.com/zh-cn/library/jj657480\(v=exchg.150\))。

6.  在 Exchange 2010 中，你必须是“组织管理”或“服务器管理”RBAC 角色组的成员。有关详细信息，请参阅[向角色组添加成员](https://go.microsoft.com/fwlink/?linkid=299212)

7.  在 Exchange 2007 中，必须分配有 Exchange 组织管理员角色或 Exchange Server 管理员角色。此外，还必须分配有公用文件夹管理员角色和目标服务器的本地管理员组。有关详细信息，请参阅[如何向管理员角色添加用户或组](https://go.microsoft.com/fwlink/p/?linkid=81779)

8.  如果你的 Exchange Server 2007 正在 Windows Server 2008 x64 上运行，那么你必须将其升级到[适用于 Windows Server 2008 x64 Edition 的 Windows PowerShell 2.0 和 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)。如果你的 Exchange Server 2007 正在 Windows Server 2003 x64 上运行，那么你必须将其升级到 Windows PowerShell 2.0。有关详细信息，请参阅[适用于 Windows Server 2003 x64 Edition 的更新](https://www.microsoft.com/zh-cn/download/details.aspx?id=10512)。

9.  为了能够跨界访问公用文件夹，用户必须将其 Outlook 客户端升级至 2012 年 11 月的 Outlook 公共更新或更高版本。
    
    1.  若要下载 2012 年 11 月发布的适用于 Outlook 2010 的 Outlook 更新程序，请参阅 [Microsoft Outlook 2010 更新 (KB2687623) 32 位版本](https://www.microsoft.com/zh-cn/download/details.aspx?id=35702)。
    
    2.  若要下载 2012 年 11 月发布的适用于 Outlook 2007 的 Outlook 更新程序，请参阅 [Microsoft Office Outlook 2007 更新 (KB2687404)](https://www.microsoft.com/zh-cn/download/details.aspx?id=35718)。

10. 不支持使用 Outlook 2016 for Mac（及早期版本）和适用于 Office 365 的 Outlook for Mac 访问跨界部署旧式公用文件夹。用户必须转到公用文件夹所在的位置，才能使用 Outlook for Mac 或适用于 Office 365 的 Outlook for Mac 访问这些公用文件夹。此外，使用 Exchange Online 邮箱的用户将无法使用 Outlook Web App 访问本地公用文件夹。

11. 按照本文中的说明配置混合部署的本地公用文件夹后，除非采取其他步骤，否则组织外部的用户将无法将邮件发送到本地公用文件夹。可以将公用文件夹的接受域设置为内部中继（有关详细信息，请参阅[在 Exchange Online 中管理接受域](https://technet.microsoft.com/zh-cn/library/jj945194\(v=exchg.150\))），也可以禁用基于目录的边缘锁定 (DBEB)，如[使用基于目录的边缘阻止拒绝发送给无效收件人的邮件](https://technet.microsoft.com/zh-cn/library/dn600322\(v=exchg.150\))中所述。

## 步骤 2：使远程公用文件夹可见

1.  如果你的公用文件夹位于 Exchange 2010 或更高版本的服务器上，则需要在所有拥有公用文件夹数据库的邮箱服务器上安装客户端访问服务器角色。这样便可运行 Microsoft Exchange RpcClientAccess 服务，从而使所有客户端都可以对公用文件夹进行访问。Exchange 2007 公用文件夹服务器不需要客户端访问角色，此步骤并非必需步骤。有关详细信息，请参阅[安装 Exchange Server 2010](https://technet.microsoft.com/zh-cn/library/bb124778\(v=exchg.141\).aspx)。对于 Exchange 2007 公用文件夹不需要执行此步骤。
    
    > [!NOTE]  
	> 客户端负载平衡不需要包含此服务器。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/ff625247(v=exchg.141).aspx">了解 Exchange 2010 中的负载平衡</a>。
    

2.  在每个公用文件夹服务器上创建一个空的邮箱数据库。
    
    对于 Exchange 2010，运行以下命令。此命令会将邮箱数据库从邮箱配置负载平衡器中排除。这样可以阻止新建邮箱被自动添加至该数据库。
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    对于 Exchange 2007，运行以下命令：
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    
    > [!NOTE]    
	> 我们建议您只将在步骤 3 中创建的代理邮箱添加至此数据库。不应在此邮箱数据库中创建任何其他邮箱。
    

3.  在新建邮箱数据库内创建一个代理邮箱，并在通讯簿中将其隐藏。该邮箱的 SMTP 会由自动发现返回为 *DefaultPublicFolderMailbox* SMTP，因此通过解析此 SMTP，客户端可以进入旧版 Exchange 服务器以访问公用文件夹。
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  对于 Exchange 2010，启用自动发现以返回代理公用文件夹邮箱。此步骤对于 Exchange 2007 并非必需步骤。
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  对组织中的每个公用文件夹服务器重复执行前面的步骤。

## 步骤 3：下载脚本

1.  从[启用邮件的公用文件夹 - 目录同步脚本](https://www.microsoft.com/en-us/download/details.aspx?id=46381)中下载以下文件：
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  将这些文件保存到将要运行 PowerShell 的本地计算机中。例如，C:\\PFScripts。

## 步骤 4：配置目录同步

目录同步服务不对启用邮件的公用文件夹进行同步。运行以下两个脚本可以对已启用邮件的跨界公用文件夹进行同步。分配给已启用邮件的公用文件夹的特殊权限将需要在云中重新创建，因为跨界权限在混合部署方案中不受支持。有关详细信息，请参阅 [Exchange Server 2013 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

> [!NOTE]  
> 已同步的启用邮件的公用文件夹将显示为邮件联系人对象，用于处理邮件流，并且不会在 Exchange 管理中心 中显示。请参阅 Get-MailPublicFolder 命令。要重新创建云中的 SendAs 权限，请使用 Add-RecipientPermission 命令。


1.  在旧版 Exchange 服务器上，运行以下命令将启用邮件的公用文件夹从本地 Active Directory 同步到 O365 中。
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    其中 `Credential` 是您的 Office 365 用户名和密码，`CsvSummaryFile` 是您要以 .csv 格式记录同步操作和错误的文件路径。

> [!NOTE]  
> 在运行此脚本之前，我们建议您先模拟此脚本将在环境中执行的操作，方法是使用 <code>-WhatIf</code> 参数按照如上所述运行此脚本。
> 我们还建议您每天都运行此脚本以同步启用邮件的公用文件夹。


## 步骤 5：配置 Exchange Online 用户以访问本地公用文件夹

此过程中的最后一步是配置 Exchange Online 组织并允许访问旧版本地公用文件夹。

允许 Exchange Online 组织访问本地公用文件夹。您可以指向在步骤 2：使远程公用文件夹可见中创建的所有代理公用文件夹邮箱。

在 **Windows PowerShell** 中运行以下命令：

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

您必须等待 ActiveDirectory 同步完成才能查看更改。此过程可能需要 3 个小时才能完成。如果您不想等待每隔三小时进行一次定期同步，可以随时强制执行目录同步。有关强制执行目录同步的详细步骤，请参阅[强制执行目录同步](http://technet.microsoft.com/zh-cn/library/jj151771.aspx)。Office 365 随机选择此命令中提供的一个公用文件夹邮箱。

> [!IMPORTANT]   
> 不是由 MailUser 本地对象代表的 Office 365 用户（对目标公用文件夹层次结构是本地的）不能访问旧版或 Exchange 2013 本地公用文件夹。请参阅知识库文章 <a href="https://go.microsoft.com/fwlink/p/?linkid=699451">Exchange 联机用户不能访问旧版本地公用文件夹</a>查找解决方案。


## 我如何知道这有效？

1.  登录到位于 Exchange Online 内的用户的 Outlook，并执行以下公用文件夹测试：
    
      - 查看层次结构。
    
      - 检查权限
    
      - 创建和删除公用文件夹。
    
      - 发布内容到公用文件夹并从公用文件夹删除内容。

## 刚开始接触 Office 365？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="“领英学习”短图标" alt="“领英学习”短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

