---
title: '配置 Active Directory 中的 Exchange 邮件路由设置: Exchange 2013 Help'
TOCTitle: 配置 Active Directory 中的 Exchange 邮件路由设置
ms:assetid: d01f8545-c201-4a96-be39-ed4c7008afcf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674705(v=EXCHG.150)
ms:contentKeyID: 50491716
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 Active Directory 中的 Exchange 邮件路由设置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

默认设置下，Microsoft Exchange Server 2013 将引用 Active Directory 中的 IP 站点链接对象来帮助确定开销最小的路由路径。但是，如果您确定 Active Directory IP 站点链接开销和流量模式对于 Exchange 中的邮件路由并非最佳，则可配置 Active Directory 中仅由 Exchange 使用的设置来帮助优化邮件流。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“Active Directory 站点间链接管理”条目。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序配置 Active Directory IP 网站链接上特定于 Exchange 的开销

确定要设置其 Exchange 开销的 Active Directory IP 网站链接的名称。较低的开销值指明了首选的路由。可检查路由表日志内容并查看 **ADTopologyPath ID** 部分的数据，以查看有关在两个 Active Directory 网站之间计算所得的开销最低的路由路径的详细信息。

要配置 Active Directory 网站链接上特定于 Exchange 的开销，请运行以下命令：

``` 
 Set-AdSiteLink <ADSiteLinkIdentity> -ExchangeCost <Integer | $null>
```

此示例在名为 IPSiteLinkAB 的 IP 站点链接上设置特定于 Exchange 的值为 10 的开销。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost 10

本示例清除名为 IPSiteLinkAB 的 IP 站点链接的 Exchange 开销。

    Set-AdSiteLink IPSiteLinkAB -ExchangeCost $null

## 您如何知道这有效？

要验证是否已在 Active Directory 网站链接上成功设置 Exchange 开销，请执行以下操作：

1.  运行以下命令：
    
        Get-AdSiteLink | Format-List Name,ExchangeCost

2.  验证是否已在 Active Directory 站点链接上配置 Exchange 开销。

## 使用命令行管理程序将 Active Directory 站点配置为集线器站点

如果集线器站点沿着邮件的最低开销路由路径存在，则必须通过集线器站点路由邮件。检查路由表日志的内容和查看 **ADTopologyPath ID** 部分的数据，以验证所选的网站是否位于开销最低的路由路径中的两个 Active Directory 站点之间。如果不是这种情况，您需要将 Exchange 的特定开销分配给 IP 站点链接，以使最低成本路由路径通过所选站点。

要将 Active Directory 站点配置为集线器站点，可运行以下命令：

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

本示例将 Active Directory 站点 Site A 配置为集线器站点。

    Set-AdSite "Site A" -HubSiteEnabled $true

本示例从 Active Directory 站点 Site B 删除集线器站点属性。

    Set-AdSite "Site B" -HubSiteEnabled $false

## 您如何知道这有效？

要验证是否已成功将 Active Directory 站点配置为集线器站点，请执行以下操作：

1.  运行以下命令：
    
        Get-AdSite | Format-List Name,HubSiteEnabled

2.  验证 *HubSiteEnabled* 的值对于 Active Directory 站点是否为 `True`。

