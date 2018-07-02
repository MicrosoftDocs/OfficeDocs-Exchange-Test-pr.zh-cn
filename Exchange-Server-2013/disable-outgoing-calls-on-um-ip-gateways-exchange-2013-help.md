---
title: '禁用 UM IP 网关的传出呼叫: Exchange Online Help'
TOCTitle: 禁用 UM IP 网关的传出呼叫
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 50491248
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 禁用 UM IP 网关的传出呼叫

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-13_

您可以启用或禁用统一邮件 (UM) IP 网关的传出呼叫。当清除 UM IP 网关的属性上的**允许拨出电话，通过此 UM IP 网关**选项时，您将配置 UM IP 网关不接受并通过 IP (VoIP) 网关，IP PBX 或会话边框控制器 (SBC) 发送到语音拨出电话。尽管它不影响设置可控制是否可以拨出电话的用户启动 UM IP 网关**通过此 UM IP 网关允许拨出电话**，呼叫转移或从 VoIP 网关，IP PBX 或 SBC 的传入呼叫。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，请确认已创建 UM 拨号计划。 有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

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

## 使用 EAC 对 UM IP 网关禁用传出呼叫

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，选择要更改的 UM IP 网关，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM IP 网关\&quot;页上，清除\&quot;允许传出呼叫通过此 UM IP 网关\&quot;旁边的复选框。

3.  单击\&quot;保存\&quot;。

## 使用命令行管理程序对 UM IP 网关禁用传出呼叫

此示例在名为 `MyUMIPGateway` 的 UM IP 网关上禁用传出呼叫。

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

