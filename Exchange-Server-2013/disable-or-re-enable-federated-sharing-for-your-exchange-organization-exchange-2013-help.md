---
title: '禁用或重新启用您的 Exchange 组织的联合共享: Exchange 2013 Help'
TOCTitle: 禁用或重新启用您的 Exchange 组织的联合共享
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 50491611
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 禁用或重新启用您的 Exchange 组织的联合共享

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-17_

有时您可能需要临时禁用组织的联合共享。您不用删除现有联合信任或者删除将来可能需要的组织关系和共享策略，只需禁用联合信任的组织标识符 (OrgID)。

> [!CAUTION]  
> 对于使用 Office 365 的混合部署，为您的本地服务器禁用联合信任也将禁用混合功能，例如共享日历闲/忙信息、邮件提示和邮件跟踪。但是，如果禁用了内部部署组织的联合身份验证信任，将不会在混合部署中禁用安全邮件传输。


有关联合身份验证信任的详细信息，请参阅[联盟](federation-exchange-2013-help.md)。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

关于混合共享的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅*Federation and certificates*[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的权限条目。

  - 不会修改其他联合 Exchange 组织的任何现有组织关系和共享策略，并且它们也不会起作用。配置为向 Internet 收件人提供日历信息访问权限的共享策略将不受影响。

  - 不能使用 Exchange 管理中心 (EAC) 来禁用或启用联合身份验证信任的 OrgID。必须使用命令行管理程序。

## 使用命令行管理程序禁用或重新启用联合共享

该示例禁用了 OrgID 并禁用了 Exchange 组织的联合及联合共享。

```powershell
Set-FederatedOrganizationIdentifier -Enabled $false
```

该示例启用了 OrgID 并重新启用了 Exchange 组织的联合及联合共享。

```powershell
Set-FederatedOrganizationIdentifier -Enabled $true
```

有关语法和参数的详细信息，请参阅 [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/zh-cn/library/dd351037\(v=exchg.150\))。

## 您如何知道这有效？

成功完成 **Set-OrganizationIdentifier** cmdlet 初步表示已禁用或启用了 OrgID。

为了进一步验证是否成功，运行以下命令行管理程序命令并检查为 *Enabled* 参数返回的值。

```powershell
Get-FederatedOrganizationIdentifier
```

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

