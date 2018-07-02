---
title: '删除全局地址列表: Exchange 2013 Help'
TOCTitle: 删除全局地址列表
ms:assetid: 65d75b69-641b-4a37-a63c-47cf018f5f22
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232077(v=EXCHG.150)
ms:contentKeyID: 50490730
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除全局地址列表

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-12-16_

全局地址列表 (GAL) 是一个目录，包含 Exchange 组织中每个组、用户和联系人的条目。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“地址列表”条目。

  - 默认情况下，在 Exchange Online 中，地址列表角色不会分配给任何角色组。若要使用需要地址列表角色的任意 cmdlet，您需要向角色组添加此角色。有关详细信息，请参阅[管理角色组](manage-role-groups-exchange-2013-help.md)主题中的“向角色组添加角色”部分。

  - 不能删除默认 GAL。

  - 您不能使用 Exchange 管理中心 (EAC) 执行此过程，必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序删除 GAL

本示例从域控制器 ad-server.fourthcoffee.com 中删除名为 Fourth Coffee 的 GAL。

    Remove-GlobalAddressList -Identity "Fourth Coffee" -DomainController ad-server.fourthcoffee.com

要确认希望删除该 GAL，请键入 **Y**，然后按 Enter。

有关语法和参数的详细信息，请参阅 [Remove-GlobalAddressList](https://technet.microsoft.com/zh-cn/library/bb124368\(v=exchg.150\))。

