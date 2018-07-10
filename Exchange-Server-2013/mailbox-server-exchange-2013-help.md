---
title: '邮箱服务器: Exchange 2013 Help'
TOCTitle: 邮箱服务器
ms:assetid: 1aacc1c9-c81b-47d4-b222-ee73956cf968
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150491(v=EXCHG.150)
ms:contentKeyID: 50490115
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮箱服务器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-19_

在 Microsoft Exchange Server 2010 中，邮箱服务器角色承载了邮箱数据库和公用文件夹数据库，并且还提供了电子邮件存储。而现在，在 Exchange Server 2013 中，邮箱服务器角色还包含了客户端访问协议、传输服务、邮箱数据库和统一消息组件。

在 Exchange 2013 中，邮箱服务器角色通过以下过程直接与 Active Directory、客户端访问服务器和 Microsoft Outlook 客户端进行交互：

  - 邮箱服务器使用 LDAP 从 Active Directory 中访问收件人、服务器和组织配置信息。

  - 客户端访问服务器将来自客户端的请求发送到邮箱服务器，并将邮箱服务器中的数据返回到客户端。客户端访问服务器还可通过 NetBIOS 文件共享访问邮箱服务器上的联机通讯簿 (OAB) 文件。客户端访问服务器在客户端和邮箱服务器之间发送邮件、忙/闲数据、客户端配置文件设置和 OAB 数据。

  - 在防火墙内部的 Outlook 客户端通过访问客户端访问服务器来发送和检索邮件。防火墙外部的 Outlook 客户端可通过使用 Outlook Anywhere（该工具使用 RPC over HTTP Proxy 组件）访问客户端访问服务器。

  - 可通过 RPC over HTTP 访问公用文件夹邮箱，而不管客户端是在防火墙外部还是内部。

  - 只有管理员的计算机才能从 Microsoft Exchange Active Directory 拓扑服务中检索 Active Directory 拓扑信息。它还检索电子邮件地址策略信息和地址列表信息。

  - 客户端访问服务器使用 LDAP 或名称服务提供程序接口（Name Service Provider Interface，NSPI）与 Active Directory 服务器通信以及检索用户的 Active Directory 信息。

**邮箱和客户端访问服务器的交互和体系结构**

![客户端访问和邮箱服务器交互](images/JJ150491.d14577bf-14f9-40fa-bd49-a92932eb003a(EXCHG.150).gif "客户端访问和邮箱服务器交互")

有关详细信息，请参阅 [Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)中的“Exchange 2013 体系结构”一节。

## 新邮箱功能

以下列表简要描述了 Exchange 2013 邮箱角色中的一些新增功能和一些改进功能：

  - Exchange 2010 数据库可用性组 (DAG) 的演变：
    
      - 事务日志代码已使用被动数据库副本上的深入检查点进行了重构，以实现快速故障转移。
    
      - 为了支持增强的站点恢复能力，服务器可以位于不同的位置。

  - Exchange 2013 目前承载部分客户端访问组件、传输组件和统一消息组件。

  - 已用托管代码重新编写 Exchange 存储，以便进一步削减 I/O 并提高可靠性。

  - 每个 Exchange 2013 数据库现在使用其自己的进程运行。

  - 智能搜索已替换 Exchange 2010 多邮箱搜索基础结构。

## 保护邮箱服务器的安全

默认情况下，邮箱服务器和其他 Exchange 服务器角色、域控制器和全局编录服务器之间的 HTTP、Microsoft Exchange ActiveSync、POP3 和 IMAP4 通信都进行了加密。此外，请确保邮箱服务器无法访问 Internet。

## 详细信息

[统一消息](unified-messaging-exchange-2013-help.md)

[邮件流](mail-flow-exchange-2013-help.md)

[高可用性和站点恢复](high-availability-and-site-resilience-exchange-2013-help.md)

[邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md)

[Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

[管理 Exchange 2013 中的邮箱数据库](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)

[邮件策略和遵从性](messaging-policy-and-compliance-exchange-2013-help.md)

[收件人](recipients-exchange-2013-help.md)

[协作](collaboration-exchange-2013-help.md)

