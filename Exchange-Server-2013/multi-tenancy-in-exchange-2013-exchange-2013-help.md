---
title: 'Exchange 2013 中的多租户: Exchange 2013 Help'
TOCTitle: Exchange 2013 中的多租户
ms:assetid: df09257d-dd98-4f59-b830-1818cedda15c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ862352(v=EXCHG.150)
ms:contentKeyID: 50556681
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 中的多租户

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

多租户（托管）Exchange 2013 部署是这样定义的：在这种部署中，Exchange 组织配置为承载多个离散组织或业务单位（租户），这些租户通常不共享电子邮件、数据、用户、全局地址列表 (GAL) 或其他常用的 Exchange 对象。通过这种硬件、软件和资源的共享（同时完全保持租户之间的逻辑分隔），组织可以利用标准 Exchange 部署的简单性，同时还能提供多租户功能和服务以满足其托管需求。

## Exchange 2013 组织中的多租户

在 Exchange 2013 中，我们继续使用类似于 Exchange 2010 Service Pack 2 (SP2) 中所用方法的标准本地 Exchange 安装支持托管。我们不再提供 `/hosting` 模式开关，而是强调结合使用通讯簿策略 (ABP) 以及认可的独立软件供应商 (ISV) 提供的托管管理解决方案和自动化工具。这些解决方案基于 Microsoft 认可的配置指导和做法的框架，可为 Exchange 组织提供更加简单、更加强大的方式来提供托管服务和功能。

Exchange 2013 通过利用下列主要组件和功能支持多租户：

  - **Active Directory**   多租户 Exchange 组织中的每个业务单位不再具有独立的 *ExchangeOrganization* Active Directory 容器，而使用单个 *ExchangeOrganization* Active Directory 容器支持 Exchange 2013 多租户。这样可以简化 Active Directory 结构，降低出现 Active Directory 相关权限问题的可能性。
    
    有关 Exchange 2013 中 Active Directory 更改的详细信息，请参阅[Active Directory](active-directory-exchange-2013-help.md)。

  - **通讯簿策略 (ABP)**   在 Exchange 2010 SP2 中引入的 ABP 在 Exchange 2013 中用于控制用户对 Exchange 组织中的地址列表、全局地址列表 (GAL) 和脱机通讯簿 (OAB) 的访问。ABP 将这些不同的 Active Directory 对象分组为可分配给个别用户的单个虚拟对象，以便按多租户组织结构创建这些资源的逻辑分组。Exchange 2013 中的 ABP 功能类似于其在 Exchange 2010 SP2 中的功能。
    
    有关 Exchange 2013 中 ABP 的详细信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。

  - **托管管理解决方案**   有些使用 Exchange 2013 提供托管 Exchange 解决方案的管理员将从使用自定义托管管理方法中受益。由于 Exchange 管理中心 (EAC) 的一些限制，Microsoft 与第三方供应商合作，帮助他们开发符合托管的 Exchange 2013 组织的指导原则和批准的框架的控制面板和自动化解决方案。我们建议配置托管 Exchange 解决方案的组织在需要的情况下，利用这些工具管理其托管组织。
    
    有关托管管理解决方案（包括经过验证的解决方案供应商）的详细信息，请参阅 [Exchange Server 2013 托管和多租户解决方案和指导](https://go.microsoft.com/fwlink/?linkid=275036)

