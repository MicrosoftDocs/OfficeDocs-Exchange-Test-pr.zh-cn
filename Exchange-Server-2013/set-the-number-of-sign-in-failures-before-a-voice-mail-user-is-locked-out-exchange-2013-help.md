---
title: '语音邮件用户被锁定之前设置的登录失败次数: Exchange Online Help'
TOCTitle: 语音邮件用户被锁定之前设置的登录失败次数
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50556610
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 语音邮件用户被锁定之前设置的登录失败次数

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置Outlook语音访问用户无法访问其邮箱之前所允许的登录失败的次数。语音邮件用户锁定之前允许的登录失败次数上统一邮件 (UM) 邮箱策略，配置并应用于所有已启用 UM 的用户与该 UM 邮箱策略相关联。默认情况下将它设置为 15。

若要提高安全性，减少失败尝试的最大数目。但是，请记住，如果缩小为比默认值要低得多的数字，用户可能会锁定不必要。统一的消息将生成警告事件，您可以查看已启用 UM 的用户的 PIN 身份验证失败时，或在尝试登录到系统时，用户是不成功，请使用事件查看器。重置 PIN 之前，此设置必须大于设置的登录失败的次数。

有关与 Outlook Voice Access PIN 安全相关的其他任务，请参阅[针的安全程序](pin-security-procedures-exchange-2013-help.md)。

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

## 使用 EAC 配置语音邮件用户被锁定之前的登录失败次数

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要更改的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击\&quot;PIN 策略\&quot;，然后在\&quot;锁定前的登录失败的次数\&quot;旁边输入一个 1 到 999 之间的值。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置语音邮件用户被锁定之前的登录失败次数

此示例将与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联并且启用了 UM 的用户的最多登录尝试次数设置为 10。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

此示例针对与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联并且启用了 UM 的用户，将重置 Outlook Voice Access 用户的 PIN 之前登录失败的次数设置为 3，将尝试登录的最大次数设置为 5，并将 PIN 的最短长度设置为 9。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

