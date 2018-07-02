---
title: '查看公用文件夹和公用文件夹项目的统计信息: Exchange 2013 Help'
TOCTitle: 查看公用文件夹和公用文件夹项目的统计信息
ms:assetid: 4e412710-9a74-4649-ab01-502e969a7eda
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997949(v=EXCHG.150)
ms:contentKeyID: 50490527
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看公用文件夹和公用文件夹项目的统计信息

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-02-14_

本主题介绍如何检索公用文件夹的统计信息，例如显示名称、创建时间、上次用户修改时间、上次用户访问时间和项目大小。可以使用此信息对删除或保留公用文件夹作出决策。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 管理中心 (EAC) 中，可以通过导航到“公用文件夹”&gt;“编辑”<img src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="编辑图标" alt="编辑图标" /> &gt;“邮箱使用情况”查看公用文件夹的部分配额和使用情况信息。但是，此信息不完整，我们建议您使用命令行管理程序查看公用文件夹统计信息。</td>
</tr>
</tbody>
</table>


有关管理公用文件夹相关的更多管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“公用文件夹”条目。

  - 不能使用 EAC 检索公用文件夹统计信息。

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

## 使用命令行管理程序检索公用文件夹统计信息

本示例返回通过管道命令格式化列表的公用文件夹 Marketing 的统计信息。

    Get-PublicFolderStatistics -Identity \Marketing | Format-List

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Identity</em> 参数的值必须包含公用文件夹的路径。例如，如果公用文件夹 Marketing 位于父文件夹 Business 下，则要提供以下值：<code>\Business\Marketing</code></td>
</tr>
</tbody>
</table>


有关语法和参数的详细信息，请参阅 [Get-PublicFolderStatistics](https://technet.microsoft.com/zh-cn/library/aa998663\(v=exchg.150\))。

## 使用命令行管理程序查看公用文件夹项目的统计信息

您可以查看下列有关公用文件夹中项目的信息：

  - 项目的类型

  - 主题

  - 上次用户修改时间

  - 上次用户访问时间

  - 创建时间

  - 附件

  - 邮件大小

您可以使用该信息来决定对您的公用文件夹采取哪些操作，例如，要删除哪些公用文件夹。例如，如果有两年多未曾访问文件夹中的项目，您可能想要删除此公用文件夹；或者，您可能希望将用作文档存储库的公用文件夹转变为另一个客户端访问应用程序。

本示例返回路径 \\Marketing\\2013 下公用文件夹 Pamphlets 中所有项目的默认统计信息。默认信息包含项目标识、创建时间和主题。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2013\Pamphlets"

本示例返回公用文件夹 Pamphlets 内项目的其他信息，如主题、上次修改时间、创建时间、附件、邮件大小和项目类型。它还包括管道传送命令，以便将列表格式化。

    Get-PublicFolderItemStatistics -Identity "\Marketing\2010\Pamphlets" | Format-List

有关语法和参数的详细信息，请参阅 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-cn/library/ee332344\(v=exchg.150\))。

## 使用命令行管理程序将 Get-PublicFolderItemStatistics cmdlet 的输出导出到 .csv 文件

本示例将 cmdlet 的输出导出到 PFItemStats.csv 文件，此文件包括公用文件夹 \\Marketing\\Reports 中所有项目的以下信息：

  - 邮件主题 (`Subject`)

  - 上次修改项目的日期与时间 (`LastModificationTime`)

  - 项目是否带有附件 (`HasAttachments`)

  - 项目的类型 (`ItemType)`

  - 项目大小 (`MessageSize`)

<!-- end list -->

    Get-PublicFolderItemStatistics -Identity "\Marketing\Reports" | Select Subject,LastModificationTime,HasAttachments,ItemType,MessageSize | Export-CSV C:\PFItemStats.csv

有关语法和参数的详细信息，请参阅 [Get-PublicFolderItemStatistics](https://technet.microsoft.com/zh-cn/library/ee332344\(v=exchg.150\))。

