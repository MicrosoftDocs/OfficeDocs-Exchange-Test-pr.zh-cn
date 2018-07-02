---
title: '管理发件人 ID: Exchange 2013 Help'
TOCTitle: 管理发件人 ID
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50490258
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理发件人 ID

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

发件人 ID 功能由发件人 ID 代理提供。发件人 ID 根据假设的发件人域所有者来验证发件人的 IP 地址，从而验证电子邮件的来源。对来自 Internet 的未经过身份验证的入站邮件执行发件人 ID 筛选。这些邮件将作为外部邮件处理。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

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

## 使用命令行管理程序启用或禁用发件人 ID

若要禁用发件人 ID，请运行以下命令：

    Set-SenderIDConfig -Enabled $false

若要启用发件人 ID，请运行以下命令：

    Set-SenderIDConfig -Enabled $true

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>禁用发件人 ID 时，基础发件人 ID 代理仍启用。要禁用发件人 ID 代理，请运行以下命令：<code>Disable-TransportAgent &quot;Sender ID Agent&quot;</code>.</td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

要验证是否已成功启用或禁用发件人 ID，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderIDConfig | Format-List Enabled

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序对欺骗性邮件配置发件人 ID 操作

要对欺骗性邮件配置发件人 ID 操作，请运行以下命令：

    Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>

此示例将发件人 ID 代理配置为拒绝以下类型的任何邮件：其发送服务器的 IP 地址未作为权威的 SMTP 发送服务器列在发送域的 DNS 发件人策略框架 (SPF) 记录中。

    Set-SenderIDConfig -SpoofedDomainAction Reject

## 您如何知道这有效？

要验证是否已成功对欺骗性邮件配置发件人 ID 操作，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderIDConfig | Format-List SpoofedDomainAction

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序对暂时性错误配置发件人 ID 操作

要对暂时性错误配置发件人 ID 操作，请运行以下命令：

    Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>

此示例将发件人 ID 代理配置为标记由于临时 DNS 服务器错误而无法确定发件人 ID 状态时的邮件。该邮件将由其他反垃圾邮件代理进行处理，并且内容筛选器代理会在确定邮件的 SCL 值时使用此标记。

    Set-SenderIDConfig -TempErrorAction StampStatus

请注意，`StampStatus` 是 *TempErrorAction* 参数的默认值。

## 您如何知道这有效？

要验证是否已成功对暂时性错误配置发件人 ID 操作，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderIDConfig | Format-List TempErrorAction

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序配置收件人和发件人域例外

要替换现有值，请运行以下命令：

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

此示例将发件人 ID 代理配置为绕过对发送到 kim@contoso.com 和 john@contoso.com 的邮件的发件人 ID 检查并绕过对从 fabrikam.com 域发送的邮件的发件人 ID 检查。

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

要在不修改任何现有值的情况下添加或删除条目，请运行以下命令：

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

此示例使用以下信息配置发件人 ID 代理：

  - 将 chris@contoso.com 和 michelle@contoso.com 添加到绕过发件人 ID 检查的现有收件人的列表。

  - 从绕过发件人 ID 检查的现有域的列表中删除 tailspintoys.com。

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## 您如何知道这有效？

要验证是否已成功配置收件人和发件人域例外，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains

2.  验证显示的值是否为您配置的值。

