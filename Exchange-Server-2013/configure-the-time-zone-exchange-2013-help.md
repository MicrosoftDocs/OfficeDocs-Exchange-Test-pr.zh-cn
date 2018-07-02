---
title: '配置时区: Exchange Online Help'
TOCTitle: 配置时区
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50556547
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置时区

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-17_

默认情况下，统一邮件 (UM) 自动助理使用创建它的邮箱服务器的时区。但是，存在以下的情况您可能需要更改为不同的时区时区 UM 自动助理。例如，如果您有两个 UM 拨号计划，并且每个拨号计划表示了不同的时区，您必须配置一个 UM 自动助理让邮箱服务器相同的时区和其他 UM 自动助理具有不同于邮箱服务器的时区。

关于 UM 自动助理的更多管理任务，请参阅[UM 自动助理过程](um-auto-attendant-procedures-exchange-2013-help.md)。

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

## 使用 EAC 配置时区

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要更改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要为其设置的时区的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 自动助理\&quot;页面上，单击\&quot;营业时间\&quot;，然后在\&quot;时区\&quot;下，从下拉列表中选择时区。

4.  若要保存更改，请单击\&quot;确定\&quot;，再单击\&quot;保存\&quot;。

## 使用命令行管理程序配置时区

本示例将名为 `MyUMAutoAttendant` 的 UM 自动助理的时区设置为太平洋时区。

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

