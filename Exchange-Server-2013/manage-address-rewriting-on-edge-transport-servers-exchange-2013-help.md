---
title: '在边缘传输服务器上管理地址重写: Exchange 2013 Help'
TOCTitle: 在边缘传输服务器上管理地址重写
ms:assetid: 323a0b55-f921-425d-b1b0-18ad0fac315c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997185(v=EXCHG.150)
ms:contentKeyID: 61060576
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在边缘传输服务器上管理地址重写

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

您可以在边缘传输服务器上使用 Exchange 命令行管理程序来执行与地址重写和地址重写代理相关的所有管理任务。有关地址重写的详细信息，请参阅[边缘传输服务器上的地址重写](address-rewriting-on-edge-transport-servers-exchange-2013-help.md)。

您可以创建适用于单个收件人、特定域或子域中的所有收件人或多个子域中的所有收件人的地址重写条目。地址重写可以是仅出站，也可以是入站和出站（双向）。当您创建地址重写条目时，请注意以下几点：

  - 验证生成的电子邮件地址是否在您的组织中具有唯一性。

  - 电子邮件地址值中仅支持文本字符串。

  - 只有内部地址（要更改的地址）才支持通配符 (\*)。验证使用通配符的语法是否是 **\*.contoso.com**。不允许使用值 **\*contoso.com** 和 **sales.\*.com**。

  - 使用通配符时，您需要将地址重写配置为仅出站（需要将 *OutboundOnly* 参数的值设置为 `$true`）。

  - 当您配置仅出站地址重写（通过将 *OutboundOnly* 参数的值设置为 `$true`）时，需要配置受影响的收件人的代理地址。这样，邮件就能发送到重写地址，从而实现正确传送。

  - 默认情况下，对于单个收件人或特定域或子域中的所有收件人而言，地址重写均为双向（*OutboundOnly* 参数的默认值为 `$false`）。

## 在开始之前，您需要知道什么？

  - 完成每个过程的估计时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“边缘传输服务器”部分。

  - 只能使用命令行管理程序执行此过程。

  - 请谨慎配置地址重写。在您运行命令时，您所做的所有更改都会立即应用。请考虑运行包含 *WhatIf* 参数的命令。有关 *WhatIf* 参数的详细信息，请参阅 [WhatIf、Confirm 和 ValidateOnly 开关](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)。

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

## 使用命令行管理程序启用或禁用地址重写

若要完全启用或禁用地址重写，请启用或禁用地址重写代理。默认情况下，边缘传输服务器上的地址重写代理处于启用状态。

若要禁用地址重写，请运行以下命令：

    Disable-TransportAgent "Address Rewriting Inbound Agent"
    Disable-TransportAgent "Address Rewriting Outbound Agent"

若要启用地址重写，请运行以下命令：

    Enable-TransportAgent "Address Rewriting Inbound Agent"
    Enable-TransportAgent "Address Rewriting Outbound Agent"

## 您如何知道这有效？

若要验证是否已成功启用或禁用地址重写，请执行以下操作：

1.  运行以下命令：
    
        Get-TransportAgent

2.  验证地址重写入站和出站代理的 **Enabled** 属性值是否为您所配置的值。

## 使用命令行管理程序查看地址重写条目

若要查看所有地址重写条目的摘要列表，请运行以下命令。

    Get-AddressRewriteEntry

若要查看地址重写条目的详细信息，请使用以下语法。

    Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List

以下示例显示“Contoso.com 重写为 Northwindtraders.com”地址重写条目的详细信息：

    Get-AddressRewriteEntry "Rewrite Contoso.com to Northwindtraders.com" | Format-List

## 使用命令行管理程序创建地址重写条目

## 重写单个收件人的电子邮件地址

若要重写单个收件人的电子邮件地址，请使用以下语法：

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> [-OutboundOnly <$true | $false>]

以下示例重写收件人 joe@contoso.com 的进入和离开 Exchange 组织的所有邮件的电子邮件地址。重写的出站邮件看起来好像来自 support@nortwindtraders.com。发送到 support@northwindtraders.com 的入站邮件重写为发送到 joe@contoso.com，以发送至相应的收件人（默认情况下，*OutboundOnly* 参数的值为 `$false`）。

    New-AddressRewriteEntry -Name "joe@contoso.com to support@northwindtraders.com" -InternalAddress joe@contoso.com -ExternalAddress support@northwindtraders.com

## 重写单个域或子域中的收件人的电子邮件地址

若要重写单个域或子域中的收件人的电子邮件地址，请使用以下语法：

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> [-OutboundOnly <$true | $false>]

以下示例重写 contoso.com 域中收件人的进入和离开 Exchange 组织的所有邮件的电子邮件地址。重写的出站邮件看起来好像来自 fabrikam.com 域。发送到 fabrikam.com 电子邮件地址的入站邮件重写为发送到 contoso.com，以发送至相应的收件人（默认情况下，*OutboundOnly* 参数的值为 `$false`）。

    New-AddressRewriteEntry -Name "Contoso to Fabrikam" -InternalAddress contoso.com -ExternalAddress fabrikam.com

以下示例重写 sales.contoso.com 子域中收件人发送的离开 Exchange 组织的所有邮件的电子邮件地址。重写的出站邮件看起来好像来自 contoso.com 域。发送到 contoso.com 电子邮件地址的入站邮件不会得到重写。

    New-AddressRewriteEntry -Name "sales.contoso.com to contoso.com" -InternalAddress sales.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

## 重写多个子域中的收件人的电子邮件地址

若要重写某个域及其所有子域中的收件人的电子邮件地址，请使用以下语法。

    New-AddressRewriteEntry -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -OutboundOnly $true [-ExceptionList <domain1,domain2...>]

以下示例重写 contoso.com 域及其所有子域中收件人发送的离开 Exchange 组织的所有邮件的电子邮件地址。重写的出站邮件看起来好像来自 contoso.com 域。发送到 contoso.com 收件人的入站邮件无法重写，因为在 *InternalAddress* 参数中使用了通配符。

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true

以下示例与上一示例类似，不同之处在于现在由 legal.contoso.com 和 corp.contoso.com 子域中的收件人发送的邮件不再会进行重写：

    New-AddressRewriteEntry -Name "Rewrite all contoso.com subdomains except legal.contoso.com and corp.contoso.com" -InternalAddress *.contoso.com -ExternalAddress contoso.com -OutboundOnly $true -ExceptionList legal.contoso.com,corp.contoso.com

## 您如何知道这有效？

若要验证是否已成功创建地址重写条目，请执行以下操作：

1.  运行命令 `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List`，并验证所显示的设置是否为您所配置的设置。

2.  从受到地址重写条目影响的邮箱向外部邮箱发送一封测试邮件。验证测试邮件是否看起来好像来自重写的电子邮件地址。

3.  从外部邮箱回复测试邮件。验证原始邮箱是否收到回复。

## 使用命令行管理程序修改地址重写条目

修改现有地址重写条目和新建地址重写条目时可用的配置选项完全相同。

## 修改单个收件人的地址重写条目

若要修改可重写单个收件人的电子邮件地址的地址重写条目，请使用以下语法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <internal email address> -ExternalAddress <external email address> -OutboundOnly <$true | $false>

以下示例修改单个收件人地址重写条目“joe@contoso.com 重写为 support@nortwindtraders.com”的下列属性：

  - 将外部地址更改为 support@northwindtraders.net。

  - 将地址重写条目的名称更改为“joe@contoso.com 重写为 support@northwindtraders.net”。

  - 将 *OutboundOnly* 的值更改为 `$true`。请注意，此更改要求您将 support@northwindtraders.net 配置为 Joe 的邮箱的代理地址。

<!-- end list -->

    Set-AddressRewriteEntry "joe@contoso.com to support@nortwindtraders.com" -Name "joe@contoso.com to support@northwindtraders.net" -ExternalAddress support@northwindtraders.net -OutboundOnly $true

## 修改单个域或子域中的收件人的地址重写条目

若要修改可重写单个域或子域中的收件人的电子邮件地址的地址重写条目，请使用以下语法。

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress <domain or subdomain> -ExternalAddress <domain> -OutboundOnly <$true | $false>

以下示例更改单个域地址重写条目“Northwind Traders 重写为 Contoso”的内部地址值。

    Set-AddressRewriteEntry "Northwindtraders to Contoso" -InternalAddress northwindtraders.net

## 修改多个子域中的收件人的地址重写条目

若要修改可重写某个域及其所有子域中的收件人的电子邮件地址的地址重写条目，请使用以下语法。

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -Name "<Descriptive Name>" -InternalAddress *.<domain> -ExternalAddress <domain> -ExceptionList <list of domains>

若要替换多个子域地址重写条目的现有例外列表值，请使用以下语法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList <domain1,domain2,...>

以下示例将多个子域地址重写条目“Contoso 重写为 Northwind”的现有例外列表值替换为 marketing.contoso.com 和 legal.contoso.com：

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList sales.contoso.com,legal.contoso.com

若要有选择性地添加或删除多个子域地址重写条目的例外列表值，而不用修改任何现有的例外列表值，请使用以下语法：

    Set-AddressRewriteEntry <AddressRewriteEntryIdentity> -ExceptionList @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

以下示例在多个子域地址重写条目“Contoso 重写为 Northwind Traders”的例外列表中添加 finanace.contoso.com，并从中删除 marketing.contoso.com。

    Set-AddressRewriteEntry "Contoso to Northwind Traders" -ExceptionList @{Add="finanace.contoso.com"; Remove="marketing.contoso.com"}

## 您如何知道这有效？

若要验证是否已成功修改地址重写条目，请执行以下操作：

1.  运行命令 `Get-AddressRewriteEntry <AddressRewriteEntryIdentity> | Format-List`，并验证所显示的设置是否为您所配置的设置。

2.  从受到地址重写条目影响的邮箱向外部邮箱发送一封测试邮件。验证测试邮件是否看起来好像来自重写的电子邮件地址。

3.  从外部邮箱回复测试邮件。验证原始邮箱是否收到回复。

## 使用命令行管理程序删除地址重写条目

若要删除单个地址重写条目，请使用以下语法：

    Remove-AddressRewriteEntry <AddressRewriteEntryIdentity>

以下示例删除名为“Contoso.com 重写为 Northwindtraders.com”的地址重写条目：

    Remove-AddressRewriteEntry "Contoso.com to Northwindtraders.com"

若要删除多个地址重写条目，请使用以下语法：

    Get-AddressRewriteEntry [<search criteria>] | Remove-AddressRewriteEntry [-WhatIf]

以下示例删除所有地址重写条目：

    Get-AddressRewriteEntry | Remove-AddressRewriteEntry

以下示例模拟删除名称中包含“重写为 contoso.com”文本的地址重写条目。通过 *WhatIf* 开关，您可以在不做出任何更改的情况下预览结果。

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry -WhatIf

如果您对结果感到满意，请再次运行不包含 *WhatIf* 开关的命令来删除地址重写条目。

    Get-AddressRewriteEntry "*to contoso.com" | Remove-AddressRewriteEntry

## 您如何知道这有效？

若要验证是否已成功删除地址重写条目，请执行以下操作：

1.  运行命令 `Get-AddressRewriteEntry`，并验证您已删除的地址重写条目是否没有列出。

2.  从受到地址重写条目影响的邮箱向外部邮箱发送一封测试邮件。验证测试邮件不再受到已删除的地址重写条目影响。

3.  从外部邮箱回复测试邮件。验证原始邮箱是否收到回复，并且该邮件是否不受已删除的地址重写条目影响。

