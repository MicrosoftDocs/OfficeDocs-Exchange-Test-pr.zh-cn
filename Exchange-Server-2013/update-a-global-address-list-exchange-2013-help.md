---
title: '更新全局地址列表: Exchange 2013 Help'
TOCTitle: 更新全局地址列表
ms:assetid: 236e8530-62dd-4c43-8a5d-8465623252e6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266966(v=EXCHG.150)
ms:contentKeyID: 50490073
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新全局地址列表

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

可以使用命令行更新全局地址列表 (GAL)。GAL 是一个目录，其中包含与组织内实施 MicrosoftExchange 的每个组、用户和联系人对应的项。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;地址列表\&quot;条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的\&quot;向角色组添加角色\&quot;部分。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行更新 GAL

本示例更新 Fourth Coffee 公司的 GAL。

> [!NOTE]  
> 运行此命令仅启动更新进程。更新 GAL 可能需要数小时的时间。


    Update-GlobalAddressList -Identity "Fourth Coffee"

有关语法和参数的详细信息，请参阅 [Update-GlobalAddressList](https://technet.microsoft.com/zh-cn/library/aa998806\(v=exchg.150\))。

