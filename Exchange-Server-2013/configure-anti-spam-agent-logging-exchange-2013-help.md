---
title: '配置反垃圾邮件代理日志记录: Exchange 2013 Help'
TOCTitle: 配置反垃圾邮件代理日志记录
ms:assetid: df157ca3-ad8e-4302-acbc-5fbb8570c21d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691337(v=EXCHG.150)
ms:contentKeyID: 50491796
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置反垃圾邮件代理日志记录

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-08_

代理日志记录特定 Exchange 反垃圾邮件代理所执行的操作。写入代理日志中的信息取决于代理、SMTP 事件和对邮件执行的操作。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”和“边缘传输服务器”条目。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。

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


## 使用命令行管理程序配置反垃圾邮件代理日志记录

运行以下命令：

    Set-TransportService <ServerIdentity> -AgentLogEnabled <$true | $false> -AgentLogMaxAge <dd.hh:mm:ss> -AgentLogMaxDirectorySize <Size> -AgentLogMaxFileSize <Size> -AgentLogPath <LocalFilePath>

本示例将在名为 Mailbox01 的邮箱服务器上设置以下代理日志：

  -  
    将代理日志文件的位置设置为 D:\\Anti-Spam Agent Log。请注意，如果文件夹不存在，系统将为您创建文件夹。

  -  
    将代理日志文件的最大大小设置为 20 MB。

  -  
    将代理日志目录的最大大小设置为 400 MB。

  -  
    将代理日志文件的最大期限设置为 14 天。

<!-- end list -->

    Set-TransportService Mailbox01 -AgentLogPath "D:\Anti-Spam Agent Log" -AgentLogMaxFileSize 20MB -AgentLogMaxDirectorySize 400MB -AgentLogMaxAge 14.00:00:00

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
<li><p>如果将 <em>AgentLogPath</em> 参数的值设置为 <code>$null</code>，将有效地禁用代理日志记录。但是当 <em>AgentLogEnabled</em> 参数的值为 <code>$true</code> 时，如果将 <em>AgentLogPath</em> 设置为 <code>$null</code>，就会生成事件日志错误。禁用代理日志记录的首选方法是将 <em>AgentLogEnabled</em> 设置为 <code>$false</code>。</p></li>
<li><p>将 <em>AgentLogMaxAge</em> 参数设置为值 <code>00:00:00</code>，可以防止由于期限问题而自动删除代理日志文件。</p></li>
</ul></td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Set-TransportService](https://technet.microsoft.com/zh-cn/library/jj215682\(v=exchg.150\)) 中的 *AgentLog* 参数。

## 您如何知道这有效？

要验证是否已成功配置反垃圾邮件代理日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        Get-TransportService <ServerIdentity> | Format-List AgentLog*

2.  验证显示的值是否为您配置的值。

