---
title: '配置全局地址列表属性: Exchange 2013 Help'
TOCTitle: 配置全局地址列表属性
ms:assetid: 5fd2c96f-fe93-4b5a-8495-70c450511a37
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232068(v=EXCHG.150)
ms:contentKeyID: 50490681
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置全局地址列表属性

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

本主题介绍如何修改全局地址列表 (GAL) 的设置。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“地址列表”条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的“向角色组添加角色”部分。

  - 不能编辑默认 GAL 的设置。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序配置 GAL 属性

本示例将新名称 FourthCoffee 分配给 GUID 为 96d0c505-eba8-4103-ad4f-577a1bf4ad7b 的 GAL。

    Set-GlobalAddressList -Identity 96d0c505-eba8-4103-ad4f-577a1bf4ad7b -Name FourthCoffee

> [!NOTE]
> 如果要使用固有条件筛选器属性，则 <em>IncludedRecipients</em> 参数的值不能为空。


本示例将 Fourth Coffee 全局 GAL 中包含的收件人更改为所属公司设为 Fourth Coffee 的收件人。

    Set-GlobalAddressList -Identity Fourth Coffee -RecipientFilter {Company -eq "Fourth Coffee"}

有关语法和参数的详细信息，请参阅 [Set-GlobalAddressList](https://technet.microsoft.com/zh-cn/library/bb123877\(v=exchg.150\))。

