---
title: '删除 UM 拨号计划: Exchange Online Help'
TOCTitle: 删除 UM 拨号计划
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 50491540
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 UM 拨号计划

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-11_

您可以删除现有统一邮件 (UM) 拨号计划。当您删除 UM 拨号计划，它将不再可用于 UM IP 网关，UM 邮箱策略，和 UM 查寻组。如果它已被引用或关联的 UM 邮箱策略、 UM 自动助理、 UM IP 网关或 UM 查寻组，则无法删除 UM 拨号计划。

有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 删除现有拨号计划

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在列表视图中，选择要删除的 UM 拨号计划，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在警告页上，单击\&quot;是\&quot;。

## 使用命令行管理程序删除现有拨号计划

此示例将删除名为 `MyUMDialPlan` 的 UM 拨号计划。

    RemoveUMDialplan -identity MyUMDialPlan

