---
title: '在个人问候语 Outlook Voice Access 用户配置限制: Exchange Online Help'
TOCTitle: 在个人问候语 Outlook Voice Access 用户配置限制
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50556680
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在个人问候语 Outlook Voice Access 用户配置限制

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

**个人问候 （分钟） 的限制**设置，您可以输入的最大与统一消息 (UM) 邮箱策略相关联的用户可以使用它来记录他们的语音邮件问候语的分钟数。此设置适用于其标准的语音邮件和他们外出语音邮件问候语。默认情况下，问候语持续时间的最大值设置为 5 分钟。但是，您可以配置问候语持续时间为 1 到 10 分钟之间的任何设置的最大值。

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

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


## 您想执行什么操作？

## 使用 EAC 更改最长问候语持续时间

1.  在 EAC，导航到**统一消息**\> **UM 拨号计划**。在列表视图中，选择您要修改，该 UM 拨号计划，然后在工具栏上，单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面 \>\&quot;常规\&quot;中的\&quot;对个人问候语的限制(分钟)\&quot;下，输入语音邮件用户个人问候语允许的时长（以分钟为单位）。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改最长问候语持续时间

此示例将 UM 邮箱策略 `MyUMMailboxPolicy` 的最长问候语持续时间配置为 3 分钟。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

