---
title: '删除脱机通讯簿: Exchange 2013 Help'
TOCTitle: 删除脱机通讯簿
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 50491636
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除脱机通讯簿

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

本主题说明如何删除脱机通讯簿 (OAB)。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“脱机通讯簿”条目。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

  - 删除链接到某个用户或某个邮箱数据库的 OAB 后，收件人将一直下载默认 OAB，直到您为该用户指派新的 OAB。如果删除默认 OAB，则必须将另一个 OAB 指派为默认 OAB。有关如何更改默认 OAB 的说明，请参阅[更改默认脱机通讯簿](change-the-default-offline-address-book-exchange-2013-help.md)。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序删除 OAB

此示例删除名为 My OAB 的 OAB。

    Remove-OfflineAddressBook -Identity "My OAB"

键入 **Y** 确认要删除该 OAB，然后按 Enter 键。

有关详细的语法和参数信息，请参阅[Remove-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/bb123594\(v=exchg.150\))。

