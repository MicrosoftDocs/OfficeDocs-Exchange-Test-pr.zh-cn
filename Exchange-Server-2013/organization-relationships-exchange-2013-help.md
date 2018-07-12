---
title: '组织关系: Exchange 2013 Help'
TOCTitle: 组织关系
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 50490488
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 组织关系

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-02-20_

设置组织关系以便与外部商业合作伙伴共享日历信息。Exchange 管理员可以设置与 Office 365 组织或其他 Exchange 本地组织之间的组织关系。如果想要与其他本地 Exchange 组织共享日历，双方的本地 Exchange 管理员都必须设置与云的身份验证关系（也称为“联合身份验证”），并且必须满足最低软件要求。

组织关系是企业之间的一对一关系，可允许每个组织中的用户查看日历可用性信息。设置组织关系时，您将设置您这一端的关系部分，并指定外部组织中的用户可以查看到的信息级别。外部组织可以在其一端设置相同或不同的设置。例如，当 Contoso 创建了与 Tailspin Toys 的组织关系后，如果 Tailspin Toys 的用户想要安排与 Contoso 用户的会议，那么可以通过将其电子邮件地址添加到会议邀请来实现。受邀请的 Contoso 用户是否能够参加会议将对 Tailspin Toys 用户显示。但是，在 Contoso 也可以查看 Tailspin Toys 用户是否能够参加会议之前，其管理员需要设置与 Contoso 的组织关系。

您可以指定三种访问级别：

  - 无访问权限

  - 仅访问可用性（闲/忙）时间

  - 访问闲/忙信息，包含时间、主题和位置

> [!NOTE]  
> 如果用户不希望与其他用户共享其闲/忙信息，可更改 Outlook 中的“默认”权限条目。为此，用户可转到“日历属性”&gt;“权限”选项卡，选择“默认”权限，然后从“权限级别”列表中选择“无”。闲/忙信息对内部或外部用户不可见，即使存在组织关系也是如此。将应用用户设置的权限。


以下主题将帮助您配置并管理作为您组织共享一部分的组织关系：

[创建组织关系](create-an-organization-relationship-exchange-2013-help.md)

[修改组织关系](modify-an-organization-relationship-exchange-2013-help.md)

[删除组织关系](remove-an-organization-relationship-exchange-2013-help.md)

要查找有关联合共享的详细信息吗？请参阅[共享](sharing-exchange-2013-help.md)。

