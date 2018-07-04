---
title: '配置管道跟踪: Exchange 2013 Help'
TOCTitle: 配置管道跟踪
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52061481
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置管道跟踪

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

在邮箱服务器和边缘传输服务器上的传输服务或邮箱传输服务中，管道跟踪在传输管道中移动时，会捕获电子邮件的副本。

## 在开始之前，您需要知道什么？

  - 估计完成该过程的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;传输服务\&quot;和\&quot;邮箱传输服务\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 管道跟踪将复制从发件人的电子邮件地址发送的电子邮件的完整内容。为了避免错误地暴露机密信息，需要在管道跟踪文件夹的位置上设置适当的安全权限。

  - 不要长时间启用管道跟踪。管道跟踪创建快速堆积的多个邮件快照文件。启用管道跟踪时，要始终监视可用磁盘空间。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 启用并配置管道跟踪

## 步骤 1：使用命令行管理程序配置管道跟踪发件人地址

使用以下语法配置管道跟踪发件人地址。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

本示例配置管道跟踪以捕获 Mailbox01 邮箱服务器上传输服务中发件人 chris@contoso.com 发送的所有邮件快照。

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

本示例配置管道跟踪以捕获 Mailbox02 邮箱服务器上传输服务收到的所有系统生成的邮件的快照。

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"

> [!CAUTION]
> 配置管道跟踪以捕获传输服务中的所有服务器生成的邮件，这可能会使服务器上的负载明显增加，迅速占用可用磁盘空间。启用管道跟踪时，要始终监视可用磁盘空间。


## 步骤 2：（可选）使用命令行管理程序指定自定义管道跟踪文件夹

启用了管道跟踪，且邮件满足您使用流通过服务器上传输服务的 *PipelineTracingSenderAddress* 参数所指定的条件后，默认的管道跟踪文件夹才会存在。对于邮箱服务器上的传输服务，默认的位置为 `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`。对于邮箱服务器上的邮箱传输服务，默认的位置为 `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`。若要指定自定义路径，该路径必须在本地 Exchange 服务器上。

使用以下语法配置管道跟踪文件夹。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

本示例将 Mailbox01 邮箱服务器上的传输服务的管道跟踪文件夹设置到 D:\\Hub\\Pipeline Tracing。

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## 步骤 3：使用命令行管理程序启用管道跟踪

默认情况下，所有 Exchange 服务器上都禁用管道跟踪。启用管道跟踪时，仅启用了指定 Exchange 服务器上特定传输服务中的管道跟踪。您需要先指定步骤 1 中说明的发件人地址，才能启用管道跟踪。

使用以下语法启用管道跟踪。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

本示例启用了 Mailbox01 邮箱服务器上传输服务中的管道跟踪。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## 您如何知道操作成功？

要验证您是否已成功配置管道跟踪，请执行下列操作：

1.  运行以下命令：
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  验证显示的值是否为您配置的值。

3.  检查传输服务或邮箱传输服务的管道跟踪文件夹，并验证邮件快照文件已在该文件夹中创建。

## 禁用管道跟踪

由于与管道跟踪相关的磁盘空间和安全问题，管道跟踪是进行诊断或故障排除的临时操作。无论何时启用管道跟踪，请始终记得在完成后禁用。

使用以下语法禁用管道跟踪。

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

本示例禁用了 Mailbox01 邮箱服务器上传输服务中的管道跟踪。

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## 您如何知道操作成功？

要验证您是否已成功禁用管道跟踪，请执行下列操作：

1.  运行以下命令：
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  验证 *PipelineTracingEnabled* 参数的值是否为 $false。

3.  检查管道跟踪文件夹，并确认邮件快照文件将不再在该文件夹中创建。

