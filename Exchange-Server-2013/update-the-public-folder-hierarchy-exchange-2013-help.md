---
title: '更新公用文件夹层次结构: Exchange Online Help'
TOCTitle: 更新公用文件夹层次结构
ms:assetid: a7b2fb51-0207-4d7d-938d-466ae110bb90
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ945055(v=EXCHG.150)
ms:contentKeyID: 52061414
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 更新公用文件夹层次结构

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2014-04-03_

只有要手动调用层次结构同步器和邮箱助理时，才需要更新公用文件夹层次结构。对于组织中的每个公用文件夹邮箱，每 24 小时至少调用一次这两者。如果有任何用户通过 Microsoft Outlook 或 Microsoft Exchange Web 服务客户端登录辅邮箱，则每 15 分钟调用一次层次结构同步器。

有关 Exchange Online 中与公用文件夹相关的其他管理任务，请参阅 [Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

有关 Exchange Server 2013 中与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的\&quot;公用文件夹\&quot;条目。

  - 您无法在 EAC 中执行此过程。必须使用命令行管理程序。

  - 使用 *InvokeSynchronizer* 参数运行此命令时，建议使用 *SuppressStatus* 参数。如果未在命令中使用此参数，则输出每 3 秒会显示一次状态消息，这个过程长达一分钟。在一分钟过去之前，您不能使用命令行管理程序的该实例。

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


## 更新公用文件夹层次结构

此示例更新公用文件夹邮箱 PF\_marketing 上的公用文件夹层次结构，并禁止命令的输出。

    Update-PublicFolderMailbox -Identity PF_marketing -InvokeSynchronizer -SuppressStatus

此示例更新所有公用文件夹邮箱，并禁止命令的输出。

    Get-Mailbox -PublicFolder | Update-PublicFolderMailbox InvokeSynchronizer -SuppressStatus

