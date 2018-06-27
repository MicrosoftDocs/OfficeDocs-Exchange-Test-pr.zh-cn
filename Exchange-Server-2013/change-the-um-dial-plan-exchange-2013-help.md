---
title: '更改 UM 拨号计划: Exchange Online Help'
TOCTitle: 更改 UM 拨号计划
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50490491
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更改 UM 拨号计划

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-05_

您可能需要移动到不同的 UM 拨号计划启用的统一邮件 (UM) 的用户或更改拨号计划与用户相关联。例如，您可以将启用 UM 的用户从电话分机拨号计划移动到 SIP URI 的拨号计划。

若要更改该 UM 拨号计划，将需要禁用统一消息的用户，然后用户启用统一邮件新建 UM 拨号计划上。这是因为不同的设置和要求，如不同的扩展名长度或不同的 URI 类型可能具有不同的拨号计划。例如，SIP URI 拨号计划需要 SIP 资源标识符分配给每个已启用 UM 的邮箱，但没有电话分机拨号计划。此外，每个 UM 邮箱包含引用 UM 拨号计划和 UM 邮箱策略。UM 邮箱策略，反过来，包含参考的 UM 拨号计划。如果要更改指向不同的拨号计划启用 UM 的用户的主代理地址时，UM 邮箱处于不一致的状态。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行此过程之前，请先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行此过程之前，请先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认，将现有的Exchange收件人启用统一消息。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

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


## 您该如何做？

## 步骤 1 ︰ 创建新的 UM 拨号计划

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要将已启用 UM 的用户迁移至 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server，必须首先创建 SIP URI 拨号计划。</td>
</tr>
</tbody>
</table>


有关详细说明，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

## 步骤 2 ︰ 禁用用户的统一邮件

有关详细说明，请参阅[禁用用户的语音邮件](disable-voice-mail-for-a-user-exchange-2013-help.md)。

## 第 3 步 ︰ 新的 UM 拨号计划上启用用户统一消息

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果您要将用户移动到Office通信服务器 2007 R2 或 Lync 服务器的环境，还必须包括 SIP 资源标识符为用户启用了 UM 时。您还必须选择与 SIP 的拨号计划关联的 UM 邮箱策略。</td>
</tr>
</tbody>
</table>


有关详细说明，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

