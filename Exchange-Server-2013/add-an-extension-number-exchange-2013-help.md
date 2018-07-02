---
title: '添加分机号码: Exchange Online Help'
TOCTitle: 添加分机号码
ms:assetid: 1a73c9c8-cb50-4bd7-a101-dadd20e28031
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335124(v=EXCHG.150)
ms:contentKeyID: 50556535
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 添加分机号码

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-14_

为某个用户启用 UM 并将其与电话分机拨号计划关联时，将为包含该用户的分机号的用户创建 EUM 代理地址。必须为要使用的 UM 至少定义一个分机号码，以便将语音邮件发送到用户的邮箱。在用户呼叫 Outlook Voice Access 号码时，也会使用分机号码。

添加当用户已启用了 UM 的主要分机号码将被列为主要 EUM 代理服务器地址。如果移除了主分机号，添加包含该用户的分机号码的第一个 EUM 代理地址将成为主 EUM 代理服务器地址。添加任何其他分机号码将被列为次要 EUM 代理地址。添加其他辅助的分机号码，调用方可以将用户的语音邮件保留在已设置的所有分机号码。所有语音邮件将被传递到同一个用户的邮箱。

您可以使用 EAC 或外壳添加主键列或用户辅助分机号码。您可以使用上用户的邮箱中 EAC**电子邮件地址**页添加主要或次要的分机号码。您无法使用**UM 邮箱**页中 EAC 添加主扩展数字，但您可以使用该页面添加辅助分机号码。

您可以通过在命令行管理程序中使用 **Get-UMMailbox** cmdlet 或 **Get-Mailbox** cmdlet，来查看用户的主分机号码和辅助分机号码。

有关与已启用语音邮件的用户相关的其他管理任务，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 邮箱\&quot;条目。

  - 在执行这些过程之前，请确认已创建了电话分机 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 邮箱策略。有关详细步骤，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。

  - 在执行这些过程之前，请确认已为用户的邮箱启用了 UM，并且用户的邮箱已经与电话分机拨号计划关联。有关详细步骤，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认要分配给用户的分机号码包含 UM 拨号计划中设置的正确位数。

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

## 使用 EAC 添加辅助分机号码

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要为其添加分机号码的邮箱。

3.  在详细信息窗格的\&quot;电话和语音功能\&quot;\&quot;统一消息\&quot;下，单击\&quot;查看详情\&quot;。

4.  在\&quot;UM 邮箱\&quot;页面上，单击\&quot;其他分机号\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  在\&quot;其他分机号\&quot;页面上的\&quot;UM 拨号计划\&quot;框旁边，单击\&quot;浏览\&quot;，然后查找该用户的拨号计划。

6.  在\&quot;其他分机号\&quot;页面上的\&quot;分机号码\&quot;框中，键入分机号码，然后单击\&quot;确定\&quot;。

7.  单击\&quot;保存\&quot;。

## 使用 EAC 添加主分机号码或辅助分机号码

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择您要添加分机号码的邮箱，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;用户邮箱\&quot;页面上的\&quot;电子邮件地址\&quot;下，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;新建电子邮件地址\&quot;页面上，选择\&quot;EUM\&quot;，然后在\&quot;地址/扩展\&quot;框中输入用户分机号码。

5.  在\&quot;新建电子邮件地址\&quot;页面的\&quot;拨号计划\&quot;下，单击\&quot;浏览\&quot;，选择电话分机拨号计划，然后单击\&quot;确定\&quot;。

6.  单击\&quot;保存\&quot;。

## 使用命令行管理程序添加分机号码

本示例为 Tony Smith（启用了 UM 的用户）添加分机号码 22222。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>添加使用 Shell 分机号码前，您需要确定您想要添加 EUM 代理地址的位置。要确定位置，请使用<strong>$mbx.EmailAddresses</strong>命令。在列表中的第一个代理地址将为 0。</td>
</tr>
</tbody>
</table>


    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

