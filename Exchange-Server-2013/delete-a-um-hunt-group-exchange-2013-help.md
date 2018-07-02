---
title: '删除 UM 智能寻线: Exchange Online Help'
TOCTitle: 删除 UM 智能寻线
ms:assetid: 11ac102d-b58d-486c-85b6-e096428e556d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996318(v=EXCHG.150)
ms:contentKeyID: 50556527
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除 UM 智能寻线

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-05_

删除统一消息 (UM) 智能寻线之后，与该 UM 智能寻线关联的 UM IP 网关将不再提供服务或应答传入呼叫。如果删除 UM 智能寻线使 UM IP 网关中没有任何其他已配置的智能寻线，则 UM IP 网关将无法处理 UM 呼叫。

有关与 UM 智能寻线相关的其他任务，请参阅 [UM 查寻组过程](um-hunt-group-procedures-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要更改 UM 智能寻线设置，则必须删除该智能寻线，然后创建另一个具有适当设置的智能寻线。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 智能寻线\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 智能寻线。有关详细步骤，请参阅[创建 UM 智能寻线](create-a-um-hunt-group-exchange-2013-help.md)。

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

## 使用 EAC 删除 UM 智能寻线

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，单击您要更改的 UM 拨号计划，然后在工具栏上单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 智能寻线\&quot;下，请选择要删除的智能寻线，然后在工具栏上单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在\&quot;警告\&quot; 页上，单击\&quot;是\&quot;。

## 使用命令行管理程序删除 UM 智能寻线

此示例将删除名为 `MyUMHuntGroup` 的 UM 智能寻线。

    Remove-UMHuntGroup -identity MyUMHuntGroup

