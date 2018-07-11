---
title: '设置语音邮件的 pin 码最小长度: Exchange Online Help'
TOCTitle: 设置语音邮件的 pin 码最小长度
ms:assetid: b2ecab54-42e6-45af-8322-615cc1f68dd9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124271(v=EXCHG.150)
ms:contentKeyID: 50556659
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置语音邮件的 pin 码最小长度

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以配置 Outlook Voice Access 用户的统一邮件 (UM) 启用小针长度。在 UM 邮箱策略配置 PIN 设置将应用于所有已启用 UM 的用户与该 UM 邮箱策略相关联。

Outlook已启用 UM 的用户使用语音访问来访问他们的语音邮件、 电子邮件、 日历和位于其邮箱中的个人联系信息。但是，它们可以访问其邮箱之前，他们必须输入 PIN，所以他们可以通过语音邮件系统进行身份验证。

> [!NOTE]  
> 如果要更改最小针长度值，现有 Outlook Voice Access 用户将会提示您输入的新 PIN，包含新的最小小数位数，然后才能继续。默认值为 6。


有关 Outlook Voice Access PIN 安全性相关的其他任务，请参阅 [针的安全程序](pin-security-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置 Outlook Voice Access 的最小 PIN 长度

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择您要更改的拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要更改的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  单击\&quot;PIN 策略\&quot;，在\&quot;最小 PIN 长度\&quot;旁边，输入一个介于 4 和 24 之间的值。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置 Outlook Voice Access 的最小 PIN 长度

此示例将与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联的 Outlook Voice Access 用户的最小 PIN 长度设置为 8 位数。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MinPINLength 8

此示例将最小 PIN 长度设置为 8 位数，并将在用户的 PIN 重置之前的登录失败次数设置为 3。这适用于与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略相关联且已启用 UM 的用户。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3 -MinPINLength 8

