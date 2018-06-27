---
title: '配置最大呼叫持续时间: Exchange Online Help'
TOCTitle: 配置最大呼叫持续时间
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 50489833
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置最大呼叫持续时间

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-09_

可以指定在结束呼叫之前，传入呼叫连接到系统但不转接到有效分机号所能持续的最大分钟数。对于大多数组织来说，应当将此值设置为默认值：30 分钟。此设置适用于所有呼叫，包括传入 Outlook Voice Access 呼叫、组织内部的语音呼叫、进入统一消息 (UM) 自动助理的语音呼叫以及从组织外部进行的传真呼叫。

此值可以设置为 10 到 120 的数字。将此值设置得太低可能会导致传入呼叫在完成之前即挂断。例如，如果组织收到许多大型传真邮件，则可能需要考虑在默认值的基础上增大此值，以便收到传真邮件的所有页面。

有关与 UM 拨号计划相关的其他任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

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

## 使用 EAC 配置最长呼叫持续时间

1.  在 EAC 中，导航到\&quot;统一消息\&quot; \>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;设置\&quot;中的\&quot;最长呼叫持续时间(分钟)\&quot;下，以分钟为单位输入数字。

5.  单击\&quot;保存\&quot;。

## 使用命令行配置最长呼叫持续时间

此示例将一个名为 `MyUMDialPlan` 的 UM 拨号计划的最大呼叫持续时间设置为 10 分钟。

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

