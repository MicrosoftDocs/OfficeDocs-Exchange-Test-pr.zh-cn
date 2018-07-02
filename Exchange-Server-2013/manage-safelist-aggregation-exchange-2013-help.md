---
title: '管理安全列表聚合: Exchange 2013 Help'
TOCTitle: 管理安全列表聚合
ms:assetid: 5ac17168-f411-4cb7-ae98-ebefb865b210
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998280(v=EXCHG.150)
ms:contentKeyID: 50490635
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理安全列表聚合

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

*安全列表聚合*指从 Microsoft Outlook 共享到 Microsoft Exchange Server 2013 的反垃圾邮件功能。此功能从安全收件人列表、安全发件人列表、阻止发件人列表以及 Outlook 用户配置的联系人数据中收集数据，并将这些数据提供给 Exchange 反垃圾邮件代理使用。安全列表聚合可以帮助减少运行反垃圾邮件代理的 Exchange 服务器执行的反垃圾邮件筛选中的误报情况。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;收件人设置权限\&quot;部分，以及[反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;部分。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 请注意在运行 **Update-SafeList** cmdlet 时可能生成的网络和复制通信。如果在大量使用安全列表的多个邮箱中运行该命令，则可能生成大量通信。如果要对多个邮箱运行该命令，则建议您在非通信高峰期或非上班时间运行该命令。

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

## 使用命令行管理程序配置邮箱安全列表集合限制

可以配置用户可配置的最大安全发件人数和阻止发件人数。默认情况下，用户最多可以配置 5000 个安全发件人和 500 个阻止发件人。

若要配置最大安全发件人数和阻止发件人数，请运行以下命令：

    Set-Mailbox <MailboxIdentity> -MaxSafeSenders <Integer> -MaxBlockedSenders <Integer>

本示例将邮箱 john@contoso.com 配置为最多具有 2000 个安全发件人和 200 个阻止发件人。

    Set-Mailbox john@contoso.com -MaxSafeSenders 2000 -MaxBlockedSenders 200

## 您如何知道这有效？

若要验证是否成功配置了邮箱安全列表集合限制，请执行以下操作：

1.  运行以下命令：
    
        Get-Mailbox <Identity> | Format-List Name,Max*Senders

2.  验证显示的值是否与配置的值匹配。

## 使用命令行管理程序运行 Update-Safelist 命令

在 Exchange 2013 中，安全列表聚合是自动执行的，因此无需计划或手动运行 **Update-Safelist** cmdlet。但是，可能需要偶尔运行此 cmdlet 以测试安全列表聚合。

此示例将邮箱 john@contoso.com 的安全发件人列表写入 Active Directory。

    Update-Safelist john@contoso.com -Type SafeSenders

有关语法和参数的详细信息，请参阅 [Update-SafeList](https://technet.microsoft.com/zh-cn/library/bb125034\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功配置了安全列表聚合，请执行以下步骤：

## 步骤 1：使用命令行管理程序验证是否在 Exchange 服务器上启用了内容筛选器代理

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List Enabled

2.  如果输出显示 *Enabled* 参数为 `True`，则已启用内容筛选。如果未启用，请运行以下命令以在 Exchange 服务器上启用内容筛选和内容筛选器代理：
    
        Set-ContentFilterConfig -Enabled $true

## 步骤 2：（可选）使用 ADSI 编辑器验证安全列表聚合数据到边缘传输服务器的复制

仅当在外围网络中的边缘传输服务器上运行内容筛选器代理时，才需要此步骤。

可以查看边缘传输服务器上的 Active Directory 轻型目录服务 (AD LDS) 实例中的用户对象，以验证是否针对用户对象更新了安全列表集合数据以及 Microsoft Exchange EdgeSync 服务是否已将数据复制到 AD LDS 实例。

每个用户对象有三个安全列表集合属性：

  - **msExchSafeRecipientsHash**   此属性存储用户的安全收件人列表集合的哈希值。

  - **msExchSafeSendersHash**   此属性存储用户的安全发件人列表集合的哈希值。

  - **msExchBlockedSendersHash**   此属性存储用户的阻止发件人列表集合的哈希值。

如果属性中出现十六进制字符串（例如，`0xac 0xbd 0x03 0xca`），则说明用户对象已更新。如果属性的值是 `<Not Set>`，则说明该属性未更新。

可以通过使用 AD LDS Active Directory 服务接口 (ADSI) 编辑管理单元来搜索和查看属性。

## 步骤 3：发送测试邮件以验证安全列表聚合是否在正常工作

若要测试安全列表聚合是否在正常工作，需要从安全发件人向自己发送以其他方式会被内容筛选阻止的邮件。如果安全列表聚合在正常工作，则收件箱应当收到该邮件。

1.  找到要使用的现有外部电子邮件帐户，或在基于 Web 的免费电子邮件提供程序上（如 Microsoft Hotmail）创建电子邮件帐户。

2.  在 Microsoft Outlook 中将该帐户添加到安全发件人列表。

3.  使用 **Update-SafeList** cmdlet 可将安全列表集合从该邮箱复制到 Active Directory。

4.  可选：如果在外围网络中的边缘传输服务器上运行内容筛选器代理，请运行 **Start-EdgeSynchronization** cmdlet 以强制进行 EdgeSync 复制。

5.  为内容筛选配置添加一个特定单词，作为阻止短语。有关详细步骤，请参阅[管理内容筛选](manage-content-filtering-exchange-2013-help.md)。

6.  从步骤 1 中的外部电子邮件帐户，向 Exchange 邮箱发送包含在步骤 5 中配置的阻止短语的邮件。
    
    如果该邮件成功传递到收件箱，则表明安全列表聚合在正常工作。

