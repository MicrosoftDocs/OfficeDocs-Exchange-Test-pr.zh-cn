---
title: '启用或禁用自动语音识别: Exchange Online Help'
TOCTitle: 启用或禁用自动语音识别
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52061388
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用自动语音识别

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-12_

您可以启用您的统一邮件 (UM) 自动助理自动语音识别 (ASR)。您语音启用后 UM 自动助理，调用方可以口头响应自动助理提示和自动助理的菜单系统中移动。默认情况下，自动助理未启用语音的时创建它。您语音启用后的自动助理，调用方可以使用仅声音命令定位自动助理的菜单系统，并不能使用按键输入。

虽然它不是必需的但我们建议您配置为每个已启用语音的自动助理双音多频 (DTMF) 回退自动助理，以便调用方可以使用按键输入，如果启用语音的自动助理不识别或不理解他们所说的词。如果配置了 DTMF 回退自动助理，调用方可以使用 DTMF 输入，也称为按键输入，导航自动助理菜单系统、 拼写的用户的名称，或使用自定义菜单提示。我们不建议您语音启用 DTMF 回退自动助理。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 为 UM 自动助理启用语音功能

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要启用语音的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 自动助理**页 \>**常规**，选择**设置自动助理对语音命令作出响应**，以启用语音识别旁边的复选框。要禁用自动语音识别，请清除此复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序为 UM 自动助理启用语音功能

本示例将为名为 `MySpeechEnabled AA` 的 UM 自动助理启用 ASR。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

