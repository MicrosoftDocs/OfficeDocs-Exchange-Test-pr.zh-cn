---
title: '设置以前语音邮件 Pin 以回收数: Exchange Online Help'
TOCTitle: 设置以前语音邮件 Pin 以回收数
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50556657
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置以前语音邮件 Pin 以回收数

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

Outlook语音访问用户拨入到 Outlook Voice Access 编号，这些系统会提示您输入他们的 PIN，这样的语音邮件系统可以对它们进行验证。他们通过身份验证后，他们可以从任何电话访问语音邮件、 电子邮件、 日历，和其邮箱中的个人联系信息。

可以统一邮件 (UM) 邮箱策略上配置多个针相关设置。**PIN 回收计数**设置指定他们可以重复使用旧的 PIN 之前，必须使用唯一的针脚用户数。您可以设置此设置 1 到 20 之间的值。对于大多数组织，此值应设置到 5 针，这是默认值。设置此值过高可以受挫的用户，因为它可为用户创建和记忆许多针困难。设置得过低可能会引入到您的网络安全威胁。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>不能禁用 PIN 再循环计数。</td>
</tr>
</tbody>
</table>


有关 Outlook Voice Access PIN 安全性相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 更改 PIN 再循环计数

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择您要更改的拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要更改的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击\&quot;PIN 策略\&quot;，在\&quot;PIN 再循环计数\&quot;旁边，输入一个介于 1 和 20 之间的值。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改 PIN 再循环计数

此示例将 UM 邮箱策略 `MyUMMailboxPolicy` 的 PIN 再循环计数设置为 10。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

