---
title: '搜索角色组更改或管理员审核日志: Exchange 2013 Help'
TOCTitle: 搜索角色组更改或管理员审核日志
ms:assetid: c7188d53-e672-492b-b57d-cd711379ddb3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff459262(v=EXCHG.150)
ms:contentKeyID: 50553917
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 搜索角色组更改或管理员审核日志

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2013-12-02_

您可以搜索管理员审核日志以查找更改组织、服务器和收件人配置的用户。这对尝试跟踪发生意外行为的原因、标识恶意管理员或者验证是否满足遵从性要求都很有帮助。有关管理员审核日志记录的详细信息，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。

如果要搜索邮箱审核日志，请参阅[邮箱审核日志记录](mailbox-audit-logging-exchange-2013-help.md)。

> [!TIP]  
> 在 Exchange Online 中，您可以使用 EAC 来查看管理员审核日志中的条目。有关详细信息，请参阅<a href="view-the-administrator-audit-log-exchange-2013-help.md">查看管理员审核日志</a>。


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：少于 5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的“仅查看管理员审核日志记录”条目。

  - 默认情况下，将启用管理员审核日志记录。若要验证是否已启用，请运行以下命令：
    
        Get-AdminAuditLogConfig | FL AdminAuditLogEnabled
    
    值为 `True` 表示管理员审核日志记录已启用。值为 `False` 表示已禁用。如果需要为内部部署 Exchange 组织启用管理员审核日志记录，请运行以下命令：
    
        Set-AdminAuditLogConfig -AdminAuditLogEnabled $true
    
    > [!NOTE]  
    > <strong>Set-AdminAuditLogConfig</strong> cmdlet 在 Exchange Online 中不可用。
    
    有关详细信息，请参阅[管理管理员审核日志记录](manage-administrator-audit-logging-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 运行管理角色组更改报告

如果要了解对组织中角色组的管理角色组成员身份所做的更改，可以在 Exchange 管理中心 (EAC) 使用“管理员角色组”报告。使用“管理员角色组”报告，可以查看指定日期范围内已更改的角色组的列表。还可以选择要查看其更改的特定角色组。

1.  在 EAC 中，选择“合规性管理”\>“审核”，然后单击“运行管理员角色组报告”。

2.  使用“开始日期”和“结束日期”字段选择日期范围。

3.  单击“选择角色组”，然后选择要显示其更改的角色组，或者将此字段留空以便在所有角色组中搜索更改。

4.  单击“搜索”。

如果使用指定的条件找到了所有更改，则会在结果窗格中显示更改列表。单击角色组可在详细信息窗格中显示对此角色组的更改。

## 使用 EAC 导出管理员审核日志

如果要创建包含对组织所做更改的 XML 文件，可以在 EAC 中使用“导出管理审核日志”报告。使用“导出管理审核日志”报告，可以指定搜索包含指定用户所做的更改的审核日志条目时所用的日期范围。随后会将 XML 文件以电子邮件附件的形式发送给收件人。该 XML 文件的最大大小为 10 兆字节 (MB)。

> [!NOTE]  
> 默认情况下，Outlook Web App 不允许您打开 XML 附件。您可以将 Exchange 配置为允许使用 Outlook Web App 查看 XML 附件，也可以使用其他电子邮件客户端（例如，Microsoft Outlook）查看该附件。有关如何将 Outlook Web App 配置为允许查看 XML 附件的信息，请参阅<a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">查看或配置 Outlook Web App 虚拟目录</a>。


1.  在 EAC 中，选择“合规性管理”\>“审核”，然后单击“导出管理员审核日志”。

2.  使用“开始日期”和“结束日期”字段选择日期范围。

3.  在“将审核报告发送到”字段中，单击“选择用户”，然后选择要将报告发送到的收件人。

4.  单击“导出”。

如果使用指定的条件找到了所有日志条目，将创建一个 XML 文件，并将其以电子邮件附件的形式发送给指定的收件人。

## 使用命令行管理程序搜索审核日志条目

可以使用命令行管理程序搜索满足指定条件的审核日志条目。有关搜索条件列表，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。此过程将使用 **Search-AdminAuditLog** cmdlet 并在命令行管理程序中显示搜索结果。如果需要返回超出在 **New-AdminAuditLogSearch** cmdlet 或 EAC“审核报告”报告中定义的限制的一组结果时，可使用此 cmdlet。

如果要以电子邮件附件的形式将审核日志搜索结果发送给收件人，请参阅本主题后面的使用命令行管理程序搜索审核日志条目并将结果发送给收件人。

若要搜索满足指定条件的审核日志，请使用以下语法。

    Search-AdminAuditLog - Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False >

> [!NOTE]  
> 默认情况下，<strong>Search-AdminAuditLog</strong> cmdlet 最多可返回 1,000 个日志条目。使用 <em>ResultSize</em> 参数最多可指定 250,000 个日志条目。或使用 <code>Unlimited</code> 值可返回所有条目。


本示例将使用以下条件执行对所有审核日志条目的搜索：

  - **开始日期**   2012-8-4

  - **结束日期**   10/03/2012

  - **用户 ID**   davids、chrisd、kima

  - **Cmdlets** **Set-Mailbox**

  - **参数** *ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

<!-- end list -->

    Search-AdminAuditLog -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima

本示例将搜索对特定邮箱所做的更改。此操作在进行故障排除或需要为调查提供信息时很有用。使用以下条件：

  - **开始日期**   2012-5-1

  - **结束日期**   10/03/2012

  - **对象 ID** contoso.com/Users/DavidS

<!-- end list -->

    Search-AdminAuditLog -StartDate 05/01/2012 -EndDate 10/03/2012 -ObjectID contoso.com/Users/DavidS

如果搜索返回多个日志条目，我们建议您使用本主题后面的使用命令行管理程序搜索审核日志条目并将结果发送给收件人中提供的过程。该部分提供的过程将 XML 文件以电子邮件附件的形式发送给指定的收件人，从而使您更易于提取您感兴趣的数据。

有关详细的语法和参数信息，请参阅 [Search-AdminAuditLog](https://technet.microsoft.com/zh-cn/library/ff459250\(v=exchg.150\))。

## 查看审核日志条目的详细信息

**Search-AdminAuditLog** cmdlet 可返回 [管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)的“审核日志内容”部分中介绍的字段。在此 cmdlet 返回的字段中，**CmdletParameters** 和 **ModifiedProperties** 两个字段包含默认情况下不可见的附加信息。

若要查看 **CmdletParameters** 和 **ModifiedProperties** 字段的内容，请执行以下步骤。或者，可以使用本主题后面的使用命令行管理程序搜索审核日志条目并将结果发送给收件人中的过程创建 XML 文件。

此过程将使用以下概念：

  - [数组](https://technet.microsoft.com/zh-cn/library/aa998267\(v=exchg.150\))

  - [用户定义的变量](https://technet.microsoft.com/zh-cn/library/bb123690\(v=exchg.150\))

<!-- end list -->

1.  确定搜索时要使用的条件，然后运行 **Search-AdminAuditLog** cmdlet，并使用以下命令将结果存储在一个变量中。
    
        $Results = Search-AdminAuditLog <search criteria>

2.  每个审核日志条目都将作为数组元素存储在变量 `$Results` 中。可以通过指定其数组元素索引来选择数组元素。数组元素索引以零 (0) 开始，即第一个数组元素的索引为 0。例如，如果要检索第 5 个数组元素，其索引为 4，则应使用以下命令进行检索。
    
        $Results[4]

3.  上述命令将返回数组元素 4 中存储的日志条目。若要查看此日志条目的 **CmdletParameters** 和 **ModifiedProperties** 字段的内容，请使用以下命令。
    
        $Results[4].CmdletParameters
        $Results[4].ModifiedProperties

4.  若要查看其他日志条目的 **CmdletParameters** 或 **ModifiedParameters** 字段的内容，请更改数组元素索引。

## 使用命令行管理程序搜索审核日志条目并将结果发送给收件人

可以使用命令行管理程序搜索满足指定条件的审核日志条目，然后将这些结果以 XML 文件附件的形式发送给指定的收件人。这些结果将在 15 分钟内发送给收件人。有关搜索条件列表，请参阅[管理员审核日志记录](administrator-audit-logging-exchange-2013-help.md)。

> [!NOTE]  
> 默认情况下，Outlook Web App 不允许您打开 XML 附件。您可以将 Exchange 配置为允许使用 Outlook Web App 查看 XML 附件，也可以使用其他电子邮件客户端（例如，Microsoft Outlook）查看该附件。有关如何将 Outlook Web App 配置为允许查看 XML 附件的信息，请参阅<a href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">查看或配置 Outlook Web App 虚拟目录</a>。


若要搜索满足指定条件的审核日志，请使用以下语法。

    New-AdminAuditLogSearch -Cmdlets <cmdlet 1, cmdlet 2, ...> -Parameters <parameter 1, parameter 2, ...> -StartDate <start date> -EndDate <end date> -UserIds <user IDs> -ObjectIds <object IDs> -IsSuccess <$True | $False > -StatusMailRecipients <recipient 1, recipient 2, ...> -Name <string to include in subject>

本示例将使用以下条件执行对所有审核日志条目的搜索：

  - **开始日期**   2012-8-4

  - **结束日期**   10/03/2012

  - **用户 ID**   davids、chrisd、kima

  - **CmdletsSet-Mailbox**

  - **参数***ProhibitSendQuota*、*ProhibitSendReceiveQuota*、*IssueWarningQuota*、*MaxSendSize*、*MaxReceiveSize*

此命令将结果发送到 davids@contoso.com SMTP 地址，邮件主题中包含“邮件限制更改”。

    New-AdminAuditLogSearch -Cmdlets Set-Mailbox -Parameters ProhibitSendQuota, ProhibitSendReceiveQuota, IssueWarningQuota, MaxSendSize, MaxReceiveSize -StartDate 08/04/2012 -EndDate 10/03/2012 -UserIds davids, chrisd, kima -StatusMailRecipients davids@contoso.com -Name "Mailbox limit changes"

> [!NOTE]  
> <strong>New-AdminAuditLogSearch</strong> cmdlet 生成的报告最大大小为 10 MB。如果执行的搜索返回了大于 10 MB 的报告，则应更改指定的搜索条件。例如，缩小日期范围大小并运行多个报告，其中每个报告的日期范围都为原始日期范围的一部分。


有关 XML 文件格式的详细信息，请参阅[管理员审核日志结构](administrator-audit-log-structure-exchange-2013-help.md)。

有关详细的语法和参数信息，请参阅 [New-AdminAuditLogSearch](https://technet.microsoft.com/zh-cn/library/ff459243\(v=exchg.150\))。

