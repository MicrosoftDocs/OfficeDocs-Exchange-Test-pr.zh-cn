---
title: '删除联合身份验证信任: Exchange 2013 Help'
TOCTitle: 删除联合身份验证信任
ms:assetid: dc4d126d-b567-470d-a5d0-e1402bf8f369
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657500(v=EXCHG.150)
ms:contentKeyID: 50491706
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除联合身份验证信任

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-04_

联合身份验证信任将建立 Microsoft Exchange 2013 组织和 Azure Active Directory 身份验证系统之间的信任关系，并支持与其他联合 Exchange 组织的共享。从本地 Exchange 组织删除联合信任将禁用与其他联合 Exchange 组织以及将您的组织作为混合部署的一部分连接的 Office 365 组织之间的联合共享。在删除联合身份验证信任之前，应当仔细考虑对您组织的整体影响。

有关联合身份验证的更多管理任务，请参阅[联合程序](federation-procedures-exchange-2013-help.md)。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“联合身份验证和证书”权限条目。

  - 在删除联合身份验证后，可从公共 DNS 服务器删除每个联合域的 TXT 记录。查看通过托管公用 DNS 记录的组织删除 TXT 记录的要求。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 删除联合身份验证信任

1.  在本地组织中的 Exchange 2013 服务器上，导航到“组织”\>“共享”。

2.  在“联合身份验证信任”部分，单击“删除”。

3.  在警告中，单击“是”确认要删除联合信任。

4.  在删除联合身份验证信任后，单击“关闭”。

## 使用命令行管理程序删除联合身份验证信任

本示例删除联合身份验证信任。

```powershell
Remove-FederationTrust
```

有关语法和参数的详细信息，请参阅 [Remove-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd351153\(v=exchg.150\))。

## 您如何知道这有效？

要检查是否成功删除了联合身份验证信任，可进行以下操作之一：

  - 在 EAC 中，导航到“组织”\>“共享”。如果成功删除了联合身份验证信任，只有“启用”按钮将在“联合身份验证信任”下可用。

  - 在命令行管理程序中，运行以下命令检查是否不再为您的 Exchange 组织返回联合身份验证信任信息。
    
    ```powershell
Get-FederationTrust
```
    
    有关语法和参数的详细信息，请参阅 [Get-FederationTrust](https://technet.microsoft.com/zh-cn/library/dd351262\(v=exchg.150\))。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

