---
title: '配置托管可用性覆盖: Exchange 2013 Help'
TOCTitle: 配置托管可用性覆盖
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890411
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置托管可用性覆盖

 

_**适用于：** Exchange Online, Exchange Server 2013 SP1_

_**上一次修改主题：** 2015-11-30_

托管可用性执行持续探测，以检测 Exchange 组件或其相关项的可能问题，它可执行恢复操作，以确保最终用户体验不会受这些组件中任一组件的问题所影响。但是，可能有一些方案的即用设置不适合您的环境。可以通过创建覆盖自定义托管可用性探测器、监视器和响应器。

有两种覆盖类型：局部和全局。顾名思义，局部覆盖仅在其创建所在的服务器上可用，全局覆盖用于将覆盖应用到多个服务器。对于特定的持续时间或特定版本的 Exchange，可以创建这两种覆盖，但不能同时创建。

> [!NOTE]  
> 创建覆盖时，它不会立即生效。Microsoft Exchange 运行状况管理服务每隔 10 分钟检查一次配置更改，并将加载检测到的任何配置更改。如果您不想等待，可以重新启动该服务。


有关与托管可用性相关的其他管理任务，请参阅[管理运行状况设置和服务器运行状况](manage-health-sets-and-server-health-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 只能使用命令行管理程序执行此过程。 若要了解如何在本地 Exchange 组织中打开 Exchange 命令行管理程序，请参阅[打开命令行管理程序](https://technet.microsoft.com/zh-cn/library/dd638134\(v=exchg.150\))。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 Exchange 命令行管理程序 创建局部覆盖

若要创建特定持续时间的局部覆盖，请使用以下语法。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

若要为特定版本的 Exchange 创建局部覆盖，请使用以下语法。

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>

> [!NOTE]  
> 在创建覆盖时，<em>Identity</em> 参数中使用的值区分大小写。


本示例在名为 EXCH03 的服务器上添加了一个将响应器 `ActiveDirectoryConnectivityConfigDCServerReboot` 禁用 20 天的局部覆盖。

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## 您如何知道操作成功？

要确认您已成功创建局部覆盖，请使用 **Get-ServerMonitoringOverride** cmdlet 查看局部覆盖列表：

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

覆盖应出现在列表中。

## 使用 Exchange 命令行管理程序 删除局部覆盖

若要删除局部覆盖，请使用以下语法。

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

本示例从 EXCH01 服务器删除 Exchange 运行状况设置中的 `ActiveDirectoryConnectivityConfigDCServerReboot` 响应器的现有局部覆盖。

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## 您如何知道这有效？

要确认您已成功删除局部覆盖，请使用 **Get-ServerMonitoringOverride** cmdlet 查看局部覆盖列表：

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

已删除的覆盖不应出现在列表中。

## 使用 Exchange 命令行管理程序 创建全局覆盖

若要创建特定持续时间的全局覆盖，请使用以下语法。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

若要为特定版本的 Exchange 创建全局覆盖，请使用以下语法。

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>

> [!NOTE]  
> 在创建覆盖时，<em>Identity</em> 参数中使用的值区分大小写。


此示例添加了一个将 `OnPremisesInboundProxy` 探测器禁用 30 天的全局覆盖。

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

本示例为运行 Exchange 版本 15.01.0225.042 的所有服务器添加了一个禁用 `StorageLogicalDriveSpaceEscalate` 响应器的全局覆盖。

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## 您如何知道操作成功？

要确认您已成功创建全局覆盖，请使用 **Get-GlobalMonitoringOverride** cmdlet 查看全局覆盖列表：

    Get-GlobalMonitoringOverride

覆盖应出现在列表中。

## 使用 Exchange 命令行管理程序 删除全局覆盖

若要删除全局覆盖，请使用以下语法。

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

本示例会删除 `FrontEndTransport` 运行状况设置中 `OnPremisesInboundProxy` 探测器的 `ExtensionAttributes` 属性的现有全局覆盖。

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## 您如何知道这有效？

要确认您已成功删除全局覆盖，请使用 **Get-GlobalMonitoringOverride** cmdlet 查看全局覆盖列表：

    Get-GlobalMonitoringOverride

已删除的覆盖不应出现在列表中。

