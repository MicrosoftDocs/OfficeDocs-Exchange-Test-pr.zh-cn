---
title: '邮箱服务器和客户端访问服务器删除 SIP URI 的拨号计划: Exchange 2013 Help'
TOCTitle: 邮箱服务器和客户端访问服务器删除 SIP URI 的拨号计划
ms:assetid: 367441e1-1a0f-42c8-9fa8-8abe80b3d015
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997238(v=EXCHG.150)
ms:contentKeyID: 54652275
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 邮箱服务器和客户端访问服务器删除 SIP URI 的拨号计划

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-16_

您可以删除客户端访问和邮箱服务器 SIP URI 拨号计划。在部署 Microsoft Lync Server 时，若要启用出站调用才能正常工作，则必须手动添加所有客户端访问和邮箱服务器对您为 Lync 服务器创建的 SIP URI 拨号计划。但是，您可能需要一个客户端访问或邮箱服务器删除 Lync 部署，例如，如果您正在执行维护或使服务器脱机。

有关与 UM 拨号计划相关的其他管理任务，请参阅 [UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，请确认已创建了 SIP URI 的拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

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

## 使用 EAC 从 SIP URI 拨号计划中删除邮箱服务器

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的邮箱服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在**UM 服务设置**\>**关联的拨号计划**，找到要删除，请单击**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")的 SIP URI 拨号计划，然后单击**保存**。如果您要删除多个 SIP URI 拨号计划，和按住 CTRL 键，选择您想要删除拨号计划，然后单击**保存**。

## 使用命令行管理程序从 SIP URI 拨号计划中删除邮箱服务器

此示例从名为 `MySIPDialPlan` 的拨号计划中删除名为 `MyMailboxServer` 的邮箱服务器。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMService MyMailboxServer
    $s.dialplans-=$dp.identity
    Set-UMService -id MyMailboxServer -dialplans:$s.dialplans

在此示例中，有三个 SIP URI 拨号计划 ︰ SipDP1、 SipDP2 和 SipDP3。本示例删除名为`MyMailboxServer` SipDP3 拨号计划中的邮箱服务器。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1,SipDP2

在此示例中，有两个 SIP URI 拨号计划 ︰ SipDP1 和 SipDP2。本示例删除名为`MyMailboxServer` SipDP2 拨号计划中的邮箱服务器。

    Set-UMService -id MyMailboxServer -DialPlans SipDP1

此示例从所有 SIP 拨号计划中删除名为 `MyMailboxServer` 的邮箱服务器。

    Set-UMService -id MyUMServer -DialPlans $null

## 使用 EAC 从 SIP URI 拨号计划中删除客户端访问服务器

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在此列表视图中，选择您要修改的客户端访问服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在**UM 呼叫路由器设置**\>**关联的拨号计划**，找到要删除，请单击**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")的 SIP URI 拨号计划，然后单击**保存**。如果您要删除多个 SIP URI 拨号计划，和按住 CTRL 键，选择您想要删除拨号计划，然后单击**保存**。

## 使用命令行管理程序从 SIP URI 拨号计划中删除客户端访问服务器

此示例从名为 `MySIPDialPlan` 的 SIP URI 拨号计划中删除名为 `MyClientAccessServer` 的客户端访问服务器。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMCallRouterSettings MyClientAccessServer
    $s.dialplans-=$dp.identity
    Set-UMCallRouterSettings -id MyClientAccessServer -dialplans:$s.dialplans

在此示例中，有三个 SIP URI 拨号计划 ︰ SipDP1、 SipDP2 和 SipDP3。本示例删除名为`MyClientAccessServer` SipDP3 拨号计划中的客户端访问服务器。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1,SipDP2

在此示例中，有两个 SIP URI 拨号计划 ︰ SipDP1 和 SipDP2。本示例删除名为`MyClientAccessServer` SipDP2 拨号计划中的客户端访问服务器。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans SipDP1

此示例从所有 SIP 拨号计划中删除名为 `MyClientAccessServer` 的客户端访问服务器。

    Set-UMCallRouterSettings -id MyClientAccessServer -DialPlans $null

