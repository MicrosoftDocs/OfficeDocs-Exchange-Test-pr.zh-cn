---
title: '配置 Outlook Voice Access 数量: Exchange Online Help'
TOCTitle: 配置 Outlook Voice Access 数量
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50556559
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 Outlook Voice Access 数量

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

数允许用户启用统一邮件 (UM) 和语音邮件的 Outlook Voice Access 访问使用Outlook语音访问其邮箱。在拨号计划配置 Outlook Voice Access 或订阅者访问号码时，启用 UM 的用户可以连接到数、 登录到他们的邮箱，并访问其电子邮件、 语音邮件、 日历和联系人的个人信息。

默认情况下，当您创建 UM 拨号计划，数目不配置 Outlook Voice Access。要配置 Outlook Voice Access 数字，首先需要创建拨号计划中，以及如何配置 Outlook Voice Access 数字拨号计划的**Outlook Voice Access**选项下。虽然 Outlook Voice Access 数量并不是必需，您需要配置至少一个 Outlook Voice Access 数字，以启用已启用 UM 的用户使用Outlook语音访问来访问其邮箱。您可以配置多个 Outlook Voice Access 号码为一个拨号计划。

字母、 数字和特殊字符、 分隔符和空格，可以包含 Outlook Voice Access 数字。例如︰

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

有关可用的Outlook语音访问用户菜单选项的详细信息，请参阅Outlook语音访问快速参考指南可从[Microsoft 下载中心获取](https://go.microsoft.com/fwlink/p/?linkid=64645)。

有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置 Outlook Voice Access 号码

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;Outlook Voice Access\&quot;的\&quot;Outlook Voice Access 号码\&quot;下，使用此框输入要使用的号码，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置 Outlook Voice Access 号码

此示例将名为 `MyUMDialPlan` 的 UM 拨号计划的 Outlook Voice Access 号码设置为 4255550100。

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

