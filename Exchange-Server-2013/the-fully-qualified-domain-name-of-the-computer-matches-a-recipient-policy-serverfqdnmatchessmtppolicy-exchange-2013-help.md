---
title: '计算机的完全限定域名匹配的收件人 policy_ServerFQDNMatchesSMTPPolicy: Exchange 2013 Help'
TOCTitle: 计算机的完全限定域名匹配的收件人 policy_ServerFQDNMatchesSMTPPolicy
ms:assetid: f3ea61f8-1788-4cbf-814e-f7c088c1ac47
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.serverfqdnmatchessmtppolicy(v=EXCHG.150)
ms:contentKeyID: 50491983
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 计算机的完全限定域名匹配的收件人 policy\_ServerFQDNMatchesSMTPPolicy

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为本地计算机的完全限定域名 (FQDN) 与收件人策略的简单邮件传输协议 (SMTP) 地址相匹配，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Microsoft Exchange 安装程序要求 Exchange 组织中服务器的 FQDN 不能与同一 Exchange 组织中收件人策略的任何 SMTP 地址相匹配。

如果计算机的 FQDN 与收件人策略的 SMTP 地址相匹配，则会导致邮件无法通过 SMTP 并滞留在 MTA 队列中。

要解决此问题，请重命名本地计算机，或者删除或重命名收件人策略，然后重新运行 Microsoft Exchange 安装程序。

重命名本地计算机

1.  打开\&quot;控制面板\&quot;中的\&quot;系统\&quot;。

2.  在\&quot;计算机名\&quot;选项卡上，单击\&quot;更改\&quot;。

3.  在**计算机名**键入一个新名称的计算机，然后单击**确定**。系统将提示您提供用户名和用户密码才能重命名域中的计算机。

4.  单击**确定**以关闭**系统属性**对话框。系统将提示您重新启动计算机以应用所做的更改。

> [!important]
> 如果要重命名的计算机是域控制器，请参阅&quot;重命名域控制器&quot;(<a href="https://go.microsoft.com/fwlink/?linkid=66828">https://go.microsoft.com/fwlink/?LinkId=66828</a>)。


修改收件人策略的 SMTP 地址

1.  启动 Exchange 系统管理器。

2.  单击\&quot;组织\&quot;，再单击\&quot;收件人\&quot;，然后单击\&quot;收件人策略\&quot;。

3.  双击要更改的策略。

4.  单击\&quot;电子邮件地址\&quot;选项卡，然后更改相应的 SMTP 地址。

有关收件人策略命名问题的详细信息，请参阅 Microsoft 知识库文章 288175，"XCON︰ 收件人策略不能与任何组织，5.4.8 中的服务器的 FQDN 匹配的 Ndr"([http://go.microsoft.com/fwlink/?linkid=3052\&kbid=288175](http://go.microsoft.com/fwlink/?linkid=3052&kbid=288175))。

