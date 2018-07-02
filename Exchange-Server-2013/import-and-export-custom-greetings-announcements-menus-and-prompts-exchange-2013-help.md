---
title: '导入和导出自定义问候语、通知、菜单和提示: Exchange 2013 Help'
TOCTitle: 导入和导出自定义问候语、通知、菜单和提示
ms:assetid: e82da5d5-625f-4d8b-8d31-ac45513aacfd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee681667(v=EXCHG.150)
ms:contentKeyID: 54652296
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 导入和导出自定义问候语、通知、菜单和提示

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-04-08_

您可以导入和导出已在统一消息 (UM) 拨号计划和自动助理上记录使用的音频文件。例如，如果您使用以前版本的 Exchange 升级一个音频文件，可能想导出或保存该音频文件的副本。或者，在配置一个拨号计划或自动助理之前，需要导入一个已记录的音频提示的副本。

音频文件有以下用处：

  - 在 UM 拨号计划中，音频文件用于自定义欢迎问候语和信息通知。当 Outlook Voice Access 用户呼叫 Outlook Voice Access 号码时，会播放这些音频文件。

  - 在 UM 自动助理中，音频文件用于自定义的非营业和营业时间问候语、信息通知、菜单提示和导航菜单。这些音频文件在呼叫者呼叫 UM 自动助理时播放。

自定义问候语、通知、菜单和提示支持下列音频文件格式：

  - 使用 Windows Media Audio 9.2 编码的 .wma 文件 - 96 kbps/44 kHz/stereo 1-pass CBR（Windows 录音机）

  - Windows Media Audio Voice 9 - 8 kbps/8 kHz/Mono，和使用线性 PCM（16 位/采样）、8 千赫 (kHz) 音频编解码器编码的 .wav 文件。

将 UM 拨号计划和自动助理使用的音频文件导入名为 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 的系统邮箱，并将其从该系统邮箱导出。可以使用 **Import-UMPrompt** cmdlet 和 **Export-UMPrompt** cmdlet 导入和导出音频文件。

有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;和\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序导入 UM 拨号计划和自动助理的自定义问候语、通知、菜单和提示

本示例将欢迎问候语文件 welcomegreeting.wav 从 d:\\UMPrompts 导入到 UM 拨号计划 `MyUMDialPlan` 中。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMDialPlan MyUMDialPlan -PromptFileName "welcomegreeting.wav" -PromptFileData $c

本示例将欢迎问候语文件 welcomegreeting.wav 从 d:\\UMPrompts 导入到 UM 自动助理 `MyUMAutoAttendant` 中。

    [byte[]]$c = Get-content -Path "d:\UMPrompts\welcomegreeting.wav" -Encoding Byte -ReadCount 0
    Import-UMPrompt -UMAutoAttendant MyUMAutoAttendant -PromptFileName "welcomegreeting.wav" -PromptFileData $c

## 使用命令行管理程序从 UM 拨号计划和自动助理导出自定义问候语、通知、菜单和提示。

本示例导出 UM 拨号计划 `MyUMDialPlan` 的欢迎问候语，并将它另存为 welcomegreeting.wav 文件。

    $prompt = Export-UMPrompt -PromptFileName "customgreeting.wav�? -UMDialPlan MyUMDialPlan
    set-content -Path "d:\DialPlanPrompts\welcomegreeting.wav" -Value $prompt.AudioData -Encoding Byte

本示例导出用于 UM 自动助理 `MYUMAutoAttendant` 的营业时间欢迎问候语，并将它另存为 BusinessHoursWelcomeGreeting.wav 文件。

    $prompt = Export-UMPrompt -BusinessHoursWelcomeGreeting -UMAutoAttendant MyUMAutoAttendant
    set-content -Path "d:\UMPrompts\BusinessHoursWelcomeGreeting.wav" -Value $prompt.AudioData -Encoding Byte

