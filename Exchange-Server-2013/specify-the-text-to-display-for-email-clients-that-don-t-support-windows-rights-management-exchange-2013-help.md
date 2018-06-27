---
title: '指定要为不支持 Windows 权限管理的电子邮件客户端显示的文本: Exchange Online Help'
TOCTitle: 指定要为不支持 Windows 权限管理的电子邮件客户端显示的文本
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52061418
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 指定要为不支持 Windows 权限管理的电子邮件客户端显示的文本

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-22_

可以指定用户收到受保护的语音邮件但他们的电子邮件客户端不支持信息权限管理 (IRM) 或 Windows 权限管理时发送到用户的文本。

只有电子邮件客户端支持 Windows 权限管理或启用 UM 的用户使用 Outlook Voice Access 访问受保护的语音邮件时，才能访问受保护的语音邮件。

受保护的语音邮件被加密。当受保护语音消息 ︰

  - 在 Microsoft Outlook 和 Outlook Web App 中，邮件会被标记为\&quot;私人\&quot;。

  - 只有语音邮件的预期收件人才能打开该语音邮件。

  - 收件人可以答复语音邮件，但无法将其转发给未包括在原始语音邮件中的人员。

如果受保护的语音邮件发送给某人的电子邮件客户端不支持 Windows 权限管理并不访问使用Outlook访问语音邮件，电子邮件将发送给他们，包括您指定的文本。该文本应包括被调用的方应执行的操作有关的说明不能接收受保护的语音邮件。

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

## 使用 EAC 指定要对不支持 Windows 权限管理的电子邮件客户端显示的文本

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要管理的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 邮箱策略\&quot;页 \>\&quot;受保护的语音邮件\&quot;上，在\&quot;发送给没有 Windows 权限管理支持的用户的邮件\&quot;下的文本框内键入邮件文本。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序指定要对不支持 Windows 权限管理的电子邮件客户端显示的文本

本示例指定要对与名为 `MyUMMailboxPolicy` 的 UM 邮箱策略关联且其电子邮件客户端不支持 Windows 权限管理用户显示的文本。

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

