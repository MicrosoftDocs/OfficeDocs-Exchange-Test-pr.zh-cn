---
title: '配置远程域自动答复: Exchange 2013 Help'
TOCTitle: 配置远程域自动答复
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 50490396
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置远程域自动答复

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

您可以使用 Exchange 命令行管理程序配置通过远程域发送和接收电子邮件的方式。下面将演示如何使用 Exchange 命令行管理程序配置 Exchange 处理自动答复的方式。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 只能使用命令行管理程序执行此过程。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“远程域”条目。

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


## 使用命令行管理程序配置自动答复

您可以使用 **Set-RemoteDomain** cmdlet 配置远程域的属性。

本示例将允许自动答复名为 Contoso 的远程域。默认情况下，禁用此设置。

    Set-RemoteDomain Contoso -AutoReplyEnabled $true

此示例允许自动转发到远程域。默认情况下，禁用此设置。

    Set-RemoteDomain Contoso -AutoForwardEnabled $true

