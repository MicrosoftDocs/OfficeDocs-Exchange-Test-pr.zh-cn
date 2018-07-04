---
title: '删除 UM IP 网关: Exchange Online Help'
TOCTitle: 删除 UM IP 网关
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50490615
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 UM IP 网关

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

删除统一消息 (UM) IP 网关时，Exchange 服务器将不再接受来自与 UM IP 网关相关联的 Voice over IP (VoIP) 网关、已启用会话初始协议 (SIP) 的专用交换机 (PBX)、IP PBX 或会话边界控制器 (SBC) 的传入呼叫。

> [!important]
> 仅当完全了解禁用与 VoIP 网关、IP PBX 或 SBC 的通信的含义时，才应删除 UM IP 网关。


有关 UM IP 网关相关的其他任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 删除 UM IP 网关

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，选择要删除的 UM IP 网关，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

2.  在\&quot;警告\&quot; 页上，单击\&quot;是\&quot;。

## 使用命令行管理程序删除 UM IP 网关

此示例将删除名为 `MyUMIPGateway` 的 UM IP 网关。

    Remove-UMIPGateway -Identity MyUMIPGateway

