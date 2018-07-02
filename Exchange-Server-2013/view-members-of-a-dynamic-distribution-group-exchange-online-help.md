---
title: '查看动态通讯组的成员: Exchange Online Help'
TOCTitle: 查看动态通讯组的成员
ms:assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232019(v=EXCHG.150)
ms:contentKeyID: 50489653
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看动态通讯组的成员

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2018-03-02_

动态通讯组是其成员基于特定的收件人筛选器而非定义的一组收件人的通讯组。MicrosoftExchange 提供固有筛选器，以使为动态通讯组创建收件人筛选器更加方便。*固有筛选器*是一种常用的筛选器，可用来满足各种收件人筛选标准。可以指定要包括在动态通讯组中的收件人类型。此外，还可以指定收件人必须满足的条件列表。你可以使用命令行管理程序预览使用固有筛选器的动态通讯组的收件人列表。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;动态通讯组\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序预览动态通讯组的成员列表

本示例返回名为全职员工的动态通讯组的成员的列表。第一个命令将动态通讯组对象存储在变量`$FTE`中。第二个命令使用**Get-Recipient** cmdlet 列出为动态通讯组定义的条件相匹配的收件人。

    $FTE = Get-DynamicDistributionGroup "Full Time Employees"

    Get-Recipient -RecipientPreviewFilter $FTE.RecipientFilter -OrganizationalUnit $FTE.RecipientContainer

有关语法和参数的详细信息，请参阅 [Get-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124762\(v=exchg.150\)) 和 [Get-Recipient](https://technet.microsoft.com/zh-cn/library/aa996921\(v=exchg.150\))。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>您不能通过 EAC 查看动态通讯组的成员。</td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

要验证您已经成功地查看动态通讯组的成员，请执行以下操作：

  - 在命令行管理程序中，运行前面的命令预览动态通讯组成员列表之后，会返回一个成员列表。例如，如果你创建的新用户邮箱的属性与动态通讯组的收件人筛选器相匹配，则该新用户应显示在组成员列表中。

