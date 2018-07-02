---
title: '管理管理员审核日志记录: Exchange 2013 Help'
TOCTitle: 管理管理员审核日志记录
ms:assetid: 15c284c0-b8e6-42ca-9913-7c59fdb6885d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335109(v=EXCHG.150)
ms:contentKeyID: 50556529
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理管理员审核日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-05-17_

通过 Microsoft Exchange Server 2013 中的管理员审核日志记录，可以在每次运行指定 cmdlet 时创建一个日志条目。日志条目提供了有关运行的 cmdlet、使用的参数、运行 cmdlet 的用户以及受影响对象的信息。有关管理员审核日志记录的详细信息，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：少于 5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“管理员审核日志记录”条目。

  - 管理员审核日志记录依赖 Active Directory 复制功能将指定的配置设置复制到贵组织中的域控制器。根据复制设置，所做的更改可能不会立即应用于组织中的所有 Exchange 2013 服务器。

  - 在打开了命令行管理程序的计算机上，在对审核日志配置进行更改之后，所做的更改会每隔 60 分钟刷新一次。如果想要立即应用所做的更改，请在每台计算机上关闭并重新打开命令行管理程序。

  - 命令运行后，最多可能需要 15 分钟才会出现在审核日志搜索结果中。这是因为审核日志条目必须先编制索引，然后才能进行搜索。如果命令未显示在管理员审核日志中，请等待几分钟，然后再次运行搜索。

  - 您必须使用命令行管理程序执行这些过程。

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

## 指定要审核的 cmdlet

默认情况下，审核日志记录会为每个运行的 cmdlet 创建日志条目。如果您是第一次启用审核日志记录并且希望执行此行为，则不必更改 cmdlet 审核列表。如果以前指定了要审核的 cmdlet，但现在希望审核所有的 cmdlet，则可以通过在 **Set-AdminAuditLogConfig** cmdlet 上使用 *AdminAuditLogCmdlets* 参数指定星号 (\*) 通配符来审核所有的 cmdlet，如以下命令所示。

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets *

通过使用 *AdminAuditLogCmdlets* 参数提供 cmdlet 列表，可以指定需要审核的 cmdlet。提供要审核的 cmdlet 列表时，可以提供单个 cmdlet、带有星号 (\*) 通配符的 cmdlet，或这两者的混合。列表中的每个条目都以逗号分隔。以下所有值均有效：

  - `New-Mailbox`

  - `*TransportRule`

  - `*Management*`

  - `Set-Transport*`

此示例审核前面列表中指定的 cmdlet。

    Set-AdminAuditLogConfig -AdminAuditLogCmdlets New-Mailbox, *TransportRule, *Management*, Set-Transport*

有关详细的语法和参数信息，请参阅 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-cn/library/dd298169\(v=exchg.150\))。

## 指定要审核的参数

默认情况下，审核日志记录会为每个运行的 cmdlet 创建日志条目，无需考虑指定的参数。如果您是第一次启用审核日志记录并且希望执行此行为，则不必更改参数审核列表。如果以前指定了要审核的参数，但现在希望审核所有的参数，则可以通过在 **Set-AdminAuditLogConfig** cmdlet 上使用 *AdminAuditLogParameters* 参数指定星号 (\*) 通配符来审核所有的参数，如以下命令所示。

    Set-AdminAuditLogConfig -AdminAuditLogParameters *

可以使用 *AdminAuditLogParameters* 参数指定要审核的参数。提供参数列表进行审核时，可以提供单个参数、带有星号 (\*) 通配符的参数，或两者的混合。列表中的每个条目都以逗号分隔。以下所有值均有效：

  - `Database`

  - `*Address*`

  - `Custom*`

  - `*Region`

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要在运行某个命令时创建审核日志条目，则该命令必须至少包括一个或多个参数，这些参数存在于使用 <em>AdminAuditLogCmdlets</em> 参数指定的至少一个或多个 cmdlet 上。</td>
</tr>
</tbody>
</table>


此示例审核前面列表中指定的参数。

    Set-AdminAuditLogConfig -AdminAuditLogParameters Database, *Address*, Custom*, *Region

有关语法和参数的详细信息，请参阅 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-cn/library/dd298169\(v=exchg.150\))。

## 指定审核日志期限

审核日志期限确定审核日志条目将保留多长时间。当日志条目超过此期限时，系统将删除该日志条目。默认为 90 天。

可以指定审核日志条目应保留的天数、小时数、分钟数和秒数。若要指定值，请使用格式 dd.hh.mm:ss，其中应用了以下条件：

  - **dd**   保留审核日志条目的天数

  - **hh**   保留审核日志条目的小时数

  - **mm**   保留审核日志条目的分钟数

  - **ss**   保留审核日志条目的秒数

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以将审核日志期限设置为小于当前期限的值。如果您这样做，则会删除寿命超过新期限的所有审核日志条目。<br />
如果将期限设置为 0，则 Exchange 会删除审核日志中的所有条目。<br />
建议您仅向高度信任的用户授予配置审核日志期限的权限。</td>
</tr>
</tbody>
</table>


此示例指定两年零六个月的期限。

    Set-AdminAuditLogConfig -AdminAuditLogAgeLimit 913.00:00:00

有关语法和参数的详细信息，请参阅 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-cn/library/dd298169\(v=exchg.150\))。

## 启用或禁用 Test cmdlet 的日志记录

默认情况下，不记录以谓词 **Test** 开头的 cmdlet。这是因为 **Test** cmdlet 可能会在短时间内生成大量数据。只能在短时间内启用 **Test** cmdlet 的日志记录。

此命令启用 **Test** cmdlet 的日志记录。

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $True

此命令禁用 **Test** cmdlet 的日志记录。

    Set-AdminAuditLogConfig -TestCmdletLoggingEnabled $False

有关语法和参数的详细信息，请参阅 [Set-AdminAuditLogConfig](https://technet.microsoft.com/zh-cn/library/dd298169\(v=exchg.150\))。

## 禁用管理员审核日志记录

若要禁用管理员审核日志记录，请使用以下命令。

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $False

## 启用管理员审核日志记录

若要启用管理员审核日志记录，请使用以下命令。

    Set-AdminAuditLogConfig -AdminAuditLogEnabled $True

## 查看管理员审核日志记录设置

若要查看已为组织配置的管理员审核日志记录设置，请使用以下命令。

    Get-AdminAuditLogConfig

