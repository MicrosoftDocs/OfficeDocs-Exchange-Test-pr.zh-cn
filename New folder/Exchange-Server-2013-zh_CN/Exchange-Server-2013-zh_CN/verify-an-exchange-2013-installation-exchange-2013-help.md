---
title: '验证 Exchange 2013 安装: Exchange 2013 Help'
TOCTitle: 验证 Exchange 2013 安装
ms:assetid: fdd20a2a-c8c1-4d17-b813-3c05d88a4411
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125254(v=EXCHG.150)
ms:contentKeyID: 50492028
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 验证 Exchange 2013 安装

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

安装 Microsoft Exchange Server 2013 后，我们建议您通过运行 **Get-ExchangeServer** cmdlet 并检查安装日志文件来验证安装。如果安装过程失败，或在安装期间出错，则可以使用安装日志文件查找问题的来源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

## 运行 Get-ExchangeServer

若要验证 Exchange 2013 安装是否成功，请在 Exchange 命令行管理程序中运行 **Get-ExchangeServer** cmdlet。将显示运行此 cmdlet 时在指定服务器上安装的所有 Exchange 2013 服务器角色。

有关语法和参数的详细信息，请参阅 [Get-ExchangeServer](https://technet.microsoft.com/zh-cn/library/bb123873\(v=exchg.150\))。

## 复查安装日志文件

通过查看设置过程期间创建的设置日志文件，您还可以了解有关安装和配置 Exchange 2013 的更多信息。

在安装期间，Exchange 安装程序将在运行 Windows Server 2008 R2（Service Pack 1）（SP1）和 Windows Server 2012 的计算机上的“事件查看器”的“应用程序”日志记录事件。查看“应用程序”日志并确保没有与 Exchange 安装程序相关的警告或错误消息。这些日志文件包含 Exchange 2013 安装期间系统所执行的每个操作历史以及任何可能出现的错误。默认情况下，日志的记录方式为 `Verbose`。提供有关每个已安装服务器角色的信息。

您可以在 *\<system drive\>*\\ExchangeSetupLogs\\ExchangeSetup.log 找到安装程序日志文件。*\<system drive\>* 变量代表安装操作系统驱动器的根目录。

安装程序日志文件将跟踪 Exchange 2013 安装和配置期间所执行的每项任务的进度。它包含以下信息：开始安装前执行的先决条件检查和系统准备情况检查的状态、应用程序安装进度以及对系统所做的配置更改。检查此日志文件，以验证服务器角色已按预期方式安装。

我们建议您通过搜索任何错误开始查看安装程序日志文件。如果找到指示出错的条目，则阅读相关文本以确定引发错误的原因。

