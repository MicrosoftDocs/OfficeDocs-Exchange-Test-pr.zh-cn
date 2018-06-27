---
title: '配置 Outlook Voice Access 用户可以联系的用户组: Exchange Online Help'
TOCTitle: 配置 Outlook Voice Access 用户可以联系的用户组
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50491353
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 Outlook Voice Access 用户可以联系的用户组

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-09_

您可以指定哪些用户可以接收已转接的呼叫或语音邮件从 Outlook Voice Access 用户的消息。默认情况下被选中**此拨号计划中**选择。您可以更改此设置以允许 Outlook Voice Access 用户传输调用或向用户位于整个组织对现有 UM 自动助理，或特定的分机号码发送语音消息。

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

## 使用 EAC 配置 Outlook Voice Access 用户可以联系的用户组

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

4.  在\&quot;转移和搜索\&quot;中的\&quot;允许呼叫者使用姓名或别名搜索用户\&quot;下，选择下列选项之一：
    
      - **仅在此拨号计划中**   使用此选项可以允许呼叫 Outlook Voice Access 号码的 Outlook Voice Access 用户找到并联系同一拨号计划中的用户。
    
      - **在整个组织中**  使用此选项以使 Outlook Voice Access 用户能够连接到 Outlook Voice Access 编号查找并联系整个组织中的任何人。这包括所有已启用邮箱的用户。
    
      - **仅在此自动助理**  使用此选项以使 Outlook Voice Access 用户能够连接到 Outlook Voice Access 号码连接到特定的自动助理。在此处指定之前，您必须创建自动助理。这允许 Outlook Voice Access 用户转移到另一个自动助理。您在此处选择的自动助理可以语音启用或不启用语音的自动助理。
    
      - **仅为此扩展**  使用此选项可以允许 Outlook Voice Access 用户连接到您指定分机号码。只有数字可用于扩展。在此字段中定义的位数必须匹配的 UM 拨号计划配置分机号码中的位数。

5.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置 Outlook Voice Access 用户可以联系的用户组

本示例设置 Outlook Voice Access 用户可以为名为 `MyUMDialPlan` 的 UM 拨号计划与整个组织联系的用户组。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

本示例设置 Outlook Voice Access 用户可以为名为 `MyUMDialPlan` 的 UM 拨号计划与 `DialPlan` 联系的用户组。

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

