---
title: '添加 SIP 地址: Exchange 2013 Help'
TOCTitle: 添加 SIP 地址
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50556569
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 添加 SIP 地址

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

在针对 UM 启用用户并将其链接到 SIP URI 拨号计划之后，会创建两个 EUM 代理地址。 一个包含用户的分机号，另一个包含用户的 SIP 地址。 在用户呼叫 Outlook Voice Access 号码时使用分机号。

集成 UM 和 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 时将使用 SIP URI 拨号计划和 SIP 地址。 Communications Server 或 Lync Server 使用 SIP 地址，将传入呼叫和语音邮件分别路由和发送至用户。 默认情况下，UM 使用的 SIP 地址为 Communications Server 或 Lync Server 使用的 SIP 地址。

在针对 UM 启用用户时添加的主 SIP 地址将作为主 EUM 代理地址列出。 如果删除了主 SIP 地址，则您添加的包含用户 SIP 地址的第一个 EUM 代理地址将作为主 EUM 代理地址列出。 您添加的任何其他 SIP 地址将作为辅助 EUM 代理地址列出。 在添加辅助 SIP 地址之后，呼叫者会在用户登录以使用 SIP 地址的 SIP 端点为此用户留下语音邮件。所有语音邮件将传递到同一用户邮箱。

您可以使用 EAC 或命令行管理程序为用户添加主 SIP 地址或辅助 SIP 地址。 您可以在 EAC 的用户邮箱中使用“电子邮件地址”页面来添加主 SIP 地址或辅助 SIP 地址。 您不能在 EAC 中使用“UM 邮箱”页面来添加主 SIP 地址或辅助 SIP 地址。

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

## 使用 EAC 添加主 SIP 地址或辅助 SIP 地址

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在此列表视图中，选择您要为其添加 SIP 地址的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“用户邮箱”页面上的“电子邮件地址”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在“新建电子邮地址”页面上，选择“EUM”，然后在“地址/扩展”框中，为此用户输入新的 SIP 地址。

5.  在“新建电子邮地址”页面上的“拨号计划”下，单击“浏览”选择 SIP URI 拨号计划，然后单击“确定”。

6.  单击“保存”。

## 使用命令行管理程序添加 SIP 地址

此示例为启用了 UM 的用户 Tony Smith 添加 SIP 地址。

> [!NOTE]  
> 在使用命令行管理程序添加 SIP 地址之前，需要确定您要添加的 EUM 代理地址的位置。要确定此位置，请使用 <strong>$mbx.EmailAddresses</strong> 命令。列表中的第一个代理地址将为 0。


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

