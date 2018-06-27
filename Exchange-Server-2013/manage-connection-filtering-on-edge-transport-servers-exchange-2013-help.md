---
title: '管理边缘传输服务器上的连接筛选: Exchange 2013 Help'
TOCTitle: 管理边缘传输服务器上的连接筛选
ms:assetid: baebc865-ec3e-48ca-ac48-7aac8b34c003
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124376(v=EXCHG.150)
ms:contentKeyID: 60829995
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理边缘传输服务器上的连接筛选

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

连接筛选是连接筛选代理提供的反垃圾邮件功能，仅可用于 Microsoft Exchange 2013 中的边缘传输服务器。连接筛选将启用以下功能：

  - IP 阻止列表 (IP Block list)

  - IP 阻止列表提供程序

  - IP 允许列表 (IP Allow list)

  - IP 允许列表提供程序

可以单独启用或禁用上述任一功能。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

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

## 使用命令行管理程序启用或禁用连接筛选

若要完全启用或禁用连接筛选，请启用或禁用连接筛选代理。更改将在重新启动 Microsoft Exchange 传输服务后生效。重新启动边缘传输服务器上的 Microsoft Exchange 传输服务时，服务器上的邮件流会临时中断。

若要禁用连接筛选，请运行以下命令：

    Disable-TransportAgent "Connection Filtering Agent"

若要启用连接筛选，请运行以下命令：

    Enable-TransportAgent "Connection Filtering Agent"

若要使更改生效，请运行以下命令以重新启动 Microsoft Exchange 传输服务：

    Restart-Service MSExchangeTransport

## 您如何知道这有效？

若要验证是否已成功启用或禁用连接筛选，请运行以下命令并验证显示的值是否是您配置的值。

    Get-TransportAgent "Connection Filtering Agent" | Format-List Enabled

## IP 阻止列表相关步骤

这些步骤适用于手动配置的 IP 阻止列表。不适用于 IP 阻止列表提供程序。

可使用 **IPBlockListConfig** cmdlet 查看和配置连接筛选使用 IP 阻止列表的方式。可使用 **IPBlockListEntry** cmdlet 查看和配置 IP 阻止列表中的 IP 地址。

## 使用命令行管理程序查看 IP 阻止列表的配置

若要查看 IP 阻止列表的配置，请运行以下命令：

    Get-IPBlockListConfig | Format-List *Enabled,*Response

## 使用命令行管理程序启用或禁用 IP 阻止列表

若要禁用 IP 阻止列表，请运行以下命令：

    Set-IPBlockListConfig -Enabled $false

若要启用 IP 阻止列表，请运行以下命令：

    Set-IPBlockListConfig -Enabled $true

## 您如何知道这有效？

若要验证是否已成功启用或禁用 IP 阻止列表，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListConfig | Format-List Enabled

## 使用命令行管理程序配置 IP 阻止列表

若要配置 IP 阻止列表，请使用以下语法：

    Set-IPBlockListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false> -MachineEntryRejectionResponse "<Custom response text>"] [-StaticEntryRejectionResponse "<Custom response text>"]

本示例使用以下设置配置 IP 阻止列表：

  - IP 阻止列表将筛选来自内部和外部邮件服务器的传入连接。默认情况下，仅筛选来自外部邮件服务器的连接（*ExternalMailEnabled* 设置为 `$true`，*InternalMailEnabled* 设置为 `$false`）。来自外部合作伙伴的未经过身份验证的连接和经过身份验证的连接都将被视为外部连接。

  - 针对按通过协议分析代理的发件人信誉功能自动添加到 IP 阻止列表的 IP 地址进行筛选的连接的自定义响应文本设置为值\&quot;来自 IP 地址 {0} 的连接被发件人信誉拒绝\&quot;。

  - 针对按手动添加到 IP 阻止列表的 IP 地址进行筛选的连接的自定义响应文本设置为值\&quot;来自 IP 地址 {0} 的连接被连接筛选拒绝\&quot;。

<!-- end list -->

    Set-IPBlockListConfig -InternalMailEnabled $true -MachineEntryRejectionResponse "Connection from IP address {0} was rejected by sender reputation." -StaticEntryRejectionResponse "Connection from IP address {0} was rejected by connection filtering."

## 您如何知道这有效？

若要验证是否已成功配置 IP 阻止列表，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListConfig | Format-List *MailEnabled,*Response

## 使用命令行管理程序查看 IP 阻止列表条目

若要查看所有 IP 阻止列表条目，请运行以下命令：

    Get-IPBlockListEntry

请注意，每个 IP 阻止列表条目都由一个整数值进行标识。在向 IP 阻止列表和 IP 允许列表添加条目时，将按升序分配标识整数。

若要查看特定的 IP 阻止列表条目，请使用以下语法：

    Get-IPBlockListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

例如，若要查看包含 IP 地址 192.168.1.13 的 IP 阻止列表条目，请运行以下命令：

    Get-IPBlockListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <em>IPAddress</em> 参数时，生成的 IP 阻止列表条目可以是单个 IP 地址、IP 地址范围或无类别域际路由选择 (CIDR) IP。若要使用 <em>Identity</em> 参数，请指定分配给 IP 阻止列表条目的整数值。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序添加 IP 阻止列表条目

若要添加 IP 阻止列表条目，请使用以下语法：

    Add-IPBlockListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-comment "<Descriptive Comment>"]

以下示例添加了 IP 地址范围为 192.168.1.10 到 192.168.1.15 的 IP 阻止列表条目，并将 IP 阻止列表条目配置为于 2014 年 7 月 4 日 15:00 过期。

    Add-IPBlockListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## 您如何知道这有效？

若要验证是否已成功添加 IP 阻止列表条目，请运行以下命令并验证是否显示新 IP 阻止列表条目。

    Get-IPBlockListEntry

## 使用命令行管理程序删除 IP 阻止列表条目

若要删除 IP 阻止列表条目，请使用以下语法：

    Remove-IPBlockListEntry <IdentityInteger>

以下示例删除了包含 *Identity* 值 3 的 IP 阻止列表条目。

    Remove-IPBlockListEntry 3

下列示例在不使用 *Identity* 整数值的情况下删除了包含 IP 地址 192.168.1.12 的 IP 阻止列表条目。请注意，IP 阻止列表条目可以是单个 IP 地址，也可以是 IP 地址范围。

    Get-IPBlockListEntry -IPAddress 192.168.1.12 | Remove-IPBlockListEntry

## 您如何知道这有效？

若要验证是否已成功删除 IP 阻止列表条目，请运行以下命令并验证删除的 IP 阻止列表条目是否已不存在。

    Get-IPBlockListEntry

## IP 阻止列表提供程序相关步骤

这些步骤适用于 IP 阻止列表提供程序。不适用于 IP 阻止列表。

可使用 **IPBlockListProvidersConfig** cmdlet 查看和配置连接筛选使用所有 IP 阻止列表提供程序的方式。可使用 **IPBlockListProvider** cmdlet 查看、配置和测试 IP 阻止列表提供程序。

## 使用命令行管理程序查看所有 IP 阻止列表提供程序的配置

若要查看连接筛选使用所有 IP 阻止列表提供程序的方式，请运行以下命令：

    Get-IPBlockListProvidersConfig | Format-List *Enabled,Bypassed*

## 使用命令行管理程序启用或禁用所有 IP 阻止列表提供程序

若要禁用所有 IP 阻止列表提供程序，请运行以下命令：

    Set-IPBlockListProvidersConfig -Enabled $false

若要启用所有 IP 阻止列表提供程序，请运行以下命令：

    Set-IPBlockListProvidersConfig -Enabled $true

## 您如何知道这有效？

若要验证是否已启用或禁用所有 IP 阻止列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListProvidersConfig | Format-List Enabled

## 使用命令行管理程序配置所有 IP 阻止列表提供程序

若要配置连接筛选使用所有 IP 阻止列表提供程序的方式，请使用以下语法：

    Set-IPBlockListProvidersConfig [-BypassedRecipients <recipient1,recipient2...>] [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

以下示例使用以下设置配置所有 IP 阻止列表提供程序：

  - IP 阻止列表提供程序将筛选来自内部和外部邮件服务器的传入连接。默认情况下，仅筛选来自外部邮件服务器的连接（*ExternalMailEnabled* 设置为 `$true`，*InternalMailEnabled* 设置为 `$false`）。来自外部合作伙伴的未经过身份验证的连接和经过身份验证的连接都将被视为外部连接。

  - 发送给内部收件人 chris@fabrikam.com 和 michelle@fabrikam.com 的邮件将不会由 IP 阻止列表提供程序进行筛选。请注意，如果要在不影响现有收件人的情况下向列表中添加收件人，请使用以下语法：`@{Add="<recipient1>","<recipient2>"...}`。

<!-- end list -->

    Set-IPBlockListProvidersConfig -BypassedRecipients chris@fabrikam.com,michelle@fabrikam.com -InternalMailEnabled $true

有关详细信息，请参阅 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/zh-cn/library/aa998543\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功配置所有 IP 阻止列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListProvidersConfig | Format-List *MailEnabled,Bypassed*

## 使用命令行管理程序查看 IP 阻止列表提供程序

若要查看所有 IP 阻止列表提供程序的摘要列表，请运行以下命令：

    Get-IPBlockListProvider

若要查看特定提供程序的详细信息，请使用以下语法：

    Get-IPBlockListProvider <IPBlockListProviderIdentity>

以下示例显示名为\&quot;Contoso IP Block List Provider\&quot;的提供程序的详细信息。

    Get-IPBlockListProvider "Contoso IP Block List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match,*Response

## 使用命令行管理程序添加 IP 阻止列表提供程序

若要添加 IP 阻止列表提供程序，请使用以下语法：

    Add-IPBlockListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

本示例使用以下选项创建名为\&quot;Contoso IP Block List Provider\&quot;的 IP 阻止列表提供程序：

  - **使用提供程序的 FQDN**   rbl.contoso.com

  - **基于提供程序使用的位掩码代码**   127.0.0.1

<!-- end list -->

    Add-IPBlockListProvider -Name "Contoso IP Block List Provider" -LookupDomain rbl.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>添加新 IP 阻止列表提供程序后，它会默认启用（<em>Enabled</em> 的值为 <code>$true</code>），并且会递增优先级值（第一个条目具有 <em>Priority</em> 值 1）。</td>
</tr>
</tbody>
</table>


有关详细信息，请参阅 [Add-IPBlockListProvider](https://technet.microsoft.com/zh-cn/library/bb124358\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功添加 IP 阻止列表提供程序，请运行以下命令并验证是否显示新 IP 阻止列表提供程序。

    Get-IPBlockListProvider

## 使用命令行管理程序启用或禁用 IP 阻止列表提供程序

若要启用或禁用特定 IP 阻止列表提供程序，请使用以下语法：

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Enabled <$true | $false>

以下示例禁用名为\&quot;Contoso IP Block List Provider\&quot;的提供程序。

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $false

以下示例启用名为\&quot;Contoso IP Block List Provider\&quot;的提供程序。

    Set-IPBlockListProvider "Contoso IP Block List Provider" -Enabled $true

## 您如何知道这有效？

若要验证是否已成功启用或禁用 IP 阻止列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List Enabled

## 使用命令行管理程序配置 IP 阻止列表提供程序

在 **Set-IPBlockListProvider** cmdlet 上可用的配置选项与在 **New-IPBlockListProvider** cmdlet 上可用的配置选项相同。

若要配置现有 IP 阻止列表提供程序，请使用以下语法：

    Set-IPBlockListProvider <IPBlockListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>] [-RejectionResponse "<Custom Text>"]

例如，若要将 IP 地址状态代码 127.0.0.1 添加到名为\&quot;Contoso IP Block List Provider\&quot;的提供程序的现有状态代码列表中，请运行以下命令：

    Set-IPBlockListProvider "Contoso IP Block List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

有关详细信息，请参阅 [Set-IPBlockListProvider](https://technet.microsoft.com/zh-cn/library/bb124979\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功配置 IP 阻止列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPBlockListProvider <IPBlockListProviderIdentity> | Format-List

## 使用命令行管理程序测试 IP 阻止列表提供程序

若要测试 IP 阻止列表提供程序，请使用以下语法。

    Test-IPBlockListProvider <IPBlockListProviderIdentity> -IPAddress <IPAddressToTest>

以下示例通过查找 IP 地址 192.168.1.1 测试名为\&quot;Contoso IP Block List Provider\&quot;的提供程序。

    Test-IPBlockListProvider "Contoso IP Block List Provider" -IPAddress 192.168.1.1

## 使用命令行管理程序删除 IP 阻止列表提供程序

若要删除 IP 阻止列表提供程序，请使用以下语法：

    Remove-IPBlockListProvider <IPBlockListProviderIdentity>

以下示例删除名为\&quot;Contoso IP Block List Provider\&quot;的 IP 阻止列表提供程序。

    Remove-IPBlockListProvider "Contoso IP Block list Provider"

## 您如何知道这有效？

若要验证是否已成功删除 IP 阻止列表提供程序，请运行以下命令并验证删除的 IP 阻止列表提供程序是否已不存在。

    Get-IPBlockListProvider

## IP 允许列表相关步骤

这些步骤适用于手动配置的 IP 允许列表。不适用于 IP 允许列表提供程序。

可使用 **IPAllowListConfig** cmdlet 查看和配置连接筛选使用 IP 允许列表的方式。可使用 **IPAllowListEntry** cmdlet 查看和配置 IP 允许列表中的 IP 地址。

## 使用命令行管理程序查看 IP 允许列表的配置

若要查看 IP 允许列表的配置，请运行以下命令。

    Get-IPAllowListConfig | Format-List *Enabled

## 使用命令行管理程序启用或禁用 IP 允许列表

若要禁用 IP 允许列表，请运行以下命令：

    Set-IPAllowListConfig -Enabled $false

若要启用 IP 允许列表，请运行以下命令：

    Set-IPAllowListConfig -Enabled $true

## 您如何知道这有效？

若要验证是否已成功启用或禁用 IP 允许列表，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListConfig | Format-List Enabled

## 使用命令行管理程序配置 IP 允许列表

若要配置 IP 允许列表，请使用以下语法：

    Set-IPAllowListConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>

本示例将 IP 允许列表配置为筛选来自内部和外部邮件服务器的传入连接。默认情况下，仅筛选来自外部邮件服务器的连接（*ExternalMailEnabled* 设置为 `$true`，*InternalMailEnabled* 设置为 `$false`）。来自外部合作伙伴的未经过身份验证的连接和经过身份验证的连接都将被视为外部连接。

    Set-IPAllowListConfig -InternalMailEnabled $true

## 您如何知道这有效？

若要验证是否已成功配置 IP 允许列表，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListConfig | Format-List *MailEnabled

## 使用命令行管理程序查看 IP 允许列表条目

若要查看所有 IP 允许列表条目，请运行以下命令：

    Get-IPAllowListEntry

请注意，每个 IP 允许列表条目都由一个整数值进行标识。在向 IP 阻止列表和 IP 允许列表添加条目时，将按升序分配标识整数。

若要查看特定的 IP 允许列表条目，请使用以下语法：

    Get-IPAllowListEntry <-Identity IdentityInteger | -IPAddress IPAddress>

例如，若要查看包含 IP 地址 192.168.1.13 的 IP 允许列表条目，请运行以下命令：

    Get-IPAllowListEntry -IPAddress 192.168.1.13

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 <em>IPAddress</em> 参数时，生成的 IP 允许列表条目可以是单个 IP 地址、IP 地址范围或无类别域际路由选择 (CIDR) IP。若要使用 <em>Identity</em> 参数，请指定分配给 IP 允许列表条目的整数值。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序添加 IP 允许列表条目

若要添加 IP 允许列表条目，请使用以下语法：

    Add-IPAllowListEntry <-IPAddress IPAddress | -IPRange IP range or CIDR IP> [-ExpirationTime <DateTime>] [-Comment "<Descriptive Comment>"]

本示例添加了 IP 地址范围为 192.168.1.10 到 192.168.1.15 的 IP 允许列表条目，并将 IP 允许列表条目配置为于 2014 年 7 月 4 日 15:00 过期。

    Add-IPAllowListEntry -IPRange 192.168.1.10-192.168.1.15 -ExpirationTime "7/4/2014 15:00"

## 您如何知道这有效？

若要验证是否已成功添加 IP 允许列表条目，请运行以下命令并验证是否显示新 IP 允许列表条目。

    Get-IPAllowListEntry

## 使用命令行管理程序删除 IP 允许列表条目

若要删除 IP 允许列表条目，请使用以下语法：

    Remove-IPAllowListEntry <IdentityInteger>

以下示例删除了包含 *Identity* 值 3 的 IP 允许列表条目。

    Remove-IPAllowListEntry 3

本示例在不使用 *Identity* 整数值的情况下删除了包含 IP 地址 192.168.1.12 的 IP 允许列表条目。请注意，IP 允许列表条目可以是单个 IP 地址，也可以是 IP 地址范围。

    Get-IPAllowListEntry -IPAddress 192.168.1.12 | Remove-IPAllowListEntry

## 您如何知道这有效？

若要验证是否已成功删除 IP 允许列表条目，请运行以下命令并验证删除的 IP 允许列表条目是否已不存在。

    Get-IPAllowListEntry

## IP 允许列表提供程序相关步骤

这些步骤适用于 IP 允许列表提供程序。不适用于 IP 允许列表。

可使用 **IPAllowListProvidersConfig** cmdlet 查看和配置连接筛选使用所有 IP 允许列表提供程序的方式。可使用 **IPAllowListProvider** cmdlet 查看、配置和测试 IP 允许列表提供程序。

## 使用命令行管理程序查看所有 IP 允许列表提供程序的配置

若要查看连接筛选使用所有 IP 允许列表提供程序的方式，请运行以下命令：

    Get-IPAllowListProvidersConfig | Format-List *Enabled

## 使用命令行管理程序启用或禁用所有 IP 允许列表提供程序

若要禁用所有 IP 允许列表提供程序，请运行以下命令：

    Set-IPAllowListProvidersConfig -Enabled $false

若要启用所有 IP 允许列表提供程序，请运行以下命令：

    Set-IPAllowListProvidersConfig -Enabled $true

## 您如何知道这有效？

若要验证是否已启用或禁用所有 IP 允许列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListProvidersConfig | Format-List Enabled

## 使用命令行管理程序配置所有 IP 允许列表提供程序

若要配置连接筛选使用所有 IP 允许列表提供程序的方式，请使用以下语法：

    Set-IPAllowListProvidersConfig [-ExternalMailEnabled <$true | $false>] [-InternalMailEnabled <$true | $false>]

本示例将所有 IP 允许列表提供程序配置为筛选来自内部和外部邮件服务器的传入连接。默认情况下，仅筛选来自外部邮件服务器的连接（*ExternalMailEnabled* 设置为 `$true`，*InternalMailEnabled* 设置为 `$false`）。来自外部合作伙伴的未经过身份验证的连接和经过身份验证的连接都将被视为外部连接。

    Set-IPAllowListProvidersConfig -InternalMailEnabled $true

有关详细信息，请参阅 [Set-IPBlockListProvidersConfig](https://technet.microsoft.com/zh-cn/library/aa998543\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功配置所有 IP 允许列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListProvidersConfig | Format-List *MailEnabled

## 使用命令行管理程序查看 IP 允许列表提供程序

若要查看所有 IP 允许列表提供程序的摘要列表，请运行以下命令。

    Get-IPAllowListProvider

若要查看特定提供程序的详细信息，请使用以下语法。

    Get-IPAllowListProvider <IPAllowListProviderIdentity>

本示例显示名为\&quot;Contoso IP Allow List Provider\&quot;的提供程序的详细信息。

    Get-IPAllowListProvider "Contoso IP Allow List Provider" | Format-List Name,Enabled,Priority,LookupDomain,*Match

## 使用命令行管理程序添加 IP 允许列表提供程序

若要添加 IP 允许列表提供程序，请使用以下语法：

    Add-IPAllowListProvider -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-Enabled <$true | $false>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

本示例使用以下选项创建名为\&quot;Contoso IP Allow List Provider\&quot;的 IP 允许列表提供程序：

  - **使用提供程序的 FQDN**   allow.contoso.com

  - **基于提供程序使用的位掩码代码**   127.0.0.1

<!-- end list -->

    Add-IPAllowListProvider -Name "Contoso IP Allow List Provider" -LookupDomain allow.contoso.com -BitmaskMatch 127.0.0.1

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>添加新 IP 允许列表提供程序后，它会默认启用（<em>Enabled</em> 的值为 <code>$true</code>），并且会递增优先级值（第一个条目具有 <em>Priority</em> 值 1）。</td>
</tr>
</tbody>
</table>


有关详细信息，请参阅 [Add-IPBlockListProvider](https://technet.microsoft.com/zh-cn/library/bb124358\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功添加 IP 允许列表提供程序，请运行以下命令并验证是否显示新 IP 允许列表提供程序。

    Get-IPAllowListProvider

## 使用命令行管理程序启用或禁用 IP 允许列表提供程序

若要启用或禁用特定 IP 允许列表提供程序，请使用以下语法。

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Enabled <$true | $false>

本示例禁用名为\&quot;Contoso IP Allow List Provider\&quot;的提供程序。

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $false

本示例启用名为\&quot;Contoso IP Allow List Provider\&quot;的提供程序。

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -Enabled $true

## 您如何知道这有效？

若要验证是否已成功启用或禁用 IP 允许列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List Enabled

## 使用命令行管理程序配置 IP 允许列表提供程序

在 **Set-IPAllowListProvider** cmdlet 上可用的配置选项与在 **New-IPAllowListProvider** cmdlet 上可用的配置选项相同。

若要配置现有 IP 允许列表提供程序，请使用以下语法：

    Set-IPAllowListProvider <IPAllowListProviderIdentity> -Name "<Descriptive Name>" -LookupDomain <FQDN> [-Priority <Integer>] [-AnyMatch <$true | $false>] [-BitmaskMatch <IPAddress>] [-IPAddressesMatch <IPAddressStatusCode1,IPAddressStatusCode2...>]

例如，若要将 IP 地址状态代码 127.0.0.1 添加到名为\&quot;Contoso IP Allow List Provider\&quot;的提供程序的现有状态代码列表中，请运行以下命令：

    Set-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddressesMatch @{Add="127.0.0.1"}

有关详细信息，请参阅 [Set-IPBlockListProvider](https://technet.microsoft.com/zh-cn/library/bb124979\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功配置 IP 允许列表提供程序，请运行以下命令并验证显示的值是否是您配置的值。

    Get-IPAllowListProvider <IPAllowListProviderIdentity> | Format-List

## 使用命令行管理程序测试 IP 允许列表提供程序

若要测试 IP 允许列表提供程序，请使用以下语法：

    Test-IPAllowListProvider <IPAllowListProviderIdentity> -IPAddress <IPAddressToTest>

以下示例通过查找 IP 地址 192.168.1.1 测试名为\&quot;Contoso IP Allow List Provider\&quot;的提供程序。

    Test-IPAllowListProvider "Contoso IP Allow List Provider" -IPAddress 192.168.1.1

## 使用命令行管理程序删除 IP 允许列表提供程序

若要删除 IP 允许列表提供程序，请使用以下语法：

    Remove-IPAllowListProvider <IPAllowListProviderIdentity>

本示例删除名为\&quot;Contoso IP Allow List Provider\&quot;的 IP 允许列表提供程序。

    Remove-IPAllowListProvider "Contoso IP Allow List Provider"

## 您如何知道这有效？

若要验证是否已成功删除 IP 允许列表提供程序，请运行以下命令并验证删除的 IP 允许列表提供程序是否已不存在。

    Get-IPAllowListProvider

