---
title: '允许用户接收传真的同一拨号计划中: Exchange Online Help'
TOCTitle: 允许用户接收传真的同一拨号计划中
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52061468
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许用户接收传真的同一拨号计划中

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

您可以启用所有用户提供统一邮件 (UM) 拨号计划，可以在其邮箱中接收传真邮件链接。默认情况下，为统一消息启用并与 UM 拨号计划链接的用户可以接收传真邮件。若要允许已启用 UM 的用户在其邮箱中接收传真，拨号计划必须配置为接受传入的传真呼叫。您还必须启用 UM 邮箱策略上和用户的传真。默认情况下，传真被启用拨号计划，UM 邮箱策略，并为用户。但是，可能是的时间，更改这些默认设置并启用 UM 的用户不能接收传真。

如果您阻止传真邮件接收拨号计划上，与拨号计划相关联的所有用户不能接收传真的信息，即使您将配置单个用户的属性，以允许他们接收传真。启用或禁用 UM 拨号计划上传真优先设置在 UM 邮箱策略或单个启用 UM 的用户发送传真。

> [!NOTE]
> EAC 用于 UM 邮箱策略上配置传真设置。但是，必须使用外壳程序打开拨号计划或为单个用户配置传真设置。


有关传真合作伙伴的详细信息，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)。

有关与传真相关的更多管理任务，请参阅[传真的步骤](faxing-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序允许与拨号计划关联的用户接收传真

此示例使与名为 `MyUMDialPlan` 的 UM 拨号计划关联的启用 UM 的用户能够接收传入传真。

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

