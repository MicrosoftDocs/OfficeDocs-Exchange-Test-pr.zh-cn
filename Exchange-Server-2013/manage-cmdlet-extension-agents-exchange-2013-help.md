---
title: '管理 cmdlet 扩展代理: Exchange 2013 Help'
TOCTitle: 管理 cmdlet 扩展代理
ms:assetid: 9141b3cb-ad13-4415-be2f-aa89f91445f5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298143(v=EXCHG.150)
ms:contentKeyID: 50556634
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理 cmdlet 扩展代理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-19_

此主题展示如何在 Microsoft Exchange Server 2013 中启用、禁用、查看 cmdlet 扩展代理以及更改 cmdlet 扩展代理的优先级。有关 Exchange 2013 中的 cmdlet 扩展代理的详细信息，请参阅 [cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：少于 5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的\&quot;Cmdlet 扩展代理\&quot;条目。

  - 启用 `Scripting Agent` 之前，必须验证其配置正确与否。有关 `Scripting Agent` 的详细信息，请参阅[cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

  - 您必须使用命令行管理程序执行这些过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 启用 cmdlet 扩展代理

在 Exchange 2013 中启用 cmdlet 扩展代理时，该代理将在组织中每个运行 Exchange 2013 的服务器上运行。启用代理后，它将对随后可以使用该代理执行其他操作的 cmdlet 可用。

> [!CAUTION]  
> 在启用代理之前，请确保您知道代理的工作方式，以及代理将对组织造成的影响。


本示例通过使用 **Enable-CmdletExtensionAgent** cmdlet 启用 cmdlet 扩展代理。运行 cmdlet 时，必须先指定要启用代理的名称。启用 `Scripting Agent` 之前，需要确保已将 `ScriptingAgentConfig.xml` 配置文件部署到组织中的所有服务器上。如果不首先部署配置文件并启用 `Scripting``Agent`，则所有非 **Get** cmdlet 在运行时都将失败。本示例启用 `Scripting Agent`。

    Enable-CmdletExtensionAgent "Scripting Agent"

有关语法和参数的详细信息，请参阅 [Enable-CmdletExtensionAgent](https://technet.microsoft.com/zh-cn/library/dd335192\(v=exchg.150\))。

## 禁用 cmdlet 扩展代理

在 Exchange 2013 中禁用 cmdlet 扩展代理时，组织中每个运行 Exchange 2013 的服务器上都会禁用该代理。如果禁用了某个代理，它将对于所有的 cmdlet 不可用。Cmdlet 将无法再使用该代理来执行其他操作。

> [!CAUTION]  
> 在禁用代理之前，请确保您知道代理的工作方式，以及禁用代理将对组织造成的影响。


若要禁用 cmdlet 扩展代理，请使用 **Disable-CmdletExtensionAgent** cmdlet。运行 cmdlet 时，指定要禁用的代理的名称。本示例将禁用 `Scripting Agent`。

    Disable-CmdletExtensionAgent "Scripting Agent"

有关语法和参数的详细信息，请参阅 [Disable-CmdletExtensionAgent](https://technet.microsoft.com/zh-cn/library/dd298132\(v=exchg.150\))。

## 查看现有的 cmdlet 扩展代理

通过查看 cmdlet 扩展代理，可以了解哪些代理先运行，哪些代理已在 Exchange 2013 组织中启用。有关管道传递和 **Format-Table** cmdlet 的详细信息，请参阅下列主题：

  - [管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))

  - [使用命令输出](working-with-command-output-exchange-2013-help.md)

本示例通过使用 **Get-CmdletExtensionAgent** cmdlet 来获取特定 cmdlet 扩展代理的详细信息。在本示例中，将返回 `Mailbox Permissions Agent` 的详细信息。

    Get-CmdletExtensionAgent "Mailbox Permissions Agent"

此示例通过使用 **Get-CmdletExtensionAgent** cmdlet 来获取多个 cmdlet 扩展代理，然后通过管道将输出传递到 **Format-Table** cmdlet。本示例显示了组织中所有 cmdlet 扩展代理的列表，而且通过使用 **Format-Table** cmdlet 将各个代理的 **Name**、**Enabled** 和 **Priority** 属性显示在表中。

    Get-CmdletExtensionAgent | Format-Table Name, Enabled, Priority

有关语法和参数的详细信息，请参阅 [Get-CmdletExtensionAgent](https://technet.microsoft.com/zh-cn/library/dd297946\(v=exchg.150\))。

## 更改 cmdlet 扩展代理的优先级

如果希望某个代理在另一个代理之前由 cmdlet 调用，能够在 Exchange 2013 中更改 cmdlet 扩展代理的优先级会非常有用。如果创建在 `Scripting Agent` 中运行的自定义脚本，并且希望该脚本的优先级高于内置代理，那么这一能力尤其有用。有关 `Scripting Agent` 的详细信息，请参阅[cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

> [!CAUTION]  
> 更改内置代理的优先级或替换内置代理的功能是一项高级操作。请确保您完全了解要进行的更改。


代理是从零到最大代理数排序的。越接近零的代理，其优先级越高。先调用具有更高优先级的代理。有关代理优先级的详细信息，请参阅[cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

本示例通过使用 **Set-CmdletExtensionAgent** cmdlet 更改 cmdlet 扩展代理的优先级。在本示例中，`Scripting Agent` 的优先级更改为 3。

    Set-CmdletExtensionAgent "Scripting Agent" -Priority 3

有关语法和参数的详细信息，请参阅 [Set-CmdletExtensionAgent](https://technet.microsoft.com/zh-cn/library/dd335175\(v=exchg.150\))。

