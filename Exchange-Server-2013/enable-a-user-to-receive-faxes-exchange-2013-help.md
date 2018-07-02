---
title: '允许用户接收传真: Exchange Online Help'
TOCTitle: 允许用户接收传真
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52061395
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许用户接收传真

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

您可以启用统一邮件 (UM) 用户可以接收传真。默认情况下，当您为用户启用统一消息，他们将能够接收传真，如果启用传真和链接到用户的 UM 邮箱策略上配置传真伙伴的 URI。传真可以启用或禁用在 UM 拨号计划、 UM 邮箱策略或启用 UM 的用户的邮箱。

默认情况下，用户的邮箱，并且链接到包含用户的拨号计划允许传入传真。但是，若要接收传真的用户必须先启用 UM 邮箱策略与已启用 UM 的用户相关联并输入传真伙伴的 URI 上的入站传真。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>EAC 用于 UM 邮箱策略上配置传真设置。但是，必须使用外壳程序打开拨号计划或为单个用户配置传真设置。</td>
</tr>
</tbody>
</table>


有关传真合作伙伴的详细信息，请参阅[Microsoft 查明其传真合作伙伴](https://go.microsoft.com/fwlink/?linkid=190238)。

有关与传真相关的更多管理任务，请参阅[传真的步骤](faxing-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认分配给用户的 UM 邮箱策略已启用传真且传真合作伙伴的 URI 已正确配置。

  - 在执行这些步骤之前，请确认该用户启用了统一消息。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 使用命令行管理程序使 UM 用户可以接收传真

此示例使 Tony Smith 可以接收传入传真。

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

