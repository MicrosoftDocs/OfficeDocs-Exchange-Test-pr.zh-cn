---
title: '查看管理员审核日志: Exchange Online Help'
TOCTitle: 查看管理员审核日志
ms:assetid: 5c62072a-556d-4fea-9973-d668c6b9fd57
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn342832(v=EXCHG.150)
ms:contentKeyID: 56271391
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看管理员审核日志

 

_**适用于：**Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**上一次修改主题：**2016-05-03_

在 Microsoft Exchange Online Protection (EOP)、Microsoft Exchange Online 和 Microsoft Exchange 2013 中，您可以使用 Exchange 管理中心 (EAC) 搜索和查看\&quot;管理员审核日志\&quot;中的条目。管理员审核日志根据管理员和具有指定管理权限的用户所执行的 Exchange 命令行管理程序 cmdlet 来记录特定的操作。管理员审核日志中的条目向您提供有关所运行的 cmdlet、所使用的参数、运行 cmdlet 的用户以及受影响的对象的相关信息。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>默认情况下，将启用管理员审核日志记录。</p></li>
<li><p>管理员审核日志不会记录基于以谓词 <strong>Get</strong>、<strong>Search</strong> 或 <strong>Test</strong> 开头的 Exchange 命令行管理程序 cmdlet 的任何操作。</p></li>
<li><p>审核日志条目将保留 90 天。当某个条目超过 90 天时，会删除该条目。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [Feature permissions in EOP](https://technet.microsoft.com/zh-cn/library/jj723125\(v=exchg.150\))主题中的\&quot;查看报告\&quot;条目。

  - 如上文所述，管理员审核日志记录已默认启用。若要验证是否已启用，您可以运行以下命令：
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    在 Exchange 2013 中，您可以通过运行以下命令，启用管理员审核日志记录（如果已被禁用）。
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $True
    
    在 Exchange Online Protection 和 Exchange Online 中，管理员审核日志记录始终启用，不能禁用。

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


## 使用 EAC 查看管理员审核日志

1.  在 EAC 中，转到\&quot;合规性管理\&quot;\>\&quot;审核\&quot;，然后选择\&quot;运行管理员审核日志报告\&quot;。

2.  选择\&quot;开始日期\&quot;和\&quot;结束日期\&quot;，然后选择\&quot;搜索\&quot;。在指定期间进行的所有配置更改都将显示并且可以使用以下信息进行排序：
    
      - **日期**   进行配置更改的日期和时间。日期和时间存储为协调世界时 (UTC) 格式。
    
      - **Cmdlet**   用于进行配置更改的 cmdlet 的名称。
    
      - **用户**   进行配置更改的用户的用户帐户名称。
    
    将分多页显示多达 5000 个条目。如果您需要缩小结果范围，请指定一个较小的日期范围。如果您选择单个搜索结果，将在详细信息窗格中显示以下附加信息：
    
      - **修改对象**   cmdlet 修改的对象。
    
      - **参数 (Parameter:Value)**   使用的 cmdlet 参数以及参数指定的任何值。

3.  如果您想打印某个特定的审核日志条目，请在详细信息窗格中选择\&quot;打印\&quot;按钮。

## 您如何知道这有效？

如果您已成功运行管理员审核日志报告，在您指定的日期范围内所做的配置更改将显示在搜索结果窗格中。如果没有结果，请更改日期范围，然后再次运行报告。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在组织中进行更改后，将需要 15 分钟才能显示在审核日志搜索结果中。如果更改未出现在管理员审核日志中，请等待几分钟，然后再次运行搜索。</td>
</tr>
</tbody>
</table>

