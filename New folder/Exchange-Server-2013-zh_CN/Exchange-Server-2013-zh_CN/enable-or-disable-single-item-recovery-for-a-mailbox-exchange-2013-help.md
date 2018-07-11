---
title: '启用或禁用邮箱的单个项目恢复: Exchange 2013 Help'
TOCTitle: 启用或禁用邮箱的单个项目恢复
ms:assetid: 2e7f1bcd-8395-45ad-86ce-22868bd46af0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633460(v=EXCHG.150)
ms:contentKeyID: 54652238
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 启用或禁用邮箱的单个项目恢复

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-03-13_

您可以使用命令行管理程序在邮箱上启用或禁用单个项目恢复。在 Exchange Online 中，在您新建邮箱时，系统会默认启用单个项目恢复。在 Exchange 2013 中，在您创建邮箱时，系统会禁用单个项目恢复。如果单个项目恢复已启用，则用户永久删除（清除）的邮件就会在已删除项目的保留期过期之前，保留在邮箱的“可恢复的项目”文件夹中。这样，管理员便可以在已删除项目的保留期过期之前，恢复用户清除的邮件。此外，如果单个项目恢复已启用，那么当用户或进程更改邮件时，原始项目的副本也会予以保留。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md) 主题中的“保留和合法保留”条目。

  - 您不能使用 Exchange 管理中心 (EAC) 启用或禁用单个项目恢复。

  - 在 Exchange Online 中，默认情况下，已删除项目保留期限设置为 14 天。您可以更改这项设置，天数最多为 30 天。有关详细信息，请参阅[更改为 Exchange Online 邮箱保留永久删除的项目的时间](https://technet.microsoft.com/zh-cn/library/dn163584\(v=exchg.150\))。

  - 在 Exchange 2013 中，邮箱默认使用邮箱数据库的已删除项目的保留设置。邮箱数据库的已删除项目保留期限设置为 14 天，但是您可以通过配置每个邮箱的设置覆盖默认设置。有关详细信息，请参阅[配置已删除邮件的保留时间和可恢复邮件配额](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。.

## 使用命令行管理程序启用单个项目恢复

这个示例对 April Summers 邮箱启用了单个项目恢复。

    Set-Mailbox -Identity "April Summers" -SingleItemRecoveryEnabled $true

这个示例对 Pilar Pinilla 邮箱启用了单个项目恢复并设置已删除项目保留的天数为 30 天。

    Set-Mailbox -Identity "Pilar Pinilla" -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

这个示例对组织内所有用户邮箱都启用了单个项目恢复。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true

此示例为组织中的所有用户邮箱都启用了单个项目恢复，并且将已删除项目的保留天数设置为 30 天。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -SingleItemRecoveryEnabled $true -RetainDeletedItemsFor 30

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 使用命令行管理程序禁用单个项目恢复

您可能需要禁用用户邮箱的单个项目恢复。例如，在您可以使用 **Search-Mailbox –DeleteContent** 来永久删除邮箱的内容之前，必须禁用单个项目恢复。有关详细信息，请参阅[搜索和删除邮件 - 管理员帮助](search-for-and-delete-messages-admin-help-exchange-2013-help.md)。

本示例禁用了 Ayla Kol 的邮箱的单个项目恢复。

    Set-Mailbox -Identity "Ayla Kol" -SingleItemRecoveryEnabled $false

## 您如何知道操作成功？

要验证您是否已对邮箱启用了单个项目恢复并显示已删除项目会保留的时间值（按天数计算），请运行以下命令。

    Get-Mailbox <Name> | FL SingleItemRecoveryEnabled,RetainDeletedItemsFor

您可以使用相同的命令来验证邮箱是否禁用了单个项目恢复。

## 详细信息

  - 有关单个项目恢复的详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。若要在已删除项目的保留期过期之前恢复用户清除的邮件，请参阅[恢复用户邮箱中的已删除邮件](recover-deleted-messages-in-a-user-s-mailbox-exchange-2013-help.md).

  - 如果您将邮箱置于就地保留或诉讼保留状态，则“可恢复的项目”文件夹中的邮件会一直保留到保留期过期。如果为无限期的保留期，则这些项目会一直保留到您删除保留设置或更改保留期。

