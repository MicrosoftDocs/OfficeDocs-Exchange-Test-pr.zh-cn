---
title: '配置邮件跟踪: Exchange 2013 Help'
TOCTitle: 配置邮件跟踪
ms:assetid: 50eb5213-cf27-4179-b427-38d751ee4a70
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997984(v=EXCHG.150)
ms:contentKeyID: 51408223
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮件跟踪

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-18_

邮件跟踪可以记录 Microsoft Exchange Server 2013 邮箱服务器中传输服务或邮箱所发送和接收的所有邮件的 SMTP 传输活动。您可以使用邮件跟踪日志进行邮件取证、邮件流分析、报告和故障排除。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”条目或[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“邮箱服务器配置”条目。

  - 可以使用 Exchange 管理中心 (EAC) 启用或禁用邮件跟踪，或设置邮件跟踪日志路径。对于所有其他邮件跟踪选项，需要使用 Exchange 命令行管理程序。

  - 在 Exchange 2013 邮箱服务器中，可以使用 **Set-TransportService** 或 **Set-MailboxServer** cmdlet 配置邮件跟踪选项。此主题中的过程使用 **Set-TransportService** cmdlet。

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


## 使用 EAC 在邮箱服务器上配置邮件跟踪

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  选择要配置的邮箱服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“服务器属性”页上单击“传输日志”。

4.  在“邮件跟踪日志”部分中，更改以下任意项：
    
      - **启用邮件跟踪日志**   要在服务器上禁用邮件跟踪，请清除此复选框。要在服务器上启用邮件跟踪，请选中此复选框。
    
      - **邮件跟踪日志路径**   您指定的值必须位于本地 Exchange 服务器上。如果文件夹不存在，则在单击“保存”时，系统会为您创建文件夹。

5.  单击“保存”。

## 使用命令行管理程序配置邮件跟踪

要配置邮件跟踪，请运行以下命令：

    Set-TransportService <ServerIdentity> -MessageTrackingLogEnabled <$true | $false> -MessageTrackingLogMaxAge <dd.hh:mm:ss> -MessageTrackingLogMaxDirectorySize <Size> -MessageTrackingLogMaxFileSize <Size> -MessageTrackingLogPath <LocalFilePath> -MessageTrackingLogSubjectLoggingEnabled <$true|$false>

本示例将在名为 Mailbox01 的邮箱服务器上设置以下邮件跟踪日志设置：

  -  将邮件跟踪日志文件的位置设置为 D:\\Message Tracking Log。请注意，如果文件夹不存在，系统将为您创建文件夹。

  -  将邮件跟踪日志文件的最大大小设置为 20 MB。

  -  将邮件跟踪日志目录的最大大小设置为 1.5 GB。

  -  将邮件跟踪文件的最长期限设置为 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -MessageTrackingLogPath "D:\Hub Message Tracking Log" -MessageTrackingLogMaxFileSize 20MB -MessageTrackingLogMaxDirectorySize 1.5GB -MessageTrackingLogMaxAge 45.00:00:00

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
<li><p>将 <em>MessageTrackingLogPath</em> 参数设置为值 <code>$null</code> 将有效地禁用邮件跟踪。但是，如果 <em>MessageTrackingLogEnabled</em> 参数的值为 <code>$true</code>，则会生成事件日志错误。</p></li>
<li><p>将 <em>MessageTrackingLogMaxAge</em> 参数设置为值 <code>00:00:00</code> 将防止由于期限问题而自动删除邮件跟踪日志文件。</p></li>
<li><p>在 Exchange 2013 邮箱服务器中，邮箱跟踪日志目录的最大大小是 <em>MessageTrackingLogMaxDirectorySize</em> 参数值的三倍。虽然由这四个不同服务生成的邮件跟踪日志文件有四个不同的名称前缀，但是与另外三个日志文件前缀相比，写入 <strong>MSGTRKMA</strong> 日志文件的数据量和数据频率几乎可以忽略不计。有关详细信息，请参阅<a href="message-tracking-exchange-2013-help.md">邮件跟踪</a>主题中的“邮件跟踪日志文件结构”部分。</p></li>
</ul></td>
</tr>
</tbody>
</table>


此示例在名为 Mailbox01 的邮箱服务器上禁用邮件跟踪日志中的邮件主题日志记录：

    Set-TransportService Mailbox01 -MessageTrackingLogSubjectLoggingEnabled $false

此示例在名为 Mailbox01 的邮箱服务器上禁用邮件跟踪：

    Set-TransportService Mailbox01 -MessageTrackingLogEnabled $false

## 您如何知道操作成功？

要验证您是否已成功配置邮件跟踪，请执行下列操作：

1.  在命令行管理程序中，运行以下命令：
    
        Get-TransportService <ServerIdentity> | Format-List MessageTrackingLog*

2.  验证显示的值是否是您配置的值。

