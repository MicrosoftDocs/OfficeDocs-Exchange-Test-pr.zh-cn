---
title: '管理内容筛选: Exchange 2013 Help'
TOCTitle: 管理内容筛选
ms:assetid: 05bd9d39-81dc-4514-8b75-7be386d5bcad
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995953(v=EXCHG.150)
ms:contentKeyID: 50489859
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理内容筛选

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

内容筛选由内容筛选器代理提供。内容筛选器代理会筛选通过 Exchange 服务器上的所有接收连接器传入的所有邮件。只会筛选从未进行身份验证的来源发来的邮件。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用内容筛选

若要禁用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -Enabled $false

要启用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -Enabled $true

> [!NOTE]  
> 当禁用内容筛选时，仍会启用基础内容筛选器代理。若要禁用内容筛选器代理，请运行命令：<code>Disable-TransportAgent &quot;Content Filter Agent&quot;</code>.


## 您如何知道这有效？

若要验证是否成功启用或禁用了内容筛选，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List Enabled

2.  验证显示的 *Enabled* 属性的值。

## 使用命令行管理程序对外部邮件启用或禁用内容筛选

默认情况下，将对外部邮件启用内容筛选功能。

若要对外部邮件禁用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -ExternalMailEnabled $false

若要对外部邮件启用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -ExternalMailEnabled $true

## 您如何知道这有效？

若要验证是否对外部邮件成功启用或禁用了内容筛选，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List ExternalMailEnabled

2.  验证显示的 *ExternalMailEnabled* 属性的值。

## 使用命令行管理程序对内部邮件启用或禁用内容筛选

最佳的做法是不筛选来自受信任伙伴或组织内部的邮件。运行反垃圾邮件筛选器时，经常出现筛选器误报的可能。若要降低筛选器错误处理合法电子邮件的可能性，应仅针对有可能来自不可信源和未知源的邮件运行反垃圾邮件代理。

若要对内部邮件启用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -InternalMailEnabled $true

若要对内部邮件禁用内容筛选，请运行以下命令：

    Set-ContentFilterConfig -InternalMailEnabled $false

## 您如何知道这有效？

若要验证是否对内部邮件成功启用或禁用了内容筛选，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List InternalMailEnabled

2.  验证显示的 *InternalMailEnabled* 属性的值。

## 使用命令行管理程序配置收件人和发件人例外

要替换现有值，请运行以下命令：

    Set-ContentFilterConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenders <sender1,sender2...> -BypassedSenderDomains <domain1,domain2...>

本示例在内容筛选中配置以下例外：

  - 内容筛选不会检查收件人 laura@contoso.com 和 julia@contoso.com。

  - 内容筛选不会检查发件人 steve@fabrikam.com 和 cindy@fabrikam.com。

  - 内容筛选不会检查域 nwtraders.com 及所有子域中的所有发件人。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients laura@contoso.com,julia@contoso.com -BypassedSenders steve@fabrikam.com,cindy@fabrikam.com -BypassedSenderDomains *.nwtraders.com

要在不修改任何现有值的情况下添加或删除条目，请运行以下命令：

    Set-ContentFilterConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

本示例在内容筛选中配置以下例外：

  - 将 tiffany@contoso.com 和 chris@contoso.com 添加到内容筛选不检查的现有收件人列表中。

  - 将 joe@fabrikam.com 和 michelle@fabrikam.com 添加到内容筛选不检查的现有发件人列表中。

  - 将 blueyonderairlines.com 添加到内容筛选不检查其发件人的现有域列表中。

  - 从内容筛选不检查其发件人的现有域列表中删除域 woodgrovebank.com 及所有子域。

<!-- end list -->

    Set-ContentFilterConfig -BypassedRecipients @{Add="tiffany@contoso.com","chris@contoso.com"} -BypassedSenders @{Add="joe@fabrikam.com","michelle@fabrikam.com"} -BypassedSenderDomains @{Add="blueyonderairlines.com"; Remove="*.woodgrovebank.com"}

## 您如何知道这有效？

若要验证是否成功配置了收件人和发件人例外，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List Bypassed*

2.  验证显示的值是否与指定的设置匹配。

## 使用命令行管理程序配置允许的和阻止的短语

若要添加允许和阻止的词语和短语，请运行以下命令：

    Add-ContentFilterPhrase -Influence GoodWord -Phrase <Phrase> -Influence BadWord -Phrase <Phrase>

本示例允许所有包含短语\&quot;customer feedback\&quot;的邮件。

    Add-ContentFilterPhrase -Influence GoodWord -Phrase "customer feedback"

本示例阻止所有包含短语\&quot;stock tip\&quot;的邮件。

    Add-ContentFilterPhrase -Influence BadWord -Phrase "stock tip"

若要删除允许或阻止的短语，请运行以下命令：

    Remove-ContentFilterPhrase -Phrase <Phrase>

本示例删除短语\&quot;stock tip\&quot;：

    Remove-ContentFilterPhrase -Phrase "stock tip"

## 您如何知道这有效？

若要验证是否成功配置了允许和阻止的短语，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterPhrase | Format-List Influence,Phrase

2.  验证显示的值是否与指定的设置匹配。

## 使用命令行管理程序配置 SCL 阈值

若要配置垃圾邮件可信度 (SCL) 阈值和操作，请运行以下命令：

    Set-ContentFilterConfig -SCLDeleteEnabled <$true | $false> -SCLDeleteThreshold <Value> -SCLRejectEnabled <$true | $false> -SCLRejectThreshold <Value> -SCLQuarantineEnabled <$true | $false> -SCLQuarantineThreshold <Value>

> [!NOTE]  
> 删除操作优先于拒绝操作，拒绝操作优先于隔离操作。因此，删除操作的 SCL 阈值应大于拒绝操作的 SCL 阈值，拒绝操作的 SCL 阈值又应大于隔离操作的 SCL 阈值。默认情况下仅启用拒绝操作，其 SCL 阈值为 7。


本示例为 SCL 阈值配置以下值：

  - 启用删除操作，并且对应 SCL 阈值设置为 9。

  - 启用拒绝操作，并且对应 SCL 阈值设置为 8。

  - 启用隔离操作，并且对应 SCL 阈值设置为 7。

<!-- end list -->

    Set-ContentFilterConfig -SCLDeleteEnabled $true -SCLDeleteThreshold 9 -SCLRejectEnabled $true -SCLRejectThreshold 8 -SCLQuarantineEnabled $true -SCLQuarantineThreshold 7

## 您如何知道这有效？

若要验证是否成功配置了 SCL 阈值，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List SCL*

2.  验证显示的值是否与指定的设置匹配。

## 使用命令行管理程序配置拒绝响应

当启用拒绝操作时，可以自定义发送给邮件发件人的拒绝响应。拒绝响应不能超过 240 个字符。

若要配置自定义拒绝响应，请运行以下命令：

    Set-ContentFilterConfig -RejectionResponse "<Custom Text>"

本示例配置内容筛选器代理以发送自定义拒绝响应。

    Set-ContentFilterConfig -RejectionResponse "Your message was rejected because it appears to be SPAM."

## 您如何知道这有效？

若要验证是否成功配置了拒绝响应，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List *Reject*

2.  验证显示的值是否与指定的设置匹配。

## 使用命令行管理程序启用或禁用 Outlook 电子邮件邮戳

\&quot;Outlook 电子邮件邮戳\&quot;验证是 Microsoft Office 应用于传出邮件的一个计算证据，用于帮助收件人邮件系统区分合法电子邮件和垃圾邮件。在 Outlook 2007 或更新版本中提供了邮戳功能。邮戳可帮助减少误报。默认情况下会启用 Outlook 电子邮件邮戳。

若要禁用 Outlook 电子邮件邮戳，请运行以下命令：

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $false

若要启用 Outlook 电子邮件邮戳，请运行以下命令：

    Set-ContentFilterConfig -OutlookEmailPostmarkValidationEnabled $true

## 您如何知道这有效？

若要验证是否成功配置了 Outlook 电子邮件邮戳，请执行以下操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List OutlookEmailPostmarkValidationEnabled

2.  验证显示的值是否与指定的设置匹配。

