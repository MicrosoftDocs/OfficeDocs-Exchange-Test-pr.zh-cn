---
title: '为语音邮件启用无 PIN 登录: Exchange 2013 Help'
TOCTitle: 为语音邮件启用无 PIN 登录
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54652279
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为语音邮件启用无 PIN 登录

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-04-08_

您可以设置统一消息 (UM)，以便用户可以在不使用 PIN 的情况下登录到其语音邮件。默认情况下，系统会提示 Outlook Voice Access 用户输入 PIN，以登录到其邮箱并访问其语音邮件、电子邮件、日历、个人联系人、目录和个人选项。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>为启用了语音邮件的单个用户或用户组启用无 PIN 登录会降低语音邮件的安全级别，并给组织带来安全风险。</td>
</tr>
</tbody>
</table>


若要启用无 PIN 登录，必须在 UM 邮箱策略上将参数 *AllowPinlessVoiceMailAccess* 设置为 `$true`，并在 UM 邮箱上将参数 *PinlessAccessToVoiceMailEnabled* 设置为 `$true`。默认情况下，这两个参数都设置为 `$false`，这便要求 Outlook Voice Access 用户在访问其语音邮件时输入其 PIN。

通过将这两个参数都设置为 `$true`，可以为与 UM 邮箱关联的一大组用户启用语音邮件无 PIN 登录，还可以为单个 UM 邮箱或 UM 邮箱的子集启用无 PIN 登录。即使为一组启用 UM 的用户或单个启用 UM 的用户启用了语音邮件无 PIN 登录，当这些用户访问其电子邮件、日历、个人联系人、目录或个人选项时，还是会提示他们输入其 PIN。

若要为用户启用针对语音邮件的无 PIN 登录，必须满足以下条件：

  - 必须已对 UM 邮箱策略运行以下 cmdlet：`Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - 必须已对启用 UM 的用户的邮箱运行以下 cmdlet：`Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - 启用 UM 的用户关联的 UM 邮箱策略与为其启用无 PIN 登录的 UM 邮箱策略相同。

  - 启用 UM 的用户通过分配给其的电话号码拨号连接到 Outlook Voice Access。

  - 只能使用命令行管理程序执行此过程。 若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。 若要了解如何使用 Windows PowerShell 连接到 Exchange Online，请参阅[连接到 Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554)。

有关与 UM 邮箱策略相关的其他任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

有关 UM 邮箱相关的其他任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，先确认已为用户启用了 UM 和语音邮件。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

## 您想执行什么操作？

## 使用命令行管理程序在 UM 邮箱策略上为启用 UM 的用户启用针对语音邮件的无 PIN 访问

此示例在名为 `MyUMMailboxPolicy` 的 UM 邮箱策略上，为与该邮箱策略关联并拨号连接到 Outlook Voice Access 的用户启用无 PIN 语音邮件访问。

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## 使用命令行管理程序在启用 UM 的用户的邮箱上，启用针对语音邮件的无 PIN 访问

此示例为拨号连接到 Outlook Voice Access 以进入名为 `tonys@contoso.com` 的邮箱的用户，启用无 PIN 语音邮件访问。

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

