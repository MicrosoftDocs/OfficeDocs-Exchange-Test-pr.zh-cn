---
title: '组的指标和邮件提醒: Exchange 2013 Help'
TOCTitle: 组的指标和邮件提醒
ms:assetid: 74a55072-4ba9-45bb-a18f-41afbf3de30b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ674302(v=EXCHG.150)
ms:contentKeyID: 50490847
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 组的指标和邮件提醒

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-16_

组指标是有关组织中通讯组和动态通讯组的以下数据的集合：

  - 成员数目

  - 组织外部的成员数目

度量值组数据用于在 Microsoft Exchange Server 2013支持邮件提醒。邮件提醒是提示性消息时他们正在撰写的邮件给发件人显示。有关邮件提醒，包括邮件提醒中Exchange 2013，可用的完整列表的详细信息，请参阅[MailTips](https://technet.microsoft.com/zh-cn/library/jj649091(v=exchg.150))。

组指标数据由以下邮件提示使用：

  - **许多观众**  发件人添加通讯组的成员计数被认为大部分人为在组织中配置时，将显示此 MailTip。默认情况下，任何邮件发往 25 个以上的收件人被视为众多观众。

  - **外部收件人**：当发件人添加的通讯组中包括组织外部的成员时，将会显示此邮件提示。

每次发件人对邮件添加一位收件人，邮件提醒进行评估。若要提供此信息， Exchange作为后台进程运行在您的组织的正常工作时间之外可以安排，计算分组度量数据。在评估时收件人的邮件提醒， Exchange读取组度量数据。

## 组指标生成

在Exchange 2013，组度量数据存储在 Active Directory 中的组对象的**msExchGroupMemberCount**和**msExchGroupExternalMemberCount**属性。还有与组指标 %exchangeinstallpath%GroupMetrics 文件夹中的下列文件 ︰

  - **Cookie\_*\<nnnnnnnn\>*.dsc**  此文本文件包含配置为生成组度量数据和上一次的成功组指标生成时间邮箱服务器的信息。这样，生成数据自上次组指标生成以来已更改的组的组标准。

  - **ChangedGroups.txt**   此文件包含上次生成组指标数据时所更新的组列表。

由仲裁邮箱，也称为组织邮箱处理组测量数据生成。当仲裁邮箱上的*GMGen*参数设置为`$true`时，仲裁邮箱负责生成组度量数据。

邮箱服务器生成完整组度量数据的所有通讯组并动态通讯组的首次运行时组指标邮箱助理，以及自上次完整生成以来已修改任何组的增量更新。默认情况下，每日一次随机当 Exchange 服务器工作负荷较轻时生成组度量数据。如果工作负荷不断高，组指标生成可能会被跳过。

要配置组指标生成，请参阅[配置组指标](configure-group-metrics-exchange-2013-help.md)。

