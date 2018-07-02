---
title: '创建通讯簿策略: Exchange Online Help'
TOCTitle: 创建通讯簿策略
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 50490711
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建通讯簿策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-12-16_

通过通讯簿策略 (ABP)，可以将用户分入特定的组，从而生成组织全局地址列表 (GAL) 的自定义视图。创建 ABP 时，可以为策略分配 GAL、脱机通讯簿 (OAB)、会议室列表以及一个或多个地址列表。然后，可以将 ABP 分配给邮箱用户，向他们提供对 Outlook 和 Outlook Web App 中自定义 GAL 的访问权限。目标是简化机制，为需要多个 GAL 的本地组织实现 GAL 分段。有关 ABP 的详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。

关于 ABP 的更多管理任务，请参阅[通讯簿策略程序](address-book-policy-procedures-exchange-2013-help.md)。

对使用此过程的应用场景感兴趣吗？请参阅[方案：部署通讯簿策略](scenario-deploying-address-book-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的\&quot;通讯簿策略\&quot;条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的\&quot;向角色组添加角色\&quot;部分。

  - 为组织创建 ABP 是一个需要包含规划的多步骤流程。有关详细信息，请参阅[方案：部署通讯簿策略](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - 不能使用 Exchange 管理中心 (EAC) 创建 ABP。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

  - 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

## 使用命令行管理程序创建 ABP

此示例将创建具有下列设置的 ABP：

  - **名称：**All Fabrikam ABP

  - **GAL：**All Fabrikam

  - **OAB：**Fabrikam-All-OAB

  - **会议室列表：**All Fabrikam Rooms

  - **地址列表：**All Fabrikam、All Fabrikam Mailboxes、All Fabrikam DLs 和 All Fabrikam Contacts

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

有关语法和参数的详细信息，请参阅[New-AddressBookPolicy](https://technet.microsoft.com/zh-cn/library/hh529913\(v=exchg.150\))。

## 有关详细信息，请参阅以下内容：

[将通讯簿策略分配给邮件用户](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

