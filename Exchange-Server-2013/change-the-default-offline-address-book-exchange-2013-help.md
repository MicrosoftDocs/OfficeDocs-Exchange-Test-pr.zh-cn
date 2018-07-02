---
title: '更改默认脱机通讯簿: Exchange 2013 Help'
TOCTitle: 更改默认脱机通讯簿
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 50490698
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 更改默认脱机通讯簿

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

默认情况下，在安装邮箱服务器角色时，会创建一个名为“默认脱机通讯簿”的基于 Web 的默认脱机通讯簿 (OAB)。您可以将 Exchange 组织中的任何 OAB 设置为默认 OAB。这一新的默认 OAB 将与所有新创建的邮箱数据库相关联。您的组织中只能有一个默认 OAB。如果删除默认 OAB，MicrosoftExchange 不会将另一个 OAB 自动指定为默认 OAB。您必须手动将另一个 OAB 指定为默认 OAB。

有关与 OAB 相关的更多管理任务，请参阅[脱机通讯簿程序](offline-address-book-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“脱机通讯簿”条目。

  - UNRESOLVED\_TOKENBLOCK\_VAL(GENL\_AddressListRole\_EXOnOP)

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


## 使用命令行管理程序更改默认 OAB

本示例将名为“My OAB”的 OAB 设置为默认 OAB。

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

有关语法和参数的详细信息，请参阅 [Set-OfflineAddressBook](https://technet.microsoft.com/zh-cn/library/aa996330\(v=exchg.150\))。

