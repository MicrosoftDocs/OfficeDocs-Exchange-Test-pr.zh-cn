---
title: '删除地址列表: Exchange 2013 Help'
TOCTitle: 删除地址列表
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 50490329
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除地址列表

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-14_

本主题介绍如何删除地址列表。您不能删除默认的全局地址列表 (GAL)。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“地址列表”条目。

  - 无法删除包含子地址列表的父地址列表。但是，可以通过按键盘上的 CTRL 键并选择父地址列表和子地址列表，来同时删除子地址列表和父地址列表。如果试图在未删除子地址列表的情况下删除父地址列表，则会收到一条错误消息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 删除地址列表

1.  导航到“组织”\>“地址列表”。

2.  在列表视图中，选择要删除的地址列表，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在警告框中，单击“是”删除地址列表。

## 使用命令行管理程序删除地址列表

本示例删除地址列表“Sales Department”，它不包含子地址列表。

    Remove-AddressList -Identity "Sales Department"

键入 **Y** 确认要删除该地址列表，然后按 Enter 键。

有关语法和参数的详细信息，请参阅 [Remove-AddressList](https://technet.microsoft.com/zh-cn/library/bb124342\(v=exchg.150\))。

## 使用命令行管理程序删除包含子地址列表的地址列表

本示例将删除父地址列表 Departments 及其全部子地址列表。

    Remove-AddressList -Identity Departments -Recursive

键入 **Y** 确认要删除该父地址列表及其子地址列表，然后按 Enter 键。

有关语法和参数的详细信息，请参阅 [Remove-AddressList](https://technet.microsoft.com/zh-cn/library/bb124342\(v=exchg.150\))。

