---
title: '禁止用户在同一拨号计划中接收传真: Exchange Online Help'
TOCTitle: 禁止用户在同一拨号计划中接收传真
ms:assetid: 4fc66414-c950-4bca-ac20-4e489f288d06
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201688(v=EXCHG.150)
ms:contentKeyID: 52061353
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁止用户在同一拨号计划中接收传真

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

可以防止已启用 UM 的用户的链接与统一消息 (UM) 拨号计划接收传真消息。默认情况下，为统一消息启用并与 UM 拨号计划链接的用户可以接收传真邮件。但是，有时可能想要阻止用户与特定接收传真 UM 拨号计划相关联的。

您可以防止已启用 UM 的用户通过配置 UM 拨号计划、 UM 邮箱策略或启用 UM 的用户的邮箱接收传真。如果您禁用传入传真邮件传递在 UM 拨号计划，与拨号计划相关联的所有用户将都无法接收传真。启用或禁用 UM 拨号计划传真功能优先于单个启用 UM 的用户的设置。

> [!NOTE]  
> EAC 用于 UM 邮箱策略上配置传真设置。但是，必须使用外壳程序打开拨号计划或为单个用户配置传真设置。


有关传真合作伙伴的详细信息，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)。

有关与传真相关的更多管理任务，请参阅[传真的步骤](faxing-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序阻止与拨号计划链接的用户接收传真

本示例阻止与名为 `MyUMDialPlan` 的 UM 拨号计划关联并且启用了 UM 的用户接收传真。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $false

