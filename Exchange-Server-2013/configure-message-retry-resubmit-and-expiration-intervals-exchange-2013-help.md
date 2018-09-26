---
title: '配置邮件重试间隔、重新提交间隔和过期间隔: Exchange 2013 Help'
TOCTitle: 配置邮件重试间隔、重新提交间隔和过期间隔
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51408228
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮件重试间隔、重新提交间隔和过期间隔

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

在 Microsoft Exchange Server 2013 中，可以在邮箱服务器和边缘传输服务器上的传输服务中配置邮件重试、重新提交和过期间隔。有关这些设置的说明，请参阅[邮件重试间隔、重新提交间隔和过期间隔](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”和“边缘传输服务器”条目。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EdgeTransport.exe.config 配置队列小故障重试计数、队列小故障重试间隔、邮箱传递队列重试间隔和重新提交间隔前的最长空闲时间。

要配置队列小故障重试计数、队列小故障重试间隔、邮箱传递队列重试间隔和重新提交间隔前的最长空闲时间，请修改邮箱服务器或边缘传输服务器上 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 应用程序配置文件中的项。重新启动 Microsoft Exchange 传输服务后，将应用保存到此文件中的更改。重新启动此服务时，会临时中断服务器上的邮件流。

1.  在邮箱服务器或边缘传输服务器上的命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 文件：
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  在 `<appSettings>` 部分中找到以下项。
    
    ```powershell
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    ```

    此示例将队列小故障重试计数更改为 6，将队列小故障重试间隔更改为 30 秒，将邮箱传递队列重试间隔更改为 3 分钟，并将重新提交间隔前的最长空闲时间更改为 6 小时。
    
    ```powershell
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />
    ```

3.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

4.  通过运行以下命令重新启动 Microsoft Exchange 传输服务：
    
    ```powershell
    net stop MSExchangeTransport && net start MSExchangeTransport
    ```

## 配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔

瞬间失败重试次数指定在由 `QueueGlitchRetryCount` 和 `QueueGlitchRetryInterval` 项控制的连接尝试失败后进行的连接尝试次数。默认的瞬间失败重试次数为 6。此参数的有效输入范围是 0 到 15。如果将瞬间失败重试次数设置为 0，则下一次连接尝试由*出站连接失败重试间隔*控制。

瞬间失败重试间隔指定由瞬间失败重试次数指定的每次连接尝试之间的间隔。在邮箱服务器上的传输服务中，默认的瞬间失败重试间隔是 5 分钟。在边缘传输服务器上，默认的瞬间失败重试间隔是 10 分钟。

出站连接失败重试间隔指定先前已失败的传出连接尝试的重试间隔。以前失败的连接尝试由瞬间失败重试次数和瞬间失败重试间隔控制。在邮箱服务器上的传输服务中，出站连接失败重试间隔的默认值是 10 分钟。在边缘传输服务器上，该默认值是 30 分钟。

## 使用 EAC 配置瞬间失败重试次数、瞬间失败重试间隔或出站连接失败重试间隔

1.  在 Exchange 管理中心 (EAC) 中，单击“服务器”\>“服务器”，选择服务器，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后单击“传输限制”。

2.  在“重试”部分，为“出站连接失败重试间隔(秒)”、“瞬间失败重试间隔(分钟)”或“瞬间失败重试次数”输入值。

3.  完成后，单击“保存”。

## 使用命令行管理程序配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔

使用以下语法在邮箱服务器或边缘传输服务器上的传输服务中配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔。

```powershell
Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>
```

此示例在名为 Mailbox01 的邮箱服务器上更改以下值：在边缘传输服务器 Exchange01 上。

  - 瞬间失败重试次数设置为 8。

  - 瞬间失败重试间隔设置为 1 分钟。

  - 出站连接失败重试间隔设置为 45 分钟。

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00
```

> [!NOTE]  
> 客户端访问服务器上的前端传输服务的 <strong>Set-FrontEndTransportService</strong> cmdlet 也提供 <em>TransientFailureRetryCount</em> 和 <em>TransientFailureRetryInterval</em> 参数。


## 配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔

## 使用 EAC 配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔

1.  在 EAC 中，单击“服务器”\>“服务器”，选择服务器，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后单击“传输限制”。

2.  在“重试”部分，为“出站连接失败重试间隔(秒)”、“瞬间失败重试间隔(分钟)”或“瞬间失败重试次数”输入值。

3.  完成后，单击“保存”。

## 使用命令行管理程序配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔

使用以下语法在邮箱服务器或边缘传输服务器上的传输服务中配置瞬间失败重试次数、瞬间失败重试间隔和出站连接失败重试间隔。

```powershell
Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>
```

此示例在名为 Mailbox01 的邮箱服务器上更改以下值：在边缘传输服务器 Exchange01 上。

  - 瞬间失败重试次数设置为 8。

  - 瞬间失败重试间隔设置为 1 分钟。

  - 出站连接失败重试间隔设置为 45 分钟。

<!-- end list -->

```powershell
Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00
```

> [!NOTE]  
> 客户端访问服务器上的前端传输服务的 <strong>Set-FrontEndTransportService</strong> cmdlet 也提供 <em>TransientFailureRetryCount</em> 和 <em>TransientFailureRetryInterval</em> 参数。


## 使用命令行管理程序配置邮件重试间隔

默认情况下，邮件重试间隔是 `00:15:00` 或 15 分钟。建议您不要修改默认值，除非 Microsoft 客户服务和支持人员建议您这样做。

使用以下语法设置邮件重试间隔。

```powershell
Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>
```

此示例在名为 Mailbox01 的邮箱服务器上将邮件重试间隔更改为 20 分钟。

```powershell
Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00
```

## 配置延迟 DSN 超时设置

可以使用 EAC 或命令行管理程序配置延迟 DSN 通知超时间隔。此设置仅适用于本地传输服务器。只能使用命令行管理程序启用或禁用将延迟 DSN 邮件发送到内部和外部发件人。这些设置适用于组织中所有的传输服务器。

> [!NOTE]  
> 在 Exchange 2007 集线器传输服务器上，所有 <em>ExternalDSN*</em> 和 <em>InternalDSN*</em> 参数在 <strong>Set-TransportServer</strong> cmdlet 都可用，在 <strong>Set-TransportConfig</strong> cmdlet 上不可用。如果组织中有任何 Exchange 2007 集线器传输服务器，则需要在每个 Exchange 2007 集线器传输服务器上使用 <strong>Set-TransportServer</strong> cmdlet 对这些值进行更改。


## 使用 EAC 配置延迟 DSN 邮件通知超时间隔

1.  在 EAC 中，单击“服务器”\>“服务器”，选择服务器，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后单击“传输限制”。

2.  在“通知”部分，为“当邮件延迟以下时间(小时)后通知发件人”输入值。

3.  完成后，单击“保存”。

## 使用命令行管理程序配置延迟 DSN 邮件通知超时间隔

使用以下语法设置邮件重试间隔。

```powershell
Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>
```

此示例在名为 Mailbox01 的邮箱服务器上将延迟 DSN 邮件通知超时间隔更改为 6 小时。

```powershell
Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00
```

## 使用命令行管理程序启用或禁用向外部或内部邮件发件人发送延迟 DSN 通知

使用以下语法配置延迟 DSN 通知设置。

```powershell
Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>
```

此示例阻止将延迟 DSN 通知邮件发送给外部发件人。

```powershell
Set-TransportConfig -ExternalDelayDSNEnabled $false
```

此示例阻止将延迟 DSN 通知邮件发送给内部发件人。

```powershell
Set-TransportConfig -InternalDelayDSNEnabled $false
```

## 配置邮件过期超时间隔

## 使用 EAC 配置邮件过期超时间隔

1.  在 EAC 中，单击“服务器”\>“服务器”，选择服务器，单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")，然后单击“传输限制”。

2.  在“邮件过期”部分，为“自提交之后的最长时间(天)”输入值。

3.  完成后，单击“保存”。

## 使用命令行管理程序配置邮件过期超时间隔

若要配置邮件过期超时间隔，请使用以下语法。

```powershell
Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>
```

此示例在名为 Mailbox01 的 Exchange 服务器上将邮件过期超时间隔更改为 4 天。

```powershell
Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00
```

