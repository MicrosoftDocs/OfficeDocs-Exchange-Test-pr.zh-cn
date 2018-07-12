---
title: '在邮箱服务器上启用反垃圾邮件功能: Exchange 2013 Help'
TOCTitle: 在邮箱服务器上启用反垃圾邮件功能
ms:assetid: 59d22c5e-64bc-4879-8ad1-364862b6ba11
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201691(v=EXCHG.150)
ms:contentKeyID: 50490614
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在邮箱服务器上启用反垃圾邮件功能

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-01-23_

在 Microsoft Exchange Server 2013 中，可在邮箱服务器上的传输服务中使用以下反垃圾邮件代理，但是默认情况下不会安装这些代理：

  - 内容筛选器代理

  - 发件人 ID 代理

  - 发件人筛选器代理

  - 收件人筛选器代理

  - 发件人信誉的协议分析代理

但是，可以通过在 Exchange 命令行管理程序中使用脚本，在邮箱服务器上安装这些反垃圾邮件代理。 通常，仅当组织接受所有传入邮件而之前未进行任何反垃圾邮件筛选时，才会在邮箱服务器上安装反垃圾邮件代理。

如果在邮箱服务器上的传输服务中安装可用反垃圾邮代理，但是会让其他 Exchange 反垃圾邮代理在邮件到达邮箱服务器之前对邮件进行操作，那么会发生什么情况？ 例如，如果在外围网络中具有将传入邮件直接传递到邮箱服务器上的传输服务的 Microsoft Exchange 2007 或 Exchange 2010 边缘传输服务器，那么会发生什么情况？ 邮箱服务器上的反垃圾邮代理可识别由其他 Exchange 反垃圾邮件代理添加到邮件的反垃圾邮件 X 标头值，并且包含这些 X 标头的邮件会通过而不再次进行扫描。 但是，会再次在邮箱服务器上进行收件人筛选器代理执行的收件人查找。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输配置”条目。

  - 连接筛选器代理和附件筛选器代理在邮箱服务器上不可用。它们仅在边缘传输服务器上可用。 但是，默认情况下会在邮箱服务器上安装并启用恶意软件代理。有关详细信息，请参阅[反恶意软件保护](anti-malware-protection-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：使用命令行管理程序运行 Install-AntispamAgents.ps1 脚本

运行以下命令：

    & $env:ExchangeInstallPath\Scripts\Install-AntiSpamAgents.ps1

## 您如何知道此步骤有效？

如果脚本运行而未出现错误，并要求您重新启动 Microsoft Exchange 传输服务，则会知道此步骤有效。

## 步骤 2：使用命令行管理程序重新启动 Microsoft Exchange 传输服务

运行以下命令：

    Restart-Service MSExchangeTransport

## 您如何知道此步骤有效？

如果 Microsoft Exchange 传输服务重新启动而未出现错误，则您会知道此步骤有效。

## 步骤 3：使用命令行管理程序指定组织中的内部 SMTP 服务器

需要指定发件人 ID 代理应忽略的任何内部 SMTP 服务器的 IP 地址。 事实上，需要指定至少一个内部 SMTP 服务器的 IP 地址。如果运行反垃圾邮件代理的邮箱服务器是组织中唯一的 SMTP 服务器，请指定该计算机的 IP 地址。

若要在不影响任何现有值的情况下添加内部 SMTP 服务器的 IP 地址，请运行以下命令：

    Set-TransportConfig -InternalSMTPServers @{Add="<ip address1>","<ip address2>"...}

此示例将内部 SMTP 服务器地址 10.0.1.10 和 10.0.1.11 添加到组织的传输配置中。

    Set-TransportConfig -InternalSMTPServers @{Add="10.0.1.10","10.0.1.11"}

## 您如何知道此步骤有效？

若要验证是否成功指定了至少一个内部 SMTP 服务器的 IP 地址，请执行以下操作：

1.  运行以下命令：
    
        Get-TransportConfig | Format-List InternalSMTPServers

2.  验证是否显示至少一个有效内部 SMTP 服务器的 IP 地址。

