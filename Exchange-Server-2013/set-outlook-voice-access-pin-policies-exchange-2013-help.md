---
title: '设置 Outlook Voice Access PIN 策略: Exchange Online Help'
TOCTitle: 设置 Outlook Voice Access PIN 策略
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50556577
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置 Outlook Voice Access PIN 策略

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以设置 PIN 策略统一邮件 (UM) 邮箱策略。UM 邮箱策略可以配置来提高通过要求用户以符合预定义的 PIN 策略，为您的组织使用 Outlook Voice Access 的启用 UM 的用户的安全级别。

若要设置 Outlook Voice Access 用户 PIN 策略，可以创建新的 UM 邮箱策略或修改现有 UM 邮箱策略。创建新的 UM 邮箱策略后，然后可以通过配置以下 PIN 设置配置的 UM 邮箱策略 ︰

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

它是实施强为 UM 的用户的 PIN 要求安全最佳做法。这可以通过创建要求 6 个或更多位数的针脚和提高网络的安全性级别的 UM PIN 策略强制执行。

更改 PIN 策略时，新 PIN 设置应用于当前与该 UM 邮箱策略关联的用户。例如，如果您修改 UM 邮箱策略，改为小针长度从 7 10 位数字，用户在下次登录他们将不得不更改 PIN 以满足更改的 PIN 要求。

有关与 Outlook Voice Access PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

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

## 使用 EAC 为 Outlook Voice Access 用户设置 PIN 策略

1.  在 EAC，导航到**统一消息**\> **UM 拨号计划**。在列表视图中，单击您想要编辑的 UM 拨号计划，然后单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要编辑的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  单击\&quot;属性\&quot;。

4.  在\&quot;UM 邮箱策略\&quot;页面上，单击\&quot;PIN 策略\&quot;。

5.  在\&quot;PIN 策略\&quot;页面上，为与此 UM 邮箱策略关联的 Outlook Voice Access 用户配置 PIN 设置，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序为 Outlook Voice Access 用户设置 PIN 策略

本示例为与 UM 邮箱策略 `MyUMMailboxPolicy` 关联的用户设置 PIN 设置。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

