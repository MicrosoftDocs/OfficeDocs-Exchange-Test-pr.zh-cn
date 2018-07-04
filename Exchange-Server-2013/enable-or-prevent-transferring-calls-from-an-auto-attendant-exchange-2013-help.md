---
title: '启用或禁止将呼叫转接从自动助理: Exchange Online Help'
TOCTitle: 启用或禁止将呼叫转接从自动助理
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52061466
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁止将呼叫转接从自动助理

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以启用呼叫者转移呼叫的用户通过自动助理，或阻止他们这样做。默认情况下此选项被启用，并允许调用方将对启用 UM 的用户的呼叫转移与 UM 自动助理的统一邮件 (UM) 拨号计划中。

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

## 使用 EAC 启用或禁止从 UM 自动助理将呼叫转移到用户

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其配置呼叫转移的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 自动助理**页 \>**地址簿和运算符访问**，在**与用户联系的选项**，选择启用呼叫转移**允许呼叫拨号用户**旁边的复选框。要防止呼叫转移，请清除复选框。

4.  单击\&quot;保存\&quot;。

> [!NOTE]
> 如果您清除此复选框并清除&amp;quot;允许呼叫者为用户留下语音消息&amp;quot;复选框，&amp;quot;用于搜索通讯簿的选项&amp;quot;会被禁用。


## 使用命令行管理工具启用或禁止从 UM 自动助理将呼叫转移到用户。

本示例将阻止名为 `MyUMAutoAttendant` 的 UM 自动助理上的呼叫转移。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

本示例将启用名为 `MyUMAutoAttendant` 的 UM 自动助理上的呼叫转移。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

