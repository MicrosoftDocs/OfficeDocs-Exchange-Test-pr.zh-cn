---
title: '禁用 UM IP 网关。: Exchange Online Help'
TOCTitle: 禁用 UM IP 网关。
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 50492053
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用 UM IP 网关。

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-13_

默认情况下，在创建统一消息 (UM) IP 网关时，UM IP 网关的状态设置为启用。在创建 UM IP 网关之后，可以通过将其状态设置为禁用，禁用网关的运行。在禁用 UM IP 网关后，被配置使用的 IP 语音 (VoIP) 网关、IP 专用交换机 (PBX) 或会话边界控制器 (SBC) 将无法处理传入统一消息呼叫。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关并且已启用。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)和[启用 UM IP 网关](enable-a-um-ip-gateway-exchange-2013-help.md)。

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

## 使用 EAC 禁用 UM IP 网关

1.  在 EAC 中，导航到\&quot;统一消息\&quot; \>\&quot;UM IP 网关\&quot;，选择要禁用的 UM IP 网关，然后单击\&quot;向下箭头\&quot;![向下键图标](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "向下键图标")。

2.  在\&quot;警告\&quot; 页上，单击\&quot;是\&quot;。

## 使用命令行管理程序禁用 UM IP 网关

本示例将禁用名为 `MyUMIPGateway` 的 UM IP 网关，并使其停止接受来自该 VoIP 网关、IP PBX 或 SBC 的传入呼叫。

    Disable-UMIPGateway -Identity MyUMIPGateway

本示例将禁用名为 `MyUMIPGateway` 的 UM IP 网关，并立即断开所有当前呼叫。

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

