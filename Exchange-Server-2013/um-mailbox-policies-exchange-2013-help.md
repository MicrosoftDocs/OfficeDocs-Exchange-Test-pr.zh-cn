---
title: 'UM 邮箱策略: Exchange Online Help'
TOCTitle: UM 邮箱策略
ms:assetid: dfae629e-ee89-4494-a3ed-9655b67eb87e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124909(v=EXCHG.150)
ms:contentKeyID: 50556691
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 邮箱策略

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2012-11-15_

当您启用统一消息的用户时，统一邮件 (UM) 邮箱策略是必需的。创建 UM 邮箱策略应用于语音邮件用户邮箱集合的一组通用的策略或安全设置。UM 邮箱策略用于指定 UM 设置如下所示 ︰

  - PIN 策略

  - 拨号限制

  - 其他常规 UM 邮箱策略属性

例如，您可以创建 UM 邮箱策略通过减少特定组启用 UM 的用户，如主管人员的登录失败的最大数量增加的 pin 码的安全级别。

## UM 邮箱策略

您可以为统一消息启用用户之前，至少一个 UM 邮箱策略必须被创建。您可以创建其他的 UM 邮箱策略要应用一组公共的设置的用户组。

您可以通过使用 Exchange 管理外壳或 Exchange 管理中心 (EAC) 创建 UM 邮箱策略。默认情况下，每次创建 UM 拨号计划创建单个 UM 邮箱策略。新建 UM 邮箱策略将自动与该 UM 拨号计划，和拨号计划名称的一部分包括在显示名称的 UM 邮箱策略。您可以编辑此默认 UM 邮箱策略。

可以将多个启用 UM 的用户链接到一个 UM 邮箱策略。但是，对于每个已启用 UM 的用户的邮箱必须链接到单个 UM 邮箱策略。这使您可以控制针安全性设置，例如最小小数位数的 PIN 或与该 UM 邮箱策略相关联的已启用 UM 的用户的登录尝试的最大数目。您还可以控制邮件文本设置或拨号限制相同的启用 UM 的邮箱。

