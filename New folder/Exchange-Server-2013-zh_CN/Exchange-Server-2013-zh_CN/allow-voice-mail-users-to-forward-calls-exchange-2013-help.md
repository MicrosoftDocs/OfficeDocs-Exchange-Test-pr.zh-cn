﻿---
title: '允许语音邮件用户转接来电: Exchange Online Help'
TOCTitle: 允许语音邮件用户转接来电
ms:assetid: 1f8e0a53-3d9d-4f8c-9be3-9f1e2a4347a3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335138(v=EXCHG.150)
ms:contentKeyID: 50556539
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 允许语音邮件用户转接来电

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-22_

呼叫应答规则功能首先是在Exchange 2010中引入的。启用语音邮件的用户使用此功能，可以控制应如何处理他们的来电。呼叫应答规则应用于传入的调用方式类似于收件箱规则应用于传入的电子邮件。

创建和配置使用Outlook或Outlook Web App的声音已启用邮件的用户呼叫应答规则。将规则以及其他语音设置在用户的邮箱存储。可以为每个已启用 UM 的邮箱设置总共九个呼叫应答规则。这些规则是独立设置的用户，并不会占据用户的收件箱规则存储空间配额的一部分的收件箱规则。

默认情况下，当为用户启用统一邮件 (UM) 和语音邮件，没有电话应答规则配置。如果通过语音邮件系统应答传入的呼叫，将提示呼叫者留下语音信息，或者如果调用方不会得到提示，请调用方还可以留下语音邮件用户。

如果您的用户希望有只回答他们来电并记录留言的语音邮件系统，您不必创建任何呼叫应答规则。但是，如果您决定您想要设置条件或操作，您可以设置它们通过使用Outlook Web App中的**语音邮件**页上的**呼叫应答规则**部分。使用**调用应答规则**部分中创建、 编辑和删除呼叫应答规则。

## 呼叫应答规则的结构

呼叫应答规则由两部分组成 ︰ 条件和操作。您可以将一个或更多的条件，与单个呼叫应答规则。规则的所有条件都满足时，将只处理呼叫应答规则。您还可以关联一个或多个操作与一个呼叫应答规则。这些操作确定哪些选项将处理该呼叫应答规则时提供给调用方。

呼叫应答规则支持以下条件：

  - 传入呼叫的呼叫者

  - 一天中的时间

  - 日历忙/闲状态

  - 电子邮件的自动答复是否处于打开状态

支持下列操作：

  - 联系方式

  - 将呼叫者转移到其他人

  - 留下语音邮件

如果用户记录呼叫应答规则自定义问候语，它们必须包括菜单选项为自定义的问候，他们配置的呼叫应答规则的一部分。如果他们不这样做，统一消息将不会产生使调用方知道他或她选择的是菜单提示。播放自定义问候语之后，服务器将等待呼叫者的输入。如果菜单选项不包含在问候语中，调用方不输入任何内容，服务器将会提示他们，询问"还在那里吗？"

## 条件

条件是可用于呼叫应答规则的规则。通过使用条件的组合，您可以创建多个呼叫应答在满足条件时将触发的规则。若要创建将应用于每个呼叫的默认规则，您可以创建不包含任何条件的规则。

设置呼叫应答规则时，可以使用的条件有三个，其中包括：

  - 呼叫者 ID

  - 一天中的时间

  - 忙/闲状态

## 操作

操作用于定义要满足某个条件时，会发生什么。有两种类型的操作 ︰

  - 联系方式

  - 呼叫转移

**添加一个\&quot;联系我\&quot;操作**

当呼叫者选择\&quot;联系我\&quot;时，语音邮件系统将尝试通过最多两个不同的电话号码联系您，如果通过其中一个电话号码联系到您，则会将呼叫者连接到您。

  - 您可以指定将向调用方读取的文本。例如，如果您输入"紧急问题"要通知调用方，他们应该有重要的事情要与您一起讨论地仅选择此操作时，语音邮件系统会说"对于紧急问题，请按 1 键。

  - 必须要找到我的操作与调用方将按选择此操作电话键盘上的数字。在上面的示例中， **1**电话键是数字的调用方将按到达您的电话号码或您指定的数字之一。

  - 接下来，您需要指定拨号语音邮件系统的一个或两个电话号码。如果指定两个电话号码，如果你不在第一个可用，将只拨打第二个数字。每个指定的电话号码都有相关联的持续时间。持续时间是其间的语音邮件系统将尝试拨打的电话号码，它将在移动到下一个数字之前的时间段。或者，如果不能与您联系，语音邮件系统将返回到选项菜单。

  - 在输入此信息之后，请单击\&quot;应用\&quot;保存\&quot;联系我\&quot;设置。

**添加呼叫转移操作**

通过设置呼叫转移的操作，则将向调用方提供转移到另一个人的电话号码的选项。有几个选项，当您想要转移到另一个电话或联系人的传入呼叫时才可用。

  - 您可以指定将向调用方读取的文本。例如，您可以输入"重要问题"要通知调用方，他们应该选择此选项，如果他们有重要的问题进行讨论，并需要与人沟通。

  - 必须将\&quot;呼叫转移\&quot;操作与电话键盘上的数字关联，以便呼叫者按该键来选择此操作。

  - 当您选择呼叫转移操作时，您必须指定调用方要转移到的人或电话号码。可以选择一个电话号码，也可以选择一个联系人以调用方在电话键盘上按正确的注册表项时调用。如果您指定联系人在公司目录中，语音邮件系统会尝试将呼叫转给该联系人的分机号码。

  - 除了指定要将呼叫者转移到的人或电话号码外，还需要在电话键盘上指定一个数字，以便呼叫者按该数字键来选择\&quot;呼叫转移\&quot;操作。

  - 在输入此信息之后，请单击\&quot;应用\&quot;保存\&quot;呼叫转移\&quot;设置。

## 为每个传入呼叫选择呼叫应答规则

创建和配置呼叫应答规则之后，统一消息将：

1.  确定用户是否已创建任何呼叫应答规则。如果不是，UM 将提供调用方保留语音邮件选项。

2.  如果已配置了一个或多个呼叫应答规则，UM 将评估每个规则。将处理的第一个规则，在满足其条件。

3.  评估完所有的规则之后，如果 UM 未找到满足条件的规则，UM 将请呼叫者留下语音邮件。

## 拨号规则

根据呼叫应答规则的配置方式，拨入的呼叫可能会呼叫转移。这种情况下，转移的目标电话号码将拨号规则和被调用的方与之关联的 UM 邮箱策略的限制。有关 outdialing 和拨号规则和限制的详细信息，请参阅[允许用户通话](allow-users-to-make-calls-exchange-2013-help.md)。

## 启用/禁用呼叫应答规则

默认情况下，会自动启用 UM 的用户启用呼叫应答规则。但是，您可以通过禁用 UM 邮箱策略或用户的邮箱上的功能禁用用户的呼叫应答规则。有关如何启用或禁用呼叫应答规则的详细信息，请参阅下列主题 ︰

  - [允许或禁止用户在相同的 UM 邮箱策略创建呼叫应答规则](allow-or-prevent-users-in-the-same-um-mailbox-policy-from-creating-call-answering-rules-exchange-2013-help.md)

  - [允许或禁止用户创建呼叫应答规则](allow-or-prevent-a-user-from-creating-call-answering-rules-exchange-2013-help.md)
