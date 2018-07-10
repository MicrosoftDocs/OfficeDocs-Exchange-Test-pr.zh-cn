---
title: '更新脱机通讯簿: Exchange 2013 Help'
TOCTitle: 更新脱机通讯簿
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 50490398
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更新脱机通讯簿

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-11-15_

创建 OAB 或修改 OAB 设置后，用户在 OAB 生成 (OABGen) 过程完成后才能得到这些更改。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅“脱机通讯簿”条目。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序更新 OAB

此示例将更新名为 My OAB 的 OAB。

    Update-OfflineAddressBook -Identity "My OAB"

有关语法和参数的详细信息，请参阅 [Update-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/aa995979\(v=exchg.150\))。

