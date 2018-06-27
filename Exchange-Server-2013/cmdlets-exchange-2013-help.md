---
title: 'Cmdlet: Exchange 2013 Help'
TOCTitle: Cmdlet
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 50490165
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlet

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

*cmdlet*，全称为\&quot;command-let\&quot;，是 Exchange 命令行管理程序中最小的功能单元。Cmdlet 类似于其他命令行管理程序中的内置命令，例如 `cmd.exe` 中的 `dir` 命令。与这些熟悉的命令一样，cmdlet 可以直接从命令行管理程序中的命令行调用，并在命令行管理程序的环境中运行，而不是作为单独的进程运行。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>自 Microsoft Exchange Server 2007 发布以来，Exchange 2013 内部使用 cmdlet 的方式已由于 Windows PowerShell 远程功能的使用而发生了更改。这些更改对使用 cmdlet 所需的方式并没有影响，但为管理 Exchange 服务器的方式提供了更大的灵活性。</td>
</tr>
</tbody>
</table>


Cmdlet 通常用于重复性管理任务，并且在命令行管理程序中，为 Exchange 特定的管理任务提供几百个 cmdlet。这些 cmdlet 还可以用于基本 Exchange PowerShell 命令行管理程序设计中包括的非 Windows 系统 cmdlet。有关如何打开 Exchange 命令行管理程序的信息，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

命令行管理程序中的所有 cmdlet 均以动词-名词对的形式表示。动词-名词对始终由连字符 (-) 分隔（不加空格），并且 cmdlet 名词始终为单数形式。动词指的是 cmdlet 执行的操作。名词指的是 cmdlet 执行操作的对象。例如，在 **Get-SystemMessage** cmdlet 中，动词是 **Get**，而名词是 **SystemMessage**。管理某个特定功能的所有命令行管理程序 cmdlet 共享同一个名词。下表提供了在命令行管理程序中可用的部分动词示例。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，如果省略动词，则命令行管理程序会假定 <strong>Get</strong> 动词。例如，呼叫 <strong>Mailbox</strong> 时，检索的结果与呼叫 <strong>Get-Mailbox</strong> 时检索的结果相同。</td>
</tr>
</tbody>
</table>


### Exchange 命令行管理程序中的动词示例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>动词</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p><strong>Disable</strong> cmdlet 可以将指定的 Exchange 对象的 <code>Enabled</code> 状态设置为 <code>$False</code>。这将阻止对象处理数据（即使对象存在）。</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p><strong>Enable</strong> cmdlet 可以将指定的 Exchange 对象的已启用状态设置为 <code>$True</code>。这将使对象可以处理数据。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p><strong>Get</strong> cmdlet 可以检索有关特定 Exchange 对象的信息。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>大多数 <strong>Get</strong> cmdlet 在运行时仅返回摘要信息。若要在运行命令时通知 <strong>Get</strong> cmdlet 返回详细信息，请将命令管道传输至 <strong>Format-List</strong> cmdlet 中。有关 <strong>Format-List</strong> 命令的详细信息，请参阅<a href="working-with-command-output-exchange-2013-help.md">使用命令输出</a>。有关管道传输的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/aa998260(v=exchg.150)">管道传输</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p><strong>Install</strong> cmdlet 可以在 Exchange 服务器上安装新对象或功能。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p><strong>Move</strong> cmdlet 可以将指定的 Exchange 对象从一个容器或服务器重定位到另一个容器或服务器。</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p><strong>New</strong> cmdlet 可以创建新的 Exchange 对象。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p><strong>Remove</strong> cmdlet 可以删除指定的 Exchange 对象。</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p><strong>Set</strong> cmdlet 可以修改现有 Exchange 对象的属性。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p><strong>Test</strong> cmdlet 可以测试特定的 Exchange 组件并提供可以检查的日志文件。</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p><strong>Uninstall</strong> cmdlet 可以从 Exchange 服务器中删除对象或功能。</p></td>
</tr>
</tbody>
</table>


以下 cmdlet 列表是完整 cmdlet 集的示例。此 cmdlet 集用于管理发送状态通知 (DSN) 邮件和 Exchange 2013 的邮箱配额邮件功能：

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**

