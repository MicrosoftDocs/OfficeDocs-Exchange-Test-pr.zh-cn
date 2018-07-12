---
title: '禁用常见的语音邮件 PIN 模式: Exchange Online Help'
TOCTitle: 禁用常见的语音邮件 PIN 模式
ms:assetid: eecc40ae-fac7-41e4-a1e1-16330f4462a3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125160(v=EXCHG.150)
ms:contentKeyID: 50556695
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用常见的语音邮件 PIN 模式

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以启用或禁用常见Outlook语音访问用户的统一邮件 (UM) 针模式。如果您启用或禁用 UM 邮箱策略上设置常见的固定模式，该设置将应用于与该 UM 邮箱策略相关联的所有已启用 UM 的用户。默认情况下，启用 UM 的用户不能创建 PIN 时使用常见的模式。

您可以在 UM 邮箱策略上配置几针相关设置。**允许通用 PIN 模式**设置用于允许或阻止通用数字模式的使用，当用户创建一个 PIN。默认情况下，此设置处于禁用状态，可以防止用户使用的下列数字模式 ︰

  - **序列号**  这些都是包括连续数字的 PIN 值。Pin 的连续编号的示例有 1234年和 65432。

  - **Repeated 号**  它们包括重复的数字的 PIN 值。重复的数字和都是 11111 22222。

  - **后缀的邮箱扩展**  这些都是包含用户的邮箱扩展的后缀的 PIN 值。例如，如果用户的邮箱扩展为 36697，该用户的 PIN 不能为 3669712。

> [!NOTE]
> 如果启用&amp;quot;允许常用 PIN 模式&amp;quot;设置，则只会拒绝邮箱分机号码后缀。


有关 Outlook Voice Access PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 禁用常见 PIN 模式

1.  在 EAC，导航到**统一消息**\> **UM 拨号计划**。在列表视图中，选择您要修改，该 UM 拨号计划，然后在工具栏上，单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面上，在\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页上的\&quot;PIN 策略\&quot;下，清除\&quot;允许常用 PIN 模式\&quot;旁边的复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序禁用常见 PIN 模式

此示例阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的用户使用包含常见模式的 PIN。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $false

