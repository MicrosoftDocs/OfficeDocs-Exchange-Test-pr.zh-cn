---
title: '为您的组织配置大型受众规模: Exchange Online Help'
TOCTitle: 为您的组织配置大型受众规模
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 50490992
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为您的组织配置大型受众规模

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

可使用 Exchange 命令行管理程序配置各种设置，定义如何在组织中使用邮件提示。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;邮件提示\&quot;条目。

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


## 使用命令行管理程序为组织配置大型受众大小

使用 **Set-OrganizationConfig** cmdlet 为组织配置大型受众大小。如果发件人将邮件发送给收件人的数量多于配置的大小，则会向发件人显示\&quot;大型受众邮件提示\&quot;。默认情况下，大型受众大小设置为 25。本示例在您的组织中将大型受众大小配置为 50。

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

有关语法和参数的详细信息，请参阅 [Set-OrganizationConfig](https://technet.microsoft.com/zh-cn/library/aa997443\(v=exchg.150\))。

