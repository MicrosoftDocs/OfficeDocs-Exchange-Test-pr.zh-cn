---
title: '配置连接日志记录: Exchange 2013 Help'
TOCTitle: 配置连接日志记录
ms:assetid: 24e46a79-33ea-44e9-b03c-549db1c86a6f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996827(v=EXCHG.150)
ms:contentKeyID: 50490083
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置连接日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-18_

连接日志记录可记录用于从 Exchange 服务器上的传输服务传输邮件的出站连接活动。连接日志记录可记录连接源、目标、传输的邮件数和字节数以及连接失败信息。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”、“前端传输服务”和“邮箱传输服务”条目。

  - 您可以使用 Exchange 管理中心 (EAC) 启用或禁用连接日志记录，也可以只设置传输服务的连接日志路径。对于其他传输服务中的所有其他连接日志记录选项，您需要使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 在传输服务中配置连接日志记录

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  选择要配置的邮箱服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“传输日志”。

4.  在“连接日志”部分中，更改以下任意项：
    
      - **启用连接日志**   要在服务器上禁用连接日志记录，请清除此复选框。要在服务器上启用连接日志记录，请选中此复选框。
    
      - **连接日志路径**   您指定的值必须位于本地 Exchange 服务器上。如果文件夹不存在，则在单击“保存”时，系统会为您创建文件夹。
    
    完成后，单击“Save”。

## 使用命令行管理程序配置连接日志记录

要配置连接日志记录，请运行以下命令：

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ConnectivityLogEnabled <$true | $false> -ConnectivityLogMaxAge <dd.hh:mm:ss> -ConnectivityLogMaxDirectorySize <Size> -ConnectivityLogMaxFileSize <Size> -ConnectivityLogPath <LocalFilePath>

此示例将在名为 Mailbox01 的邮箱服务器上的传输服务中设置以下连接日志设置：

  -  
    将连接日志文件的位置设置为 D:\\Hub Connectivity Log。请注意，如果文件夹不存在，系统将为您创建文件夹。

  -  
    将连接日志文件的最大大小设置为 20 MB。

  -  
    将连接日志目录的最大大小设置为 1.5 GB。

  -  
    将连接日志文件的最长期限设置为 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -ConnectivityLogPath "D:\Hub Connectivity Log" -ConnectivityLogMaxFileSize 20MB -ConnectivityLogMaxDirectorySize 1.5GB -ConnectivityLogMaxAge 45.00:00:00

> [!NOTE]
> <ul>
> <li><p>要在邮箱服务器上的邮箱传输服务中配置连接日志设置，请使用 <strong>Set-MailboxTransportService</strong> cmdlet。要在客户端访问服务器上的前端传输服务中配置连接日志设置，请使用 <strong>Set-FrontEndTransportService</strong> cmdlet。</p></li>
> <li><p>将 <em>ConnectivityLogPath</em> 参数设置为值 <code>$null</code> 将有效地禁用连接日志记录。但是，如果 <em>ConnectivityLogEnabled</em> 参数的值为 <code>$true</code>，则会生成事件日志错误。</p></li>
> <li><p>将 <em>ConnectivityLogMaxAge</em> 参数设置为值 <code>00:00:00</code> 将防止由于期限问题而自动删除连接日志文件。</p></li>
> </ul>


## 您如何知道这有效？

要验证您是否已成功配置连接日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        <Get-TransportService | Get-FrontEndTransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List ConnectivityLog*

2.  验证显示的值是否为您配置的值。

