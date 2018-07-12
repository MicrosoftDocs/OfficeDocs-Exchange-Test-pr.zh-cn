---
title: '通过使用收件人筛选器创建电子邮件地址策略: Exchange 2013 Help'
TOCTitle: 通过使用收件人筛选器创建电子邮件地址策略
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50491831
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通过使用收件人筛选器创建电子邮件地址策略

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-16_

您可借助命令行管理程序使用收件人筛选器来创建电子邮件地址策略。 有关电子邮件地址策略的详细信息，请参阅[电子邮件地址策略](email-address-policies-exchange-2013-help.md)。

有关电子邮件地址策略的其他管理任务，请参阅 [电子邮件地址策略程序](email-address-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 要使用 *RecipientFilter* 参数创建一个自定义筛选器，必须为该筛选器指定一个字符串。 命令行管理程序将 OPath 用于筛选语法。 OPath 是一种为查询对象数据源而设计的查询语言。
    
    > [!IMPORTANT]  
    > 如果使用收件人筛选器创建或编辑电子邮件地址策略，则不能使用 Exchange 管理中心 (EAC) 编辑电子邮件地址策略。必须使用命令行管理程序。 有关语法和参数的详细信息，请参阅 <a href="https://technet.microsoft.com/zh-cn/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</a>。


  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿](email-addresses-and-address-books-exchange-2013-help.md)主题中的“电子邮件地址策略”条目。

  - 必须先配置接受域，然后才能在电子邮件地址策略中使用 SMTP 地址域。有关详细信息，请参阅[接受域](accepted-domains-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!WARNING]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序通过收件人筛选器创建电子邮件地址策略

要通过收件人筛选器创建电子邮件地址策略，可使用以下语法。

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

该示例创建应用于所有高级管理人员的电子邮件地址策略，并且其电子邮件地址的本地部分由他们名字的前两个字母和整个姓氏组成。

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

有关语法和参数的详细信息，请参阅 [New-EmailAddressPolicy](https://technet.microsoft.com/zh-cn/library/aa996800\(v=exchg.150\))。

