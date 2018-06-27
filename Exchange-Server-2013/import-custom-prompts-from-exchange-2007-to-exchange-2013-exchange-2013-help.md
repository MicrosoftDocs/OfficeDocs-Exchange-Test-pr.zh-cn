---
title: '将自定义提示从 Exchange 2007 导入 Exchange 2013: Exchange 2013 Help'
TOCTitle: 将自定义提示从 Exchange 2007 导入 Exchange 2013
ms:assetid: 70c0b0bc-c0de-4e3c-8144-1fe59f86ebf4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg309147(v=EXCHG.150)
ms:contentKeyID: 54652278
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将自定义提示从 Exchange 2007 导入 Exchange 2013

 

_**适用于：**Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2015-04-08_

您可以将包含自定义问候语、通知、菜单和提示的音频文件从 Exchange 2007 统一消息 (UM) 导入至 Exchange 2013 统一消息。使用命令行管理程序脚本，提示将导入到安装 Microsoft Exchange 2013 时创建的名为 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的 Exchange 系统邮箱。该系统邮箱用于在统一消息中存储拨号计划和自动助理自定义问候语、通知、菜单、提示和 UM 报告。

.wav 或 .wma 格式的音频文件使用方法如下：

  - 在 UM 拨号计划中，音频文件用于自定义欢迎问候语和信息通知。当 Outlook Voice Access 用户呼叫 Outlook Voice Access 号码时，会播放这些音频文件。

  - 在 UM 自动助理中，音频文件用于自定义的非营业和营业时间问候语、信息通知、菜单提示和导航菜单。当呼叫者呼叫 UM 自动助理时，会播放这些音频文件。

可使用 MigrateUMCustomPrompts.ps1 脚本将所有 Exchange Server 2007 UM 自定义问候语、通知、菜单和提示的副本迁移至所有 Exchange 2007 UM 拨号计划和 UM 自动助理迁移的 Exchange 2013 UM。

默认情况下，MigrateUMCustomPrompts.ps1 脚本位于 Exchange 2013 服务器的 \<Program Files\>\\Microsoft\\Exchange Server\\V15\\Scripts 文件夹中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>MigrateUMCustomPrompts.ps1 脚本包含在 Exchange 2013 中。该脚本必须通过 Exchange 2007 UM 服务器在同一组织的 Exchange 2013 邮箱服务器上运行。</td>
</tr>
</tbody>
</table>


有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;和\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。 若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 使用 MigrateUMCustomPrompts.ps1 脚本迁移 UM 拨号计划和自动助理的所有自定义提示的副本

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange Server 2013\&quot;\>\&quot;Exchange 命令行管理程序\&quot;。

2.  在命令行管理程序中，在提示符处键入脚本的路径。例如，键入 **cd "D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**，然后按 Enter。

3.  在命令行管理程序提示符处，键入 **".\\MigrateUMCustomPrompt"**，然后按 Enter。

