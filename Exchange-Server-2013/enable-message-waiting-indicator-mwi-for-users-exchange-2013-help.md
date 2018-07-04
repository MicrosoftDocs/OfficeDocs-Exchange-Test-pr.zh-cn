---
title: '为用户启用消息等待指示符 (MWI): Exchange Online Help'
TOCTitle: 为用户启用消息等待指示符 (MWI)
ms:assetid: 3d0ca657-00b6-4108-a850-b092fede1f75
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335216(v=EXCHG.150)
ms:contentKeyID: 50556553
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为用户启用消息等待指示符 (MWI)

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

您可以启用或禁用消息等待指示符与统一消息 (UM) 邮箱策略相关联的用户。消息等待指示符是最传统的语音邮件系统中找到的功能。以其最常见的形式，它在语音邮件订阅者的电话，以指示存在新的语音邮件信息光源灯。消息等待指示符也可以为已启用 UM 的用户的移动电话发送文本消息。默认设置为启用。

如果在 UM IP 网关上禁用邮件等待指示器，则此功能不对与 UM 邮箱策略关联的启用 UM 的用户可用。

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用邮件等待指示器

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页面上，选中\&quot;允许邮件等待指示器\&quot;旁的复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序启用邮件等待指示器

本示例为与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户启用邮件等待指示器。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $true

