---
title: '将地址列表添加至脱机通讯簿或从脱机通讯簿删除地址列表: Exchange 2013 Help'
TOCTitle: 将地址列表添加至脱机通讯簿或从脱机通讯簿删除地址列表
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 50491114
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将地址列表添加至脱机通讯簿或从脱机通讯簿删除地址列表

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

可以使用命令行管理程序向脱机通讯簿 (OAB) 中添加或从中删除地址列表。默认情况下，存在一个名为“默认脱机通讯簿”的 OAB，它包含全局地址列表 (GAL)。OAB 的生成基于 OAB 所包含的地址列表。若要创建用户可以下载的自定义 OAB，您可以向 OAB 中添加或从中删除地址列表。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“脱机通讯簿”条目。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

  - 在生成驻留地址列表的 OAB 后，对地址列表所作的更改才可供客户下载。有关详细信息，请参阅[更新脱机通讯簿](update-an-offline-address-book-exchange-2013-help.md)。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序将地址列表添加到 OAB

使用 *AddressLists* 参数时，将覆盖目前存在的所有地址列表。如果要继续生成 OAB 中的那些地址列表，则在使用 *AddressLists* 参数时，必须包含现有地址列表。本示例中，具有 AddressList1 和 AddressList2，要添加 AddressList3。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

有关语法和参数的详细信息，请参阅 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/aa996330\(v=exchg.150\))。

## 使用命令行管理程序从 OAB 中删除地址列表

要从 OAB 中删除地址列表，只需从地址列表的列表中忽略该地址列表即可。本示例中，具有 AddressList1、AddressList2 和 AddressList3，要删除 AddressList3。

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

有关语法和参数的详细信息，请参阅 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/aa996330\(v=exchg.150\))。

