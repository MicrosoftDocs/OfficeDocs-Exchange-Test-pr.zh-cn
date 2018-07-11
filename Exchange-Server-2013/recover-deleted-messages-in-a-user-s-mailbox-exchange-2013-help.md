---
title: '恢复用户邮箱中的已删除邮件: Exchange 2013 Help'
TOCTitle: 恢复用户邮箱中的已删除邮件
ms:assetid: 9e0e34ce-efc5-454e-8d15-57b4da867f12
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff660637(v=EXCHG.150)
ms:contentKeyID: 50556622
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 恢复用户邮箱中的已删除邮件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

（本主题目标用户是 Exchange 管理员。）

管理员可以搜索和恢复用户邮箱中的已删除电子邮件。这包括用户永久删除（清除）的项目（可使用 Outlook 或 Outlook Web App 中的“恢复已删除项目”功能进行恢复）或由自动进程删除的项目（如分配到用户邮箱的保留策略）。在这种情况下，用户无法恢复已清除的项目。不过，如果已删除项目的保留期尚未过期，则管理员可以恢复已清除的邮件。

> [!NOTE]  
> 除了使用此步骤搜索并恢复删除的项目（如果启用了单个项目恢复或诉讼保留，则会将这些项目移动到 Recoverable Items\Purges 文件夹中）外，还可以使用此步骤搜索驻留在邮箱中其他文件夹的项目并从源邮箱删除项目（也称为“搜索和破坏”）。


## 在开始之前，您需要知道什么？

  - 估计完成时间：15-30 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 在删除要恢复的项目之前，必须为邮箱启用单个项目恢复。在 Exchange Online 中，在您新建邮箱时，系统会默认启用单个项目恢复。在 Exchange 2013 中，在您创建邮箱时，系统会禁用单个项目恢复。有关详细信息，请参阅[启用或禁用邮箱的单个项目恢复](enable-or-disable-single-item-recovery-for-a-mailbox-exchange-2013-help.md)。

  - 要搜索并恢复项目，必须拥有以下信息：
    
      - **源邮箱**   源邮箱指要搜索的邮箱。
    
      - **目标邮箱**   目标邮箱指将要恢复其中的邮件的发现邮箱。Exchange 安装程序将创建一个默认发现邮箱。Exchange Online 中也会默认创建发现邮箱。如果需要，您可以创建其他发现邮箱。有关详细信息，请参阅[创建发现邮箱](create-a-discovery-mailbox-exchange-2013-help.md)。
        
        > [!NOTE]  
        > 使用 <strong>Search-Mailbox</strong> cmdlet 时，也可以指定不是发现邮箱的目标邮箱。但是，不能将同一个邮箱指定为源邮箱和目标邮箱。
    
      - **搜索条件**   条件包括发件人、收件人或邮件中的关键字（词或短语）。

  - 本主题集中讲述如何使用 PowerShell 来恢复用户邮箱中已删除的项目。你还可以使用基于 GUI 的就地电子数据展示工具查找已删除的项目并将其导出为 PST 文件。用户将使用此 PST 文件将已删除的邮件还原到其邮箱中。有关详细说明，请参阅[恢复用户邮箱中已删除的项目 - 管理员帮助](https://go.microsoft.com/fwlink/p/?linkid=722928)。

## （可选）第 1 步：使用远程 PowerShell 连接到 Exchange Online

如果您具有 Exchange Online 或 Office 365 组织，您仅需执行此步骤。如果您具有 Exchange 2013 组织，转到下一步，并在 Exchange 命令行管理程序 中运行命令。

1.  在本地计算机上，打开 Windows PowerShell 并运行以下命令。
    
        $UserCredential = Get-Credential
    
    在“Windows PowerShell 凭据请求”对话框中，键入 Office 365 全局管理员帐户的用户名和密码，然后单击“确定”。

2.  运行以下命令。
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  运行以下命令。
    
        Import-PSSession $Session

4.  要验证您是否已连接至您的 Exchange Online 组织，请运行以下命令获取组织中所有邮箱的列表。
    
        Get-Mailbox

有关详细信息，或者如果您在连接到 Exchange Online 组织时遇到问题，请参阅[使用远程 PowerShell 连接到 Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=517283)。

## 步骤 2：搜索并恢复缺失项目

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地 eDiscovery”条目。

> [!NOTE]  
> 您可以在 Exchange 管理中心 (EAC) 中使用就地电子数据展示来搜索缺少的项目。但是，在使用 EAC 时，不能将搜索限制到“可恢复的项目”文件夹。即使是未删除的邮件，也会作为与搜索参数匹配的邮件返回。在将邮件恢复到指定的发现邮箱之后，可能需要检查搜索结果并删除不必要的邮件，然后将剩余的邮件恢复到用户的邮箱或将其导出到 .pst 文件。<br />
> 有关如何使用 EAC 执行 In-Place eDiscovery 搜索的详细信息，请参阅<a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">创建就地电子数据展示搜索</a>。


恢复进程的第一步是在源邮箱中搜索邮件。使用以下方法之一来搜索用户邮箱并将邮箱复制到发现邮箱。

此示例在 April Stewart 的邮箱中搜索符合以下条件的邮件：

  - 发件人：Ken Kwok

  - 关键字：西雅图

<!-- end list -->

    Search-Mailbox "April Stewart" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "Discovery Search Mailbox" -TargetFolder "April Stewart Recovery" -LogLevel Full

> [!NOTE]  
> 使用 <strong>Search-Mailbox</strong> cmdlet 时，可以通过使用 <em>SearchQuery</em> 参数来指定使用关键字查询语言 (KQL) 设置格式的查询来界定搜索范围。也可以使用 <em>SearchDumpsterOnly</em> 开关，以便仅搜索“可恢复的项目”文件夹中的项目。


有关详细的语法和参数信息，请参阅 [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))。

**您如何知道这有效？**

若要验证是否已成功搜索要恢复的邮件，请登录到选择为目标邮箱的发现邮箱，然后检查搜索结果。

## 第 3 步：还原已恢复的项目

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地 eDiscovery”条目。

> [!NOTE]  
> 不能使用 EAC 还原已恢复的项目。


将邮件恢复到发现邮箱后，可以使用 **Search-Mailbox** cmdlet 将邮件还原到用户的邮箱中。在 Exchange 2013 中，您还可以使用 **New-MailboxExportRequest** 和 **New-MailboxImportRequest** cmdlet 将邮件导出到 .pst 文件或从中导入邮件。

## 使用命令行管理程序还原邮件

此示例将邮件还原到 April Stewart 的邮箱并将邮件从发现搜索邮箱中删除。

    Search-Mailbox "Discovery Search Mailbox" -SearchQuery "from:'Ken Kwok' AND seattle" -TargetMailbox "April Stewart" -TargetFolder "Recovered Messages" -LogLevel Full -DeleteContent

有关语法和参数的详细信息，请参阅 [Search-Mailbox](https://technet.microsoft.com/zh-cn/library/dd298173\(v=exchg.150\))。

**您如何知道这有效？**

若要验证是否已成功将邮件恢复到用户的邮箱，请让用户检查在上面的命令中指定的目标文件夹中的邮件。

## (Exchange 2013) 使用命令行管理程序将邮件导出到 .pst 文件或从中导入邮件

在 Exchange 2013 中，您可以将邮箱的内容导出到 .pst 文件中，也可以将 .pst 文件的内容导入到邮箱中。要了解有关邮箱导入和导出的详细信息，请参阅[邮箱导入和导出请求](mailbox-import-and-export-requests-exchange-2013-help.md)。您无法在 Exchange Online 中执行此任务。

此示例使用以下设置将发现搜索邮箱中的“April Stewart 恢复”文件夹中的邮件导出到 .pst 文件：

  - **邮箱**   发现搜索邮箱

  - **源文件夹**   April Stewart 恢复

  - **ContentFilter**   四月旅行计划

  - **PST 文件路径**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxExportRequest -Mailbox "Discovery Search Mailbox" -SourceRootFolder "April Stewart Recovery" -ContentFilter {Subject -eq "April travel plans"} -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst

有关详细的语法和参数信息，请参阅 [New-MailboxExportRequest](https://technet.microsoft.com/zh-cn/library/ff607299\(v=exchg.150\))。

此示例使用以下设置将邮件从 .pst 文件中导入到 April Stewart 邮箱中的“由支持人员恢复”文件夹：

  - **邮箱**   April Stewart

  - **目标文件夹**   由支持人员恢复

  - **PST 文件路径**   \\\\MYSERVER\\HelpDeskPst\\AprilStewartRecovery.pst

<!-- end list -->

    New-MailboxImportRequest -Mailbox "April Stewart" -TargetRootFolder "Recovered By Helpdesk" -FilePath \\MYSERVER\HelpDeskPst\AprilStewartRecovery.pst 

有关详细的语法和参数信息，请参阅 [New-MailboxImportRequest](https://technet.microsoft.com/zh-cn/library/ff607310\(v=exchg.150\))。

**您如何知道这有效？**

若要验证是否已成功将邮件导出到 .pst 文件，请使用 Outlook 打开 .pst 文件并检查其内容。若要验证是否已成功从 .pst 文件导入邮件，请让用户检查在上面的命令中指定的目标文件夹中的内容。

## 详细信息

  - 能否恢复已删除项目取决于*单个项目恢复*是否已启用；启用后，只要已删除项目的保留期尚未过期，管理员就可以恢复已由用户或保留策略清除的邮件。若要详细了解单个项目恢复，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

  - 默认情况下，Exchange Online 邮箱的已删除项目的保留期配置为 14 天。您最多可以将此设置更改为 30 天。在 Exchange 2013 中，邮箱数据库的已删除项目的保留期默认配置为 14 天。您可以配置邮箱或邮箱数据库的已删除项目的保留设置。有关详细信息，请参阅：
    
      - [更改为 Exchange Online 邮箱保留永久删除的项目的时间](https://technet.microsoft.com/zh-cn/library/dn163584\(v=exchg.150\))
    
      - [配置已删除邮件的保留时间和可恢复邮件配额](configure-deleted-item-retention-and-recoverable-items-quotas-exchange-2013-help.md)

  - 如之前所述，你还可以使用就地电子数据展示工具查找已删除的项目并将其导出为 PST 文件。用户将使用此 PST 文件将已删除的邮件还原到其邮箱中。有关详细说明，请参阅[恢复用户邮箱中已删除的项目 - 管理员帮助](https://go.microsoft.com/fwlink/p/?linkid=722928)。

  - 如果项目尚未清除且已删除项目的保留期尚未过期，则用户可以恢复已删除项目。如果用户需要从“可恢复的项目”文件夹中恢复已删除项目，应指导他们阅读下列主题：
    
      - [在 Outlook 2010 中恢复已删除的项目](https://go.microsoft.com/fwlink/p/?linkid=524923)
    
      - [在 Outlook 2013 中恢复已删除的项目](https://go.microsoft.com/fwlink/p/?linkid=624829)
    
      - [在 Outlook Web App 中恢复已删除的项目或电子邮件](https://go.microsoft.com/fwlink/p/?linkid=524924)

  - 此主题介绍了如何使用 **Search-Mailbox** cmdlet 来搜索和恢复缺少的项目。如果使用此 cmdlet，则一次只能搜索一个邮箱。如果您想同时搜索多个邮箱，则可以在 Exchange 管理中心 (EAC) 中使用[就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)，或在 Windows PowerShell 中使用 [New-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298064\(v=exchg.150\)) cmdlet。

  - 除了按照此步骤操作来搜索和恢复已删除项目之外，您还可以按照相似的步骤操作，搜索用户邮箱中的项目，然后从源邮箱中删除这些项目。有关详细信息，请参阅[搜索和删除邮件 - 管理员帮助](search-for-and-delete-messages-admin-help-exchange-2013-help.md)。

