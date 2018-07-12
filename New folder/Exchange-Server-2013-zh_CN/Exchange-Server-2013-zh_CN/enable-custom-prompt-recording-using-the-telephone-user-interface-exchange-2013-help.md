---
title: '允许使用电话用户界面录制自定义提示语: Exchange Online Help'
TOCTitle: 允许使用电话用户界面录制自定义提示语
ms:assetid: f2e5c636-2be9-4d48-b5e7-37913ded62d1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691404(v=EXCHG.150)
ms:contentKeyID: 54652297
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许使用电话用户界面录制自定义提示语

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2014-09-17_

您可以使用命令行管理程序并通过电话用户界面 (TUI)，为统一消息 (UM) 拨号计划和自动助理录制自定义提示以及问候语。当要使用 EAC 或命令行管理程序更改自定义问候语或通知时，或者在发生紧急情况（如组织由于恶劣天气而关闭）时，该功能非常有用。在 UM 自动助理中更改自定义问候语或通知时，必须在 UM 自动助理链接到的拨号计划上进行 TUI 提示录制。

有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;和\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行管理程序通过 TUI 启用自定义提示或问候语记录

若要通过电话用户界面 (TUI) 录制自定义提示和问候语，执行以下步骤：

1.  创建无法交互登录的域用户帐户。

2.  向该域用户帐户委派 Exchange 组织管理员角色。

3.  为该域用户创建一个邮箱。

4.  为该域用户邮箱启用统一消息。
    
    > [!important]
    > 仅允许将管理提示和问候语的管理员访问该用户帐户的分机号码和 PIN。该用户帐户仅用于通过电话管理提示。


5.  创建并保存一个将用作 UM 拨号计划或自动助理的自定义问候语的 .wav 或 .wma 文件。
    
    > [!NOTE]
    > 自定义提示不能使用 MP3 文件。


6.  使用 EAC 或命令行管理程序将拨号计划配置为使用自定义欢迎问候语，或者将自动助理配置为使用营业时间或非营业时间问候语。有关配置拨号计划的详细信息，请参阅[启用 Outlook Voice Access 用户自定义的问候语](enable-a-customized-greeting-for-outlook-voice-access-users-exchange-2013-help.md)。有关配置自动助理的详细信息，请参阅[启用自定义的营业时间问候语](enable-a-customized-business-hours-greeting-exchange-2013-help.md)或[启用自定义非-营业时间问候语](enable-a-customized-non-business-hours-greeting-exchange-2013-help.md)。

7.  运行以下 cmdlet：
    
        Set-UMDialPlan -identity MyUMDialPlan -TUIPromptEditingEnabled $true

> [!NOTE]
> 必须先登录设置了录制提示的邮箱，才能录制自定义提示或问候语。录制了新的提示或问候语后，必须注销并重新登录，才能在使用 TUI 时听到新的提示或问候语。


## 在 UM 自动助理中执行 TUI 提示录制

1.  验证自动助理是否链接到为 TUI 提示录制启用的拨号计划上。

2.  呼叫在 UM 自动助理中配置的电话号码。

3.  播放自动助理的非营业时间或营业时间问候语时，按井号键 (\#)，然后按星号键 (\*)。

4.  系统将提示您输入用户的分机号码。输入启用 UM 并有权限执行 TUI 提示录制的用户的分机号码。

5.  此时将提示您输入 PIN。输入用户的 PIN。

6.  按照系统提示编辑或更新自动助理的问候语或信息通知。

## 在 UM 拨号计划中执行 TUI 提示录制

1.  呼叫用于登录 Outlook Voice Access 的 Outlook Voice Access 号码。

2.  播放拨号计划的欢迎问候语时，请按井号键 (\#)，然后按星号键 (\*)。

3.  如果从启用 UM 的用户使用的电话进行呼叫，系统将提示您输入 PIN。请按星号键 (\*)，而无需输入 PIN。此时将提示您输入分机号码。输入启用 UM 并有权限执行 TUI 提示录制的用户的分机号码。

4.  如果从不是由启用 UM 的用户使用的电话进行呼叫，将自动提示您输入分机号码。输入启用 UM 并有权限执行 TUI 提示录制的用户的分机号码。

5.  此时将提示您输入 PIN。输入用户的 PIN。

6.  按照系统提示编辑或更新拨号计划的欢迎问候语或信息通知。

