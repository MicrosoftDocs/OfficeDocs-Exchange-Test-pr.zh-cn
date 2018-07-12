---
title: '邮箱导入和导出请求: Exchange 2013 Help'
TOCTitle: 邮箱导入和导出请求
ms:assetid: 157a7d88-d3aa-4056-9a50-df67451b14be
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee633455(v=EXCHG.150)
ms:contentKeyID: 50489953
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮箱导入和导出请求

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

使用 Exchange 命令行管理程序中的 **MailboxImportRequest** 或 **MailboxExportRequest** cmdlet 集，您可以从 .pst 文件导入数据或将数据导出到这些文件。发出邮箱导入或导出请求后，由 Microsoft Exchange 邮箱复制服务 (MRS) 异步完成该过程。MRS 驻留在所有 Exchange 2010 客户端访问服务器上，该服务负责移动邮箱以及导入和导出 .pst 文件。

**目录**

导入或导出邮箱数据的原因

使用导入和导出请求的优势

注意事项

导入邮箱数据

导出邮箱数据

## 导入或导出邮箱数据的原因

可能由于以下原因而需要导入或导出邮箱数据：

  - **满足合规性要求**   可以出于法律发现目的将邮箱内容导出到 .pst 文件。完成导出后，可以将内容导入到专用于合规性用途的邮箱。

  - **创建时间点邮箱快照**   通过创建特定邮箱的快照，您就无需再为邮箱数据库保留整个备份集。

  - **将用户的 .pst 文件移至其邮箱或个人存档中**   Microsoft Outlook 用户可以将其电子邮件在本地另存为 .pst 文件。您可以使用 [New-MailboxImportRequest](https://technet.microsoft.com/zh-cn/library/ff607310\(v=exchg.150\)) cmdlet 将数据从用户的 .pst 文件移至其邮箱或个人存档中。该方法是将电子邮件从用户的本地计算机传送到 Exchange 服务器的简单方法。

## 使用导入和导出请求的优势

在 Exchange 2013 中使用导入和导出请求的优势包括以下这些：

  - 在 Exchange 2013 中包含一个 .pst 提供程序，可以读写 .pst 文件。

  - 导入和导出请求是异步的。该过程由 MRS 执行，其利用队列和限制框架。

  - .pst 文件可以直接导入到用户的个人存档中。

  - 可以同时导入或导出多个 .pst 文件。

  - .pst 文件可以驻留在 Exchange 服务器能够访问的任何共享网络驱动器上。

  - Exchange 2013 支持这些 .pst 文件：由 Office Outlook 2007 和 Outlook 2010 创建的 Unicode 文件

## 注意事项

在导入或导出邮箱数据之前，请考虑以下事项：

  - 若要导入或导出邮箱数据，必须设置可由 Exchange 服务器访问的网络共享文件夹。还必须为 Exchange 受信任子系统组授予读/写权限，这样该组便可访问您在其中导入和导出邮箱数据的网络共享。如果不授予此权限，您将收到一条错误消息，指示 Exchange 无法与目标邮箱建立连接。

  - Outlook 支持的最大 .pst 文件大小为 50 GB。因此建议您不要导入 50 GB 以上的 .pst 文件。您可以通过指定要包含或排除的特定文件夹，或者通过使用内容过滤器，为 50 GB 以上的邮箱创建多个 .pst 文件。

  - 导入和导出请求由 MRS 执行，它还负责处理移动请求和邮箱还原请求。所有请求都由 MRS 进行排队和限制。

  - 根据文件大小、网络带宽以及 MRS 限制，导入和导出邮箱数据可能需要数小时时间。

  - 数据不能导入到公用文件夹或公用文件夹数据库中。

## 导入邮箱数据

使用 **MailboxImportRequest** cmdlet 集将数据从 .pst 文件导入到邮箱或个人存档中。下面是从 .pst 文件导入邮箱数据时可以指定的选项的列表：

> [!NOTE]  
> 导入数据的邮箱必须已经存在。您不能将数据导入没有邮箱的用户帐户。


  - 可以将数据导入不同于从中导出该数据的其他用户帐户。例如，可以从 john@contoso.com 导出数据，并将数据导入到 legaldiscovery@contoso.com。

  - 通过指定 *IsArchive* 参数，可以将数据项仅导入到用户的个人存档中。

  - 如果 .pst 文件中存在关联的文件夹邮件，则可以使用 *AssociatedMessagesCopyOption* 参数导入这些邮件。关联的邮件包含隐藏数据，其中包含有关规则、视图和表单的信息。如果它们存在于 .pst 文件中，则会导入安全网络中的所有邮件。

  - 可以使用 *IncludeFolders* 或 *ExcludeFolders* 参数包含或排除特定文件夹。

  - 可以使用 *ExcludeDumpster* 参数排除“可恢复的项目”文件夹。默认情况下，如果 .pst 文件中存在用户的“可恢复的项目”文件夹，则导入请求中就会包含该文件夹。

## 邮箱导入请求 cmdlet

将以下 cmdlet 用于邮箱导入请求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607310(v=exchg.150)">New-MailboxImportRequest</a></p></td>
<td><p>启动将 .pst 文件导入到邮箱或个人存档的过程。可以为每个邮箱创建多个导入请求。每个请求必须具有唯一的名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607317(v=exchg.150)">Set-MailboxImportRequest</a></p></td>
<td><p>创建请求或从失败的请求恢复后，更改导入请求选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607309(v=exchg.150)">Suspend-MailboxImportRequest</a></p></td>
<td><p>在请求创建之后但达到“已完成”状态之前的任何时候，挂起导入请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607306(v=exchg.150)">Resume-MailboxImportRequest</a></p></td>
<td><p>恢复已挂起或失败的导入请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607311(v=exchg.150)">Remove-MailboxImportRequest</a></p></td>
<td><p>删除全部或部分完成的导入请求。已完成的导入请求不会自动清除。必须使用此 cmdlet 删除这些请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607368(v=exchg.150)">Get-MailboxImportRequest</a></p></td>
<td><p>查看关于导入请求的一般信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607315(v=exchg.150)">Get-MailboxImportRequestStatistics</a></p></td>
<td><p>查看关于导入请求的详细信息。</p></td>
</tr>
</tbody>
</table>


## 导出邮箱数据

使用 **MailboxExportRequest** cmdlet 集将邮箱数据导出到 .pst 文件。可以导出一个或多个邮箱，但一次只将一个请求写入每个 .pst 文件。下面是将邮箱数据导出到 .pst 文件时可以指定的选项的列表：

  - 可以使用 *IsArchive* 参数导出个人存档数据。

  - 可以使用 *ContentFilter* 参数筛选导出的邮件。可以按邮件内容、附件、发件人、收件人、收件箱类别、重要性、邮件类型、邮件大小、邮件发送时间、邮件接收时间或邮件到期时间来进行筛选。

  - 可以使用 *IncludeFolders* 或 *ExcludeFolders* 参数指定要包含或排除的文件夹。如果是从 Exchange 2013 邮箱导出数据，还可以使用 *ExcludeDumpster* 参数排除“可恢复的项目”文件夹。

  - 可以使用 *AssociatedMessagesCopyOption* 参数导出相关联的邮件。关联的邮件包含隐藏数据，其中包含有关规则、视图和表单的信息。默认情况下，关联的项目不会复制到 .pst 文件中。

## 邮箱导出请求 cmdlet

将以下 cmdlet 用于邮箱导出请求。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607299(v=exchg.150)">New-MailboxExportRequest</a></p></td>
<td><p>启动将数据从主邮箱或个人存档导出到 .pst 文件的过程。可以为每个邮箱创建多个导出请求。每个请求必须具有唯一的名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607312(v=exchg.150)">Set-MailboxExportRequest</a></p></td>
<td><p>创建请求或从失败的请求恢复后，更改导出请求选项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607305(v=exchg.150)">Suspend-MailboxExportRequest</a></p></td>
<td><p>在请求创建之后但达到“已完成”状态之前的任何时候，挂起导出请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607476(v=exchg.150)">Resume-MailboxExportRequest</a></p></td>
<td><p>恢复已挂起或失败的导出请求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607464(v=exchg.150)">Remove-MailboxExportRequest</a></p></td>
<td><p>删除全部或部分完成的导出请求。已完成的导出请求不会自动清除。必须使用此 cmdlet 删除这些请求。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607479(v=exchg.150)">Get-MailboxExportRequest</a></p></td>
<td><p>查看关于导出请求的一般信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/zh-cn/library/ff607316(v=exchg.150)">Get-MailboxExportRequestStatistics</a></p></td>
<td><p>查看关于导出请求的详细信息。</p></td>
</tr>
</tbody>
</table>

