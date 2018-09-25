---
title: '管理站点邮箱设置策略: Exchange 2013 Help'
TOCTitle: 管理站点邮箱设置策略
ms:assetid: 2f160d1a-a031-461f-8d29-c9cd49ca1645
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ710340(v=EXCHG.150)
ms:contentKeyID: 50490137
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理站点邮箱设置策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-21_

站点邮箱设置策略仅适用于发送到站点邮箱和从站点邮箱发送的电子邮件以及 Exchange 服务器上站点邮箱的大小。

要了解有关站点邮箱的详细信息，请参阅[网站邮箱](site-mailboxes-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“站点邮箱”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 尽管您可以创建多个站点邮箱设置策略，但是仅将默认设置策略应用到所有站点邮箱。您不能在组织内应用多个策略。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建站点邮箱设置策略

此示例创建了默认设置策略 SM\_ProvisioningPolicy，该策略具有以下设置：

  - 站点邮箱的警告配额为 9 GB。

  - 当邮箱大小达到 10 GB 时，禁止站点邮箱接收邮件。

  - 可发送给站点邮箱的最大电子邮件大小为 50 MB。

<!-- end list -->

```powershell
    New-SiteMailboxProvisioningPolicy -Name SM_ProvisioningPolicy -IsDefault -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB -MaxReceiveSize 50MB
```

## 查看站点邮箱设置策略的设置

此示例返回有关组织中所有站点邮箱设置策略的详细信息。

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List
```

此示例返回组织中的所有策略，但仅显示 `IsDefault` 信息以确定默认策略。

```powershell
Get-SiteMailboxProvisioningPolicy | Format-List IsDefault
```

## 更改现有的站点邮箱设置策略

此示例更改了站点邮箱设置策略 Default，使站点邮箱可以接收的最大电子邮件大小达到 25 MB。（在安装 Exchange 时，会创建一个名为“Default”的设置策略。）

```powershell
Set-SiteMailboxProvisioningPolicy -Identity Default -MaxReceiveSize 25MB
```

此示例将警告配额更改为 9.5 GB，将禁止发送和接收的配额更改为 10 GB。

```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -IssueWarningQuota 9GB -ProhibitSendReceiveQuota 10GB
```

## 配置一个站点邮箱名前缀

新站点邮箱创建后，默认情况下电子邮件地址会有一个前缀。电子邮件地址前缀允许您轻松地搜索并查询站点邮箱，也可能帮助用户鉴别电子邮件地址。如果让您选择，您可以禁用前缀，也可以更改 Office 365 中您租户的前缀或内部部署中指定林的前缀。在默认的前缀行为下，如果您的站点邮箱是在 Office 365 中创建，那么默认前缀是 **SMO-**。另外，如果您的站点邮箱是在您的内部部署中创建，前缀就是 **SM-**。这些部署中的默认行为不同，所以如果站点邮箱在这两个位置上创建，然后同步跨内部部署，混合客户也不会发生冲突。

这个示例通过设置 *DefaultAliasPrefixEnabled* 参数为 $false 禁用前缀命名。

```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -DefaultAliasPrefixEnabled $false -AliasPrefix $null
```

这个示例更改了默认设置策略并将 *AliasPrefix* 设置为 FOREST01。

> [!NOTE]  
> 对于多个林的部署，在两个或多个林中采用相同的名称创建站点邮箱的情况下，建议在跨林同步对象时在每个林中使用不同的前缀以避免冲突。

```powershell
    Set-SiteMailboxProvisioningPolicy -Identity Default -AliasPrefix FOREST01 -DefaultAliasPrefixEnabled $false
```

> [!NOTE]  
> 如果是 Exchange 内部部署和 Office 365 中的混合部署，所有基于云的站点邮箱均采用前缀 <strong>SMO-</strong> 创建。Office 365 和 Exchange 内部部署中的前缀不同，因此，如果站点邮箱在这两个位置中创建，然后同步跨内部部署，混合客户也不会发生冲突。AliasPrefix 参数优先于 DefaultAliasPrefixEnabled 参数，因此，如果 <em>AliasPrefix</em> 参数设置为有效的非 Null 字符串，每个新站点邮箱都会将该字符串添加到别名前。


## 删除站点邮箱设置策略

此示例删除在 Exchange 安装期间创建的默认站点邮箱策略。

```powershell
Remove-SiteMailboxProvisioningPolicy -Identity Default
```

> [!IMPORTANT]  
> 在删除名为“Default”的策略之前，必须先创建并指定另一个默认策略。


## 详细信息

有关语法和参数的详细信息，请参阅下列主题：

[New-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-cn/library/jj218647\(v=exchg.150\))

[Get-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-cn/library/jj218617\(v=exchg.150\))

[Set-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-cn/library/jj218624\(v=exchg.150\))

[Remove-SiteMailboxProvisioningPolicy](https://technet.microsoft.com/zh-cn/library/jj218672\(v=exchg.150\))

