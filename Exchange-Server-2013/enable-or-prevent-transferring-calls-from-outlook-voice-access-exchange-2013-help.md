---
title: '启用或禁止将呼叫转接从 Outlook Voice Access: Exchange Online Help'
TOCTitle: 启用或禁止将呼叫转接从 Outlook Voice Access
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52061443
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁止将呼叫转接从 Outlook Voice Access

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

您可以使 Outlook Voice Access 用户传送到用户的统一邮件 (UM) 拨号计划，与相关联的呼叫或阻止他们这样做。默认情况下，同时启用了此选项，并**将保留而不响的用户电话的语音邮件**选项，以便 Outlook Voice Access 用户可以转移呼叫的用户在同一个 UM 拨号计划和为它们留下语音信息。此设置仅适用于 Outlook Voice Access 用户输入他们的 PIN 并进行身份验证。

有关与 UM 拨号计划相关的其他任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

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

## 使用 EAC 允许或阻止 Outlook Voice Access 用户转移呼叫

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

3.  在**传输和搜索**下**到允许呼叫**，, 选择**传输到用户**，以便调用方转移呼叫的拨号计划中其他用户旁边的复选框。如果您想要防止 Outlook Voice Access 用户转移呼叫的用户，请清除此复选框。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序允许或阻止 Outlook Voice Access 用户转移呼叫

此示例允许 Outlook Voice Access 用户在名为 `MyUMDialPlan` 的 UM 拨号计划上将呼叫转移至同一拨号计划内的用户。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

此示例阻止 Outlook Voice Access 用户在名为 `MyUMDialPlan` 的 UM 拨号计划上将呼叫转移至同一拨号计划内的用户。

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

