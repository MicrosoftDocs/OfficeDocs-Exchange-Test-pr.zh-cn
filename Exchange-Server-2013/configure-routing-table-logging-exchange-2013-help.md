---
title: '配置路由表日志记录: Exchange 2013 Help'
TOCTitle: 配置路由表日志记录
ms:assetid: 7184f8f7-4eb8-468a-aafe-b2d72868f820
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201696(v=EXCHG.150)
ms:contentKeyID: 50490822
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置路由表日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

路由表日志记录定期记录 Microsoft Exchange Server 2013 用来将邮件路由到其目标的路由表快照。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”和“边缘传输服务器”条目。

  - 只能使用命令行管理程序执行此过程。

  - 要配置自动重新计算路由表的时间间隔，可修改 EdgeTransport.exe.config XML 应用程序配置文件。重新启动 Microsoft Exchange 传输服务后，将应用保存到此文件中的更改。重新启动此服务时，会临时中断服务器上的邮件流。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

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

## 使用命令行管理程序配置路由表日志记录

运行以下命令：

    Set-TransportService <ServerIdentity> -RoutingTableLogMaxAge <dd.hh:mm:ss> -RoutingTableLogMaxDirectorySize <Size>  -RoutingTableLogPath <LocalFilePath>

此示例将在名为 Mailbox01 的邮箱服务器上设置以下路由表日志设置：

  - 将路由表日志文件的位置设置为 D:\\Routing Table Log。请注意，如果文件夹不存在，系统将为您创建文件夹。

  - 将路由表日志文件夹的最大大小设置为 70 MB。

  - 将路由表日志文件的最长期限设置为 45 天。

<!-- end list -->

    Set-TransportService Mailbox01 -RoutingTableLogPath "D:\Routing Table Log" -RoutingTableLogMaxDirectorySize 70MB -RoutingTableLogMaxAge 45.00:00:00

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将 <em>RoutingTableLogMaxAge</em> 参数设置为值 <code>00:00:00</code> 可防止由于期限问题而自动删除路由表日志文件。</td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

要验证是否成功配置了路由表日志记录，请执行以下操作：

1.  在此命令行管理程序中，运行以下命令：
    
        Get-TransportService <ServerIdentity> | Format-List RoutingTableLog*

2.  验证显示的值是否为您配置的值。

## 使用命令提示符在 EdgeTransport.exe.config 文件中配置自动重新计算路由表的时间间隔

1.  在命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 应用程序配置文件：
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  修改 `<appSettings>` 部分中的以下键。
    
        <add key="RoutingConfigReloadInterval" value="<hh:mm:ss>" />
    
    例如，要将自动重新计算路由表的时间间隔更改为 10 小时，请使用以下值：
    
        <add key="RoutingConfigReloadInterval" value="10:00:00" />

3.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

4.  通过运行以下命令重新启动 Microsoft Exchange 传输服务：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 您如何知道这有效？

要验证是否已成功配置自动重新计算路由表的时间间隔，请验证路由表日志是否在您指定的时间间隔期间进行更新。

请注意，如果发生以下任意一种情况，将在 *RoutingConfigReloadInterval* 键指定的时间间隔值之前重新计算路由表并进行日志记录：

  - 检测到路由配置更改。例如，添加、删除或修改了发送连接器或接收连接器；或进行了每 6 小时一次的 Kerberos 令牌续订。

  - Microsoft Exchange 传输服务已启动。

