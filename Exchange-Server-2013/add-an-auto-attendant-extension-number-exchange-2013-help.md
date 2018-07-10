---
title: '添加自动助理的分机号码: Exchange Online Help'
TOCTitle: 添加自动助理的分机号码
ms:assetid: f2bd62ba-1e01-4cb7-862c-c750752e20e0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232200(v=EXCHG.150)
ms:contentKeyID: 50491972
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 添加自动助理的分机号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

您可以配置统一邮件 (UM) 自动助理的分机号码或多个分机号码。分机号码添加到 UM 自动助理时，该数字可由调用方能够调入的自动助理。此外，您可能需要添加分机号码，因为有多个调用方可以使用访问自动助理的分机号码。默认情况下，当创建自动助理配置没有分机号码。

而不设置为自动助理的分机号码，您可以创建新的自动助理。您还可以使用单一的自动助理关联多个电话号码或分机号码。当您创建 UM 自动助理或将其添加在您配置的自动助理之后，也可以添加分机号码。在您配置 UM 自动助理的分机号码的位数必须匹配的配置与 UM 自动助理关联的 UM 拨号计划分机号码的位数。

> [!NOTE]
> 您还可以添加一个会话启动协议 (SIP) 地址而不是添加分机号码。SIP 地址由某些 IP 专用分组交换机 (Pbx) 和办公室通信服务器 2007 R2 或 Microsoft Lync Server。


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

## 使用 EAC 为 UM 自动助理添加分机或电话号

1.  在 EAC，导航到**统一消息**\> **UM 拨号计划**。在列表视图中，选择您想要编辑，然后单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")UM 拨号计划。

2.  在\&quot;UM 拨号计划\&quot;页上，在\&quot;UM 自动助理\&quot;下，选择您希望添加分机或电话号的 UM 自动助理。

3.  在工具栏上，单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

4.  在\&quot;UM 自动助理\&quot;页面上的\>\&quot;常规\&quot;中，\&quot;访问号码\&quot;下的文本框中，输入您想要使用的分机或电话号码并单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  单击\&quot;保存\&quot;添加数字。

## 使用命令行管理程序在 UM 自动助理上配置分机号码

此示例配置一个名为 `MyUMAutoAttendant` 且具有多个分机号码的 UM 自动助理。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -PilotIdentifierList "12345, 72000, 75000"

