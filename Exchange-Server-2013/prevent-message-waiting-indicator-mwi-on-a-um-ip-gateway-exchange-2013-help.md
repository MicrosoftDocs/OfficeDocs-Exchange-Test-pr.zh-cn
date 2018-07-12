---
title: '消息等待指示符 (MWI) 如果不在 UM IP 网关: Exchange Online Help'
TOCTitle: 消息等待指示符 (MWI) 如果不在 UM IP 网关
ms:assetid: 7af6d094-199f-4134-a25d-9fc7e9c05fe1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673536(v=EXCHG.150)
ms:contentKeyID: 50490983
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 消息等待指示符 (MWI) 如果不在 UM IP 网关

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

您可以阻止用户的统一邮件 (UM) IP 网关接收到的电话语音邮件通知。如果您启用此设置，UM IP 网关可以接收和发送通知的 SIP 消息的用户。消息等待指示符 (MWI) 默认启用的允许消息等待通知发送给用户，但可以根据需要将其关闭。

消息等待指示符通知用户有关新的或从未体验过的语音邮件。它将出现在收件箱中如Outlook和Outlook Web App的客户端。它也可以是文本 (SMS) 消息发送到已注册的移动电话，对从 Exchange 服务器被配置为在用户的桌面电话上播放新的邮件或亮起的灯号传出调用。

> [!TIP]  
> 也可以在 UM 邮箱策略上为一组用户启用和禁用 MWI 通知。


有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 阻止邮件等待指示器

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，选择要更改的 UM IP 网关，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM IP 网关\&quot;页上，清除\&quot;允许邮件等待指示器\&quot;旁边的复选框。

3.  单击\&quot;保存\&quot;。

## 使用命令行管理程序阻止邮件等待指示器

此示例阻止向与名为 `MyUMIPGateway` 的 UM IP 网关（IP 地址为 10.10.10.1）关联的用户显示邮件等待指示器。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $false

