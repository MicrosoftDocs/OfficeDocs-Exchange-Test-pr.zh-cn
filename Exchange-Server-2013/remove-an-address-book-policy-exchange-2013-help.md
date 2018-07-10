---
title: '删除通讯簿策略: Exchange 2013 Help'
TOCTitle: 删除通讯簿策略
ms:assetid: c20c6f82-2f75-4116-9be1-c5af10113f71
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529946(v=EXCHG.150)
ms:contentKeyID: 50491459
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除通讯簿策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-03-25_

使用此过程可以删除通讯簿策略 (ABP)。

关于 ABP 的更多管理任务，请参阅[通讯簿策略程序](address-book-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“通讯簿策略”条目。

  - 如果 ABP 分配给用户的邮箱或软删除的邮箱，则无法将其删除。若要确定某个 ABP 是否分配给用户，请运行以下命令行管理程序命令：
    
    `Get-Mailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`
    
    若要确定 ABP 是否分配给了软删除的邮箱，请运行以下命令：
    
    `Get-Mailbox -SoftDeletedMailbox | Where $._AddressBookPolicy -eq <AddressBookPolicyName>`

  - 要从用户的邮箱中删除 ABP，可以使用邮箱属性的“邮箱功能”页，也可以使用 **Set-Mailbox** cmdlet。

  - 不能使用 Exchange 管理中心 (EAC) 来删除 ABP。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序删除 ABP

此示例将删除 ABP ABP\_TailspinToys。

    Remove-AddressBookPolicy -Identity "ABP_TailspinToys"

有关语法和参数的详细信息，请参阅 [Remove-AddressBookPolicy](https://technet.microsoft.com/zh-cn/library/hh529929\(v=exchg.150\))。

