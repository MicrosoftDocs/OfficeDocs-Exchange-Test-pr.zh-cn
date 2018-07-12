---
title: '更改 E.164 号码: Exchange Online Help'
TOCTitle: 更改 E.164 号码
ms:assetid: 2a3da11b-bb9b-4d4d-9238-6a1a47ef63f2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335162(v=EXCHG.150)
ms:contentKeyID: 50556546
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改 E.164 号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

在为用户启用 UM 将其与 E.164 拨号计划关联时，将创建两个 EUM 代理地址。一个地址包含用户的分机号码，另一个地址包含用户的 E.164 号码。在用户呼叫 Outlook Voice Access 号码时，会使用分机号码。

您可以更改已启用 UM 的用户被添加主 E.164 号码或包括用户 EUM 代理地址以后，添加辅助 E.164 号码。添加当用户已启用了 UM 主 E.164 号码均列为 EUM 主代理服务器地址。添加任何其他辅助 E.164 号码均列为辅助 EUM 代理服务器地址。当 E.164 编号已更改时，调用方可以保留用户的语音邮件根本已设置新的 E.164 编号。所有语音邮件将被传递到同一个用户的邮箱。

您可以使用 EAC 或外壳来更改用户的主要和次要 E.164 号码。对用户的邮箱中，可以使用**电子邮件地址**页更改主要或次要 E.164 编号。但是，不能使用**UM 邮箱**页中 EAC 更改主要或次要 E.164 编号。

您可以通过在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet，来查看用户的主 E.164 号码和辅助 E.164 号码。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 E.164 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已启用 UM 和 E.164 拨号计划与用户的邮箱。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认要分配给已启用 UM 的用户的 E.164 号码有效。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改主或辅助 E.164 号码

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要更改 E.164 号码的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**用户邮箱**页中的**电子邮件地址**下,，选择您要更改，E.164 号码，然后单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。主的 E.164 号码列入粗体字母和数字。

4.  在**电子邮件地址**页**地址/扩展**框中，输入新的 E.164 号码的用户，，然后单击**确定**。如果您需要选择新的 UM 拨号计划，您可以单击**浏览**。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序更改主或辅助 E.164 号码

本示例为 Tony Smith（启用了 UM 的用户）更改 E.164 号码。

> [!NOTE]  
> 更改使用 Shell E.164 号码之前，您需要确定您想要更改 EUM 代理地址的位置。要确定位置，请使用<strong>$mbx.EmailAddresses</strong>命令。第一个 EUM 代理地址是默认 （为主） E.164 号码，则会在列表中的 0。


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:+14255550123;phone-context=MyE.164DialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

