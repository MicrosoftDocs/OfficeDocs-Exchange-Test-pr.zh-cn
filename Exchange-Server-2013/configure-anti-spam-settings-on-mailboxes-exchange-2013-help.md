---
title: '在邮箱上配置反垃圾邮件设置: Exchange 2013 Help'
TOCTitle: 在邮箱上配置反垃圾邮件设置
ms:assetid: 868d7fd8-e817-46ba-9b67-edf2f50b9494
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123559(v=EXCHG.150)
ms:contentKeyID: 50491112
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在邮箱上配置反垃圾邮件设置

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-11-17_

可以在各个邮箱上配置不同于应用于 Exchange 组织中其余邮箱的反垃圾邮件设置的特定反垃圾邮件设置。在邮箱上配置反垃圾邮件设置时，该设置将覆盖对应的组织范围内容筛选或组织配置反垃圾邮件设置。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>2016 年 11 月 1 日起，Microsoft 停止为 Exchange 和 Outlook 中的 SmartScreen 筛选器生成垃圾邮件定义更新。现有的 SmartScreen 垃圾邮件定义将予以保留，但其效力可能会随时间的推移而逐渐降低。有关详细信息，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=835894">停止为 Outlook 和 Exchange 中的 SmartScreen 提供支持</a>。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的“反垃圾邮件功能”条目和[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“反垃圾邮件”条目。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。

  - “垃圾邮件”文件夹 SCL 阈值的行为不同于 SCL 删除、拒绝和隔离的值。有关详细信息，请参阅[垃圾邮件可信度阈值](spam-confidence-level-threshold-exchange-2013-help.md)。

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

## 使用命令行管理程序配置单个邮箱的反垃圾邮件功能

要在单个邮箱上配置反垃圾邮件设置，请使用以下语法。

    Set-Mailbox <MailboxIdentity> -AntispamBypassEnabled <$true | $false> -RequireSenderAuthenticationEnabled <$true | $false> -SCLDeleteEnabled <$true | $false | $null> -SCLDeleteThreshold <0-9 | $null> -SCLJunkEnabled <$true | $false | $null > -SCLJunkThreshold <0-9 | $null> -SCLQuarantineEnabled <$true | $false | $null > -SCLQuarantineThreshold <0-9 | $null> -SCLRejectEnabled <$true | $false | $null > -SCLRejectThreshold <0-9 | $null>

此示例将 Jeff Phillips 用户的邮箱配置为绕过所有反垃圾邮件筛选器，并将符合或超过“垃圾邮件”文件夹 SCL 阈值 5 的邮件传递到其 Microsoft Outlook 中的“垃圾邮件”文件夹。

    Set-Mailbox "Jeff Phillips" -AntispamBypassEnabled $true -SCLJunkEnabled $true -SCLJunkThreshold 4

## 您如何知道这有效？

要验证是否成功在单个邮箱上配置了反垃圾邮件功能，请执行以下操作：

1.  运行以下命令：
    
        Get-Mailbox <MailboxIdentity> | Format-List SCL*,Bypass*,*SenderAuth*

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序在多个邮箱上配置反垃圾邮件功能

要在多个邮箱上配置所有反垃圾邮件设置，请使用以下语法。

    Get-Mailbox [<Filter>]| Set-Mailbox <Anti-Spam Settings>

本示例对 Contoso.com 域中“用户”容器内的所有邮箱启用了值为 7 的 SCL 隔离阈值。

    Get-Mailbox -OrganizationalUnit Contoso.com/Users | Set-Mailbox -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 您如何知道这有效？

要验证是否成功在多个邮箱上配置了反垃圾邮件功能，请执行以下操作：

1.  运行以下命令：
    
        Get-Mailbox [<Filter>] | Format-List Name,SCL*,*SenderAuth*

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序为组织中的所有邮箱配置垃圾邮件阈值

运行以下命令：

    Set-OrganizationConfig -SCLJunkThreshold <Integer>

此示例将组织的垃圾邮件阈值设置为 5。

    Set-OrganizationConfig -SCLJunkThreshold 5

## 您如何知道这有效？

要验证是否成功为组织中的所有邮箱配置了垃圾邮件阈值，请执行以下操作：

1.  运行以下命令：
    
        Get-OrganizationConfig | Format-List SCLJunkThreshold

2.  验证显示的值是否为您配置的值。

