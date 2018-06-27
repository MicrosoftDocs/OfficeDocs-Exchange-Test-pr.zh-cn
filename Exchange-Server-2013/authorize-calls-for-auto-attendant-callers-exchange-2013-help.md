---
title: '用于自动助理调用方授权调用: Exchange Online Help'
TOCTitle: 用于自动助理调用方授权调用
ms:assetid: c6c94fad-64df-44aa-a198-980f017ef716
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691238(v=EXCHG.150)
ms:contentKeyID: 51408274
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 用于自动助理调用方授权调用

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-21_

您可以启用统一邮件 (UM) 自动助理的拨号授权。自动助理的拨号授权用于禁止用户连接到自动助理进行国家/地区或国际电话呼叫，或*outdialing*。统一消息发出传出调用用户之后他们已经称其为 UM 自动配置的电话号码助理时将发生 outdialing。

有关与外拨相关的其他管理任务，请参阅[允许用户进行调用过程](allowing-users-to-make-calls-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：少于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 自动助理\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，先确认已创建 UM 自动助理。有关详细步骤，请参阅[创建 UM 自动助理](create-a-um-auto-attendant-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已在 UM 拨号计划上创建了国家/地区和国际的拨号规则。有关详细步骤，请参阅[创建用户的拨号规则](create-dialing-rules-for-users-exchange-2013-help.md)。

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

## 使用 EAC 启用对国家/地区内规则组的 UM 自动助理的拨号授权

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其创建拨号授权的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页 \>\&quot;拨号授权\&quot;上，单击\&quot;经授权的国家/地区内的拨号规则组\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;选择要允许的拨号规则组\&quot;页上，选择拨号规则组，单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用 EAC 启用对国际规则组的 UM 自动助理的拨号授权

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其创建拨号授权的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页 \>\&quot;拨号授权\&quot;上，单击\&quot;已授权国际拨号规则组\&quot;下的\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;选择要允许的拨号规则组\&quot;页上，选择拨号规则组，单击\&quot;确定\&quot;，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序启用对 UM 自动助理的国家/地区内拨号授权以及国际拨号授权

本示例启用 InCountry/RegionGroup1，InCountry/RegionGroup2。InternationalGroup1 和 InternationalGroup2 拨号授权 UM 自动助理在名为`MyUMAutoAttendant`。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowedInCountryOrRegionGroups InCountry/RegionGroup1,InCountry/RegionGroup2 -AllowedInternationalGroups InternationalGroup1,InternationalGroup2

