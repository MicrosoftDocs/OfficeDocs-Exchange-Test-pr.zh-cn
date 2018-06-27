---
title: '管理员的送达报告: Exchange 2013 Help'
TOCTitle: 管理员的送达报告
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51408280
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理员的送达报告

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

使用管理员的送达报告，可以对你组织中任何特定邮箱所收发邮件的送达信息进行跟踪。具体来说，管理员的送达报告使用 Exchange 管理中心 (EAC) 执行邮件跟踪日志的目标搜索。该搜索始终仅限于特定的邮箱。用户可以搜索邮箱发出的邮件，或发送至邮箱的邮件，并且可以通过邮件主题筛选搜索结果。

邮件正文的内容不会在送达报告中返回，但是主题行会显示在结果中。如果想要根据邮件内容在组织中的邮箱内搜索特定电子邮件，请参阅[就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)。

在下列情况下，您可能会发现送达报告搜索非常有用：

  - 由于学员没有按时提交作业，管理者对该学员给出了较差的评论。该学员坚持说他发送了带有作业附件的邮件。管理者请您验证该邮件的状态。

  - 已向用户发送安全公告来请求他们立即答复，但他们尚未答复。是他们未理睬邮件还是他们根本没有收到邮件？

  - 用户报怨他们发送的邮件无法送达收件人。他们检查邮件的送达状态，但是却无法弄清楚具体的情况。这可能是因为在组织级别对邮件应用了某条规则。

创建送达报告搜索之后，生成的送达报告将显示以下信息：邮件的发件人和收件人、主题行以及邮件的发送时间。送达报告还会显示邮件送达状态以及送达延迟或失败的原因。

## 关于送达报告的更多信息

  - 以下部分介绍了如何创建新的送达报告：[使用送达报告跟踪邮件](track-messages-with-delivery-reports-exchange-2013-help.md).

  - 内部部署 Exchange 组织可以使用 Exchange 命令行管理程序直接查询邮件跟踪日志。有关详细信息，请参阅[搜索邮件跟踪日志](search-message-tracking-logs-exchange-2013-help.md)。

  - 用户可以跟踪他们的邮件。有关详细信息，请参阅[用户的送达报告](https://go.microsoft.com/fwlink/?linkid=279920)。

  - 如果组织包括 Exchange 的以前版本，需要考虑送达报告功能如何通过各个 Exchange 版本在 Exchange 2013 中发挥作用。
    
      - Exchange 2013 送达报告可以在同一个 Active Directory 站点中跨 Exchange 2010 服务器跟踪邮件。
    
      - Exchange 2013 送达报告无法在同一个 Active Directory 站点中跨 Exchange 2007 服务器跟踪邮件。送达报告功能使用 Exchange 2007 中不存在的远程过程调用和 Web 服务界面。

