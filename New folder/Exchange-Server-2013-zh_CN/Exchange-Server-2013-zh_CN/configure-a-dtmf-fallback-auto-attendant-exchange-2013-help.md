---
title: '配置 DTMF 回退自动助理: Exchange Online Help'
TOCTitle: 配置 DTMF 回退自动助理
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50491351
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 DTMF 回退自动助理

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-30_

您可以配置语音启用统一邮件 (UM) 自动助理具有双音多频 (DTMF) 回退自动助理。当 UM 启用语音的自动助理不能理解或识别由调用方提供的语音输入使用 DTMF 回退自动助理。如果已配置 DTMF 回退自动助理，调用方必须 DTMF 输入，也称为按键输入，用于导航的自动助理的菜单系统、 拼写的用户的名称，或使用自定义菜单提示。如果已配置没有 DTMF 回退自动助理，，因为系统不能理解调用方所说的内容超过了语音输入的最大数量，系统将在响应此提示:"很抱歉，我不能帮。请回电后面。"

默认情况下，自动助理未启用语音的时创建它。您语音启用后的自动助理，调用方可以使用仅声音命令定位自动助理的菜单系统，并不能使用按键输入。虽然它不是必需的但我们建议您配置为每个已启用语音的自动助理 DTMF 回退自动助理，以便调用方可以使用按键输入，如果启用语音的自动助理不识别或不理解他们所说的词。我们还建议您不要语音启用 DTMF 回退自动助理。

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

## 使用 EAC 配置启用语音且具有 DTMF 回退自动助理的自动助理

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在列表视图中，选择要修改的 UM 拨号计划并单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在**UM 拨号计划**页的**UM 自动助理**下,，选择您要为其创建 DTMF 回退自动助理 UM 自动助理。在工具栏上，单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面\>\&quot;常规\&quot;上，选中\&quot;在语音命令未正常工作时使用此自动助理\&quot;旁的复选框，然后单击\&quot;浏览\&quot;。

4.  在\&quot;选择 UM 自动助理\&quot;页上，选择要用作 DTMF 回退自动助理的自动助理，然后单击\&quot;保存\&quot;。

> [!important]
> 必须先启用语音自动语音助理，才能浏览已设置的 DTMF 回退自动助理。


## 使用命令行管理程序配置启用语音且具有 DTMF 回退自动助理的自动助理

此示例将名为 `MySpeechEnabledAA` 的 UM 自动助理配置为使用名为 `MyDTMFAA` 的 DTMF 回退自动助理。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

