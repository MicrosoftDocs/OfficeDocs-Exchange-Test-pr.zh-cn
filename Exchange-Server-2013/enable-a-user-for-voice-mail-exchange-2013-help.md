---
title: '为用户启用语音邮件: Exchange 2013 Help'
TOCTitle: 为用户启用语音邮件
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50491370
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: HT
---

# 为用户启用语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

在为用户启用统一消息 (UM) 时，会将一组默认的 UM 属性应用于用户，用户可以使用统一消息随附的语音邮件功能。为某用户启用语音邮件后，如果为其分配一个链接到 SIP URI 拨号计划的 UM 邮箱策略，则您可以选择为该用户添加一个会话初始协议 (SIP) 地址。如果为其分配一个链接到 E.164 拨号计划的 UM 邮箱策略，您也可以为该用户添加一个 E.164 号码。无论哪种情况，用户必须仍然配置分机号码。

每个用户与电话分机、SIP 统一资源标识符 (URI) 或 E.164 拨号计划相关联时，都需要分机号码。分机号码的位数必须与在 UM 邮箱策略的 UM 拨号计划中指定的位数一致。

> [!NOTE]  
> 您必须使用 EAC 或命令行管理程序为所有启用 UM 的用户添加、删除或修改分机号码，即使他们已链接到 SIP URI 或 E.164 拨号计划。您需要使用命令行管理程序为用户添加、删除或修改 SIP 地址或 E.164 号码，因为 EAC 中不提供这些选项。


有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM 邮箱”条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为用户启用语音邮件

1.  在 EAC 中，单击“收件人”。

2.  在列表视图中，选择要为其邮箱启用统一消息的用户。

3.  在“详细信息”窗格的“电话和语音功能”下，单击“启用”。

4.  在“启用 UM 邮箱”页上，单击“UM 邮箱策略”旁的“浏览”按钮，找到 UM 邮箱策略，以从列表中分配用户，然后单击“确定”。

5.  在“启用 UM 邮箱”页上，填写下列框：
    
      - **SIP 地址**或 **E.164 号码**   在“SIP 地址”或“E.164 号码”文本框中，输入此用户的 SIP 地址或 E.164 号码。仅当将为统一消息启用的用户分配给关联到 SIP URI 或 E.164 拨号计划的 UM 邮箱策略时，这些选项才可用。如果用户与电话分机拨号计划关联，则无法为此用户添加 SIP 地址或 E.164 号码。
        
        将用户分配到链接到 SIP URI 或 E.164 拨号计划的 UM 邮箱策略后，还必须输入此用户的分机号码。用户通过 Outlook Voice Access 访问其邮箱时，将使用此分机号码。在此框中配置的位数必须与 SIP URI 或 E.164 拨号计划中配置的位数相匹配。
    
      - **分机号码**   使用此文本框为将启用 UM 的用户手动输入分机号码。
        
        必须为用户提供有效的分机号码，且该号码必须与在拨号计划中指定的位数匹配。您只能输入介于 1 到 20 之间的数字。典型的分机号码长度为 3 位到 7 位。分机号码中的位数在与分配给用户的 UM 邮箱策略关联的拨号计划中设置。
    
      - 根据“PIN 设置”，完成下列操作：
        
          - **自动生成 PIN**   单击此按钮可为已启用 UM 的用户自动生成 PIN，从而可以通过 Outlook Voice Access 进行语音邮件访问。这是默认设置。PIN 会基于分配给用户的 UM 邮箱策略上配置的 PIN 策略自动生成。使用该设置可以保护用户的 PIN。此 PIN 会通过一封欢迎邮件发送给用户，在启用 UM 策略后，用户就可以收到此邮件。默认情况下，他们必须在首次登录其邮箱以接收其语音邮件时更改此 PIN。
        
          - **键入 PIN**   单击此按钮，输入用户用于访问语音邮件系统的 PIN。PIN 必须符合与已启用 UM 的用户关联的 UM 邮箱策略上所配置的 PIN 策略设置。例如，如果将 UM 邮箱策略配置为只接受包含七位数或更多位数的 PIN，则在此文本框中输入的 PIN 长度至少必须有七位数。
        
          - **要求用户在第一次登录时重置其 PIN**   选中此复选框会强制用户在首次使用 Outlook Voice Access 通过电话访问语音邮件系统时重置其语音邮件 PIN。系统将会提示用户输入他们更熟悉的 PIN。最佳的安全做法是，强制已启用 UM 的用户在首次登录时更改其 PIN，以防止其数据和收件箱受到未经授权的访问。默认情况下此复选框处于选中状态。

6.  在“启用 UM 邮箱”页上，查看设置。单击“完成”对用户启用语音邮件。单击“上一步”可以更改配置。

## 使用命令行管理程序为用户启用语音邮件

本示例将为邮箱 tonysmith@contoso.com 启用统一消息，将分机号码设置为 51234，为用户将 PIN 设置为 5643892，然后将用户分配到名为 `MyUMMailboxPolicy` 的 UM 邮箱策略。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

本示例将为邮箱 tonysmith@contoso.com 启用统一消息，将用户分配到名为 `MyUMMailboxPolicy` 的 UM 邮箱策略，然后为用户设置分机号码、SIP 地址和 PIN。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

