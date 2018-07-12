---
title: '启用 UM IP 网关: Exchange Online Help'
TOCTitle: 启用 UM IP 网关
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 50490223
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用 UM IP 网关

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

默认情况下，当创建统一邮件 (UM) IP 网关时，其状态设置为已启用。但是，您可能需要禁用 UM IP 网关将它脱机并不允许它采取传入或传出调用。创建 UM IP 网关之后，可以通过设置其状态变量来启用或禁用控制其操作和功能。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认 UM IP 网关已创建并已被禁用。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 启用 UM IP 网关

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，选择要启用的 UM IP 网关，然后单击\&quot;向上箭头\&quot;![向上键图标](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "向上键图标")。

2.  在\&quot;警告\&quot; 页上，单击\&quot;是\&quot;。

## 使用命令行管理程序启用 UM IP 网关

此示例将启用名为 `MyUMIPGateway` 的 UM IP 网关。

    Enable-UMIPGateway -Identity MyUMIPGateway

