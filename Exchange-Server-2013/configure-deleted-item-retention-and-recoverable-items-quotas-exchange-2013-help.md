---
title: '配置已删除邮件的保留时间和可恢复邮件配额: Exchange 2013 Help'
TOCTitle: 配置已删除邮件的保留时间和可恢复邮件配额
ms:assetid: de7d667a-1c93-4364-a4f9-2aa5e3678b12
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee364752(v=EXCHG.150)
ms:contentKeyID: 50556689
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置已删除邮件的保留时间和可恢复邮件配额

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

当用户使用 Delete、Shift+Delete 或\&quot;清空已删除邮件文件夹\&quot;操作从\&quot;已删除邮件\&quot;默认文件夹中删除邮件时，这些邮件将移动到\&quot;可恢复邮件\\删除\&quot;文件夹。已删除邮件保留在此文件夹中的持续时间取决于为邮箱数据库或邮箱配置的已删除邮件保留时间设置。默认情况下，将邮箱数据库配置为保留已删除邮件 14 天，将可恢复邮件警告配额和可恢复邮件配额分别设置为 20 GB 和 30 GB。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>已删除的项目经历、 Microsoft Outlook和 Microsoft OfficeOutlook Web App在保留时间之前用户可以通过使用恢复已删除邮件功能恢复已删除的项目。有关这些功能的详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=198206">Outlook</a>或<a href="https://go.microsoft.com/fwlink/p/?linkid=198207">Outlook Web App</a>&quot;恢复已删除邮件&quot;主题。</td>
</tr>
</tbody>
</table>


可以使用命令行管理程序配置已删除邮件保留时间设置以及邮箱或邮箱数据库的可恢复邮件配额。如果对邮箱实施了就地保留或诉讼保留，则将忽略已删除邮件保留设置。

有关已删除邮件保留、\&quot;可恢复邮件\&quot;文件夹、就地保留和诉讼保留的详细信息，请参阅[\&quot;可恢复的项目\&quot;文件夹](recoverable-items-folder-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件传递记录管理\&quot;条目。

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

## 配置邮箱的已删除邮件保留

**使用 EAC 配置邮箱的已删除邮件保留**

1.  导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择一个邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页面上，依次单击\&quot;邮箱使用情况\&quot;和\&quot;更多选项\&quot;，然后选择下列选项之一：
    
      - **使用邮箱数据库中的默认保留设置**   使用此设置可使用为邮箱数据库配置的已删除邮件保留设置。
    
      - **为此邮箱自定义设置**   使用此设置可为邮箱配置已删除邮件保留设置。
        
        \&quot;保留已删除项目的期限(天)\&quot;   此框显示在用户永久删除并且无法恢复项目之前，已删除项目的保留时间长度。在创建邮箱后，该值基于为邮箱数据库配置的已删除项目保留设置。默认情况下，邮箱数据库配置为将已删除项目保留 14 天。此属性的值范围介于 0 到 24,855 天之间。
    
      - **完成对数据库的备份之后才永久删除项目**   选中此复选框可避免在备份此邮箱所在的邮箱数据库之前永久删除邮箱和电子邮件。

**使用命令行管理程序配置邮箱的已删除邮件保留时间**

本示例将 April Stewart 的邮箱配置为保留已删除邮件 30 天。

    Set-Mailbox -Identity - "April Stewart" -RetainDeletedItemsFor 30

有关详细的语法和参数信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序配置邮箱的可恢复邮件配额

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 配置邮箱的可恢复邮件配额。</td>
</tr>
</tbody>
</table>


此示例将 April Stewart 的邮箱的可恢复邮件警告配额配置为 12 GB，将可恢复邮件配额配置为 15 GB。

    Set-Mailbox -Identity "April Stewart" -RecoverableItemsWarningQuota 12GB -RecoverableItemsQuota 15GB -UseDatabaseQuotaDefaults $false

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要将邮箱配置为使用不同于其所在邮箱数据库的可恢复邮件配额，必须将 <em>UseDatabaseQuotaDefaults</em> 参数设置为 <code>$false</code>。</td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序配置邮箱数据库的已删除邮件保留时间

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 配置邮箱数据库的已删除邮件保留。</td>
</tr>
</tbody>
</table>


本示例将邮箱数据库 MDB2 的已删除邮件保留期配置为 10 天。

    Set-MailboxDatabase -Identity MDB2 -DeletedItemRetention 10

有关详细的语法和参数信息，请参阅 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))。

## 使用命令行管理程序配置邮箱数据库的可恢复邮件配额

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能使用 EAC 配置邮箱数据库的可恢复邮件配额</td>
</tr>
</tbody>
</table>


本示例将邮箱数据库 MDB2 上的可恢复邮件警告配额配置为 15 GB，将可恢复邮件配额配置为 20 GB。

    Set-MailboxDatabase -Identity MDB2 -RecoverableItemsWarningQuota 15GB -RecoverableItemsQuota 20GB

有关语法和参数的详细信息，请参阅 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))。

