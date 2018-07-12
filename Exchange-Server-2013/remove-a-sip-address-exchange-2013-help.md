---
title: '删除 SIP 地址: Exchange Online Help'
TOCTitle: 删除 SIP 地址
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50556692
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 SIP 地址

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

当您启用 um 的用户，并将它们链接到 SIP URI 拨号计划时，创建两个 EUM 代理服务器地址。一个包含该用户的分机号码，另一个包含用户的 SIP 地址。当用户连接到 Outlook Voice Access 数字使用的分机号码。

您正在集成 UM 和 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 时，将使用 SIP URI 拨号计划和 SIP 地址。SIP 地址将通信服务器或使用 Lync Server 将传入呼叫转接并将语音邮件发送给用户。默认情况下，使用的 UM 的 SIP 地址将通信服务器或 Lync Server 使用的 SIP 地址。

您可以删除已添加当用户已启用了 UM 的主 SIP 地址或辅助的 SIP 地址以及用户 EUM 代理地址以后，添加。添加当用户已启用了 UM 的主 SIP 地址将被列为主要 EUM 代理服务器地址。您添加的任何其他 SIP 地址均列为辅助 EUM 代理服务器地址。删除 SIP 地址后，调用方可以在 SIP 地址，即使用户登录 SIP 地址分配给该用户通信服务器或 Lync Server 中移除了不再保留用户的语音邮件。

如果删除了主的 SIP 地址，UM 不能将语音邮件发送到用户的邮箱和呼叫应答规则将不会处理。主要的 SIP 地址后，用户 EUM 代理地址均列为**空**用户的邮箱中 EAC 和您在 Shell 中运行**Get-Mailbox** cmdlet。此外，当您运行**Get-UMMailbox** cmdlet， *Extensions*、 *PhoneNumber*和*CallAnsweringRulesExtensions*参数将空白或空。

您可以使用 EAC 或外壳删除主要或次要的 SIP 地址。可以使用在用户的邮箱中 EAC**电子邮件地址**页删除主要或次要的 SIP 地址。您不能使用中 EAC **UM 邮箱**页删除主要或次要的 SIP 地址。

可以在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet 查看用户的主 SIP 地址和辅助 SIP 地址。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已启用了 UM 和 SIP URI 拨号计划与用户的邮箱。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认已为用户配置了主 SIP 地址和辅助 SIP 地址。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 删除主 SIP 地址或辅助 SIP 地址

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在此列表视图中，选择要从中删除 SIP 地址的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**用户邮箱**页上，在**电子邮件地址**中选择要从列表中删除的 SIP 地址，然后单击**删除**![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。粗体字母和数字中列出的主要 EUM 代理地址或 SIP 地址。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序删除主 SIP 地址或辅助 SIP 地址

此示例从启用了 UM 的用户 Tony Smith 的邮箱中删除 SIP 地址 tsmith@contoso.com。

> [!NOTE]  
> 删除使用 Shell 的 SIP 地址之前，您需要确定您想要修改 EUM 代理地址的位置。要确定位置，请使用<strong>$mbx.EmailAddresses</strong>命令。在列表中的第一个 EUM 代理地址将为 0。


    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

