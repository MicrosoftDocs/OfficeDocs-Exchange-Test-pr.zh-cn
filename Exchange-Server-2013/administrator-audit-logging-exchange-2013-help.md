---
title: '管理员审核日志记录: Exchange 2013 Help'
TOCTitle: 管理员审核日志记录
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50556541
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理员审核日志记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-03-05_

您可以使用 Microsoft Exchange Server 2013 中的管理员审核日志记录来记录用户或管理员在组织中进行更改的时间。通过保留更改日志，您可以跟踪对进行更改的人员所做的更改、随着更改的实施使用更改的详细记录来扩充更改日志、遵守法规要求和发现请求等等。

默认情况下，审核日志记录在 Exchange 2013 的新安装中已启用。

**目录**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## 要审核的内容

对于直接在 Exchange 命令行管理程序中运行的 cmdlet 要进行审核。此外，由于使用 Exchange 管理中心 (EAC) 执行的操作将在后台运行 cmdlet，因此这些操作也会记录。

Cmdlet，无论他们在哪里运行，审核如果 cmdlet 是在审核列表和一个 cmdlet 或者该 cmdlet 的详细参数在参数审核列表。审核日志将显示已采取何种措施修改Exchange组织中的对象而不是已查看过哪些对象。

> [!IMPORTANT]  
> 如果某个 cmdlet 调用管理审核日志 cmdlet 扩展代理之前发生错误，则可能不会记录该 cmdlet。如果在调用管理审核日志代理之后发生错误，则会记录该 cmdlet 以及关联的错误。有关详细信息，请参阅本主题后面的Admin Audit Log Agent一节。
> 使用 Microsoft Exchange Server 2010 管理工具所做的更改将会记录；但是，使用 Microsoft Exchange Server 2007 管理工具所做的更改不会记录。
> 在打开了命令行管理程序的计算机上，在对审核日志配置进行更改之后，所做的更改会每隔 60 分钟刷新一次。如果想要立即应用所做的更改，请在每台计算机上关闭并重新打开命令行管理程序。
> 命令运行后，最多可能需要 15 分钟才会出现在审核日志搜索结果中。这是因为审核日志条目必须先编制索引，然后才能进行搜索。如果命令未显示在管理员审核日志中，请等待几分钟，然后再次运行搜索。


## 审核日志记录配置

默认情况下，如果启用审核日志记录，则日志条目创建每次运行时任何 cmdlet。如果您不想审核每个运行的 cmdlet，您可以配置审核日志审核的 cmdlet 和感兴趣的参数。您可以使用**Set-AdminAuditLogConfig** cmdlet 配置审核日志。与此 cmdlet 使用在以下各节中引用的参数。

> [!IMPORTANT]  
> 无论 <strong>Set-AdministratorAuditLog</strong> cmdlet 是否包括在要审核的 cmdlet 列表中，也无论是启用还是禁用了审核日志记录，始终都会记录对管理员审核日志配置进行的更改。


运行命令后，Exchange 将检查所使用的 cmdlet。如果所运行的 cmdlet 与随 *AdminAuditLogConfigCmdlets* 参数提供的任何 cmdlet 匹配，则 Exchange 随后将检查在 *AdminAuditLogConfigParameters* 参数中指定的参数。如果参数列表中至少有一个或多个参数匹配，则 Exchange 将记录使用 *AdminAuditLogMailbox* 参数指定的邮箱中运行的 cmdlet。以下各部分详细介绍审核日志记录配置的各个方面。

有关管理审核日志记录配置的详细信息，请参阅[管理管理员审核日志记录](manage-administrator-audit-logging-exchange-2013-help.md)。

返回顶部

## Cmdlet

通过提供要记录的 cmdlet 及其参数的列表，可以控制要审核哪些 cmdlet。配置审核日志记录时，可以指定审核每个 cmdlet，也可以使用 *AdminAuditLogConfigCmdlets* 参数指定要审核的 cmdlet。可以指定完整 cmdlet 名称（如 **New-Mailbox**），也可以指定部分 cmdlet 名称并在通配符（如星号 `*`）中包含这些名称。例如，如果要记录任何包含字符串 `Transport` 的 cmdlet 何时运行，可以指定一个 `*Transport*` 值。可以同时混合使用完整 cmdlet 名称和部分 cmdlet 名称，以使审核日志记录符合您的需要。

## 参数

除了指定要记录哪些 cmdlet 之外，还可以指明只有在使用这些 cmdlet 中的某些参数时才应记录这些 cmdlet。使用 *AdminAuditLogConfigParameters* 参数指定应记录哪些参数。与 cmdlet 一样，可以指定完整参数名称（如 `Database`），也可以将部分参数名称包含在通配符 (`*`) 中（如 `*Address*`）或采用二者的组合形式。

## 审核日志期限

默认情况下，审核日志记录配置为将审核日志条目存储 90 天。90 天后将删除审核日志条目。您可以使用 *AdminAuditLogAgeLimit* 参数更改审核日志期限。可以指定审核日志条目应保留的天数、小时数、分钟数和秒数。若要指定值，请使用 `dd.hh:mm:ss` 格式，其中应用了以下条件：

  - **dd**   保留审核日志条目的天数。

  - **hh**   保留审核日志条目的小时数。

  - **mm**   保留审核日志条目的分钟数。

  - **ss**   保留审核日志条目的秒数。

您必须使用 `dd` 字段指定多年时间。例如，365 天等于一年；730 天等于两年；913 天等于两年零六个月。例如，若要将审核日志期限设置为两年零六个月，请使用语法 `913.00:00:00`。

> [!CAUTION]  
> 可以将审核日志期限设置为小于当前期限的值。如果执行此操作，则会删除寿命超过新期限的所有审核日志条目。
> 如果将期限设置为 0，则 Exchange 会删除审核日志中的所有条目。
> 建议您仅向高度信任的用户授予配置审核日志期限的权限。


## 详细日志记录

默认情况下，管理员审核日志仅记录 cmdlet 名称、cmdlet 参数（和指定的值）、修改对象、cmdlet 的运行用户、cmdlet 的运行时间以及 cmdlet 运行所在的服务器。管理员审核日志不会记录对象中已修改的那些属性。如果您希望审核日志还包括记录已修改的对象属性，则可以通过将 *LogLevel* 参数设置为 `Verbose` 来启用详细日志记录。启用详细日志记录之后，除了默认情况下记录的信息以外，对象中修改的属性（包括旧值和新值）也会记录在审核日志中。

## 测试 cmdlet

默认情况下，不记录以谓词 **Test** 开头的 cmdlet。可以通过将 *TestCmdletLoggingEnabled* 参数设置为 `$true`，来指示应记录 **Test** cmdlet。虽然可以启用测试 cmdlet 的日志记录，但由于测试 cmdlet 将生成大量信息，因此建议您只在短时间内执行此操作。

## 审核日志

每次记录 cmdlet 时，都会创建审核日志条目。审核日志存储在隐藏的专用仲裁邮箱中，该邮箱只能使用 EAC 或 **Search-AdminAuditLog** 或 **New-AdminAuditLogSearch** cmdlet 进行访问。不能使用 Microsoft Outlook Web App 或 Microsoft Outlook 进行打开。以下各节提供有关以下内容的信息：

  - 日志中包含的内容

  - EAC\&quot;审核\&quot;页面上的可用报告

  - 审核日志搜索 cmdlet

## 审核日志内容

每个审核日志条目都包含下表所述的信息。审核日志包含一个或多个审核日志条目。审核日志条目的数量由使用 **Set-AdminAuditLogConfig** cmdlet 指定的审核日志期限进行控制。超过期限的任何审核日志条目都会被删除。

### 审核日志条目字段

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>字段</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>此字段由 Exchange 在内部使用。</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>此字段包含由 <code>CmdletName</code> 字段中指定的 cmdlet 修改的对象。</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>此字段包含由 <code>Caller</code> 字段中的用户运行的 cmdlet 的名称。</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>此字段包含在运行 <code>CmdletName</code> 字段中的 cmdlet 时指定的参数。使用参数指定的值（如果有）也存储在此字段中，但是在默认输出中不可见。有关如何访问此字段中的其他信息的详细信息，请参阅<a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">搜索角色组更改或管理员审核日志</a>。</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>此字段包含在 <code>ObjectModified</code> 字段中的对象上修改的属性。属性的旧值和存储的新值也存储在此字段中，但是在默认输出中不可见。有关如何访问此字段中的其他信息的详细信息，请参阅<a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">搜索角色组更改或管理员审核日志</a>。</p>

> [!IMPORTANT]  
> 仅当 <strong>Set-AdminAuditLogConfig</strong> cmdlet 中的 <em>LogLevel</em> 参数设置为 <code>Verbose</code> 时，此字段才会填充。

</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>此字段包含运行 <code>CmdletName</code> 字段中的 cmdlet 的用户的用户帐户。</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>此字段指定是否成功运行了 <code>CmdletName</code> 字段中的 cmdlet。值为 <code>True</code> 或 <code>False</code>。</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>此字段包含在 <code>CmdletName</code> 字段中的 cmdlet 未能成功完成时生成的错误消息。</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>此字段包含运行 <code>CmdletName</code> 字段中的 cmdlet 时的日期和时间。日期和时间存储为协调世界时 (UTC) 格式。</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>此字段指出 <code>CmdletName</code> 字段中指定的 cmdlet 在哪台服务器上运行。</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>此字段由 Exchange 在内部使用。</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>此字段由 Exchange 在内部使用。</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>此字段由 Exchange 在内部使用。</p></td>
</tr>
</tbody>
</table>


返回顶部

## EAC 审核报告

EAC 中的\&quot;审核\&quot;页面包括若干个报告，提供有关各种类型的合规性和管理配置更改的信息。以下报告提供有关您组织中的配置更改的信息：

  - **管理员角色组报告**   使用此报告可以搜索在指定时间段内对指定管理角色组所做的更改。返回的结果包括已更改的角色组、更改这些角色组的人员和时间以及进行了哪些更改。最多可以返回 3,000 个条目。如果搜索返回的条目可能超过 3,000 个，请使用\&quot;管理员审核日志\&quot;报告或 **Search-AdminAuditLog** cmdlet。

  - **管理员审核日志**   使用此报告可以将指定时间段内记录的审核日志条目导出到一个 XML 文件，然后通过电子邮件将该文件发送给您指定的收件人。有关 XML 文件内容的详细信息，请参阅[管理员审核日志结构](administrator-audit-log-structure-exchange-2013-help.md)。

有关如何使用这些报告的信息，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

有关\&quot;审核\&quot;页面中包括的其他报告的信息，请参阅[Exchange 审核报告](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports)。

## Search-AdminAuditLog cmdlet

在运行 **Search-AdminAuditLog** cmdlet 时，会返回与指定的搜索条件匹配的所有审核日志条目。可以指定以下搜索条件：

  - **Cmdlet**   指定要在管理员审核日志中搜索的 cmdlet。

  - **参数**   指定要在管理员审核日志中搜索的、以逗号分隔的参数。仅当指定了要搜索的 cmdlet 时，才能搜索参数。

  - **结束日期**   将管理员审核日志结果的范围限定为在指定日期当天或之前生成的日志条目。

  - **开始日期**   将管理员审核日志结果的范围限定为在指定日期当天或之后生成的日志条目。

  - **对象 ID**   指定仅返回包含指定更改对象的管理员审核日志条目

  - **用户 ID**   指定仅返回包含运行 cmdlet 的用户的指定 ID 的管理员审核日志条目。

  - **成功完成**   指定是应该仅返回指示成功的管理员审核日志条目，还是仅返回指示失败的管理员审核日志条目。

返回的每个审核日志条目都包含Audit Log Contents中的表所述的信息。默认情况下，仅返回与指定条件匹配的前 1,000 个日志条目。不过，可以使用 *ResultSize* 参数覆盖此默认设置并返回更多或更少的条目。可以使用 *ResultSize* 参数指定值 `Unlimited`，以返回与指定条件匹配的所有日志条目。

有关如何使用 **Search-AdminAuditLog** cmdlet 的信息，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

## New-AdminAuditLogSearch cmdlet

**New-AdminAuditLogSearch** cmdlet 如同 **Search-AdminAuditLog** cmdlet 一样，用于搜索审核日志。然而，**New-AdminAuditLogSearch** cmdlet 会执行搜索，然后通过电子邮件将搜索结果发送给指定的收件人，而不是在命令行管理程序中显示审核日志搜索的结果。结果作为 XML 附件包含在电子邮件中。

可以对 **New-AdminAuditLogSearch** cmdlet 使用与 **Search-AdminAuditLog** cmdlet 相同的搜索条件。有关搜索条件的列表，请参阅 Search-AdminAuditLog Cmdlet。

在运行 **New-AdminAuditLogSearch** cmdlet 之后，Exchange 可能最多需要 15 分钟将报告传递给指定收件人。附加了 XML 文件的报告最大可以为 10 MB。XML 文件包含Audit Log Contents中的表所述的相同信息。有关 XML 文件结构的详细信息，请参阅[管理员审核日志结构](administrator-audit-log-structure-exchange-2013-help.md)。

> [!NOTE]  
> 默认情况下，Outlook Web App 不允许您打开 XML 附件。您可以将 Exchange 配置为允许使用 Outlook Web App 查看 XML 附件，也可以使用其他电子邮件客户端（例如，Microsoft Outlook）查看该附件。有关如何将 Outlook Web App 配置为允许查看 XML 附件的信息，请参阅<a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">查看或配置 Outlook Web App 虚拟目录</a>。


有关如何使用 **New-AdminAuditLogSearch** cmdlet 的信息，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

返回顶部

## 手动审核日志条目

除了在 Exchange cmdlet 运行时对其进行记录以外，Exchange 2013 还允许您将日志条目手动写入审核日志。Exchange 2013 通过使用 **Write-AdminAuditLog** cmdlet 来支持这一点。可能需要添加手动日志条目的情况包括以下几种：

  - 自定义脚本进入和退出

  - 更改控制信息

  - 维护开始和结束时间

对于 **Write-AdminAuditLog** cmdlet，您可以使用 *Comment* 参数指定要包括在审核日志中的文本字符串。*Comment* 参数接受的字母数字字符串最多可包含 500 个字符。手动审核日志条目中包含的内容以及注释字符串便是在记录 Exchange cmdlet 时捕获的信息。有关审核日志中包括的每个字段的描述，请参阅Audit Log Contents中的表。

可以使用 EAC\&quot;审核\&quot;页面或者使用 **Search-AdminAuditLog** 或 **New-AdminAuditLogSearch** cmdlet，按照与检索任何其他日志条目相同的方式来检索手动审核日志条目。

若要查看手动审核日志条目中 **Write-AdminAuditLog** cmdlet 的 *Comment* 参数的内容，请参阅[搜索角色组更改或管理员审核日志](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)。

## Active Directory 复制

管理员审核日志记录依赖 Active Directory 复制功能将指定的配置设置复制到贵组织中的域控制器。根据复制设置，您所做的更改可能无法立即应用于组织中运行 Exchange 2013 或 Exchange 2010 的所有服务器。

## 管理审核日志代理

Admin Audit Log 内置 cmdlet 扩展代理执行对 Exchange 2013 中 cmdlet 操作的管理员审核日志记录。此代理读取审核日志配置，然后对组织中运行的每个 cmdlet 执行评估。如果您在审核日志配置中指定的条件与所运行的 cmdlet 匹配，则代理会生成审核日志。

默认情况下启用 Admin Audit Log 代理，此代理对于审核日志记录正常工作至关重要。不能将其禁用，并且不能更改其优先级。有关 cmdlet 扩展代理的详细信息，请参阅[cmdlet 扩展代理](cmdlet-extension-agents-exchange-2013-help.md)。

