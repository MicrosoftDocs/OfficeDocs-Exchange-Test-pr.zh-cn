---
title: '配置协议日志记录: Exchange 2013 Help'
TOCTitle: 配置协议日志记录
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50491513
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置协议日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-03-15_

协议日志记录可记录在发送连接器和接收连接器上作为邮件交付一部分进行的 SMTP 会话。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”、“前端传输服务”、“邮箱传输服务”、“接收连接器”和“发送连接器”条目。

  - 您可使用 Exchange 管理控制台 (EAC) 在邮箱服务器上的传输服务中为发送连接器和接收连接器启用或禁用协议日志记录，或者在客户端访问服务器上的前端传输服务中为接收连接器启用或禁用协议日志记录。也可使用 EAC 只对传输服务配置协议日志路径。对于所有其他协议日志记录选项，您需要使用命令行管理程序。

  - 按每个连接器启用或禁用协议日志记录。Exchange 服务器上的所有接收连接器共享相同的协议日志文件和协议日志选项。这些协议日志设置与同一服务器上的发送连接器协议日志文件和协议日志选项分离。

  - 
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>不要在已通过使用 EdgeSync 订阅到 Exchange 组织的边缘传输服务器上执行此步骤。相反，请在邮箱服务器上的传输服务中进行更改。这样更改将在下次发生 EdgeSync 同步时复制到边缘传输服务器上。</td>
    </tr>
    </tbody>
    </table>


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

## 使用 EAC 配置协议日志记录

要使用 EAC 在邮箱服务器上的传输服务中为发送连接器和接收连接器启用或禁用协议日志记录，或者在客户端访问服务器上的前端传输服务中为接收连接器启用或禁用协议日志记录，请执行以下操作：

1.  在 EAC 中，导航到“邮件流”\>“发送连接器”或“邮件流”\>“接收连接器”。

2.  选择要配置的连接器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“协议日志记录级别”部分中的“常规”选项卡上，选择以下选项之一：
    
      - **无**   连接器上禁用协议日志记录。
    
      - **详细**   连接器上启用协议日志记录。
    
    完成后，单击“保存”。

要使用 EAC 在邮箱服务器上的传输服务中为发送连接器和接收连接器配置协议日志路径，请执行以下操作：

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  选择要配置的邮箱服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页上，单击“传输日志”。

4.  在“协议日志”部分，更改以下任何设置之一：
    
      - **发送协议日志路径**   您指定的值必须在本地 Exchange 服务器上。如果文件夹不存在，则在单击“保存”时，系统会为您创建文件夹。
    
      - **接收协议日志路径**   您指定的值必须在本地 Exchange 服务器上。如果文件夹不存在，则在单击“保存”时，系统会为您创建文件夹。
    
    完成后，单击“保存”。

## 您如何知道这有效？

要验证是否成功使用 EAC 配置协议日志设置，请执行以下操作：

1.  浏览到您为发送连接器或接收连接器协议日志指定的位置。

2.  如果您启用了协议日志记录，请验证是否创建了一个日志文件。如果您禁用了协议日志记录，请验证最新日志文件是否已不再更新。

## 使用命令行管理程序在发送连接器或接收连接器上启用或禁用协议日志记录

要在发送连接器或接收连接器上启用或禁用协议日志记录，运行以下命令：

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

此示例将为名为“Connection from Contoso.com”的接收连接器启用协议日志记录。

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## 您如何知道这有效？

要验证是否已成功启用或禁用了协议日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序在组织内部发送连接器上启用或禁用协议日志记录

要在邮箱服务器上的传输服务中和客户端访问服务器上的前端传输服务中存在的隐含和不可见组织内发送连接器上启用或禁用协议日志记录，请运行以下命令：

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

本示例将在名为 Mailbox01 的邮箱服务器上的传输服务中的组织内发送连接器上启用协议日志记录。

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## 您如何知道这有效？

要验证是否已在组织内发送连接器上成功启用或禁用了协议日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序在邮箱交付发送连接器上启用或禁用协议日志记录

要在邮箱服务器上的邮箱传输服务中存在的隐含和不可见邮箱交付发送连接器上启用或禁用协议日志记录，请运行以下命令：

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

本示例将在名为 Mailbox01 的邮箱服务器上的邮箱传输服务中的邮箱交付接收连接器上启用协议日志记录。

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## 您如何知道这有效？

要验证是否已在邮箱交付连接器上成功启用或禁用了协议日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序配置协议日志记录设置

若要配置协议日志设置，请运行以下命令：

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

本示例将在名为 Mailbox01 的邮箱服务器上的传输服务中设置以下协议日志设置：

  -  
    将所有接收连接器协议日志的位置设置为 D:\\Hub Receive SMTP Log 并将所有发送连接器协议日志的位置设置为 D:\\Hub Send SMTP Log。请注意，如果文件夹不存在，系统将为您创建文件夹。

  -  
    将接收连接器协议日志文件和发送连接器协议日志文件的最大大小设置为 20 MB。

  -  
    将接收连接器协议日志文件夹和发送连接器协议日志文件夹的最大大小设置为 400 MB。

  -  
    将接收连接器协议日志文件和发送连接器协议日志文件的最大期限设置为 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00

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
<li><p>要在邮箱服务器上的邮箱传输服务中配置协议日志设置，可使用 <strong>Set-MailboxTransportService</strong> cmdlet。要在客户端访问服务器上的前端传输服务中配置协议日志设置，可使用 <strong>Set-FrontEndTransportService</strong> cmdlet。</p></li>
<li><p>将 <em>SendProtocolLogPath</em> 参数或 <em>ReceiveProtocolLogPath</em> 参数的值设置为 <code>$null</code> 会有效禁用服务器上所有发送连接器或所有接收连接器的协议日志记录。但是，当对服务器上的任何其他连接器启用协议日志记录时，将这两个参数中的任何一个设置成 <code>$null</code> 都将生成事件日志错误。</p></li>
<li><p>将 <em>ReceiveProtocolLogMaxAge</em> 或 <em>SendProtocolLogMaxAge</em> 参数的值设置为 <code>00:00:00</code>，可以防止由于期限问题而自动删除协议日志文件。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

要验证是否已成功配置协议日志设置，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  验证显示的值是否为您配置的值。

