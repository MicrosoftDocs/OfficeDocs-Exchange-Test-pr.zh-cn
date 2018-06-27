---
title: '如何计算保留时间: Exchange 2013 Help'
TOCTitle: 如何计算保留时间
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50491270
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 如何计算保留时间

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-07-27_

托管文件夹助理 (MFA) 是在邮箱服务器上运行的众多*邮箱助理*进程之一。它负责处理已应用保留策略的邮箱、将策略中包含的保留标记添加到邮箱中，以及处理邮箱中的项目。如果项目具有保留标记，则此助理会测试这些项目的保留时间。如果某个项目已经超过其*保留时间*，则此助理会执行指定的*保留操作*。保留操作包括将项目移动到用户存档、删除项目并允许恢复，或者永久删除项目。

有关详细信息，请参阅[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)。

## 确定不同类型项目的保留时间

邮箱项目的保留时间从传递日期或项目被创建的日期（例如用户创建但未传递的草稿）开始计算。当托管文件夹助理处理邮箱中的项目时，它将为带有保留标记（具有“**删除但允许恢复**”或“**永久删除**”保留操作）的所有项目标记开始日期和截止日期。具有存档标记的项目还标记有移动日期。

如下表中所示，“已删除项目”文件夹中的项目以及可能具有开始日期和结束日期的项目（如日历项目（会议和约会）和任务）采用不同的处理方式。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果项目类型是…</th>
<th>则项目为…</th>
<th>保留时间的计算依据为…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>电子邮件</p></li>
<li><p>文档</p></li>
<li><p>传真</p></li>
<li><p>日记项目</p></li>
<li><p>会议请求、响应或取消</p></li>
<li><p>未接来电</p></li>
</ul></td>
<td><p>不位于“已删除项目”文件夹中</p></td>
<td><p>传递日期或创建日期</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>电子邮件</p></li>
<li><p>文档</p></li>
<li><p>传真</p></li>
<li><p>日记项目</p></li>
<li><p>会议请求、响应或取消</p></li>
<li><p>未接来电</p></li>
</ul></td>
<td><p>位于“已删除项目”文件夹中</p></td>
<td><ul>
<li><p>传递日期或创建日期，除非项目已从不具有继承或隐式保留标记的文件夹中删除。</p></li>
<li><p>如果某个项目位于未应用继承或隐式保留标记的文件夹中，则说明此项目不由 MFA 处理，因此也就没有开始日期标记。当用户删除此类项目，且 MFA 在“已删除项目”文件夹中首次对其进行处理时，它会将当前日期标记为开始日期。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>日历</p></td>
<td><p>不位于“已删除项目”文件夹中</p></td>
<td><ul>
<li><p>非定期日历项目的到期时间取决于结束日期。</p></li>
<li><p>定期日历项目的到期时间取决于其最后一次发生时的结束日期。没有结束日期的定期日历项目不会到期。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>日历</p></td>
<td><p>位于“已删除项目”文件夹中</p></td>
<td><ol>
<li><p>日历项目的过期时间可由 <code>message-received date</code>（如果存在）确定。</p></li>
<li><p>如果日历项目没有 <code>message-received date</code>，则过期时间可由其 <code>message-creation date</code> 确定。</p></li>
<li><p>如果日历项目既没有 <code>message-received date</code>，也没有 <code>message-creation date</code>，它将不会过期。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>任务</p></td>
<td><p>不位于“已删除项目”文件夹中</p></td>
<td><ul>
<li><p>非定期任务：</p>
<ol>
<li><p>非定期任务的过期时间由 <code>message-received date</code>（如果存在）确定。</p></li>
<li><p>如果非定期任务没有 <code>message-received date</code>，其过期时间由 <code>message-creation date</code> 确定。</p></li>
<li><p>如果非定期任务既没有 <code>message-received date</code>，又没有 <code></code><code>message-creation date</code>，它将不会过期。</p></li>
</ol></li>
<li><p>定期任务的过期时间由其最后一次发生的 <code>end date</code> 确定。如果定期任务没有 <code>end date</code>，它将不会过期。</p></li>
<li><p>重新生成的任务指任务的上一实例完成后重新生成指定时间的定期任务，它不会过期。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>任务</p></td>
<td><p>位于“已删除项目”文件夹中</p></td>
<td><ol>
<li><p>任务的过期时间由其 <code>message-received date</code>（如果存在）确定。</p></li>
<li><p>如果任务没有 <code>message-received date</code>，其过期时间由 <code>message-creation date</code> 确定。</p></li>
<li><p>如果任务既没有 <code>message-received date</code>，也没有 <code>message-creation date</code>，它将不会过期。</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>联系人</p></td>
<td><p>在任何文件夹中</p></td>
<td><p>联系人没有标记开始日期或到期日期，因此被托管文件夹助理跳过且不会过期。</p></td>
</tr>
<tr class="even">
<td><p>已损坏</p></td>
<td><p>在任何文件夹中</p></td>
<td><p>托管文件夹助理会跳过已损坏的项目，并且此类项目不会到期。</p></td>
</tr>
</tbody>
</table>


## 示例


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>如果用户…</th>
<th>文件夹上的保留标记…</th>
<th>托管文件夹助理…</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>2013 年 1 月 26 日在收件箱中收到邮件。</p></li>
<li><p>2013 年 2 月 27 日删除此邮件。</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>收件箱：365 天后删除</p></li>
<li><p>已删除项目：30 天后删除</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>2013 年 1 月 26 日在收件箱中处理邮件，并标记<em>开始日期</em> 2013 年 1 月 26 日和<em>到期日期</em> 2014 年 1 月 26 日。</p></li>
<li><p>2013 年 2 月 27 日在“已删除项目”文件夹中再次处理邮件。它根据相同的开始日期（2013 年 1 月 26 日）重新计算到期日期。</p></li>
<li><p>由于项目已超过 30 天，因此它会立即到期。</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>2013 年 1 月 26 日在收件箱中收到邮件。</p></li>
<li><p>2013 年 2 月 27 日删除此邮件。</p></li>
</ol></td>
<td><ul>
<li><p>收件箱：无（继承或隐式）</p></li>
<li><p>已删除项目：30 天后删除</p></li>
</ul></td>
<td><ol>
<li><p>2013 年 2 月 27 日在“已删除项目”文件夹中处理邮件，并确定项目没有开始日期。它会将当前日期标记为开始日期，并将 2013 年 3 月 27 日标记为到期日期。</p></li>
<li><p>此项目于 2013 年 3 月 27 日到期，即用户将其删除或移动到“已删除项目”文件夹中后的第 30 天。</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 更多信息

  - 在 Exchange Online 中，托管文件夹助理可能会每 7 天处理一次邮箱。结果可能是，项目在标记到期日期后最多 7 天即到期。

  - 在删除保留挂起前，托管文件夹助理不会处理放置在保留挂起上的邮箱中的项目。

  - 如果邮箱处于就地保留或诉讼保留状态，则到期项目会从收件箱中删除，但会保留在“可恢复的项目”文件夹中，直到邮箱的[就地保留和诉讼保留](in-place-hold-and-litigation-hold-exchange-2013-help.md)状态解除为止。

  - 在混合部署中，您的本地和 Exchange Online 组织中必须存在相同的保留标记和保留策略，这样项目才能在组织之间一致地移动和到期。有关详细信息，请参阅[导出和导入保留标记](export-and-import-retention-tags-exchange-2013-help.md)。

