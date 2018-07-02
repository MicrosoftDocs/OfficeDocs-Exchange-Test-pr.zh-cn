---
title: '转换邮箱: Exchange 2013 Help'
TOCTitle: 转换邮箱
ms:assetid: dfed045e-a740-4a90-aff9-c58d53592f79
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ710164(v=EXCHG.150)
ms:contentKeyID: 50491805
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 转换邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-04-26_

将邮箱转换为其他类型的邮箱与在 Exchange 2010 中的体验非常相似。仍必须使用 Shell 中的 Set-Mailbox cmdlet 来执行转换。

可以将以下邮箱从一种类型转换为另一种类型：

  - 用户邮箱转换为资源（会议室或设备）邮箱

  - 共享邮箱转换为用户邮箱

  - 共享邮箱转换为资源邮箱

  - 资源邮箱转换为用户邮箱

  - 资源邮箱转换为共享邮箱

注意：如果组织使用混合 Exchange 环境，你需要通过使用本地 Exchange 管理工具来管理邮箱。要在混合环境中转换邮箱，你可能需要将邮箱移回本地 Exchange，转换邮箱类型，然后将邮箱移回 Office 365。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果将用户邮箱转换为共享邮箱，应在转换前从邮箱删除任何移动设备，或应在转换后阻止移动访问邮箱。这是因为将邮箱转换为共享邮箱后，移动功能将无法正常使用。有关阻止访问的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=847873">从 Office 365 中删除以前的员工</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序转换邮箱

估计完成时间：5 分钟。

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

本示例将共享邮箱 MarketingDept1 转换为用户邮箱。

    Set-Mailbox MarketingDept1 -Type Regular

可以为 *Type* 参数使用如下值：

  - Regular

  - Room

  - Equipment

  - Shared

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功转换了邮箱，可运行以下命令行管理程序命令：

    Get-Mailbox -Identity MarketingDept1 | Format-List RecipientTypeDetails

*RecipientTypeDetails* 的值应为 *UserMailbox*。

有关语法和参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

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

