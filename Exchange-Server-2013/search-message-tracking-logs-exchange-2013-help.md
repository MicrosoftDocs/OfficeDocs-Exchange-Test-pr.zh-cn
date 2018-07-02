---
title: '搜索邮件跟踪日志: Exchange 2013 Help'
TOCTitle: 搜索邮件跟踪日志
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51408284
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 搜索邮件跟踪日志

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-25_

在 Microsoft Exchange Server 2013 中，邮件跟踪日志详细记录了邮件从邮箱服务器上的传输服务、邮箱服务器上的邮箱和边缘传输服务器来回传输产生的所有邮件活动。

您可以使用 Exchange 命令行管理程序中的 **Get-MessageTrackingLog** cmdlet 通过具体的搜索条件来搜索邮件跟踪日志条目。

## 在开始之前，您需要知道什么？

  - 估计完成时间：30 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“邮件跟踪”条目。

  - 必须运行 Microsoft Exchange 传输日志搜索服务才能搜索邮件跟踪日志。如果您禁用或停止运行此服务，则无法搜索邮件跟踪日志或生成送达报告。但是，停止运行此服务不会影响 Exchange 的其他功能。

  - **Get-MessageTrackingLog** cmdlet 的结果中显示的字段名称类似于邮件跟踪日志中使用的实际字段名称。最大的区别在于：
    
      - 字段名称中没有短划线。例如 **internal-message-id** 显示为 `InternalMessageId`。
    
      - **date-time** 字段显示为 `Timestamp`。
    
      - **recipient-address** 字段显示为 `Recipients`。
    
      - **sender-address** 字段显示为 `Sender`。

  - 邮件跟踪日志中的 **date-time** 字段以协调世界时 (UTC) 格式存储信息。但是，您应该使用用于执行搜索的计算机上的区域日期-时间格式输入 *Start* 或 *End* 参数的日期-时间搜索条件。

  - 您无法复制其他 Exchange 服务器上的邮件跟踪日志并使用 **Get-MessageTrackingLog** cmdlet 进行搜索。此外，如果您手动保存一个现有的邮件跟踪日志文件，那么该文件的日期-时间时间戳的变化会破坏 Exchange 用来搜索邮件跟踪日志的查询逻辑。

  - Exchange 2013**Get-MessageTrackingLog** cmdlet 能够在同一 Active Directory 站点中的 Exchange 2007 和 Exchange 2010 服务器上搜索邮件跟踪日志。

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


## 要执行什么操作？

## 使用命令行管理程序搜索邮件跟踪日志

若要搜索具体事件的邮件跟踪日志条目，请使用下列语法：

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

若要查看服务器上的 1000 条最新邮件跟踪日志条目，请运行下列命令：

    Get-MessageTrackingLog

本示例为 **FAIL** 事件（其中邮件发件人为 pat@contoso.com）搜索本地服务器上介于 2013 年 3 月 28 日上午 8:00 到 2013 年 3 月 28 日下午 5:00 之间的所有邮件跟踪日志条目。

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## 使用命令行管理程序控制邮件跟踪日志搜索输出

使用下列语法：

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

本示例使用下列搜索条件搜索邮件跟踪日志：

  - 返回前 1000 个 **Send** 事件的结果。

  - 结果通过列表格式显示。

  - 只显示以 `Send` 或 `Recipient` 开头的字段名称。

  - 将输出结果写入名为 `D:\Send Search.txt` 的新文件。

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## 使用命令行管理程序搜索多个服务器上的邮件跟踪日志条目

一般来说，**MessageID:** 头字段中的值在邮件通过整个 Exchange 组织的过程中保持不变。此属性在队列视图实用工具中名为 **InternetMessageId**，而在邮件跟踪日志视图实用工具中名为 **MessageId**。在您确定某邮件的 `MessageID:` 值后，就可以在 Exchange 组织中每台邮箱服务器上的邮件跟踪日志中搜索该邮件的信息。

若要搜索某邮件在所有邮箱服务器上的全部邮件跟踪日志条目，请使用下列语法：

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

本示例使用下列搜索条件搜索所有 Exchange 2013 邮箱服务器上的邮件跟踪日志：

  - 查找与包含 **MessageID:** 值 `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>` 的邮件有关的所有条目。请注意，您可以省略尖括号字符 (`<``>`)。如果不省略，您需要在整个 **MessageID:** 值的两边添加引号。

  - 对于每个条目，系统都显示字段 **date-time**、**server-hostname**、**client-hostname**、**source**、**event-id** 和 **recipient-address**。

  - 按 **date-time** 字段对结果进行排序。

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## 使用 EAC 搜索邮件跟踪日志

您可以使用 Exchange 管理中心 (EAC) 中的送达报告（管理员功能）搜索邮件跟踪日志中有关组织中特定邮箱发送或接收的邮件的信息。有关详细信息，请参阅[使用送达报告跟踪邮件](track-messages-with-delivery-reports-exchange-2013-help.md)。

