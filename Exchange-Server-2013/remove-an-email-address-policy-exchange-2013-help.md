---
title: '删除电子邮件地址策略: Exchange 2013 Help'
TOCTitle: 删除电子邮件地址策略
ms:assetid: f1d05223-7d41-406d-8fae-f4227be1c1c2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125181(v=EXCHG.150)
ms:contentKeyID: 50491969
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 删除电子邮件地址策略

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-13_

默认情况下， Exchange包含电子邮件地址策略指定收件人的别名用作电子邮件地址的本地部分，并使用默认的接受域。电子邮件地址的本地部分是出现之前"at"符号的名称 (@)。此电子邮件地址策略应用于组织中的所有用户。您不能删除此电子邮件地址策略。

有关电子邮件地址策略的其他管理任务，请参阅 [电子邮件地址策略程序](email-address-policy-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 如果您删除收件人作为主策略使用的电子邮件地址，而没有为收件人配置任何其他策略，则使用默认策略。

  - 不能删除默认策略。如果您想要删除默认策略，首先必须为默认分配不同的策略。

  - 如果您正在删除的电子邮件地址策略中包含超过 3,000 个收件人，则应使用命令行管理程序执行此步骤。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿](email-addresses-and-address-books-exchange-2013-help.md)主题中的\&quot;电子邮件地址策略\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 删除电子邮件地址策略

1.  导航到\&quot;邮件流\&quot; \> \&quot;电子邮件地址策略\&quot;。

2.  在列表视图中，选择您要删除的电子邮件地址策略，然后单击\&quot;删除\&quot;![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  在警告中，单击\&quot;是\&quot;删除策略。

## 使用命令行管理程序删除电子邮件地址策略

本示例将删除电子邮件地址策略 South East Offices。

    Remove-EmailAddressPolicy -Identity "South East Offices"

键入 **Y** 确认要删除该策略，然后按 Enter 键。

有关语法和参数的详细信息，请参阅 [Remove-EmailAddressPolicy](https://technet.microsoft.com/zh-cn/library/bb124504\(v=exchg.150\))。

