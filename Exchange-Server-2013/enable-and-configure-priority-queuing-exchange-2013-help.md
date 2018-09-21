---
title: '启用和配置队列优先级: Exchange 2013 Help'
TOCTitle: 启用和配置队列优先级
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51408201
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用和配置队列优先级

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

*优先级队列*是 Microsoft Exchange Server 2013 ，使配置在 Microsoft Outlook 或Outlook Web Access影响的邮箱服务器上的传输服务处理消息的发件人的邮件优先级的功能。启用优先级队列后，高优先级的邮件将被传输到目的地之前正常优先级的邮件，和普通优先级消息被传输到目的地之前低优先级的邮件。有关详细信息，请参阅[排队优先级](priority-queuing-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - Exchange 权限不适用于本主题中的过程。这些过程在 Exchange Server 的操作系统中执行。

  - 保存到 EdgeTransport.exe.config 应用程序配置文件中的更改在重新启动 Microsoft Exchange 传输服务之后应用。

  - 重新启动 Microsoft Exchange 传输服务时，会临时中断服务器上的邮件流。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令提示符在 EdgeTransport.exe.config 文件中启用和配置排队优先级

1.  在命令提示符窗口中，通过运行以下命令在记事本中打开 EdgeTransport.exe.config 应用程序配置文件：
    
    ```powershell
Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
```

2.  找到 `<appSettings>` 部分中的以下键。
    
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    
    要在邮箱服务器上的传输服务中启用排队优先级，请使用以下值：
    
    ```command line
<add key="PriorityQueuingEnabled" value="true" />
```
    
    配置其余排队优先级值，或保留默认值。

3.  完成后，保存并关闭 EdgeTransport.exe.config 文件。

4.  通过运行以下命令重新启动 Microsoft Exchange 传输服务：
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 您如何知道操作成功？

要验证是否已成功启用和配置排队优先级，请执行以下操作：

1.  验证 EdgeTransport.exe.config 文件中的 **PriorityQueueinEnabled** 键的值为 `"true"`。

2.  使用 Outlook 创建高优先级测试邮件，其值大于 **MaxHighPriorityMessageSize** 键指定的值，并验证该邮件和普通优先级邮件同时到达。

3.  尝试验证优先级高的消息，在低优先级的邮件发送到同一个收件人或目标之前到达。您可以尝试使用多个邮箱发送多个，同时使用不同的优先级值到同一个收件人邮件类似测试。

