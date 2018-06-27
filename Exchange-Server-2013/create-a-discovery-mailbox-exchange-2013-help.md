---
title: '创建发现邮箱: Exchange 2013 Help'
TOCTitle: 创建发现邮箱
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 50491525
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建发现邮箱

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

默认情况下，Microsoft Exchange Server 2013 安装程序会创建发现邮箱。在 Exchange Online 中也会默认创建发现邮箱。在 Exchange 管理中心 (EAC) 中，可将发现邮箱用作 [就地电子数据展示](in-place-ediscovery-exchange-2013-help.md) 搜索的目标邮箱。可以根据需要创建其他发现邮箱。创建新的发现邮箱后，您必须为适合的用户分配“完全访问”权限，以便他们能够访问复制到发现邮箱的电子数据展示搜索结果。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>发现管理员将电子数据展示搜索结果复制到发现邮箱后，该邮箱可能包含敏感信息。您需要控制对发现邮箱的访问，确保只有授权用户才可以访问。</td>
</tr>
</tbody>
</table>


有关详细信息，请参阅[Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“创建发现邮箱”条目。

  - 发现邮箱的邮箱存储配额为 50 千兆字节 (GB)。不能增加此存储配额。

  - 您无法使用 EAC 创建发现邮箱或分配访问该邮箱的权限。您必须使用命令行管理程序。在 Office 365 中，使用远程 PowerShell 连接到您的 Exchange Online 组织。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## （可选）步骤 1：使用远程 PowerShell 连接到 Exchange Online

如果您具有 Exchange Online 或 Office 365 组织，您仅需执行此步骤。如果您具有 Exchange Server 2013 组织，转到下一步，并在 Exchange 命令行管理程序 中运行命令。

1.  在本地计算机上，打开 Windows PowerShell 并运行以下命令。
    
        $UserCredential = Get-Credential
    
    在“Windows PowerShell 凭据请求”对话框中，键入 Office 365 全局管理员帐户的用户名和密码，然后单击“确定”。

2.  运行以下命令。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  运行以下命令。
    
        Import-PSSession $Session

4.  要验证您是否已连接至您的 Exchange Online 组织，请运行以下命令获取组织中所有邮箱的列表。
    
        Get-Mailbox

有关详细信息，或者如果您在连接到 Exchange Online 组织时遇到问题，请参阅[使用远程 PowerShell 连接到 Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=517283)。

## 步骤 2：创建发现邮箱

本示例创建名为“SearchResults”的发现邮箱。

    New-Mailbox -Name SearchResults -Discovery 

有关语法和参数的详细信息，请参阅[New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

若要显示 Exchange 组织中的所有发现邮箱列表，请运行以下命令：

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

## 步骤 3：分配发现邮箱的权限

您必须明确地将打开所创建发现邮箱所需的权限分配给用户或群组。若要为用户或群组分配打开发现邮箱和查看搜索结果所需的权限，请使用以下语法：

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

例如，以下命令为“Litigation Managers”群组分配了“完全访问”权限，因此该群组中的所有成员都可以打开“Fabrikam Litigation”发现邮箱。

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

有关语法和参数的详细信息，请参阅 [Add-MailboxPermission](https://technet.microsoft.com/zh-cn/library/bb124097\(v=exchg.150\))。

## 详细信息

  - 默认情况下，只有发现管理角色组的成员具有打开默认发现搜索邮箱的“完全访问”权限。如果您希望“发现管理”角色组的成员可以打开您创建的发现邮箱，则必须明确地为该组分配“完全访问”权限。

  - 虽然电子邮件在 Exchang 地址列表中可见，但用户不能将其发送至发现邮箱。使用传递限制来禁止对发现邮箱进行电子邮件传递。这可保持复制到发现邮箱的搜索结果的完整性。

  - 发现邮箱将不能用作其他用途或转换为其他类型的邮箱。

  - 您可以像删除任何其他类型邮箱那样删除发现邮箱。

