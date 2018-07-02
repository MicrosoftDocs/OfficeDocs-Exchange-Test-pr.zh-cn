---
title: '设置 Outlook Voice Access 针的安全性: Exchange Online Help'
TOCTitle: 设置 Outlook Voice Access 针的安全性
ms:assetid: ef6d9151-d333-4f52-9338-273f7a291e54
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125162(v=EXCHG.150)
ms:contentKeyID: 50556696
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置 Outlook Voice Access 针的安全性

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-16_

当统一邮件 (UM) 用户通过电话连接到语音邮件系统时，它们使用Outlook访问语音导航菜单系统。用户可以访问语音邮件系统之前，系统会提示他们输入他们的 PIN。作为管理员，您可以配置 PIN 设置和要求并执行管理任务，针。用户已启用了语音邮件并已生成 PIN 后，加密用户的邮箱中存储用户的 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Outlook Voice Access 用户必须使用按键 （也称为双音多频 (DTMF)） 输入可以输入他们的 PIN 来访问其启用 UM 的邮箱。语音识别不可用输入 PIN。</td>
</tr>
</tbody>
</table>


**目录**

PIN overview

PIN requirements

Managing Outlook Voice Access PINs

## PIN 概述

针为数值字符串，可在某些系统中，以便用户可以验证并获得对系统的访问。针脚最常用的自动取款机 (Atm)。他们还习惯而不是字母数字密码的语音邮件系统。针的强度取决于其长度、 保护程度，并猜测是多么的困难。

在统一消息中，Outlook Voice Access 用户在模拟、数字或移动电话上输入其 PIN，从而可以访问其 Exchange Server 邮箱中的电子邮件、语音邮件、联系人和日历信息。

在 UM，PIN 策略定义和 UM 邮箱策略上配置。您可以根据您的要求创建多个 UM 邮箱策略。当您启用语音邮件的用户时，您将链接到现有 UM 邮箱策略的用户。在 UM 邮箱策略配置的 UM PIN 策略应基于您的组织的安全要求。

## PIN 要求

以下是可以在 UM 邮箱策略中配置的几个 PIN 配置设置。

## 最小 PIN 长度

**小针长度**设置指定邮箱 PIN 必须包含的数字的最小数目。范围是 4 至 24，缺省值为 6。如果输入 0，则用户无需输入 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>将此设置配置零并不是建议的做法。如果您配置的设置为零，大大减少安全的级别为您的网络。</td>
</tr>
</tbody>
</table>


如果将 PIN 最小长度值更改为一个较大的值，则现有的 Outlook Voice Access 用户在继续使用之前，系统将提示他们输入包含新的最小位数的新 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>增加此数字创建更安全的 UM 环境。但是，设置过高会导致用户忘记他们的 PIN。</td>
</tr>
</tbody>
</table>


## 强制 PIN 生存期

**强制使用 PIN 生存期**设置控制的时间间隔，以天为单位中日期的 Outlook Voice Access 用户上次更改其 PIN 到它们将不得不再次改变他们的 PIN 的日期。范围是 0 到 999 之间，默认值为 60 天。如果输入 0，则不会过期 PIN。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当用户的 PIN 将要过期时，统一消息不会向用户发出通知。</td>
</tr>
</tbody>
</table>


## PIN 重置之前登录失败的次数

**重置 PIN 之前登录失败的次数**设置指定邮箱将自动重置 PIN 之前的连续失败登录尝试的数。若要禁用此功能，请将此设置设置为无限上。否则，它必须设置为数字低于**前锁定的登录失败次数的**设置。范围是 1 到 998，并且默认值为 5。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要提高启用 UM 的用户的安全性，请输入小于 5 的数字。</td>
</tr>
</tbody>
</table>


## 锁定前登录失败的次数

**在锁定之前登录失败的次数**设置 Outlook Voice Access 用户可以使他们在锁定之前到其邮箱的后续调用中指定多少 PIN 输入错误。默认情况下，进行了 5 次尝试后，针将自动重置。范围是 1 到 999 之间，并且默认值为 15。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>若要提高安全性，减少允许的失败尝试的次数。但是，请记住它减少到数字要远低于默认值可能会导致不必要地被锁定的用户。统一的消息将生成警告事件，可如果启用 UM 的用户的 PIN 身份验证失败或用户都不能成功尝试登录到系统，请使用事件查看器查看。</td>
</tr>
</tbody>
</table>


## 允许常见 PIN 模式

**允许公共 PIN 模式**设置用于启用或禁用使用的通用数字模式时创建 PIN。默认情况下，此设置被禁用，将不会允许 Outlook Voice Access 用户输入下列数字模式 ︰

  - **序列号**  完全由连续的数字组成的 PIN 值。连续数字 PIN 的例子有 1234年和 65432。

  - **Repeated 号**  由重复的数字组成的 PIN 值。重复的数字和都是 11111 22222。

  - **后缀的邮箱扩展**  用户的邮箱扩展的后缀组成的 PIN 值。如果邮箱扩展 36697，针不能为 6697。

## PIN 再循环计数

**PIN 回收计数**设置用于配置不同针脚先前用过的可重复使用之前，用户必须使用的针脚数目。范围是 1 到 20，并且默认值为 5。

## 管理 Outlook Voice Access PIN

为 Outlook Voice Access 针脚规划时，必须为您的组织选择了适当的安全级别。您必须仔细考虑的 Outlook Voice Access PIN 要求和 PIN 安全设置如何满足或超过您的组织的安全策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>它是实现强 Outlook Voice Access 用户的 PIN 要求安全最佳做法。这可以通过实现创建 UM 邮箱策略 PIN 策略所需六个或更多位数的针，这可以提高网络的安全性级别。</td>
</tr>
</tbody>
</table>


设置 Outlook Voice Access 针要求后，您必须创建和配置 UM 邮箱策略强制执行组织的 PIN 要求。有关如何创建 UM 邮箱策略的详细信息，请参阅[创建 UM 邮箱策略](create-a-um-mailbox-policy-exchange-2013-help.md)。有关如何管理 UM 邮箱策略的详细信息，请参阅[管理 UM 邮箱策略](manage-a-um-mailbox-policy-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>创建 UM 邮箱策略后，必须将已启用 UM 的用户或用户提供相应的 UM 邮箱策略的链接。通过使用Exchange命令行管理程序中的<strong>Enable-UMMailbox</strong> cmdlet 或使用 Exchange 管理中心 (EAC)，您可以执行此操作。Exchange命令行管理程序 cmdlet 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/aa998033(v=exchg.150)">Enable-UMMailbox</a>。</td>
</tr>
</tbody>
</table>


有一些情况下 Outlook Voice Access 用户忘记他们的 PIN 或锁定了语音邮件访问其邮箱。在任一情况下，可能需要重置启用 UM 的用户的 PIN。有关详细信息，请参阅[重置语音邮件 PIN](reset-a-voice-mail-pin-exchange-2013-help.md)。

您可以启用统一消息的用户的 PIN 信息。通过使用加密存储在用户的邮箱的 PIN 数据计算返回给您的信息。这使您可以查看该用户的 PIN 信息并指出用户是否已锁定他们的邮箱。有关详细信息，请参阅[检索语音邮件 PIN 信息](retrieve-voice-mail-pin-information-exchange-2013-help.md)。

