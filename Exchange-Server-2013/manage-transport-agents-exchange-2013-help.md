---
title: '管理传输代理: Exchange 2013 Help'
TOCTitle: 管理传输代理
ms:assetid: f15ab7e4-015d-45b1-9c10-f733d7cd2a36
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125175(v=EXCHG.150)
ms:contentKeyID: 50491953
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理传输代理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

传输代理使用 SMTP 事件对传输管道中运行的邮件进行操作。大多数 Microsoft Exchange Server 2013 中所包含的内置传输代理不可见，也不可管理。然而，您可以在您组织中的 Exchange 服务器上安装和配置第三方传输代理。有关传输代理的详细信息，请参阅[传输代理](transport-agents-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md) 主题中的“传输代理”条目。

  - 只能使用命令行管理程序执行此过程。

  - 旧版传输代理支持未默认启动，但是您可以启动。有关说明，请参阅[启用对旧版传输代理的支持](enable-support-for-legacy-transport-agents-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 关于客户端访问服务器上的前端传输服务的传输代理程序

您不可以使用 Exchange 命令行管理程序对在客户端访问服务器上的前端传输服务的传输代理进行管理。而是要打开客户端访问服务器上的 Windows PowerShell，然后导入 Exchange cmdlets 至 Windows PowerShell 会话。

> [!CAUTION]  
> 支持运行 Windows PowerShell 中的 Exchange cmdlets 以执行任务，而不支持对前端传输服务中的传输代理进行管理。如果您运行 Windows PowerShell 中的 Exchange cmdlets 并绕过 Exchange 命令行管理程序和基于角色的访问控制 (RBAC)，会造成严重的结果。在 Exchange 命令行管理程序中，应始终运行 Exchange cmdlet。有关详细信息，请参阅 <a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange 2013 发行说明</a>。


要执行前端传输服务中本主题所描述的任何传输代理程序，您应执行以下附加步骤：

1.  在客户端访问服务器上，打开 Windows PowerShell 并运行以下命令：
    
        Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn

2.  运行所述命令，并向命令中添加下列值：`-TransportService FrontEnd`.
    
    例如，要查看客户端访问服务器上的前端传输服务中的传输代理，应运行以下命令：
    
        Get-TransportAgent -TransportService FrontEnd

## 使用命令行管理程序安装传输代理

安装传输代理时，Exchange 只注册与该传输代理关联的 DLL。需要确保已正确安装和配置传输代理所依赖的所有文件、注册表项和其他对象。当 Exchange 加载了 DLL 之后，它会在命令完成后继续引用这些 DLL。

传输代理对其遇到的所有电子邮件都具有完全访问权限。Exchange 对传输代理的行为没有任何限制。不稳定的或带有安全缺陷的传输代理可能会影响 Exchange 的稳定性和安全性。因此，您应该只安装自己完全信任并且已在测试环境中经过全面测试的传输代理。

在禁用状态下安装传输代理，以确保邮件流不受尚未配置的传输代理的影响。因此，在正确配置了传输代理之后，需要启用该传输代理。

使用以下语法安装传输代理。

    Install-TransportAgent -Name <TransportAgentIdentity> -TransportAgentFactory <"TransportAgentFactory"> -AssemblyPath <"FilePath">

本示例将在邮箱服务器上的传输服务中安装一个名为 Contoso Transport Agent 的虚假传输代理。

    Install-TransportAgent -Name "Contoso Transport Agent" -TransportAgentFactory "vendor.exchange.ContosoTransportAgentfactory" -AssemblyPath "C:\Program Files\Vendor\TransportAgent\ContosoTransportAgentFactory.dll"

## 您如何知道这有效？

要验证是否成功安装传输代理，应运行命令 `Get-TransportAgent` 并验证传输代理已列出。

## 使用命令行管理程序启动传输代理

使用以下语法启动传输代理。

    Enable-TransportAgent <TransportAgentIdentity>

本示例将在邮箱服务器上的传输服务中启动一个名为 Contoso Transport Agent 的传输代理。

    Enable-TransportAgent "Contoso Transport Agent"

## 您如何知道这有效？

要验证是否成功启动传输代理，应运行命令 `Get-TransportAgent | Format-List Name,Enabled` 并验证传输代理已启动。

## 使用命令行管理程序禁用传输代理

使用以下语法禁用传输代理：

    Disable-TransportAgent <TransportAgentIdentity>

本示例将在邮箱服务器上的传输服务中禁用一个名为 Fabirkam Transport Agent 的传输代理。

    Disable-TransportAgent "Fabrikam Transport Agent"

## 您如何知道这有效？

要验证是否成功禁用传输代理，应运行命令 `Get-TransportAgent | Format-List Name,Enabled` 并验证传输代理已禁用。

## 使用命令行管理程序查看传输代理

若要查看所有传输代理的摘要列表，请运行以下命令：

    Get-TransportAgent

若要查看特定传输代理的详细配置，请运行以下命令：

    Get-TransportAgent <TransportAgentIdentity> | Format-List

本示例将提供名为传输规则代理的传输代理的详细配置。

    Get-TransportAgent "Transport Rule Agent" | Format-List

## 使用命令行管理程序配置传输代理的优先级

优先级最接近 0 的传输代理将首先处理电子邮件。然而，传输代理注册的传输管道中的 SMTP 事件可能导致低优先级的代理在高优先级代理之前对邮件进行操作。

若要修改现有传输代理的优先级，请运行以下命令：

    Set-TransportAgent <TransportAgentIdentity> -Priority <Integer>

本示例将为邮箱服务器上的传输服务中名为 Contoso Transport Agent 的现有传输代理将优先级代理值设置为 3。

    Set-TransportAgent "Contoso Transport Agent" -Priority 3

## 您如何知道这有效？

要验您是否成功配置了传输代理的优先级，请运行命令 `Get-TransportAgent | Format-List Name,Priority` 并验证传输代理的优先级值。

## 使用命令行管理程序卸载传输代理

卸载传输代理时，Exchange 将取消注册与代理一起使用的 DLL 文件。Exchange 不会删除任何文件、注册表项或由传输代理安装操作添加的其他对象。

要卸载传输代理，请运行以下命令：

    Uninstall-TransportAgent <TransportAgentIdentity>

本示例将在邮箱服务器上的传输服务中卸载一个名为 Fabirkam Transport Agent 的传输代理。

    Uninstall-TransportAgent "Fabrikam Transport Agent"

## 您如何知道这有效？

要验证是否成功卸载传输代理，应运行命令 `Get-TransportAgent` 并验证传输代理未列出。

