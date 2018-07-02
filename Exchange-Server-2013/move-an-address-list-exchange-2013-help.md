---
title: '移动地址列表: Exchange 2013 Help'
TOCTitle: 移动地址列表
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 50491514
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 移动地址列表

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-14_

本主题说明将现有地址列表移动到根地址列表下的新容器中。

有关地址列表的更多管理任务，请参阅[地址列表程序](address-list-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [电子邮件地址和通讯簿权限](email-address-and-address-book-permissions-exchange-2013-help.md)主题中的“地址列表”条目。

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


## 使用命令行管理程序移动地址列表

本示例使用地址列表的 GUID 将地址列表移动到位于 All Users\\Sales 容器下的 Building4 容器中。

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

键入 **Y** 确认要移动该地址列表，然后按 ENTER 键。

有关语法和参数的详细信息，请参阅 [Move-AddressList](https://technet.microsoft.com/zh-cn/library/bb124520\(v=exchg.150\))。

