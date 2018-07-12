---
title: '设置进行脱机通讯簿下载的收件人: Exchange 2013 Help'
TOCTitle: 设置进行脱机通讯簿下载的收件人
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50489949
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置进行脱机通讯簿下载的收件人

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2013-02-15_

如果您的组织中使用多个脱机通讯簿 (OAB)，则可以通过若干方式指定哪些收件人下载哪些 OAB：

  - **按邮箱数据库**   可使用 EAC 或命令行管理程序，通过将邮箱数据库链接到 Office Outlook 2007、Outlook 2010 和 Outlook 2013 客户端的默认 OAB，针对 OAB 下载配置收件人。

  - **按收件人：** 通过将 OAB 直接链接到收件人的邮箱，可以在命令行管理程序中使用 **Set-Mailbox** cmdlet 指定下载哪个 OAB。

  - **按多个收件人：** 可以在命令行管理程序中使用管道命令基于公用属性指定多个收件人下载 OAB。

  - **按通讯簿策略：** 可以将通讯簿策略 (ABP) 分配给邮箱用户的帐户以指定将哪个 OAB 下载到收件人的邮箱。如果将 ABP 分配给已经分配有 OAB 的用户帐户，则将优先使用显式分配给邮箱的 OAB。有关详细信息，请参阅[将通讯簿策略分配给邮件用户](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 不能使用 Exchange 管理中心 (EAC) 执行这些过程。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序，可通过将邮箱数据库链接到公用文件夹数据库或默认 OAB 来针对 OAB 下载配置收件人

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“邮箱数据库”条目。

此示例为默认邮箱数据库设置 My OAB 的基于 Web 的分发。

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

有关语法和参数的详细信息，请参阅 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))。

## 使用命令行管理程序，通过将 OAB 直接链接到收件人的邮件指定下载哪个 OAB

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

若要通过将 OAB 直接链接到收件人的邮件来指定下载哪个 OAB，请使用下面的语法：

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>

> [!NOTE]  
> <em>Identity</em> 参数标识邮箱，并可以采用下列值：GUID、ADObjectID、可分辨名称 (DN)、<em>domain\account</em>、用户主要名称 (UPN)、LegacyExchangeDN、SMTP 地址和别名。


此示例指定用户 Kim 将下载 OAB My OAB。

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序指定多个收件人将下载的 OAB

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

此示例指定 Contoso 的所有美国用户邮箱将下载 OAB Contoso United States。

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

有关语法和参数的详细信息，请参阅 [Get-User](https://technet.microsoft.com/zh-cn/library/aa996896\(v=exchg.150\)) 和 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

