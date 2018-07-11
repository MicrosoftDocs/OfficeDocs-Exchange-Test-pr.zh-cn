---
title: '管理发件人筛选: Exchange 2013 Help'
TOCTitle: 管理发件人筛选
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50491348
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理发件人筛选

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

发件人筛选由发件人筛选器代理提供。发件人筛选器代理依赖于 **MAIL FROM:** SMTP 头可以确定要对入站电子邮件执行的操作（如果有）。

在 Exchange 服务器上启用发件人筛选功能之后，发件人筛选功能会对通过此计算机上所有接收连接器传入的所有邮件进行筛选。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用发件人筛选

若要禁用发件人筛选，请运行以下命令：

    Set-SenderFilterConfig -Enabled $false

若要启用发件人筛选，请运行以下命令：

    Set-SenderFilterConfig -Enabled $true

> [!NOTE]  
> 当禁用发件人筛选时，仍会启用基础发件人筛选器代理。若要禁用发件人筛选器代理，请运行以下命令：<code>Disable-TransportAgent &quot;Sender Filter Agent&quot;</code>.


## 您如何知道这有效？

若要验证是否成功启用或禁用了发件人筛选，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderFilterConfig | Format-List Enabled

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序配置阻止发件人和域

要替换现有值，请运行以下命令：

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

此示例将配置发件人筛选器代理，以阻止来自 kim@contoso.com 和 john@contoso.com 的邮件、来自 fabrikam.com 域的邮件以及来自 northwindtraders.com 及其所有子域的邮件。

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

要在不修改任何现有值的情况下添加或删除条目，请运行以下命令：

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

本示例将使用以下信息配置发件人筛选器代理：

  - 将 chris@contoso.com 和 michelle@contoso.com 添加到被阻止的现有发件人列表。

  - 从被阻止的现有发件人域列表中删除 tailspintoys.com。

  - 将 blueyonderairlines.com 添加到被阻止的现有发件人域和子域列表。

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## 您如何知道这有效？

若要验证您是否已成功配置阻止发件人，请执行下列操作：

1.  运行以下命令：
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序来启用或禁用阻止发件人为空的邮件

若要启用或禁用阻止发件人为空的邮件，请运行以下命令：

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

此示例将配置发件人筛选器代理，以阻止未在 MAIL FROM:SMTP 命令中指定发件人的邮件：

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## 您如何知道这有效？

若要验证是否成功启用或禁用了阻止发件人为空的邮件，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  验证显示的值是否为您配置的值。

