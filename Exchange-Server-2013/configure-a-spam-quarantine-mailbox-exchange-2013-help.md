---
title: '配置垃圾邮件隔离邮箱: Exchange 2013 Help'
TOCTitle: 配置垃圾邮件隔离邮箱
ms:assetid: 907d2f90-2a62-4d59-a4cf-945fef2e963f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123746(v=EXCHG.150)
ms:contentKeyID: 50491160
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置垃圾邮件隔离邮箱

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-19_

由内容筛选器代理确定为垃圾邮件的邮件可转至垃圾邮件隔离邮箱。如果已启用垃圾邮件可信度 (SCL) 隔离阈值，则所有隔离的邮件都将打包为未送达报告 (NDR) 并发送到你指定作为邮件隔离邮箱的 SMTP 地址。你可以复查隔离的邮件，并可使用 Microsoft Outlook 中的\&quot;重新发送\&quot;功能将这些邮件释放给预定收件人。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：45 分钟。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 负责管理垃圾邮件隔离邮箱的人员可以查看潜在的私人和敏感邮件，然后代表 Exchange 组织中的任意人员发送邮件。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：验证是否启用了内容筛选功能

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

1.  运行下列命令验证 Exchange 服务器上是否已安装并启用了内容筛选器代理：
    
        Get-TransportAgent "Content Filter Agent"

2.  运行下列命令验证是否已启用了内容筛选功能：
    
        Get-ContentFilterConfig | Format-List Enabled

有关详细信息，请参阅[管理内容筛选](manage-content-filtering-exchange-2013-help.md)。

## 步骤 2：创建专门用于垃圾邮件隔离的邮箱

要创建一个专门的垃圾邮件隔离邮箱，请执行下列步骤：

  - **创建专用 Exchange 数据库**   建议你为垃圾邮件隔离邮箱创建专用数据库。垃圾邮件隔离邮箱应具有较大的数据库，因为如果达到存储配额限制，邮件将会丢失。有关详细信息，请参阅[管理 Exchange 2013 中的邮箱数据库](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)。

  - **创建专用的邮箱和用户帐户**   建议你创建专门的邮箱和 Active Directory 用户帐户以用于垃圾邮件隔离邮箱。有关详细信息，请参阅[创建用户邮箱](create-user-mailboxes-exchange-2013-help.md)。
    
    根据组织的合规性策略和需要，你可以应用各种收件人策略，如邮件记录管理、邮箱配额以及委派权限。有关详细信息，请参阅[邮件记录管理](messaging-records-management-exchange-2013-help.md)。
    
    > [!NOTE]
    > 如果某封隔离的邮件因为存储配额而遭到拒收，该邮件将会丢失。Exchange 不会为隔离的邮件生成 NDR，因为隔离的邮件将打包为 NDR。


  - **配置 Outlook**   你需要配置 Outlook 代理访问权限，以满足组织的各种需要。此外，还建议你配置 Outlook 配置文件，以便在\&quot;**邮件**\&quot;视图中显示原始的 `Sender[#0x0069001E]`、`Recipient[#0x0E04001E]` 和 `Bcc[#0x0E02001E]` 字段。有关详细信息，请参阅[从垃圾邮件隔离邮箱中释放隔离的邮件](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)。

## 步骤 3：指定垃圾邮件隔离邮箱

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

运行以下命令：

    Set-ContentFilterConfig -QuarantineMailbox <SmtpAddress>

本示例将所有超出垃圾邮件隔离阈值的邮件发送到 spamQ@contoso.com。

    Set-ContentFilterConfig -QuarantineMailbox spamQ@contoso.com

## 您如何知道此步骤有效？

要验证是否已成功指定了垃圾邮件隔离邮箱，请执行下列操作：

1.  运行以下命令：
    
        Get-ContentFilterConfig | Format-List QuarantineMailbox

2.  验证显示的值是否为您配置的值。

## 步骤 4：配置 SCL 隔离阈值

SCL 隔离阈值是一个值，标识为潜在垃圾邮件的特定邮件的 SCL 值达到此值时，将被传递到垃圾邮件隔离邮箱。你可以将 SCL 隔离阈值设置为 0 到 9 之间的一个值，其中 0 表示被视为垃圾邮件的可能性较低，9 表示被视为垃圾邮件的可能性最大。

有关如何调整 SCL 阈值以适应组织的要求以及如何调整每个收件人 SCL 阈值的详细信息，请参阅[管理内容筛选](manage-content-filtering-exchange-2013-help.md)。

## 步骤 5：管理垃圾邮件隔离邮箱

管理垃圾邮件隔离邮箱时，请按照下列指南操作：

  - 使用 Outlook 中的\&quot;重新发送\&quot;功能重新发送原始邮件，释放发送到垃圾邮件隔离邮箱的邮件。
    
    有关详细信息，请参阅[从垃圾邮件隔离邮箱中释放隔离的邮件](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md)。

  - 监视垃圾邮件隔离邮箱，以使该邮箱的大小保持在可接受的范围内。电子邮件的数量可能会因收件人数量的增多、邮件变大的自然趋势或者 SCL 隔离操作的阈值设置等因素而发生变化。

  - 监视垃圾邮件隔离邮箱的误报情况。如果你的垃圾邮件隔离邮箱包含许多误报，请调整 SCL 隔离阈值。有关如何确定向垃圾邮件隔离邮箱传递误报的原因的详细信息，请参阅[反垃圾邮件标记](anti-spam-stamps-exchange-2013-help.md)。

  - 使用相同的 Outlook 配置文件从垃圾邮件隔离邮箱中恢复隔离的邮件。不支持通过将权限应用于不同 Outlook 配置文件来恢复邮件。你不能使用不同的 Outlook 配置文件从垃圾邮件隔离邮箱中恢复或释放邮件。

> [!important]
> 被标识为垃圾邮件的未送达报告被删除，即使其 SCL 分级指示应隔离它们。不将未送达报告传递到垃圾邮件隔离邮箱。若要跟踪此类邮件，请使用代理日志或邮件跟踪日志。有关详细信息，请参阅<a href="anti-spam-agent-logging-exchange-2013-help.md">反垃圾邮件代理日志记录</a>。


## 步骤 6：调整 SCL 隔离阈值

配置 SCL 隔离阈值之后，定期监视其设置，并根据组织的需要对其进行调整。例如，如果过多误报邮件被筛选到垃圾邮件隔离邮箱，请将 SCL 隔离阈值提升到一个较大的数。有关如何调整 SCL 隔离阈值的详细信息，请参阅[垃圾邮件可信度阈值](spam-confidence-level-threshold-exchange-2013-help.md)。

