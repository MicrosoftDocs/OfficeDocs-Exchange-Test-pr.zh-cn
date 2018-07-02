---
title: '管理运行状况设置和服务器运行状况: Exchange 2013 Help'
TOCTitle: 管理运行状况设置和服务器运行状况
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890409
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理运行状况设置和服务器运行状况

 

_**适用于：**Exchange Online, Exchange Server 2013 SP1_

_**上一次修改主题：**2013-12-02_

您可以使用内置运行状况报告 cmdlet 来执行与托管可用性相关的各种任务，例如：

  - 查看服务器或服务器组的运行状况

  - 查看运行状况设置列表

  - 查看与特定运行状况设置相关的探测器、监视器和响应器列表

  - 查看监视器及其当前运行状况的列表

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：2 分钟

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 查看服务器运行状况

您可以使用命令行管理程序获取运行 Exchange 2013 的服务器的运行状况摘要。

## 使用命令行管理程序查看服务器运行状况

运行下列命令之一，查看运行 Exchange 2013 的服务器的运行状况设置和运行状况信息。

    Get-HealthReport -Identity <ServerName>

    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto

运行下列任一命令，查看运行 Exchange 2013 的服务器或数据库可用性组的运行状况设置。

    Get-ExchangeServer | Get-HealthReport -RollupGroup

    Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>

    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup

## 查看运行状况设置列表

运行状况设置是用于组件的一组监视器、探测器和响应器，可确定组件是否正常运行。您可以使用命令行管理程序查看运行 Exchange 2013 的服务器的运行状况设置列表。

## 使用命令行管理程序查看运行状况设置列表

运行以下命令，查看运行 Exchange 2013 的服务器的运行状况设置。

    Get-HealthReport -Server <ServerName>

## 查看运行状况设置的探测器、监视器和响应器

运行状况设置是用于组件的一组监视器、探测器和响应器，可确定组件是否正常运行。您可以使用命令行管理程序查看与运行 Exchange 2013 的服务器的运行状况设置相关的探测器、监视器和响应器列表。

## 使用命令行管理程序查看运行状况设置的探测器、监视器和响应器

运行以下命令，查看与运行 Exchange 2013 的服务器的运行状况设置相关的探测器、监视器和响应器。

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## 查看监视器及其当前运行状况的列表

监视器的运行状况使用运行状况设置中的“最差”监视器报告。您可以查看运行状况设置的详细信息，以查看哪些监视器正常运行，哪些运行不正常。

## 使用命令行管理程序查看监视器及其当前运行状况的列表

运行以下命令查看运行 Exchange 2013 的服务器的监视器及其当前运行状况的列表。

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

