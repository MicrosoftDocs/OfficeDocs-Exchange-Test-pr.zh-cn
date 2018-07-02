---
title: '配置组可以联系到的用户: Exchange Online Help'
TOCTitle: 配置组可以联系到的用户
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52061345
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置组可以联系到的用户

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-09_

您可以指定的组中的用户的统一邮件 (UM) 自动助理到呼叫时，呼叫者可以联系。默认情况下，调用方可以联系同一与 UM 自动助理关联的拨号计划中的用户。但是，您可以更改允许呼叫转移呼叫或向用户发送语音消息者所在组织的通讯簿，或者对于一组特定的用户的用户分组。

有关与 UM 自动助理相关的更多管理任务，请参阅[管理 UM 自动助理](manage-a-um-auto-attendant-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

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

## 使用 EAC 配置呼叫者可以联系的用户组

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择您要配置的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页 \>\&quot;通讯簿和话务员权限\&quot;的\&quot;用于搜索通讯簿的选项\&quot;下，可从下列选项中进行选择：
    
      - **仅在此拨号计划中**   选择此选项可以允许连接到 UM 自动助理的呼叫者查找并联系在与该 UM 自动助理相关联的拨号计划中的用户。
    
      - **在整个组织中**  选择此选项可允许呼叫者连接到 UM 自动助理，若要查找并联系组织的通讯簿中列出的所有人。这包括所有已启用邮箱的用户。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序配置呼叫者可以联系的用户组

本示例将呼叫者可以联系的用户范围设置为 UM 自动助理（名为 `MyUMAutoAttendant`）上组织的通讯簿中的所有用户。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

