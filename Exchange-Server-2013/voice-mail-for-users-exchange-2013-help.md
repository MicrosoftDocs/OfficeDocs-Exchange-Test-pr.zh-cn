---
title: '用户的语音邮件: Exchange Online Help'
TOCTitle: 用户的语音邮件
ms:assetid: 48e1f43b-fb7e-4a52-a2cb-0fb5da6ca65f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997885(v=EXCHG.150)
ms:contentKeyID: 50490477
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用户的语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-19_

与统一消息 (UM)，Exchange 组织中的用户可以在一个邮箱中接收其所有电子邮件和语音邮件。统一消息功能和语音邮件功能提高用户生产效率，使整个组织更加灵活的消息。

正在将用户添加到您的组织中，当您提供了创建邮箱或连接到现有的邮箱的用户的选项。为用户创建邮箱，或在用户连接到现有的邮箱后，可以为统一消息启用邮箱，使用户可以使用语音邮件系统和语音邮件中包含的功能如此。后为用户启用统一邮件，所有电子邮件、 语音邮件和传真邮件将被传递到用户的邮箱。通过使用 Microsoft Office Outlook 2007或更高版本、 Outlook Web App、 启用 Microsoft ExchangeActiveSync或正则表达式的移动电话或移动电话，用户可以访问其电子邮件、 语音邮件、 个人联系人和日历信息。

**目录**

语音邮件用户属性

语音邮件用户和其他 UM 组件之间的关系

Extension numbers and SIP addresses

Using the EAC to enable a user for UM and voice mail

Using the Shell to enable a user for UM and voice mail

Disabling UM for a user

## 语音邮件用户属性

为统一消息启用之前，用户必须拥有一个邮箱。但是，默认情况下，具有邮箱的用户未启用统一消息。用户启用了 UM 之后，可以管理、 修改和配置 UM 属性和它们的语音邮件功能。用户可以启用统一消息使用 EAC 或外壳。有关详细信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。要启用多个 UM 用户，使用Exchange命令行管理程序 EAC 或**Enable-UMMailbox** cmdlet。

## 语音邮件用户和其他 UM 组件之间的关系

当用户启用统一邮件时，用户必须与关联或链接到现有 UM 邮箱策略，并且必须为它们提供分机号码。通过在 Shell 中使用**Enable-UMMailbox** cmdlet 或用户启用统一邮件时选择的 UM 邮箱策略，您可以与 UM 邮箱策略关联的用户。默认情况下，当创建 UM 拨号计划，被创建新的 UM 邮箱策略。可以修改此策略，或者可以创建另一个策略并将其链接到拨号计划，以确定哪些功能或设置将应用到用户或用户组。

UM 邮箱策略包含如拨号限制和用户的 PIN 策略的设置。当创建 UM 邮箱策略时，它必须与只有一个 UM 拨号计划关联。任何与 Exchange server 可以应答传入呼叫并与 UM 拨号计划提供语音链接的任何已启用 UM 的用户的邮件服务。为用户启用统一邮件之后，从 UM 邮箱策略设置应用到启用 UM 的用户。

## 分机号码和 SIP 地址

当用户启用统一邮件时，您必须定义至少一个分机号码统一消息时使用的语音邮件被提交到用户的邮箱。为统一消息启用用户后，可以将辅助分机号码添加到用户的邮箱，或修改或通过对用户的邮箱配置Exchange统一消息代理地址 （EUM 代理地址） 来删除这些或添加或删除中 EAC 的附加的或辅助用户扩展。您可以通过删除 EUM 代理地址，EAC 在删除主分机号码，但建议您不要将其删除。删除主分机号码将不会允许调用正确转发到用户的邮箱。

> [!NOTE]  
> 对已启用 UM 的用户可添加的辅助分机号码数没有限制，但每位用户只能有一个主分机号码。


可以与只有一个 UM 拨号计划关联的已启用 UM 的用户的邮箱。已启用 UM 的用户可以分配如下 ︰

  - 一个拨号计划的一个主分机号码、会话初始协议 (SIP) 地址或 E.164 地址。

  - 一个拨号计划的多个辅助分机号码、SIP 地址或 E.164 地址。

  - 两个独立拨号计划的多个主分机号码、SIP 地址或 E.164 地址。

> [!NOTE]  
> 拨号计划中的每个分机号码、SIP 地址和 E.164 号码必须是唯一的，并且该拨号计划中的位数将用于与拨号计划链接的所有用户。


例如，已启用 UM 的用户经常旅行从纽约到东京。用户的邮箱与纽约拨号计划相关联，在用户的邮箱上配置单个分机号码。在东京的拨号计划的用户邮箱上配置第二个的分机号码。调用方拨任何一个分机号码，并留下语音信息的用户，语音邮件将传递到同一个启用 UM 的邮箱中。

返回顶部

## 使用 EAC 为用户启用 UM 和语音邮件

创建用户的 Exchange 邮箱后，您可以通过 EAC 中**查看详细信息**在**统一消息**下配置 UM 邮箱设置。当您启用用户时，有几个您需要配置的设置 ︰

1.  **SIP 地址**  这是用户的 SIP 地址。如果在启用了 UM 的用户分配给链接到 SIP URI 拨号计划的 UM 邮箱策略，您将看到此设置。您正在集成办公通信服务器 2007 R2 或 Microsoft Lync Server 时，将使用 SIP URI 拨号计划。当您将用户分配到链接到 SIP URI UM 邮箱策略或 E.164 拨号计划时，仍然还必须输入用户的分机号。主要的分机号码是用户用于访问 Outlook Voice Access。

2.  **分机号码**   必须为将启用 UM 的用户手动输入分机号码。
    
    您必须为用户提供有效的分机号码并匹配指定的小数位数的拨号计划上。您只能输入数字的字符或数字以从 1 到 20。典型的分机号码是长，3 到 7 位，拨号计划与之链接和分配给用户的 UM 邮箱策略上配置。

3.  **用户的 PIN 设置：** 
    
      - **自动生成 PIN**  此设置将自动生成对启用 UM 的用户使用的 Outlook Voice Access 通过语音邮件访问 PIN。这是默认设置。当您单击此按钮时，自动根据分配给用户的 UM 邮箱策略上配置的 PIN 策略生成 PIN。我们建议使用此设置来帮助保护用户的 PIN。针被发送到他们正在启用了 UM 之后他们收到欢迎邮件中的用户。默认情况下，他们还必须在首次登录到他们的邮箱来获取他们的语音邮件时更改此端口。
    
      - **键入 PIN**   通过此设置可以手动指定用户将用来访问语音邮件系统的 PIN。
        
        PIN 必须遵守与此启用 UM 的用户关联的 UM 邮箱策略上配置 PIN 策略设置。例如，如果 UM 邮箱策略配置为接受包含七个或更多位数的针脚，则在此框中输入的 PIN 必须至少七个数字长。
    
      - **要求用户重置其 PIN 登录他们第一次**  此设置迫使用户重置其语音邮件 PIN，当他们第一次使用 Outlook Voice Access 用电话访问语音邮件系统。他们将会提示您输入的 PIN，给他们更熟悉。它是一种安全最佳做法强制启用 UM 的用户更改他们的 PIN，在首次登录有助于防止未经授权访问其数据和收件箱时。默认情况下选中此复选框。

## 使用命令行管理程序为用户启用 UM 和语音邮件

本示例将为邮箱 tonysmith@contoso.com 启用统一消息和语音邮件，为用户设置分机并手动设置 PIN，然后将用户分配到名为 `MyUMMailboxPolicy` 的 UM 邮箱策略。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

本示例将为邮箱 tonysmith@contoso.com 启用统一消息和语音邮件，将用户分配到名为 `MyUMMailboxPolicy` 的 UM 邮箱策略，然后为用户设置分机号码和 SIP 地址，并手动设置 PIN。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

## 为用户禁用 UM

当用户禁用统一消息时，当调用方执行目录搜索使用 UM 自动助理菜单或使用Outlook语音访问，可能仍被列出的用户帐户。调用方可能能够找到用户目录中，但当它们与用户联系时，他们要带回统一消息中的主菜单。这可能会导致调用方变得沮丧与系统。您可以阻止调用方使用目录搜索联系通过将用户连接到另一个语音邮件系统、 用户删除 UM 自动助理的目录搜索，或删除该用户帐户被禁用统一消息的用户。

禁用统一消息启用 UM 的用户帐户后，用户到单个启用 UM 的邮箱使用Outlook语音访问或 Microsoft Outlook可能仍然可以访问。这可以将不一致的目录中所有更改时发生。若要减少用户获取邮箱访问权限，即使该帐户已被禁用统一邮件的风险，可以手动强制复制发生或用户禁用统一消息时从用户邮箱中删除统一邮件的所有信息。

