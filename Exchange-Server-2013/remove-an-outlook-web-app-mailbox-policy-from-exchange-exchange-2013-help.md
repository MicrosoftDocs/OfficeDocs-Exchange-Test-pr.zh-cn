---
title: '从 Exchange 中删除 Outlook Web App 邮箱策略: Exchange Online Help'
TOCTitle: 从 Exchange 中删除 Outlook Web App 邮箱策略
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 50491896
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从 Exchange 中删除 Outlook Web App 邮箱策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2013-03-15_

您可以使用 EAC 或命令行管理程序从 Exchange 组织中删除 MicrosoftOutlook Web App 邮箱策略。

有关与 Outlook Web App 邮箱策略相关的其他管理任务，请参阅 [Outlook Web App 邮箱策略](outlook-web-app-mailbox-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;Outlook Web App 邮箱策略\&quot;条目。

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

## 使用 EAC 删除 Outlook Web App 邮箱策略

1.  在 EAC 中，单击\&quot;权限\&quot; \> \&quot;Outlook Web 应用程序策略\&quot;。

2.  在结果窗格中，单击以选择要删除的邮箱策略。

3.  单击\&quot;删除\&quot;按钮。

4.  在确认窗口中，单击\&quot;是\&quot;删除该邮箱策略，或者单击\&quot;否\&quot;取消删除操作。

## 使用命令行管理程序删除 Outlook Web App 邮箱策略

本示例将删除一个名为 `Policy1` 的 Outlook Web App 邮箱策略。

    Remove-OwaMailboxPolicy -Name Policy1 

有关语法和参数的详细信息，请参阅 [Remove-OwaMailboxPolicy](https://technet.microsoft.com/zh-cn/library/dd298103\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已经成功地删除 Outlook Web App 邮箱策略：

  - 在 EAC，单击**权限**\> **Outlook Web App 策略**。您删除的策略应该不会再出现在列表中。

