---
title: '查看 UM 查寻组: Exchange Online Help'
TOCTitle: 查看 UM 查寻组
ms:assetid: f038f7b4-4de9-4373-bd58-09d49e37a3ed
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125167(v=EXCHG.150)
ms:contentKeyID: 50556683
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看 UM 查寻组

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

当您查看统一邮件 (UM) 查寻组的属性时，您可以查看与单个 UM 查寻组或所有与单个 UM IP 网关关联的 UM 查寻组关联的属性。如果未指定任何参数，则将返回所有 UM 查寻组。不能使用 EAC 来查看 UM 查寻组属性;您必须使用外壳程序。

已创建 UM 查寻组之后，不能更改的配置的设置。如果您想要更改的配置设置，如引导标识在 UM 查寻组，则必须删除现有 UM 查寻组并创建新的 UM 查寻组具有正确的设置。

有关与 UM 智能寻线相关的其他任务，请参阅[UM 查寻组过程](um-hunt-group-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间 ︰ 少于 1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 智能寻线\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 执行此过程之前，请确认已创建 UM 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 执行此过程之前，请确认已创建 UM 查寻组。有关详细步骤，请参阅[创建 UM 智能寻线](create-a-um-hunt-group-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序查看 UM 智能寻线的属性

本示例将显示 Active Directory 林中的所有 UM 智能寻线。

    Get-UMHuntGroup

本示例将在格式化列表中显示名为 `MyUMHuntGroup` 的 UM 智能寻线的详细信息。

    Get-UMHuntGroup -identity MyUMIPGateway\MyUMHuntGroup | Format-List

> [!NOTE]  
> 当您使用<strong>Get-UMHuntGroup</strong> cmdlet 时，不能输入只有 UM 查寻组的名称。您还必须包含与该 UM 查寻组关联的 UM IP 网关的名称。

