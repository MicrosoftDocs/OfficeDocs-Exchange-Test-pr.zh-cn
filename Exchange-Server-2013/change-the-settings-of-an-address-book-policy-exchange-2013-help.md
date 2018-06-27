---
title: '更改通讯簿策略的设置: Exchange 2013 Help'
TOCTitle: 更改通讯簿策略的设置
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 50491421
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改通讯簿策略的设置

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-03-30_

在创建了通讯簿策略 (ABP) 之后，可以查看或修改名称和分配的全局地址列表 (GAL)、脱机通讯簿 (OAB)、会议室列表和地址列表。

关于 ABP 的更多管理任务，请参阅[通讯簿策略程序](address-book-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“通讯簿策略”条目。

  - 为组织创建 ABP 是一个需要计划的多步骤流程。有关详细信息，请参阅[方案：部署通讯簿策略](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - 不能使用 Exchange 管理中心 (EAC) 配置 ABP。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 您想执行什么操作？

## 更改 ABP 的 OAB、会议室列表和 GAL

此示例将更改分配了名为 All Fabrikam ABP 的 ABP 的邮箱用户将要使用的 OAB、房间列表和 GAL。

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## 替换 ABP 中的地址列表

您为现有 ABP 指定的地址列表可替换 ABP 中所有的地址列表。

此示例要将现有的地址列表替换为地址列表 GovernmentAgencyA-Atlanta 和 GovernmentAgencyA-Moscow（针对名为 Government Agency A 的 ABP）。

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## 向 ABP 添加地址列表

若要保留在 ABP 中已定义的地址列表，当您向 ABP 添加新的地址列表时，您需要指定那些地址列表。

本示例将名为 Contoso-Chicago 的地址列表添加到名为 ABP Contoso 的 ABP（已被配置为使用名为 Contoso-Seattle 的地址列表）中。

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## 从 ABP 中删除地址列表

若要删除在 ABP 中已定义的现有地址列表，您需要指定要保留的地址列表。

例如，名为 ABP Fabrikam 的 ABP 使用地址列表 Fabrikam-HR 和 Fabrikam-Finance。若要删除 ABP 中的 Fabrikam-HR 地址列表，请指定您想要保留的 Fabrikam-Finance 地址列表。

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## 详细信息

有关语法和参数的详细信息，请参阅 [Set-AddressBookPolicy](https://technet.microsoft.com/zh-cn/library/hh529945\(v=exchg.150\))。

