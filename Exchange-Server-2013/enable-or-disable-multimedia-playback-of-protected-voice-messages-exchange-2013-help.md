---
title: '启用或禁用多媒体播放受保护的语音邮件: Exchange Online Help'
TOCTitle: 启用或禁用多媒体播放受保护的语音邮件
ms:assetid: 3c33370c-4262-42b1-8d83-d61fc7c426cd
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423543(v=EXCHG.150)
ms:contentKeyID: 52061337
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用多媒体播放受保护的语音邮件

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以强制用户接收受保护的语音邮件电话功能使用播放收听他们的邮件发件人。或者，如果客户端软件不支持权限管理，用户必须使用Outlook语音访问来侦听消息。

收听语音邮件，启用统一邮件 UM 的用户可以使用播放电话功能或使用的计算机或移动设备上的多媒体软件。多媒体播放允许启用 UM 的用户可以通过计算机的扬声器使用媒体播放器或移动设备上使用媒体播放器收听语音邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>受保护的语音邮件是 _z0z_ 的仅适用于使用支持权限管理Outlook版本的客户端。如果客户端软件不支持权限管理，用户必须使用Outlook访问语音监听其电话。</td>
</tr>
</tbody>
</table>


默认情况下，在 UM 邮箱策略上的**RequireProtectedPlayOnPhone**属性的值设置为 false。这意味着与该 UM 邮箱策略相关联的启用 UM 的用户可收听由受保护的语音邮件 ︰

  - 使用 Outlook Voice Access。

  - 使用 Outlook 2010 或更高版本中的内置媒体播放器或\&quot;在电话上播放\&quot;按钮。

  - 使用 Outlook Web App 中的内置媒体播放器或\&quot;在电话上播放\&quot;按钮。

如果将此值设置为 true，多媒体播放受保护的语音邮件不被允许。启用 UM 的用户关联的 UM 邮箱策略的情况下，此值设置为 true 可以仅通过收听受保护的语音邮件 ︰

  - 使用 Outlook Voice Access。

  - 使用 Outlook 2010 或更高版本中的\&quot;在电话上播放\&quot;按钮。

  - 使用 Outlook Web App 中的\&quot;在电话上播放\&quot;按钮。

当启用了 UM 的用户在公共场所使用公用计算机、便携式计算机或其移动设备的媒体播放器来收听可能包含私人信息的受保护语音邮件时，这尤其有用。

有关与受保护语音邮件步骤相关的其他管理任务，请参阅[受保护的语音邮件过程](protected-voice-mail-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱策略\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

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

## 使用 EAC 启用或禁用受保护语音邮件的多媒体播放

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在**UM 邮箱策略**页 \>**受保护的语音邮件**，选择**需要播放受保护的语音邮件的电话上**启用该设置旁的复选框。清除该复选框以禁用此设置。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序启用或禁用受保护语音邮件的多媒体播放

此示例允许与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略相关联的用户使用媒体播放器来播放受保护的语音邮件。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $false

此示例阻止与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略相关联的用户使用媒体播放器来播放受保护的语音邮件。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -RequireProtectedPlayOnPhone $true

