---
title: '重命名策略的通讯组: Exchange Online Help'
TOCTitle: 重命名策略的通讯组
ms:assetid: 9eb23fc9-3f59-4d09-9077-85c89a051ee0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218685(v=EXCHG.150)
ms:contentKeyID: 50489704
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 重命名策略的通讯组

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-10-13_

组的通讯组命名策略仅应用于所创建的用户组。当您或其他管理员使用 Exchange 管理中心 (EAC) 创建通讯组时，组命名策略被忽略，不应用于组名。

但是，如果您使用 Exchange 命令行管理程序创建或重命名通讯组，则将组命名策略应用到管理员创建的组，除非您使用 *IgnoreNamingPolicy* 参数覆盖该组命名策略。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;通讯组\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建新组时使用命令行管理程序覆盖组命名策略

若要覆盖组命名策略，请运行以下命令。

    New-DistributionGroup -Name <Group Name> -IgnoreNamingPolicy

例如，如果组织的组命名策略为 **DG\_\<Group Name\>\_Users**，则运行以下命令来创建名为 **All Administrators** 的组。

    New-DistributionGroup -Name "All Administrators" -IgnoreNamingPolicy

当 Microsoft Exchange 创建该组时，它将 **All Administrators** 用于 *Name* 和 *DisplayName* 参数。

## 重命名组时使用命令行管理程序覆盖组命名策略

若要在使用命令行管理程序重命名现有组时覆盖组命名策略，请运行以下命令。

    Set-DistributionGroup -Identity <Old Group Name> -Name <New Group Name> -DisplayName <New Group Name> -IgnoreNamingPolicy

例如，假设您创建一组命名策略的一个深夜，第二天早上您意识到您拼写错误的前缀中的文本字符串。第二天，您会看到，已创建一个新组的拼写错误的前缀。您可以修复组命名策略中 EAC，但您必须使用 Shell 拼错名称的组进行重命名。运行以下命令。

    Set-DistributionGroup -Identity "Goverment_Contracts_NWRegion" -Name "Government_ContractEstimates_NWRegion" -DisplayName "Government_ContractEstimates_NWRegion" -IgnoreNamingPolicy

> [!important]
> 请务必包括<em>DisplayName</em>参数，当您重命名组。如果不这样做，旧的名称仍将显示在收件人上的共享的地址簿:，抄送:，并从 ︰ 在电子邮件中的行。


## 您如何知道这有效？

若要验证是否已成功创建或重命名忽略组命名策略的通讯组，请运行以下命令。
```
    Get-DistributionGroup <Name> | FL DisplayName
```
```
    Get-OrganizationConfig | FL DistributionGroupNamingPolicy
```

如果该组的显示名称的格式不同于组织的组命名策略强制实施的组，则命令有效。

