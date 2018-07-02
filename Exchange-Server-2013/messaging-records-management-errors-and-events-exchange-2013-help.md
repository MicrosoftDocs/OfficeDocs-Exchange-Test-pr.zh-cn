---
title: '邮件记录管理错误和事件: Exchange 2013 Help'
TOCTitle: 邮件记录管理错误和事件
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 51408249
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 邮件记录管理错误和事件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

邮件记录管理 (MRM) 生成您可以在事件查看器中查看的事件。这允许您排除故障，并验证托管文件夹助理的性能。事件查看器跟踪事件按以下顺序，根据重要性以下几种 ︰

1.  错误事件

2.  警告事件

3.  信息性事件

## MRM 错误和事件

下表提供了可用于解决 MRM 的事件的列表。日志记录类型如下所示 ︰

  - 标记为 **LogAlways** 的事件总是单独记录。

  - 在五分钟的时间内，每次发生时不只一次记录标记为**LogPeriodic**的事件。这有助于防止过多的日志条目。

### 托管文件夹助理类别中的 MRM 事件

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
<th><strong>事件 ID</strong></th>
<th><strong>类别</strong></th>
<th><strong>事件类型</strong></th>
<th><strong>日志记录</strong></th>
<th><strong>值或说明</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>10003</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogPeriodic</p></td>
<td><p>无法从Active Directory获取服务器配置对象。&lt;<em>Exception details</em>&gt;。检查域控制器的网络连接问题或 DNS 配置不正确。</p></td>
</tr>
<tr class="even">
<td><p>10004</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>将不应用邮箱 &lt;<em>mailbox</em>&gt; &lt;<em>folder</em>&gt; 文件夹的保留策略。托管的文件夹助理程序无法处理托管内容设置 &lt;<em>content setting</em>&gt; &lt;<em>managed folder</em>&gt; 托管文件夹。RetentionAction 是 MoveToFolder，但未指定目标文件夹。请指定目标文件夹。</p></td>
</tr>
<tr class="odd">
<td><p>10005</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>保留策略不会应用于邮箱 &lt;<em>mailbox</em>&gt; &lt;<em>folder</em>&gt; 文件夹中。无法处理托管内容设置 &lt;<em>content setting</em>&gt; &lt;<em>managed folder</em>&gt; 中的管理文件夹。RetentionAction 是 MoveToFolder，但是 &lt;<em>folder</em>&gt; 目标文件夹是源文件夹 &lt;<em>folder</em>&gt; 相同。请指定一个不同于源文件夹的目标文件夹。</p></td>
</tr>
<tr class="even">
<td><p>10009</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>托管的文件夹助理跳过处理本地服务器上的所有数据库，因为它不能从Active Directory来读取审核日志参数。它将尝试稍后再次在时间表窗口。当前数据库 ︰ &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10010</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>托管的文件夹助理跳过处理本地服务器上的所有数据库，因为审核日志已启用但缺少在Active Directory审核日志的路径。它将尝试稍后再次在时间表窗口。当前数据库 ︰ &lt;<em>database</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10011</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>托管的文件夹助理无法配置审核日志。它将停止处理当前的数据库: '%1'。它将尝试稍后再次在时间表窗口。异常详细信息 ︰ &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>10012</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>托管的文件夹助理未写入审核日志。它将停止处理当前数据库 ︰ &lt;<em>database</em>&gt;。它会尝试写入审核日志以后再次在时间表窗口。异常详细信息 ︰ &lt;<em>details</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>10017</p></td>
<td><p>托管文件夹助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>当处理邮箱时，在托管文件夹助理出现异常 ︰ &lt;<em>mailbox</em>&gt; 文件夹 ︰ 名称 ︰ &lt;<em>folder name</em>&gt; Id: &lt;<em>folder ID</em>&gt; 项 ︰ Id: &lt;<em>IDs</em>&gt;。异常 ︰ &lt;<em>exception</em>&gt;。</p></td>
</tr>
</tbody>
</table>


### 助理类别中的 MRM 事件

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
<th><strong>事件 ID</strong></th>
<th><strong>类别</strong></th>
<th><strong>事件类型</strong></th>
<th><strong>日志记录</strong></th>
<th><strong>值或描述</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9004</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。无法处理邮箱 &lt;<em>mailbox</em>&gt; &lt;<em>service</em>&gt;。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9014</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。无法处理日程安排更改。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9017</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 有关数据库 &lt;<em>database</em>&gt; 正在进入一个预定的时间窗口。有 &lt;<em>number</em>&gt; 邮箱来处理。</p></td>
</tr>
<tr class="even">
<td><p>9018</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>服务</em>&gt;。数据库 &lt;<em>数据库</em>&gt; 的 &lt;<em>服务</em>&gt; 将退出计划时间窗口。已成功处理 &lt;<em>数字</em>&gt; 个邮箱中的 &lt;<em>数字</em>&gt; 个邮箱。&lt;<em>数字</em>&gt; 个邮箱由于错误已跳过。&lt;<em>数字</em>&gt; 个邮箱已单独处理。由于时间不足，&lt;<em>数字</em>&gt; 个邮箱未处理。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>托管文件夹助理下次运行时，将从停止的位置继续进行。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="odd">
<td><p>9019</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogPeriodic</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。无法保存对数据库 &lt;<em>database</em>&gt; &lt;<em>service</em>&gt; 的进度。（助手无法保存它停止，以便它可以继续存在在它重新启动时的位置。）下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9020</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。无法启动数据库 &lt;<em>database</em>&gt; &lt;<em>assistant name</em>&gt;。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9021</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; &lt;<em>database</em>&gt; 数据库处理的点播请求的。有 &lt;<em>number</em>&gt; 邮箱来处理。</p></td>
</tr>
<tr class="even">
<td><p>9022</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>服务</em>&gt;。数据库 &lt;<em>数据库</em>&gt; 的 &lt;<em>服务</em>&gt; 已完成按需请求。已成功处理 &lt;<em>数字</em>&gt; 个邮箱中的 &lt;<em>数字</em>&gt; 个邮箱。&lt;<em>数字</em>&gt; 个邮箱由于错误已跳过。</p></td>
</tr>
<tr class="odd">
<td><p>9023</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; &lt;<em>database</em>&gt; 数据库上启动时间窗口处理失败。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9025</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 跳上数据库 &lt;<em>database</em>&gt; &lt;<em>number</em>&gt; 邮箱。邮箱 ︰ &lt;<em>mailboxes</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9026</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。无法启动按需处理数据库 &lt;<em>database</em>&gt; &lt;<em>service</em>&gt;。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9027</p></td>
<td><p>助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 导致进程终止时处理邮箱 &lt;<em>mailbox</em>&gt; 数据库 &lt;<em>database</em>&gt; &lt;<em>number</em>&gt; 时间。此邮箱不能再将在请求的时间窗口或按需请求进行处理。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>9028</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; 导致进程终止时处理邮箱 &lt;<em>mailbox</em>&gt; 数据库 &lt;<em>database</em>&gt; &lt;<em>number</em>&gt; 时间。下面的异常导致了失败 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p>9033</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。&lt;<em>service</em>&gt; &lt;<em>database</em>&gt; 数据库接收到的点播请求的。但是，没有要处理的邮箱。</p></td>
</tr>
<tr class="odd">
<td><p>9034</p></td>
<td><p>助理</p></td>
<td><p>信息</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>服务</em>&gt; 停止对数据库 &lt;<em>数据库</em>&gt; 执行基于时间的托管文件夹助理操作。</p></td>
</tr>
<tr class="even">
<td><p>9035</p></td>
<td><p>助理</p></td>
<td><p>警告</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>服务</em>&gt;。由于时间不充足，&lt;<em>助理名称</em>&gt; 无法处理 &lt;<em>数字</em>&gt; 个邮箱。</p></td>
</tr>
<tr class="odd">
<td><p>9037</p></td>
<td><p>助理</p></td>
<td><p>错误</p></td>
<td><p>LogAlways</p></td>
<td><p>服务 &lt;<em>service</em>&gt;。当处理 RPC 时遇到异常。方法 ︰ &lt;<em>method</em>&gt;，异常 ︰ &lt;<em>exception</em>&gt;</p></td>
</tr>
</tbody>
</table>

