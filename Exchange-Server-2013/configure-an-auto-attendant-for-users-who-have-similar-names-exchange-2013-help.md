---
title: '配置为具有类似名称的用户自动助理: Exchange Online Help'
TOCTitle: 配置为具有类似名称的用户自动助理
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52061334
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置为具有类似名称的用户自动助理

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-12-16_

您可以配置为具有相似名称的自动助理的**地址簿和运算符访问**选项，用户使用的方法或可以在自动助理保留默认设置，并在与该自动助理关联的拨号计划配置此设置。默认情况下，自动助理可以区分两个或多个具有相同或类似的名称，因为上的默认设置自动助理是**拨号计划从继承**用户之间。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>对于为了让拥有相似姓名的用户能正常工作而包含的信息，您必须为您 Microsoft Exchange 组织中的收件人提供职务、部门和位置信息。</td>
</tr>
</tbody>
</table>


有关与 UM 自动助理相关的更多管理任务，请参阅 [UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

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


## 要执行什么操作？

## 使用 EAC 为用户名类似的用户配置 UM 自动助理

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择您要配置的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面上，单击\&quot;通讯簿和话务员权限\&quot;，然后在\&quot;为用户名相同的用户添加的信息\&quot;下，选择下列选项之一：
    
      - **称谓**   自动助理在列出匹配项时包括每个用户的称谓。
    
      - **部门**   自动助理在列出匹配项时包括每个用户的部门。
    
      - **位置**   自动助理在列出匹配项时包括每个用户的位置。
    
      - **无**   自动助理在列出匹配项时不包括其他任何信息。
    
      - **提示输入别名**   自动助理将提示呼叫方输入用户的别名。
    
      - **从拨号计划继承**   自动助理将使用与其相关联的拨号计划的默认设置。

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序为用户名类似的用户配置 UM 自动助理

本示例将与用户名类似的用户一起添加的信息设置为\&quot;提示输入别名\&quot;（对于名为 `MyUMAutoAttendant` 的 UM 自动助理）。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

本示例将与用户名类似的用户一起添加的信息设置为用户称谓，启用名称查找，并使拨入自动助理的呼叫方按下 \* 即显示名为 `MyUMAutoAttendant` 的 UM 自动助理的 Outlook Voice Access 欢迎问候语。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

