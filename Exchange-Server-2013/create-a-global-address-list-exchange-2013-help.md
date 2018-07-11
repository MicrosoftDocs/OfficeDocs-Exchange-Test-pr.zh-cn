---
title: '创建全局地址列表: Exchange Online Help'
TOCTitle: 创建全局地址列表
ms:assetid: 59e4955a-8999-4d17-be9f-23a41a23b929
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232063(v=EXCHG.150)
ms:contentKeyID: 50490618
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建全局地址列表

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

全局地址列表 (GAL) 是一个目录，其中包含实现 MicrosoftExchange 的组织中每个组、用户和联系人的条目。如果组织使用通讯簿策略，你可能需要创建额外的 GAL。有关详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;地址列表\&quot;条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的\&quot;向角色组添加角色\&quot;部分。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 通过使用命令行管理程序，使用条件筛选器属性创建一个 GAL

本示例为其公司列为 Contoso 的邮箱用户收件人创建名为 GAL\_Contoso 的 GAL。

    New-GlobalAddressList -Name "GAL_Contoso" -IncludedRecipients MailboxUsers -ConditionalCompany Contoso

> [!NOTE]  
> 如果要使用固有条件筛选器属性，则 <em>IncludedRecipients</em> 参数不能为空。


有关语法和参数的详细信息，请参阅 [New-GlobalAddressList](https://technet.microsoft.com/zh-cn/library/bb123785\(v=exchg.150\))。

## 通过使用命令行管理程序，使用收件人筛选器创建一个 GAL

此示例创建一个名为 GAL\_AgencyA 的 GAL，其中包含的收件人的 *CustomAttribute15* 参数的值为 `AgencyA`。

    New-GlobalAddressList -Name "GAL_AgencyA" -RecipientFilter {CustomAttribute15 -like "AgencyA"}

有关语法和参数的详细信息，请参阅 [New-GlobalAddressList](https://technet.microsoft.com/zh-cn/library/bb123785\(v=exchg.150\))。

