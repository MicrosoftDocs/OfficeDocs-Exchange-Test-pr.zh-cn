---
title: '创建 UM 邮箱策略: Exchange 2013 Help'
TOCTitle: 创建 UM 邮箱策略
ms:assetid: 7f20874b-c46c-4505-9a78-f63eacb578ff
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123510(v=EXCHG.150)
ms:contentKeyID: 50556608
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMMailboxPolicyWizardForm.CreateUMMailboxPolicyWizardPage
ms.translationtype: HT
---

# 创建 UM 邮箱策略

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-03-08_

可以创建统一消息 (UM) 邮箱策略，以便对启用 UM 的邮箱集合应用一组常用的 UM 策略设置，例如 PIN 策略设置或拨号限制。UM 邮箱策略将启用 UM 的用户与 UM 拨号计划相链接，并对启用 UM 的邮箱集合应用一组通用策略或安全设置。为启用 UM 的用户应用和标准化 UM 配置设置时，UM 邮箱策略十分有用。

默认情况下，创建 UM 拨号计划时，也会创建一个 UM 邮箱策略。在组织中部署了统一消息后，可能需要创建和配置其他 UM 邮箱策略或修改现有的 UM 邮箱策略。

有关与 UM 邮箱策略相关的其他管理任务，请参阅 [UM 邮箱策略过程](um-mailbox-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM 邮箱策略”条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 创建 UM 邮箱策略

1.  
    
    在 EAC 中，导航到“统一消息”\>“UM 拨号计划”。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“UM 拨号计划”页上的“UM 邮箱策略”下，单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“新建 UM 邮箱策略”页面上，在“名称”文本框中，输入新的 UM 邮箱策略的名称。
    
    使用此框可为 UM 邮箱策略指定唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM 邮箱策略后需要更改其显示名，则必须首先删除现有的 UM 邮箱策略，然后创建具有相应名称的其他 UM 邮箱策略。如果有任何启用了 UM 的用户与 UM 邮箱策略关联，则不能删除该策略。
    
    UM 邮箱策略名称是必需的，但其仅用于显示目的。由于您的组织可能使用多个 UM 邮箱策略，因此建议您使用对 UM 邮箱策略有意义的名称。UM 邮箱策略名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.

4.  单击“保存”来保存新的 UM 邮箱策略。在保存 UM 邮箱策略时，会启用所有默认设置，包括 PIN 策略、语音邮件功能以及“受保护的语音邮件”设置。如果想自定义或更改任何默认设置，可使用 **Set-UMMailbox** cmdlet 来更改刚创建的 UM 邮箱策略的设置。

## 使用命令行管理程序创建 UM 邮箱策略

此示例创建名为 `MyUMMailboxPolicy` 的 UM 邮箱策略，该邮箱策略与名为 `MyUMDialPlan` 的 UM 拨号计划关联。

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

