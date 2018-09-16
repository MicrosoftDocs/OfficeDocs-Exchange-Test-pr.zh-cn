---
title: '邮箱审核日志记录: Exchange 2013 Help'
TOCTitle: 邮箱审核日志记录
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50490237
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 邮箱审核日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

由于邮箱可能包含一些敏感、对业务影响很大 (HBI) 的信息和个人的可识别信息 (PII)，因此，跟踪登录组织内邮箱的人员及其所执行的操作非常重要。跟踪邮箱所有者之外的其他用户对邮箱的访问情况尤其重要。这些用户称为“委派用户”。

使用*邮箱审核日志记录*可以记录邮箱所有者、委派用户（包含具有完全邮箱访问权限的管理员）和管理员对邮箱的访问。

为邮箱启用审核日志记录时，可以指定将记录一种登录类型（管理员、委派用户或所有者）的哪些用户操作。审核日志条目还包含客户端 IP 地址、主机名以及用于访问邮箱的进程或客户端等重要信息。对于移动的项目，条目中包含目标文件夹的名称。

## 邮箱审核日志

邮箱审核日志针对每个启用了邮箱审核日志记录功能的邮箱而生成。日志条目存储在已审核邮箱“可恢复邮件”文件夹的“审核”子文件夹中。这样能够保证可以从一个位置获得全部审核日志条目，而无论使用哪种客户端访问方法来访问邮箱，或者管理员使用哪个服务器或工作站来访问邮箱审核日志。如果将邮箱移至其他邮箱服务器，则由于邮箱中包含该邮箱的审核日志，因此这些审核日志也会移动到其他邮箱服务器。

默认情况下，邮箱审核日志条目在邮箱中保留 90 天，然后被删除。可以使用 *AuditLogAgeLimit* 参数和 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 来修改此保留期限。如果邮箱为就地保留或诉讼保留，审核日志条目仅保留到邮箱的审核日志保留期限为止。要将审核日志条目保留更长时间，您必须通过更改 *AuditLogAgeLimit* 参数的值来增加保留期。您也可以在保留期到期之前导出审核日志条目。有关详细信息，请参阅：

  - [导出邮箱审核日志](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs)

  - [创建邮箱审核日志搜索](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## 启用邮箱审核日志记录

审核日志记录是按邮箱启用的。使用 **Set-Mailbox** cmdlet 启用或禁用邮箱审核日志记录。有关详细信息，请参阅[启用或禁用邮箱的邮箱审核日志记录](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

当启用邮箱的邮箱审核日志记录功能时，默认情况下会记录对邮箱的访问以及管理员和委派用户执行的某些操作。若要记录邮箱所有者执行的操作，必须指定应审核哪些所有者操作。

## 邮箱审核日志记录所记录的邮箱操作

下表列出了邮箱审核日志记录功能所记录的操作，其中包括所记录的操作的登录类型。


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>描述</th>
<th>管理员</th>
<th>委派用户</th>
<th>所有者</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>复制</p></td>
<td><p>将项目复制到另一个文件夹。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>Create</p></td>
<td><p>在邮箱的日历、联系人、备注或任务文件夹中创建项目；例如，创建新的会议请求。请注意，不审核邮件或文件夹创建。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>访问邮箱文件夹。</p></td>
<td><p>是*</p></td>
<td><p>是**</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>从“可恢复的项目”文件夹中永久删除项目。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>在读取窗格中访问或打开项目。</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p>移动</p></td>
<td><p>将项目移动到另一个文件夹。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>将项目移动到“已删除邮件”文件夹中。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>使用 Send As 权限发送邮件。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>使用 Send on Behalf 权限发送邮件。</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>从“已删除邮件”文件夹中删除项目。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>更新</p></td>
<td><p>更新项目的属性。</p></td>
<td><p>是*</p></td>
<td><p>是*</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


\* 如果为邮箱启用了审核功能，则默认为已审核。

\*\* 合并由委派用户执行的文件夹绑定操作的条目。在 24 小时的时间跨度内为每个文件夹访问生成一个日志条目。

如果不再需要审核某些类型的邮箱操作，应修改邮箱的审核日志记录配置，以禁用这些操作。在达到审核日志条目期限之前，不会清除现有日志条目。

## 搜索邮箱审核日志条目

可以使用下列方法搜索邮箱审核日志条目：

  - **同步搜索单个邮箱**   可以使用 [Search-MailboxAuditLog](https://technet.microsoft.com/zh-cn/library/ff522360\(v=exchg.150\)) cmdlet 同步搜索单个邮箱的邮箱审核日志条目。此 cmdlet 在 Exchange 命令行管理程序窗口中显示搜索结果。有关详细信息，请参阅[搜索邮箱邮箱审核日志](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md)。

  - **异步搜索一个或多个邮箱**   可以创建邮箱审核日志搜索来异步搜索一个或多个邮箱的邮箱审核日志，然后将搜索结果发送到指定的电子邮件地址。搜索结果以 XML 附件的形式发送。要创建搜索，请使用 [New-MailboxAuditLogSearch](https://technet.microsoft.com/zh-cn/library/ff522362\(v=exchg.150\)) cmdlet。有关详细信息，请参阅[创建邮箱审核日志搜索](create-a-mailbox-audit-log-search-exchange-2013-help.md)。

  - **使用 Exchange 管理中心 (EAC) 中的审核报告**   您可以使用 EAC 中的“审核”选项卡运行非所有者邮箱访问报告，或者从邮箱审核日志中导出条目。有关详细信息，请参阅：
    
      - [运行非所有者邮箱访问报告](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [导出邮箱审核日志](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs)

## 邮箱审核日志条目

下表说明在邮箱审核日志记录条目中记录的字段。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>填入内容</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>下列操作之一：</p>
<ul>
<li><p>Copy</p></li>
<li><p>Create</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Move</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Update</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>下列结果之一：</p>
<ul>
<li><p>Failed</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Succeeded</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>执行操作的用户的登录类型。登录类型包括：</p>
<ul>
<li><p>所有者</p></li>
<li><p>委派用户</p></li>
<li><p>管理员</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>移动操作的目标文件夹 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>移动操作的目标文件夹路径。</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>文件夹 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>文件夹路径。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>可确定是哪个客户端或 Exchange 组件执行了此操作的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>客户端计算机 IP 地址。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>客户端计算机名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>客户端应用程序进程的名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>客户端应用程序版本。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>执行操作的用户的登录类型。登录类型包括：</p>
<ul>
<li><p>所有者</p></li>
<li><p>委派用户</p></li>
<li><p>管理员</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>邮箱所有者用户主体名称 (UPN)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>邮箱所有者安全标识符 (SID)。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>目标邮箱所有者 UPN（为跨邮箱操作而记录）。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>目标邮箱所有者 SID（为跨邮箱操作而记录）。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>目标邮箱所有者 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>关于记录的操作是否是跨邮箱操作（例如，在多个邮箱间复制或移动邮件）的信息。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>显示登录用户的名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>委派用户显示名称。</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>登录用户的 SID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>对其执行了所记录的操作（例如移动或删除）的邮箱项目的 ItemID。对于在许多项目上执行的操作，该字段会返回一个项目集合。</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>源文件夹 GUID。</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>项目 ID。</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>项目主题。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>邮箱 GUID。</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>采用 <em>DOMAIN</em>\<em>SamAccountName</em> 格式的邮箱用户解析名称。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>执行操作的时间。</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>审核日志条目 ID。</p></td>
</tr>
</tbody>
</table>


## 详细信息

  - **邮箱的管理员访问权限**   只有在以下情况下，才视为由管理员访问邮箱：
    
      - [就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery) 用于搜索邮箱。
    
      - 使用 [New-MailboxExportRequest](https://technet.microsoft.com/zh-cn/library/ff607299\(v=exchg.150\)) cmdlet 导出邮箱。
    
      - [Microsoft Exchange Server MAPI Editor](https://go.microsoft.com/fwlink/p/?linkid=204086) 用于访问邮箱。

  - **绕过邮箱审核日志记录**   由授权自动化进程（如第三方工具使用的帐户或用于合法监视的帐户）执行的邮箱访问可以创建大量邮箱审核日志条目，而您的组织可能不感兴趣。可以将这些帐户配置为绕过邮件审核日志功能。有关详细信息，请参阅[绕过用户帐户从邮箱审核日志记录](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md)。

  - **记录邮箱所有者操作**   对于像发现搜索邮箱这样可能包含更多敏感信息的邮箱，可以考虑为诸如邮件删除等邮箱所有者操作启用邮箱审核日志记录。

邮箱审核日志

