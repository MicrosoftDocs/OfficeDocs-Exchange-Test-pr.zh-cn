---
title: '禁用 UM 自动助理: Exchange Online Help'
TOCTitle: 禁用 UM 自动助理
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 50491372
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用 UM 自动助理

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

默认情况下，当创建统一邮件 (UM) 自动助理时，其状态设置为禁用。创建 UM 自动助理后，您可以向控件更改其状态，是否它可以应答传入呼叫。例如，您可能需要在录制或自定义的提示和消息重新录制时禁用 UM 自动助理。

有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。此外确认 UM 自动助理的状态设置为启用。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 禁用 UM 自动助理

1.  在 EAC，导航到**统一消息**\> **UM 拨号计划**。在列表视图中，选择您要更改拨号计划并在工具栏中，单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在**UM 拨号计划**页的**UM 自动助理**下,，选择您想要禁用 UM 自动助理。在工具栏上，单击**向下箭头键**![向下键图标](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下键图标")

3.  在\&quot;警告\&quot; 页上，单击\&quot;是\&quot;。

## 使用命令行管理程序禁用 UM 自动助理

本示例将禁用名为 `MyUMAutoAttendant` 的 UM 自动助理。

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

