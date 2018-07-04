---
title: '添加 E.164 号码: Exchange 2013 Help'
TOCTitle: 添加 E.164 号码
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50556699
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 添加 E.164 号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

在为用户启用 UM 将其与 E.164 拨号计划关联时，将创建两个 EUM 代理地址。一个地址包含用户的分机号码，另一个地址包含用户的 E.164 号码。在用户呼叫 Outlook Voice Access 号码时，会使用分机号码。

为用户启用 UM 时添加的主 E.164 号码将作为主 EUM 代理地址列出。如果删除主 E.164 号码，则您添加的包含用户的 E.164 号码的第一个 EUM 代理地址将列出为主 EUM 代理地址。添加的任何其他 E.164 号码将作为辅助 EUM 代理地址列出。如果添加了其他 E.164 号码，则呼叫者可在已设置的所有 E.164 号码上为用户留言。所有语音邮件都将传递到同一个用户的邮箱。

可以使用 EAC 或命令行管理程序为用户添加主 E.164 号码或辅助 E.164 号码。您可以在 EAC 中使用用户邮箱的“电子邮件地址”页面添加主 E.164 号码或辅助 E.164 号码。不能使用 EAC 中的“UM 邮箱”页面添加主 E.164 号码或辅助 E.164 号码。

可以在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet 查看用户的主 E.164 号码和辅助 E.164 号码。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM 邮箱”条目。

  - 在执行这些步骤之前，先确认已创建 E.164 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认已为用户的邮箱启用了 UM，并且已将其与 E.164 拨号计划关联。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认要分配给用户的 E.164 号码有效并且格式正确。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 添加主 E.164 号码或辅助 E.164 号码

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在列表视图中，选择要为其添加 E.164 号码的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“用户邮箱”页面上的“电子邮件地址”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“新建电子邮件地址”页面上，选择“EUM”；在“地址/分机号码”框中，输入用户的新 E.164 号码。

5.  在“新建电子邮件地址”页面上的“拨号计划”下，单击“浏览”选择 E.164 拨号计划，然后单击“确定”。

6.  单击“保存”。

## 使用命令行管理程序添加 E.164 号码

此示例为启用了 UM 的用户 Tony Smith 添加 E.164 号码。

> [!NOTE]
> 使用命令行管理程序添加 E.164 号码之前，需要确定要添加的 EUM 代理地址的位置。若要确定该位置，请使用 <strong>$mbx.EmailAddresses</strong> 命令。列表中的第一个代理地址将为 0。


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

