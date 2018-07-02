﻿---
title: '启用或禁用 Outlook Voice Access 的用户: Exchange Online Help'
TOCTitle: 启用或禁用 Outlook Voice Access 的用户
ms:assetid: c0c244a0-ad2f-4adf-bc1f-1d55fd7ea2d5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351106(v=EXCHG.150)
ms:contentKeyID: 52061463
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用 Outlook Voice Access 的用户

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-12-12_

您可以启用或禁用Outlook语音与统一消息 (UM) 邮箱策略相关联的已启用 UM 的用户的访问权。Outlook访问语音是由启用 UM 的用户通过手机访问其邮箱的功能。默认情况下，启用此设置。

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅　[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

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

## 使用 EAC 启用或禁用 Outlook Voice Access

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面上，选择或清除\&quot;允许 Outlook Voice Access\&quot;旁的复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序启用或禁用 Outlook Voice Access

此示例允许与 UM 邮箱策略 `MyUMMailboxPolicy` 关联的用户使用 Outlook Voice Access。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $true

此示例组织与 UM 邮箱策略 `MyUMMailboxPolicy` 关联的用户使用 Outlook Voice Access。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowSubscriberAccess $false

