---
title: '断开连接的邮箱: Exchange 2013 Help'
TOCTitle: 断开连接的邮箱
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50556567
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 断开连接的邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

每个 Microsoft Exchange 邮箱都由 Active Directory 用户帐户以及存储在 Exchange 邮箱数据库中的邮箱数据组成。邮箱的所有配置数据都存储在 Active Directory 用户对象的 Exchange 属性中。邮箱数据库中包含与用户帐户关联的邮箱中的邮件数据。下图显示了邮箱的各个组件。

**邮箱组件**

![组成邮箱的部分](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "组成邮箱的部分")

*断开连接的邮箱*是邮箱数据库中不与 Active Directory 用户帐户关联的邮箱对象。有两种类型的断开连接的邮箱：

  - **禁用的邮箱**   在 Exchange 管理中心 (EAC) 或在 Exchange 命令行管理程序中使用 **Disable-Mailbox** 或 **Remove-Mailbox** cmdlet 禁用或删除邮箱时，Exchange 会将已删除的邮箱保留在邮箱数据库中，然后将此邮箱切换到禁用状态。这就是为什么已禁用或删除的邮箱称为*禁用的邮箱*。但不同的是，在您禁用邮箱时，将从对应的 Active Directory 用户帐户中删除 Exchange 属性，但保留此用户帐户。而删除邮箱之后，Exchange 属性和 Active Directory 用户帐户均会删除。
    
    禁用和删除的邮箱保留在邮箱数据库中，直到已删除的邮箱保留期过期（默认为 30 天）。在保留期过期后，此邮箱将被永久删除（也称为*清除*）。如果使用 **Remove-Mailbox** cmdlet 删除邮箱，它也会在保留期加以保留。
    
    > [!IMPORTANT]  
    > 如果使用 <strong>Remove-Mailbox</strong> cmdlet 和 <em>Permanent</em> 或 <em>StoreMailboxIdentity</em> 参数删除邮箱，则该邮箱将立即从邮箱数据库中删除。
    
    要确定您组织中已禁用的邮箱，请在命令行管理程序中运行以下命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **软删除邮箱**   在将邮箱移动到不同的邮箱数据库时，移动完成后，Exchange 无法从源邮箱数据库完全删除邮箱。而是将源邮箱数据库中的邮箱切换为*软删除*状态。与禁用的邮箱类似，软删除邮箱将保留在源数据库中，直到已删除邮箱保留期过期或直到使用 **Remove-StoreMailbox** cmdlet 清除此邮箱。
    
    运行以下命令，以确定您的组织中的软删除邮箱。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**目录**

处理已禁用邮箱

处理已禁用的存档邮箱

处理软删除的邮箱

处理已断开连接的邮箱的摘要信息

已断开连接的邮箱文档

## 处理已禁用邮箱

您可以先对禁用的邮箱执行几项操作，之后再从邮箱数据库中将其清除：

  - 重新将其连接到相同的用户帐户。

  - 将其连接到没有启用邮件的不同用户帐户，这意味着此用户帐户没有邮箱。

  - 将其还原到一个具有现有邮箱的用户帐户。例如，如果删除了邮箱的用户具有新邮箱，则可以将用户的禁用邮箱还原到其新邮箱。

  - 将其从 Exchange 邮箱数据库中永久删除。

## 连接或还原已禁用邮箱

方案是，您要在邮箱保留期限过期之前或将其永久删除之前，连接或还原已禁用邮箱：

  - 您已禁用邮箱，现在想要将该邮箱重新连接到同一 Active Directory 用户帐户。

  - 您使用 EAC 或 [Remove-Mailbox](https://technet.microsoft.com/zh-cn/library/aa995948\(v=exchg.150\)) cmdlet 删除了邮箱，但现在想要将该邮箱重新连接到另一个 Active Directory 用户帐户。

  - 您已删除了邮箱，但现在希望将该邮箱还原到现有邮箱。例如，如果删除了邮箱的用户具有新邮箱，则可以将用户的禁用邮箱还原到其新邮箱。

  - 您希望将用户邮箱转换为与您的 Exchange 组织所在的林外部的某个用户帐户相关联的链接邮箱。希望将邮箱与外部帐户关联的情况可用资源林方案为例。在此方案中， Exchange 林中的用户对象具有邮箱，但这些用户对象已被禁用，无法登录。必须将 Exchange 林中的某个邮箱与外部帐户林中的某个用户帐户相关联。

您可以使用两种方法重新连接或还原已禁用的邮箱。第一种方法是使用 EAC 或 **Connect-Mailbox** cmdlet 将已禁用邮箱连接到某个用户帐户。要了解重新连接已禁用邮箱的步骤，请参阅[连接禁用的邮箱](connect-a-disabled-mailbox-exchange-2013-help.md)。

第二种方法是使用 **New-MailboxRestoreRequest** cmdlet 将已禁用邮箱的内容与现有邮箱合并。此 cmdlet 使用邮箱复制服务 (MRS) 还原此邮箱。要了解还原已禁用邮箱的步骤，请参阅[连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)。

## 永久删除已禁用邮箱

如前所述， Exchange 会根据为邮箱数据库配置的已删除邮箱保留设置，在该邮箱数据库中保留禁用的邮箱。在指定的保留期限过后，将从 Exchange 邮箱数据库中永久清除已禁用的邮箱。您也可以通过使用 **Remove-StoreMailbox** cmdlet 永久删除已禁用的邮箱，并从该邮箱数据库中删除其所有邮件内容。在已禁用邮箱被自动清除或由管理员永久删除之后，该邮箱中的数据将永久丢失，无法恢复。

有关详细信息，请参阅[永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)。

处理已禁用邮箱

## 处理已禁用的存档邮箱

存档邮箱在被禁用后将变为断开连接状态。与已禁用的主邮箱类似的是，可使用 **Connect-Mailbox** cmdlet 和 *Archive* 参数连接已断开的存档邮箱。

主邮箱和存档邮箱共享同一个旧版可分辨名称 (DN)，所以必须将存档邮箱连接到它之前连接的同一用户邮箱。无法将存档邮箱连接到其他用户邮箱。

您可以对已断开连接的存档邮箱执行两个操作：

  - **将其连接到现有主邮箱**   与已断开连接的主邮箱类似，已断开连接的存档邮箱将保留在邮箱数据库中，直到已删除的邮箱保留期过期（默认为 30 天）。在此期间，您可以通过将存档邮箱重新连接到它在被禁用前所连接的同一用户帐户，恢复存档邮箱。
    
    > [!NOTE]  
    > 如果对用户邮箱禁用存档邮箱，然后再对该相同用户启用存档邮箱，则用户邮箱将获取一个新的存档邮箱。尽管可以使用 <strong>Connect-Mailbox</strong> cmdlet 将主邮箱连接到用户，但您必须使用 <strong>Enable-Mailbox</strong> cmdlet 将禁用的存档邮箱连接到现有邮箱。
    
    有关详细信息，请参阅[在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。

  - **从 Exchange 邮箱数据库中永久删除**    Exchange 将根据为邮箱数据库配置的已删除邮箱保留设置，保留已断开连接的存档邮箱。默认保留期为 30 天。在指定的邮箱保留期限过后，将从 Exchange 邮箱数据库中清除已断开连接的存档邮箱。
    
    与已禁用主邮箱类似，您可以通过使用 **Remove-StoreMailbox** cmdlet 在任意时间永久删除已禁用的存档邮箱。有关详细信息，请参阅[永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)。

处理已禁用邮箱

## 处理软删除的邮箱

将邮箱从一个 Exchange 邮箱数据库移至任何其他邮箱数据库时，就会创建软删除的邮箱。为防止在会导致目标数据库上的邮箱发生故障的邮箱移动操作期间出现错误，移动邮箱之后，Exchange 不会从源数据库中完全删除该邮箱。您始终可以还原源邮箱并重试。Exchange 将在整个邮箱保留期内保留软删除的邮箱。

您可以对软删除的邮箱执行两个操作：

  - 将其还原到现有邮箱中。

  - 将其从 Exchange 邮箱数据库中永久删除。

还原和永久删除软删除的邮箱的过程与已禁用邮箱的过程类似。有关详细信息，请参阅下列主题：

  - [还原软删除的邮箱](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

处理已禁用邮箱

## 处理已断开连接的邮箱的摘要信息

下表汇总了有关已断开连接的邮箱的信息，包括如何断开邮箱连接，在断开邮箱连接时对应的 Active Directory 用户帐户会发生什么问题，以及您连接或还原已断开连接的邮箱所必须使用的选项和工具。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>如何禁用邮箱</th>
<th><em>DisconnectReason</em> 属性的值</th>
<th>是否保留 Active Directory用户帐户？</th>
<th>连接或还原选项</th>
<th>工具</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>EAC：“收件人”&gt;“邮箱”&gt;“禁用”</p></li>
<li><p>命令行管理程序：<strong>Disable-Mailbox</strong> cmdlet</p></li>
</ul></td>
<td><p>已禁用</p></td>
<td><p>是</p></td>
<td><p>连接到同一用户帐户</p></td>
<td><ul>
<li><p>EAC：“收件人”&gt;“邮箱”&gt;“连接邮箱”</p></li>
<li><p>命令行管理程序：<strong>Connect-Mailbox</strong> cmdlet</p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>EAC：“收件人”&gt;“邮箱”&gt;“删除”</p></li>
<li><p>命令行管理程序：<strong>Remove-Mailbox</strong> cmdlet</p></li>
</ul></td>
<td><p>已禁用</p></td>
<td><p>否</p></td>
<td><ul>
<li><p>连接到不同的用户帐户</p></li>
<li><p>还原到不同的邮箱</p></li>
</ul></td>
<td><ul>
<li><p>EAC：“收件人”&gt;“邮箱”&gt;“连接邮箱”</p></li>
<li><p>命令行管理程序：<strong>Connect-Mailbox</strong> cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>命令行管理程序：<strong>New-MailboxRestore</strong> cmdlet</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>已移动到不同的邮箱数据库</p></td>
<td><p>软删除</p></td>
<td><p>是</p></td>
<td><ul>
<li><p>连接到不同的用户帐户</p></li>
<li><p>还原到不同的邮箱</p></li>
</ul></td>
<td><ul>
<li><p>EAC：“收件人”&gt;“邮箱”&gt;“连接邮箱”</p></li>
<li><p>命令行管理程序：<strong>Connect-Mailbox</strong> cmdlet</p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>命令行管理程序：<strong>New-MailboxRestore</strong> cmdlet</p></li>
</ul></td>
</tr>
</tbody>
</table>


处理已禁用邮箱

## 已断开连接的邮箱文档

下表包含指向将帮助您管理已断开连接的邮箱的主题的链接。这包含管理已断开连接的用户邮箱、链接的邮箱、资源邮箱和共享邮箱。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">禁用或删除邮箱</a></p></td>
<td><p>了解如何禁用或删除邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">连接禁用的邮箱</a></p></td>
<td><p>了解如何将已禁用邮箱连接到现有用户帐户。</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">连接或还原已删除的邮箱</a></p></td>
<td><p>了解如何将已删除邮箱连接到某个用户帐户，或将已删除邮箱的内容还原到现有邮箱。</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">还原软删除的邮箱</a></p></td>
<td><p>了解如何将软删除邮箱连接到某个用户帐户，或将软删除邮箱还原到现有邮箱。</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">管理邮箱还原请求</a></p></td>
<td><p>了解如何使用命令行管理程序管理邮箱还原请求。</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">永久删除邮箱</a></p></td>
<td><p>了解如何永久删除邮箱。</p></td>
</tr>
</tbody>
</table>


处理已禁用邮箱

