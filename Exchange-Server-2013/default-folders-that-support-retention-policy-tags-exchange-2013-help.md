---
title: '支持保留策略标记的默认文件夹: Exchange 2013 Help'
TOCTitle: 支持保留策略标记的默认文件夹
ms:assetid: d2e2064f-4102-4018-b688-504d09da6d39
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn783294(v=EXCHG.150)
ms:contentKeyID: 62835915
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 支持保留策略标记的默认文件夹

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2017-04-20_

您可以使用[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)来管理电子邮件生命周期。保留策略包含保留标记，您可以使用这些设置指定邮件应在何时自动移动到存档或应在何时删除。

保留策略标记 (RPT) 是保留标记的一种类型，您可以应用于邮箱中的默认文件夹，例如**“收件箱”**和**“已删除邮件”**。

![创建保留策略标记 (RPT)](images/Dn783294.b59a96fd-94e1-4c9b-bff6-97a1bd98dfe7(EXCHG.150).png "创建保留策略标记 (RPT)")

## 受支持的默认文件夹

可以为下表中显示的默认文件夹创建 RPT。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件夹名</th>
<th>详细信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存档</p></td>
<td><p>此文件夹是在 Outlook 中使用“存档”按钮存档的邮件的默认目标。存档功能为用户提供了一种从其收件箱中移除邮件而不删除邮件的快速方式。</p>
<p>此 RPT 仅适用于 Exchange Online。</p></td>
</tr>
<tr class="even">
<td><p>日历</p></td>
<td><p>此默认文件夹用于存储会议和约会。</p></td>
</tr>
<tr class="odd">
<td><p>待筛选邮件</p></td>
<td><p>此文件夹中包含低优先级电子邮件。待筛选邮件功能会查看您以往执行的操作，以确定您最有可能忽略的邮件。然后，它会将这些邮件移到“待筛选邮件”文件夹中。</p></td>
</tr>
<tr class="even">
<td><p>会话历史记录</p></td>
<td><p>此文件夹由 Microsoft Lync（以前称为 Microsoft Office Communicator）创建。虽然未被 Outlook 视为默认文件夹，但是此文件夹会被 Exchange 视为特殊文件夹，可以应用 RPT。</p></td>
</tr>
<tr class="odd">
<td><p>已删除邮件</p></td>
<td><p>此默认文件夹用于存储从邮箱中其他文件夹删除的项目。Outlook 和 Outlook Web App 用户可以手动清空此文件夹。用户还可以将 Outlook 配置为在关闭 Outlook 时清空此文件夹。</p></td>
</tr>
<tr class="even">
<td><p>草稿</p></td>
<td><p>此默认文件夹用于存储用户尚未发送的草稿邮件。Outlook Web App 还使用此文件夹保存用户已发送但是未提交给集线器传输服务器的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>收件箱</p></td>
<td><p>此默认文件夹用于存储传递给邮箱的邮件。</p></td>
</tr>
<tr class="even">
<td><p>日记</p></td>
<td><p>此默认文件夹包含由用户选择的操作。这些操作由 Outlook 自动记录，放置在一个时间线视图中。</p></td>
</tr>
<tr class="odd">
<td><p>垃圾邮件</p></td>
<td><p>此默认文件夹用于保存由 Exchange 服务器上的内容筛选器或 Outlook 中的反垃圾邮件筛选器标记为垃圾邮件的邮件。</p></td>
</tr>
<tr class="even">
<td><p>注释</p></td>
<td><p>此文件夹包含用户在 Outlook 中创建的备注。这些备注还会显示在 Outlook Web App 中。</p></td>
</tr>
<tr class="odd">
<td><p>发件箱</p></td>
<td><p>此默认文件夹用于临时存储用户发送的邮件，直至这些邮件提交给集线器传输服务器。已发送邮件的副本会保存在“已发送邮件”默认文件夹中。由于邮件通常在此文件夹中只会保留一小段时间，因此不必为此文件夹创建 RPT。</p></td>
</tr>
<tr class="even">
<td><p>RSS 源</p></td>
<td><p>此默认文件夹包含 RSS 源。</p></td>
</tr>
<tr class="odd">
<td><p>可恢复的项目</p></td>
<td><p>这是非 IPM 子树中的一个隐藏文件夹。其中包含“Deletions”、“Versions”、“Purges”、“DiscoveryHolds”和“Audits”子文件夹。此文件夹的保留标记可将项目从用户主邮箱中的“可恢复的项目”文件夹移至用户存档邮箱中的“可恢复的项目”文件夹。只能向此文件夹的标记分配“移动到存档”保留操作。若要了解详细信息，请参阅<a href="recoverable-items-folder-exchange-2013-help.md">“可恢复的项目”文件夹</a>。</p></td>
</tr>
<tr class="even">
<td><p>已发送邮件</p></td>
<td><p>此默认文件夹用于存储已提交给集线器传输服务器的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>同步问题</p></td>
<td><p>此文件夹包含同步日志。若要了解详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=198215">同步错误文件夹</a>。</p></td>
</tr>
<tr class="even">
<td><p>任务</p></td>
<td><p>此默认文件夹用于存储任务。若要为“Tasks”文件夹创建 RPT，您必须使用 Exchange 命令行管理程序。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dd335226(v=exchg.150)">New-RetentionPolicyTag</a>。在为“Tasks”文件夹创建了 RPT 之后，您可以通过使用 Exchange 管理中心对其进行管理。</p></td>
</tr>
</tbody>
</table>


## 更多信息

  - RPT 是默认文件夹的保留标记。您只能选择 RPT 的删除操作 – **“删除但允许恢复”**或**“永久删除”**。

  - 您不能通过创建 RPT 将邮件移动到存档中。若要将旧邮件移动到存档，可以创建*默认策略标记* (DPT)，它适用于整个邮箱，也可以创建*个人标记*，它在 Outlook 和 Outlook Web App (OWA) 中显示为“存档策略”。您的用户可以将它们应用于文件夹或单个邮件中。

  - 不能将 RPT 应用于“联系人”文件夹。

  - 只能将特定默认文件夹的一个 RPT 添加到保留策略。例如，如果某一保留策略有一个“收件箱”标记，则不能将“收件箱”类型的其他 RPT 添加到该保留策略。

  - 若要了解如何创建 RPT 或其他类型的保留标记，并将它们添加到保留策略，请参阅[创建保留策略](create-a-retention-policy-exchange-2013-help.md)。

  - 在 Exchange 2013 和 Exchange Online 中，DPT 也适用于默认文件夹“**日历**”和“**任务**”。这可能导致系统根据 DPT 设置将项目删除或移动到存档中。若要防止 DPT 设置删除这些文件夹中的项目，请创建禁用保留的 RPT。若要防止 DPT 设置移动默认文件夹中的项目，你可以使用“移动到存档”操作创建禁用的个人标记，将其添加到保留策略，然后让用户将其应用到默认文件夹。有关详细信息，请参阅[防止对 Exchange 2010 中默认文件夹中的项目进行存档](https://go.microsoft.com/fwlink/?linkid=511071)。

