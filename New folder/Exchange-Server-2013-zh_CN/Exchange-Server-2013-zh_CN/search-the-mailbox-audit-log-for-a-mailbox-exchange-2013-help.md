---
title: '搜索邮箱邮箱审核日志: Exchange 2013 Help'
TOCTitle: 搜索邮箱邮箱审核日志
ms:assetid: 5b518a08-3b51-4ba3-bfbd-0e35cc5ff374
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff461930(v=EXCHG.150)
ms:contentKeyID: 50490640
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 搜索邮箱邮箱审核日志

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

您可以同步搜索邮箱的邮箱审核日志条目，并在命令行管理程序中显示搜索结果。

如果您想要搜索多个邮箱的邮箱审核日志并有结果通过电子邮件发送到指定地址，您必须创建邮箱审核日志搜索。有关详细信息，请参阅[创建邮箱审核日志搜索](create-a-mailbox-audit-log-search-exchange-2013-help.md)。

关于邮箱审核日志记录的更多管理任务，请参阅[邮箱审核日志记录程序](mailbox-audit-logging-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮箱审核日志记录\&quot;条目。

  - 默认情况下，邮箱审核日志记录已禁用的所有邮箱。为您要审核的每个邮箱，必须启用审核日志记录并指定想要审计的邮箱所有者、 委托或管理员操作。有关详细信息，请参阅[启用或禁用邮箱的邮箱审核日志记录](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md)。

  - 您不能使用 EAC 搜索邮箱邮箱审核日志。但是，您可以使用 EAC 运行或搜索并导出非所有者邮箱访问报告。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序搜索邮箱的邮箱审核日志

有关如何使用命令行管理程序搜索邮箱的邮箱审核日志的示例，请参阅 [Search-MailboxAuditLog](https://technet.microsoft.com/zh-cn/library/ff522360\(v=exchg.150\)) 中的[Examples](https://technet.microsoft.com/zh-cn/ff522360\(exchg.150\)#examples)。

