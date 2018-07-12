---
title: '更改 SIP 地址: Exchange 2013 Help'
TOCTitle: 更改 SIP 地址
ms:assetid: 33f4f464-9baa-48af-bf5e-a0d55bb45f60
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335189(v=EXCHG.150)
ms:contentKeyID: 50556549
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改 SIP 地址

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

在针对 UM 启用用户并将其链接到 SIP URI 拨号计划之后，会创建两个 EUM 代理地址。 一个包含用户的分机号，另一个包含用户的 SIP 地址。 在用户呼叫 Outlook Voice Access 号码时使用分机号。

集成 UM 和 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 时将使用 SIP URI 拨号计划和 SIP 地址。 Communications Server 或 Lync Server 使用 SIP 地址，将传入呼叫和语音邮件分别路由和发送至用户。 默认情况下，UM 使用的 SIP 地址为 Communications Server 或 Lync Server 使用的 SIP 地址。

您可以更改为用户启用 UM 时所添加的主 SIP 地址，也可以更改稍后添加的辅助 SIP 地址，以及用户的 EUM 代理地址。 在针对 UM 启用用户时添加的主 SIP 地址将作为主 EUM 代理地址列出。 您添加的任何其他辅助 SIP 地址将作为辅助 EUM 代理地址列出。 辅助 SIP 地址更改之后，呼叫者可以为位于所有 SIP 终结点的用户留下语音邮件，提示该用户使用新的 SIP 地址登录。所有语音邮件将传递到同一用户邮箱。

您可以使用 EAC 或命令行管理程序更改主 SIP 地址或辅助 SIP 地址。 您可以使用 EAC 中用户邮箱内的“电子邮件地址”页面来更改主 SIP 地址或辅助 SIP 地址。 您不能使用 EAC 中的“UM 邮箱”页面更改主 SIP 地址或辅助 SIP 地址。

您可以通过在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet，查看用户的主 SIP 地址或辅助 SIP 地址。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM 邮箱”条目。

  - 在执行这些步骤之前，先确认已创建 SIP URI UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已针对 UM 启用现有用户并链接到 SIP URI 拨号计划。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认将分配给用户的 SIP 地址有效，且格式正确。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 更改主要或辅 SIP 地址

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在列表视图中，选择要更改 SIP 地址的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“用户邮箱”页面的“电子邮件地址”下，选择要更改的 SIP 地址，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。主要 SIP 地址用粗体字母和数字列出。

4.  在“电子邮件地址”页面的“地址/分机号码”框中，输入用户的新 SIP 地址，然后单击“确定”。 如果需要选择新的 UM 拨号计划，则可单击“浏览”。

5.  单击“保存”。

## 使用命令行管理程序更改主 SIP 地址或辅助 SIP 地址

本示例将更改 Tony Smith 的 SIP 地址。

> [!NOTE]  
> 使用命令行管理程序更改 SIP 地址之前，需要确定要更改的 EUM 代理地址的位置。若要确定此位置，请使用 <strong>$mbx.EmailAddresses</strong> 命令。 第一个 EUM 代理地址是默认的（主要）SIP 地址，它在列表中为 0。


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:tsmith@contoso.com;phone-context=MySIPDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

