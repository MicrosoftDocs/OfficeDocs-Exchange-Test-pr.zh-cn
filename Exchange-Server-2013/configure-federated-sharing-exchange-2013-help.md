---
title: '配置联合共享: Exchange 2013 Help'
TOCTitle: 配置联合共享
ms:assetid: b25ae450-def3-4797-a5fc-6e9bcee71a5d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657483(v=EXCHG.150)
ms:contentKeyID: 50491317
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置联合共享

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

通过 Exchange Server 2013 中的联合共享，用户可以与外部联盟组织中的收件人共享信息。这包括共享他们的忙/闲（也称为日历可用性）信息以便进行日程安排，或根据业务关系的性质，共享更详细的日历信息。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

> [!important]
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：1 小时。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：创建和配置联合身份验证信任

联合身份验证信任会在 Exchange 2013 组织和 Azure Active Directory 身份验证系统之间建立信任关系，它是联合共享所必需的。

有关详细说明，请参阅[配置联合身份验证信任](configure-a-federation-trust-exchange-2013-help.md)。

## 步骤 2：创建组织关系

组织关系使 Exchange 组织中的用户可以将日历忙/闲信息作为联合共享的一部分与其他联盟 Exchange 组织共享。可以在两个联盟 Exchange 2013 组织之间或在联盟 Exchange 2013 组织与联盟 Exchange 2010 组织之间配置联合共享。

有关详细说明，请参阅[创建组织关系](create-an-organization-relationship-exchange-2013-help.md)。

## 步骤 3：创建共享策略

共享策略允许与不同类型的外部用户进行用户建立的、人对人的日历信息共享。它们支持与具有 Internet 访问权限的外部联盟组织、外部非联盟组织和个人共享日历和联系人信息。如果不需要配置人对人共享或联系人共享（仅限组织级共享），则不需要配置共享策略。

有关详细说明，请参阅[创建共享策略](create-a-sharing-policy-exchange-2013-help.md)。

## 步骤 4：配置自动发现公用 DNS 记录

您需要将别名规范名称 (CNAME) 资源记录添加到您面向公众的 DNS。新 CNAME 记录应指向面向 Internet 并运行自动发现服务的 Exchange 2013 客户端访问服务器。

有关如何添加 CNAME 记录的详细说明，请参阅公用 DNS 记录的主机服务。通常这是基于 Internet 的服务，并且该服务还可以托管域网站。

