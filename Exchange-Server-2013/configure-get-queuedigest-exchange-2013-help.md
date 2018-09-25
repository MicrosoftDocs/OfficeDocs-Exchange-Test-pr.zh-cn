---
title: '配置 Get-QueueDigest: Exchange 2013 Help'
TOCTitle: 配置 Get-QueueDigest
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59636434
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 Get-QueueDigest

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

**Get-QueueDigest** cmdlet 允许您使用单个命令来查看有关 Exchange 组织中部分或全部队列的信息。

默认情况下，由 **Get-QueueDigest** cmdlet 返回的结果是一到两分钟之前刚刚生成的。这些值受以下设置控制：

  - **EdgeTransport.exe.config 中的 QueueLoggingInterval 键**   该键指定记录队列数据的频率以及队列数据对 **Get-QueueDigest** 可用的频率。默认值为 `00:01:00`（一分钟）。若要指定值，请以时间跨度的形式输入：*hh:mm:ss*，其中 *h* = 小时，*m* = 分钟，*s* = 秒。默认情况下，EdgeTransport.exe.config 文件中不存在此键。

  - **Set-TransportConfig 上的 QueueDiagnosticsAggregationInterval 参数**   此参数指定邮箱服务器之间共享队列数据的频率。默认值为 `00:01:00`（一分钟）。若要指定值，请以时间跨度的形式输入：*hh:mm:ss*，其中 *h* = 小时，*m* = 分钟，*s* = 秒。

**QueueLoggingInterval** 键和*QueueDiagnosticsAggregationInterval* 参数值的总和决定由 **Get-QueueDigest** 返回的结果的最长期限。

此外，根据队列类型和队列状态，**Get-QueueDigest** 会返回不同的结果。例如，只要包含至少一条消息，以下队列就会显示在结果中：

  - \&quot;提交\&quot;队列、\&quot;无法到达\&quot;队列和病毒消息队列（持久性队列）。

  - 处于挂起状态的传递队列（由管理员手动挂起的队列）。

默认情况下，仅当队列包含 10 条或更多消息时，结果才返回具有状态\&quot;活动\&quot;、\&quot;正在连接\&quot;、\&quot;就绪\&quot;或\&quot;重试\&quot;的传递队列。该值由 EdgeTransport.exe.config 文件中的 **QueueLoggingThreshold** 键控制。您可以指定一个更小或更大的整数值。默认情况下，EdgeTransport.exe.config 文件中不存在此键。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 若要查看 Exchange 权限，您需要在 Exchange 命令行管理程序中运行 **Set-TransportConfig**，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;传输配置\&quot;条目。

  - Exchange 权限不适用于修改 EdgeTransport.exe.config 文件和重新启动 Microsoft Exchange 传输服务。这些过程在 Exchange Server 的操作系统中执行。

  - 保存到 EdgeTransport.exe.config 文件中的更改在重新启动 Microsoft Exchange 传输服务之后应用。重新启动此服务时，会临时中断服务器上的邮件流。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 使用 **Set-TransportConfig** 所做的修改将影响您组织内的所有邮箱服务器。在 EdgeTransport.exe.config 文件中所做的更改只会影响本地邮箱服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 配置 Get-QueueDigest

1.  在命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 文件：
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  添加 `<appSettings>` 部分中的一个或两个键。
    
    ```powershell
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    ```

    例如，若要将 **QueueLoggingThreshold** 值设置为 1，将 **QueueLoggingInterval** 值设置为 30 秒，使用下列值：
    
    ```powershell
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />
    ```

3.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

4.  通过运行以下命令重新启动 Microsoft Exchange 传输服务：
    
    ```powershell
        net stop MSExchangeTransport && net start MSExchangeTransport
    ```

5.  若要在 Exchange 命令行管理程序中更改 *QueueDiagnosticsAggregationInterval* 参数的值，使用以下语法：
    
    ```powershell
    Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    ```
    
    例如，若要将值更改为 30 秒，请运行以下命令：
    
    ```powershell
    Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30
    ```

## 您如何知道这有效？

若要验证您是否已成功配置 **Get-QueueDigest**，请执行下列操作：

1.  在 EdgeTransport.exe.config 文件中验证 **QueueLoggingThreshold** 和 **QueueLoggingInterval** 键的值。如果键不存在，则使用默认值。

2.  通过运行以下命令验证 *QueueDiagnosticsAggregationInterval* 参数的值：
    
    ```powershell
        Get-TransportConfig | Format-List *queue*
    ```
