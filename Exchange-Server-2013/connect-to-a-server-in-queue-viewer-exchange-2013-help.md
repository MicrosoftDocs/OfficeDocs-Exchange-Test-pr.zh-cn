---
title: '使用队列查看器连接到服务器: Exchange 2013 Help'
TOCTitle: 使用队列查看器连接到服务器
ms:assetid: 6c1ad574-9ab5-4dcc-9398-ec10eca4fd11
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998669(v=EXCHG.150)
ms:contentKeyID: 50490777
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用队列查看器连接到服务器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

在位于 Exchange 组织内部的 Microsoft Exchange Server 2013 服务器上使用 Exchange 工具箱中的队列查看器时，可以连接到其他邮箱服务器。默认情况下，在邮箱服务器上打开队列查看器时，队列查看器会连接到本地服务器上的队列数据库。不过，可以启动多个队列查看器实例，以使每个实例侧重于不同的服务器。还可以平铺队列查看器窗口，以便可以同时轻松监视多个邮箱服务器。

还可以指定远程 PowerShell 用于在队列查看器中执行指定任务的服务器。此服务器不需要匹配正在队列查看器中管理的远程服务器。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“队列”条目。

  - 本主题中的过程不适用于边缘传输服务器。在边缘传输服务器上使用队列查看器时，无法更改此工具的侧重点。

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


## 您想执行什么操作？

## 使用 Exchange 工具箱指定要在队列查看器中管理的服务器

1.  单击“开始”\>“所有程序”\>“Microsoft Exchange Server 2013”\>“Exchange 工具箱”。

2.  在“邮件流工具”下，双击“队列查看器”。

3.  在操作窗格中，单击“连接到服务器”。

4.  在“连接到服务器”窗口中，单击“浏览”查看可用邮箱服务器的列表。

5.  在“选择 Exchange 服务器”窗口中，选择一个邮箱服务器。要搜索邮箱服务器，请使用以下过程之一：
    
      - 在“搜索”字段中输入确切的服务器名称或服务器名称的前几个字母，然后单击“立即查找”。从结果窗格中选择一个服务器。
    
      - 选择“查看”菜单，然后单击“显示筛选器”。在“名称”列或“版本”列中，单击筛选器图标，然后选择筛选器运算符。在“在此输入文本”字段中键入筛选条件。按 Enter 键。从结果窗格中选择一个服务器。

6.  单击“确定”关闭“选择 Exchange 服务器”窗口。

7.  选择服务器之后，如果希望队列查看器只要打开便首先针对此服务器执行操作，请在“连接到服务器”窗口中，选中“设置为默认服务器”复选框。

8.  在“连接到服务器”窗口中，单击“连接”。

## 使用 Exchange 工具箱指定队列查看器用于运行远程 PowerShell 的服务器

1.  单击“开始”\>“所有程序”\>“Microsoft Exchange Server 2013”\>“Exchange 工具箱”。

2.  在“邮件流工具”部分，双击“队列查看器”。

3.  在操作窗格中，单击“属性”。

4.  在“队列查看器 - \<服务器名称\> 属性”对话框中，选择下列选项之一：
    
      - **连接到自动选择的服务器**：选择此选项可自动连接到为运行远程 PowerShell 而管理队列的服务器。
    
      - **指定要连接到的服务器**：选择此选项可指定要运行远程 PowerShell 的服务器。如果选择此选项，单击“浏览”可打开“选择 Exchange 服务器”对话框。选择要运行远程 PowerShell 的服务器，然后单击“确定”。

## 您如何知道这有效？

您应该能够在指定的邮箱服务器上管理队列。

