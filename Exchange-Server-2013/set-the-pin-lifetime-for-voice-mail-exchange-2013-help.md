---
title: '设置语音邮件的 pin 码寿命: Exchange Online Help'
TOCTitle: 设置语音邮件的 pin 码寿命
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50556673
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置语音邮件的 pin 码寿命

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-22_

您可以配置用户的统一邮件 (UM) 启用 PIN 生存期。PIN 生存期是Outlook语音访问 PIN 将是有效的已启用 UM 的收件人的最大时间。PIN 生存期设置在 UM 邮箱策略上配置并应用于所有已启用 UM 的用户与该 UM 邮箱策略相关联。

可以在 UM 邮箱策略上配置几个针相关设置。PIN 生存期设置控制的时间间隔，以天为单位，从日期Outlook语音访问用户上次更改其 PIN 到它们将不得不再次改变他们的 PIN 的日期。范围是 0 到 999 之间，默认值为 60 天。如果输入 0，则用户的 PIN 不会过期。建议您不配置此设置为 0，因为通过这样可以显著降低网络的安全性。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当用户的 PIN 将要过期时，统一消息不会向用户发出通知。</td>
</tr>
</tbody>
</table>


有关 Outlook Voice Access PIN 安全相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 配置 PIN 生存期

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要更改的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击\&quot;PIN 策略\&quot;，在\&quot;强制 PIN 生存期(天)\&quot;旁边，输入一个介于 0 和 999 之间的值。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置 PIN 生存期

此示例将 PIN 可用于 Outlook Voice Access 用户的天数设置为 30，这些用户与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

此示例为 Outlook Voice Access 用户配置以下 PIN 相关设置，这些用户与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联：

  - 将重置用户的 PIN 之前的登录失败次数设置为 3。

  - 将最大登录尝试次数设置为 5。

  - 将最小 PIN 长度设置为 9 位。

  - 将 PIN 设置为在 40 天内过期。

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

