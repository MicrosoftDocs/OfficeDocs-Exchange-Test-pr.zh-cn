---
title: '更改分机号码: Exchange Online Help'
TOCTitle: 更改分机号码
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50556700
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改分机号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

为某个用户启用 UM 并将其与电话分机拨号计划关联时，将为包含该用户的分机号的用户创建 EUM 代理地址。必须为要使用的 UM 至少定义一个分机号码，以便将语音邮件发送到用户的邮箱。在用户呼叫 Outlook Voice Access 号码时，也会使用分机号码。

可以更改为用户启用 UM 时添加的主分机号码，也可以更改后来添加的辅助分机号码，同时删除用户的相关 EUM 代理地址。为用户启用 UM 时添加的主分机号码将作为主 EUM 代理地址列出。添加的任何其他辅助分机号码将作为辅助 EUM 代理地址列出。如果更改了分机号码，呼叫者可以在已设置的所有新分机号码上为用户留言。所有语音邮件都将传递到同一个用户的邮箱。

可以使用 EAC 或命令行管理程序更改用户的主分机号码或辅助分机号码。可以在 EAC 中使用用户邮箱上的\&quot;电子邮件地址\&quot;页面更改主分机号码或辅助分机号码。不能使用 EAC 中的\&quot;UM 邮箱\&quot;页面更改主分机号码，但可以使用该页面更改辅助分机号码。如果要更改辅助分机号码，必须先删除现有的辅助分机号码，然后为用户添加正确的辅助分机号码。

可以在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet 查看用户的主分机号码和辅助分机号码。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些过程之前，请确认已创建了电话分机 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认已为用户的邮箱启用了 UM，并且用户的邮箱已经与电话分机拨号计划关联。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认将要分配给用户的分机号码包含在 UM 拨号计划上设置的正确位数。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改主分机号码或辅助分机号码

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要为其更改分机号码的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;用户邮箱\&quot;页面上的\&quot;电子邮件地址\&quot;下，选择要更改的分机号码，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。主分机号码以黑体字母或数字列出。

4.  在\&quot;电子邮件地址\&quot;页面上的\&quot;地址/分机号码\&quot;框中，输入用户的新分机号码。如果需要选择新的 UM 拨号计划，可以单击\&quot;浏览\&quot;。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改主分机号码或辅助分机号码

此示例将启用了 UM 的用户 Tony Smith 的分机号码更改为 22222。

> [!NOTE]  
> 在使用命令行管理程序更改分机号码之前，需要确定要更改的 EUM 代理地址的位置。若要确定该位置，请使用 <strong>$mbx.EmailAddresses</strong> 命令。第一个 EUM 代理地址是默认的（主）分机号码，在列表中的编号将为 0。


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

