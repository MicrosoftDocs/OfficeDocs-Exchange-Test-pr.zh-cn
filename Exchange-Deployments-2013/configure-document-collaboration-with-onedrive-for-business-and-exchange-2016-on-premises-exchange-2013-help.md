---
title: '通过 OneDrive for Business 和本地 Exchange 2016 配置新式附件: Exchange 2013 Help'
TOCTitle: 通过 OneDrive for Business 和本地 Exchange 2016 配置新式附件
ms:assetid: 799518aa-7cfe-4708-92ee-98057ff168f5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Mt589761(v=EXCHG.150)
ms:contentKeyID: 70318045
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通过 OneDrive for Business 和本地 Exchange 2016 配置新式附件

 

_**适用于：**Exchange Server 2016_

_**上一次修改主题：**2016-12-09_

**摘要：**如何允许本地 Exchange Server 2016 用户在混合配置期间利用 OneDrive for Business 和 SharePoint Online 的文档协作。

最近，在 Office 365 中推出了新的附件选项。在 Exchange 2016 中，该选项被称为“*文档协作*”，它允许本地用户将存储在 OneDrive for Business 上的附件与其 Outlook 网页版客户端直接集成。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>从 Exchange Server 2016 的发布开始，Outlook Web App 现在被称为 Outlook 网页版。</td>
</tr>
</tbody>
</table>


通常情况下，用户通过将文件附加到邮件向他人发送该文件。然后，一个或多个收件人在其各自的文件副本中进行更改，最终需要在某个时刻将所有这些文件进行合并。此外，这些附加的文件会占用每个用户邮箱的存储空间。通过文档协作，用户改为向存储在 OneDrive for Business 帐户中的文件插入链接，以使文件可在相同源位置由多个人员进行编辑，而无需额外存储。

为文档协作正确配置 Exchange 2016 环境前，Outlook 网页版用户的默认附件对话框将类似于：

![传统附件对话框](images/Mt589761.f8c74d70-42f9-48c6-b263-ce6cef8591a8(EXCHG.150).png "传统附件对话框")

使用以下说明配置环境后，Outlook 网页版附件对话框将类似于：

![已启用现代附件的附件对话框](images/Mt589761.89eeae65-ce3a-4c47-b57e-db734a1de95b(EXCHG.150).png "已启用现代附件的附件对话框")

组织中具有本地邮箱的用户以及在 Office 365 中具有 OneDrive for Business 帐户的用户有权使用新式的附件方法，允许他们与多个收件人共享存储在 OneDrive for Business 中的文档。收件人的位置（联机和本地）无关紧要。

在 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md) 中了解有关混合部署的详细信息。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 检查 [Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md) 主题，并确保您清楚会受到配置混合部署影响的方面。

  - 检查并完成 [混合部署先决条件](hybrid-deployment-prerequisites-exchange-2013-help.md) 概括的所有混合部署要求。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](https://technet.microsoft.com/zh-cn/library/jj150484\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ659053.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 在混合环境中配置 Exchange 2016 以启用文档协作

验证以下先决条件步骤已完成，然后使用下面的过程启用文档协作。

**先决条件**

  - 使用 [“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md) (HCW) 配置 Exchange 混合环境。

  - Exchange 2016 必须安装在本地组织中。Exchange 2016 可与早期版本的 Exchange 共存，但文档协作适用于 Exchange 2016 服务器上的邮箱。

  - 必须安装身份验证服务器并同步所有用户。可使用 [Get-AuthServer](https://technet.microsoft.com/zh-cn/library/jj218613\(v=exchg.150\)) cmdlet 查找身份验证服务器。我们建议使用来自 Exchange 2016 服务器的 HCW 对 OAuth 进行必要的配置。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>需要正确配置 Exchange 2016 和 Office 365 之间的 OAuth。有关详细信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/dn594521(v=exchg.150)">配置 Exchange 和 Exchange Online 组织之间的 OAuth 身份验证</a>。</td>
    </tr>
    </tbody>
    </table>


  - 用户必须拥有正确的许可证。具有 OneDrive for Business 帐户的用户需获得 SharePoint Online 或 OneDrive for Business 的授权。可通过在 Office 365 门户中选择用户，并选择“**编辑**”按钮来验证用户的许可证。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>有关详细信息，请参阅 <a href="http://go.microsoft.com/fwlink/p/?linkid=627455">Set up OneDrive for Business in Office 365</a>（在 Office 365 中设置 OneDrive for Business）。</td>
    </tr>
    </tbody>
    </table>


执行以下步骤：

1.  配置默认 Outlook 网页版邮箱策略以设置 OneDrive for Business 宿主 URL。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn986544.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可转到 Office 365 SharePoint Online 租户管理，以检索 OneDrive for Business 宿主 URL。例如，https://contoso-my.sharepoint.com 是 Contoso 的 O365 租户中的“我的网站宿主”URL。<br />
    尽管 Exchange 2016 随附的 Outlook 网页版邮箱策略称为“默认”策略，但它不会自动应用到任何邮箱，除非将其设置为默认策略或直接将其分配到某个邮箱。</td>
    </tr>
    </tbody>
    </table>
    
    使用以下示例作为基础，使用 Exchange 命令行管理程序 在默认 Outlook 网页版邮箱策略上配置内部和外部“我的网站”URL：
    
        Set-OwaMailboxPolicy Default -InternalSPMySiteHostURL https://Contoso-my.sharepoint.com -ExternalSPMySiteHostURL https://Contoso-my.sharepoint.com

2.  接下来，将刚配置的策略设置为默认策略，以使其应用于所有邮箱，或将策略分配到个人用户。
    
    若要将该策略作为 Outlook 网页版邮箱策略的默认策略，请在 Exchange 命令行管理程序 中键入以下命令。
    
        Set-OwaMailboxPolicy Default -IsDefault 
    
    若要向个人邮箱分配策略，请在 Exchange 命令行管理程序 中键入以下命令：
    
        Set-CASMailbox <user mailbox> -OwaMailboxPolicy Default

3.  （可选）在每个 Exchange 2016 服务器上，重启 **OWAApplicationPool**，这将可以使配置立即生效。如果不运行此命令，则 Exchange 2016 服务器需要几分钟应用更新的邮件策略。在 Exchange 命令行管理程序 中，运行：
    
        Restart-WebAppPool MSExchangeOWAAppPool

配置完成后，Outlook 网页版用户将可以选择想要应用到其邮件的附件类型：传统或新式。

![附件选项对话框，“使用 OneDrive 共享”或“以附件形式发送”](images/Mt589761.7d2f27c2-3638-479a-a577-029ac61e7d95(EXCHG.150).png "附件选项对话框，“使用 OneDrive 共享”或“以附件形式发送”")

