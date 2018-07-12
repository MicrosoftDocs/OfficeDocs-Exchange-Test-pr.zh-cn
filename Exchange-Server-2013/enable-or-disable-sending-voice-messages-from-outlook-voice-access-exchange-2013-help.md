---
title: '启用或禁用 Outlook Voice Access 从发送语音邮件: Exchange Online Help'
TOCTitle: 启用或禁用 Outlook Voice Access 从发送语音邮件
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52061365
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用 Outlook Voice Access 从发送语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-13_

您可以让 Outlook Voice Access 用户将语音邮件发送到与同一拨号计划关联且启用 UM 的用户，也可以阻止他们这么做。

默认情况下，启用此设置。如果您禁用此设置，可以调入 Outlook Voice Access 数的 Outlook Voice Access 用户不能向同一拨号计划中的用户发送语音消息。

有关与 UM 拨号计划相关的其他任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 让 Outlook Voice Access 用户向同一拨号计划中的用户发送语音邮件或者对其加以阻止

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在**传输和搜索**，**允许调用方**下, 选择**留下语音信息，而用户的电话响不**允许发送语音消息。如果您希望阻止发送语音邮件的用户，清除此设置。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序让 Outlook Voice Access 用户向同一拨号计划中的用户发送语音邮件或者对其加以阻止

此示例使与名为 `MyUMDialPlan` 的 UM 拨号计划关联的 Outlook Voice Access 用户能够向与同一拨号计划关联的用户发送语音邮件。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

此示例使与名为 `MyUMDialPlan` 的 UM 拨号计划关联的 Outlook Voice Access 用户无法向与同一拨号计划关联的用户发送语音邮件。

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

