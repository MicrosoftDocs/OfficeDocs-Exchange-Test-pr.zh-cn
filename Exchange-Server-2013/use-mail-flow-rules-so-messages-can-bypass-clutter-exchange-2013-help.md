---
title: '使用邮件流规则以便邮件可以规避待筛选邮件功能: Exchange 2013 Help'
TOCTitle: 使用邮件流规则以便邮件可以规避待筛选邮件功能
ms:assetid: 58e413f0-aa27-4307-bffd-4df03090a15e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn896639(v=EXCHG.150)
ms:contentKeyID: 64141271
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用邮件流规则以便邮件可以规避待筛选邮件功能

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

如果您想要确保收到特定邮件，您可以创建 Exchange 传输规则，以确保这些邮件绕过混乱邮件文件夹。有关混乱邮件的详细信息，请查看[在 Outlook Web App 中使用混乱邮件排序低优先级邮件](https://go.microsoft.com/fwlink/p/?linkid=528411)。

有关与传输规则相关的其他管理任务，请查看[Exchange Online 中的邮件流规则（传输规则）](https://technet.microsoft.com/zh-cn/library/jj919238\(v=exchg.150\))和 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\)) PowerShell 主题。如果您是初次使用 PowerShell，请查看以下有关使用 Powershell 的帮助主题：

  - [使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))

  - [使用远程命令行管理程序连接到 Exchange](https://technet.microsoft.com/zh-cn/library/dd335083\(v=exchg.150\))

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“传输规则”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 使用 UI 创建传输规则，以便绕过“待筛选邮件”文件夹

此示例允许带标题“会议”的所有邮件绕过待筛选邮件。

1.  在 Exchange 管理中心，导航到“邮件流”\>“规则”。单击“![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")”，然后选择“新建规则…”。

2.  创建新规则完成后，请单击“保存”启动该规则。

![图片示例：如果主题中包含会议，则绕过待筛选邮件](images/Dn896639.75957aa4-4b2a-4142-92ff-07f8ccc64d82(EXCHG.150).png "图片示例：如果主题中包含会议，则绕过待筛选邮件")

## 使用命令行管理程序创建传输规则，以便绕过混乱邮件文件夹

此示例允许带标题“会议”的所有邮件绕过混乱邮件。

    New-TransportRule -Name <name_of_the_rule> -SubjectContainsWords "Meeting" -SetHeaderName "X-MS-Exchange-Organization-BypassClutter" -SetHeaderValue "true"

> [!IMPORTANT]  
> 在此示例中，“X-MS-Exchange-Organization-BypassClutter”和“true”区分大小写。


有关语法和参数的详细信息，请参阅 [New-TransportRule](https://technet.microsoft.com/zh-cn/library/bb125138\(v=exchg.150\))。

## 您如何知道操作成功？

你可以检查电子邮件头以查看是否由于待筛选邮件传输规则绕过导致电子邮件登录收件箱。在已应用待筛选邮件绕过传输规则的组织中，从邮箱中挑选电子邮件。查看邮件上标记的邮件头，你应该会看到 **X-MS-Exchange-Organization-BypassClutter: true** 邮件头。这意味着正在绕过。有关如何查找邮件头的信息，请参阅[查看电子邮件的 Internet 邮件头](https://go.microsoft.com/fwlink/p/?linkid=822530)。

> [!NOTE]  
> 日历项目（如接受、发送或拒绝的会议）不会有这些邮件头。我们很快会将待筛选邮件功能扩展到这些日历项目。

