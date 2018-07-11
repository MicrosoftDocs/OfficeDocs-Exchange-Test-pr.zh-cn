---
title: '删除 E.164 号码: Exchange Online Help'
TOCTitle: 删除 E.164 号码
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50556531
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 E.164 号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

在为用户启用 UM 将其与 E.164 拨号计划关联时，将创建两个 EUM 代理地址。一个地址包含用户的分机号码，另一个地址包含用户的 E.164 号码。在用户呼叫 Outlook Voice Access 号码时，会使用分机号码。

您可以删除已添加当用户已启用了 UM 主 E.164 号码或包括用户 EUM 代理地址以后，添加辅助 E.164 号码。添加当用户已启用了 UM 主 E.164 号码均列为 EUM 主代理服务器地址。您添加的任何其他 E.164 号码均列为辅助 EUM 代理服务器地址。E.164 号码删除时，调用方可以不再留在移除了 E.164 号码的用户的语音邮件。

如果删除了主 E.164 号码，UM 不能将语音邮件发送到用户的邮箱和呼叫应答规则将不会处理。删除主 E.164 号码后，用户 EUM 代理地址均列为**空**用户的邮箱中 EAC 和您在 Shell 中运行**Get-Mailbox** cmdlet。此外，当您运行**Get-UMMailbox** cmdlet， *Extensions*、 *PhoneNumber*和*CallAnsweringRulesExtensions*参数将空白或空。

可以使用 EAC 或外壳程序若要删除主键列或用户的辅助 E.164 号码。可以使用在用户的邮箱中 EAC**电子邮件地址**页删除主要或次要的 E.164 号码。您不能使用中 EAC **UM 邮箱**页删除主要或次要的 E.164 号码。

您可以通过在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet，来查看用户的主 E.164 号码和辅助 E.164 号码。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 执行此过程之前，请确认已创建了一个 E.164 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已启用 UM 和 E.164 拨号计划与用户的邮箱。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认是否已为用户配置了主 E.164 号码和辅助 E.164 号码。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 删除主 E.164 号码或辅助 E.164 号码

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在此列表视图中，选择您要为其添加 E.164 号码的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**用户邮箱**页中的**电子邮件地址**下,，选择要从列表中删除的 E.164 号码，然后单击**删除**![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。粗体字母和数字中列出的主要 EUM 代理地址或 E.164 号码。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序删除主 E.164 号码或辅助 E.164 号码

此示例将从 Tony Smith （启用了 UM 的用户）的邮箱中删除 E.164 号码 +14255551010。

> [!NOTE]  
> 删除使用 Shell E.164 号码前，您需要确定您想要修改 EUM 代理地址的位置。要确定位置，请使用<strong>$mbx.EmailAddresses</strong>命令。在列表中的第一个 EUM 代理地址将为 0。


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

