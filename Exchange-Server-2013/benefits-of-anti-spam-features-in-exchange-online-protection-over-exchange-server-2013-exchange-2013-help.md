---
title: 'Exchange Online Protection 中的反垃圾邮件功能的优点（相对于 Exchange Server 2013）: Exchange 2013 Help'
TOCTitle: Exchange Online Protection 中的反垃圾邮件功能的优点（相对于 Exchange Server 2013）
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 50489825
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Online Protection 中的反垃圾邮件功能的优点（相对于 Exchange Server 2013）

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-05-26_

下面介绍了与 Microsoft Exchange Server 2013（大多数的内置反垃圾邮件功能与 Microsoft Exchange Server 2010 相同）相比，在云（Microsoft Exchange Online 或 Microsoft Exchange Online Protection）中使用 Exchange 反垃圾邮件保护的好处：

  - **更多控制和更方便的配置**   管理员可以使用 Exchange 管理中心 (EAC) 基于 Web 的管理控制台来自定义垃圾邮件筛选设置，以便这些设置可最好地满足组织需求。Exchange Server 2013 中没有反垃圾邮件用户界面。Exchange Online 中包含了 EOP 反垃圾邮件保护功能

  - **更强大的连接筛选**   在 Exchange 2013 中，只有在外围网络中安装了边缘传输服务器的情况下，连接筛选 IP 允许列表和 IP 阻止列表才可用。有关详细信息，请参阅[边缘传输服务器](edge-transport-servers-exchange-2013-help.md)。在云中，可以选择跳过对从受信任发件人（从不同第三方来源收集）发送的电子邮件进行垃圾邮件筛选，从而确保不会将这些邮件错误地标记为垃圾邮件。托管筛选服务还使用 Microsoft 自己的阻止列表以及从供应商聚合的列表来提供更强大的 IP 级别筛选。

  - **更强大的内容筛选**   可以方便地配置内容筛选器策略以便：
    
      - 筛选以特定语言撰写的邮件。
    
      - 筛选从特定国家或地区发送的邮件。
    
      - 将批量电子邮件（如广告和市场营销电子邮件）标记为垃圾邮件。
    
      - 在邮件中搜索属性并在邮件与特定高级垃圾邮件选项属性匹配时对邮件执行操作。如果担心网络钓鱼，则其中一些选项可提供发件人 ID 和 SPF 技术组合来进行身份验证并验证邮件是否带有欺骗性质。
    
    除了可以在 EAC 中配置的以上内容筛选器选项之外，托管筛选服务还使用其他 URL 列表阻止在邮件正文中包含特定 URL 的可疑邮件。

  - **更快的更新**   垃圾邮件更新可在网络间更快地传播。在 Exchange Server 2013 中，每个月更新两次，而服务则是每小时更新多次。

  - **出站筛选**   如果您使用托管服务来发送出站邮件，那么出站垃圾邮件筛选总是被启用的，从而保护使用此服务的组织及其目标收件人。

