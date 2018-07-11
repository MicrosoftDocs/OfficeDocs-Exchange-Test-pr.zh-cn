---
title: '针对组织关系管理邮件提示: Exchange Online Help'
TOCTitle: 针对组织关系管理邮件提示
ms:assetid: 6e6b48ef-c41c-47ad-8063-66901765c2a5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ649324(v=EXCHG.150)
ms:contentKeyID: 50490796
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 针对组织关系管理邮件提示

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

可以使用 Exchange 命令行管理程序在各种组织之间配置邮件提示的自定义设置。

通过建立组织关系，您可以共享忙/闲数据、配置安全邮件流并启用邮件跟踪，从而增强两个组织的用户体验。有关组织关系的详细信息，请参阅[有关组织关系的邮件提示](mailtips-over-organization-relationships-exchange-2013-help.md)。

可以使用各种设置控制在建立了组织关系的两个组织之间如何使用邮件提示。本节中的步骤说明了这些不同控制。在所有示例中，内部部署组织为 contoso.com，远程组织为 online.contoso.com，而组织关系名为 Contoso Online。

使用 **Set-OrganizationRelationship** cmdlet 可配置这些设置。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;邮件提示\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用两个组织之间的邮件提示

此示例配置组织关系，以便在撰写发往您组织中的收件人的邮件时，向远程组织中的发件人返回邮件提示。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $true

此示例配置组织关系，以便在撰写发往您组织中的收件人的邮件时，阻止向远程组织中的发件人返回邮件提示。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessEnabled $false

有关语法和参数的详细信息，请参阅 [Set-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332326\(v=exchg.150\))。

## 使用命令行管理程序配置向远程组织返回哪些邮件提示

对于每个组织关系，您都可以确定向另一个组织中的发件人返回哪组邮件提示。此示例配置组织关系，以便返回所有邮件提示。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel All

此示例配置组织关系，以便仅返回自动答复、超大邮件、受限制收件人以及邮箱已满邮件提示。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel Limited

此示例配置组织关系，以便不返回任何邮件提示。

> [!NOTE]  
> 请勿使用此方法禁用此关系的邮件提示。若要禁用邮件提示，请将 <em>MailTipsAccessEnabled</em> 参数设置为 <code>$false</code>。


    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessLevel None

有关语法和参数的详细信息，请参阅 [Set-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332326\(v=exchg.150\))。

## 使用命令行管理程序配置为其返回特定于收件人的邮件提示的一组特定用户

可以限制向一组特定用户返回特定于收件人的邮件提示。默认情况下，在为组织关系启用邮件提示时，会为所有用户返回以下特定于收件人的邮件提示：

  - 自动答复

  - 邮箱已满

  - 自定义邮箱提示

您可以在组织关系上指定邮件提示访问组。在指定了某个组后，仅为作为该组成员的邮箱、邮件联系人和邮件用户返回特定于收件人的邮件提示。此示例配置组织关系，以便仅为 ShareMailTips@contoso.com 组的成员返回特定于收件人的邮件提示。

    Set-OrganizationRelationship "Contoso Online" -MailTipsAccessScope ShareMailTips@contoso.com

有关语法和参数的详细信息，请参阅 [Set-OrganizationRelationship](https://technet.microsoft.com/zh-cn/library/ee332326\(v=exchg.150\))。

