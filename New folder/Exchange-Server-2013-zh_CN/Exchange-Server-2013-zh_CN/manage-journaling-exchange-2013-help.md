---
title: '管理日记: Exchange 2013 Help'
TOCTitle: 管理日记
ms:assetid: d517f27e-f80a-4a06-988c-cbbf981c701d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ651670(v=EXCHG.150)
ms:contentKeyID: 50491733
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理日记

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

通过记录入站和出站电子邮件通信，日记功能可以帮助组织符合法律法规和组织合规性要求。本主题展示了如何执行与管理 Exchange 2013 和 Exchange Online 中日记相关的基本任务。

标准日记是在邮箱数据库上配置的。通过使用标准日记，日记代理能够记录特定邮箱数据库中的邮箱所接收和发送的所有邮件。您也可使用高级日记，让日记代理能够使用日记规则执行更详细的日记记录。可以通过记录单个收件人或通讯组成员来配置日记规则，以满足组织的需要，而不是记录邮箱数据库上驻留的所有邮箱。您必须拥有 Exchange Enterprise 客户端访问许可证 (CAL) 才能使用高级日记。

有关日记的详细信息，请参阅[日记](journaling-exchange-2013-help.md)。

**目录**

创建日记规则

查看或修改日记规则

启用或禁用日记规则

删除日记规则

每邮箱数据库启用或禁用日记功能

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“日记功能”条目。

  - 已经创建了日记邮箱，或现有邮箱可用作日记邮箱。不能将 Exchange Online 邮箱指定为日记邮箱。不能将日记报告传递给本地存档系统或第三方存档服务。如果运行将邮箱在本地服务器与 Exchange Online 之间进行拆分的混合部署，则可以将本地邮箱指定为 Exchange Online 和本地邮箱的日记邮箱。
    
    > [!important]
    > 如果你已在 Exchange Online 中将日记规则配置为向不存在或目标无效的日记邮箱发送日记报告，日记报告会保留在 Microsoft 数据中心服务器上的传输队列中。如果发生这种情况，Microsoft 数据中心工作人员会尝试联系你的组织，要求你解决此问题，以便日记报告能够成功传递到日记邮箱。如果你在联系两天后还没有解决此问题，Microsoft 会禁用有问题的日记规则。


  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。如果无法使用 <strong>JournalingReportDNRTo</strong> 邮箱，请参阅 <a href="https://go.microsoft.com/fwlink/p/?linkid=331674">Transport and Mailbox Rules in Exchange Online don’t work as expected</a>（Exchange Online 中的传输和邮箱规则不按预期运行）。


## 创建日记规则

## 使用 EAC 创建日记规则

1.  在 EAC 中，转至“**合规性管理**”\>“**日记规则**”，然后单击“**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")”。

2.  在“日记规则”中，为日记规则提供名称，然后完成以下字段：
    
      - “如果已发送或接收消息”   指定作为规则目标的收件人。您可选择特定收件人或将规则应用至所有邮件。
    
      - “记录以下邮件”   指定日记规则的范围。可只记录内部邮件、外部邮件或记录所有邮件而不考虑来源和目的地。
    
      - “将日志报告发送到”   键入将接收所有日志报告的日记邮箱的地址。
        
        > [!NOTE]
        > 还可以键入邮件用户或邮件联系人的显示名称或别名作为日记邮箱。在这种情况下，日记报告将发送到邮件用户或邮件联系人的外部电子邮件地址。但正如前面所述，邮件用户或邮件联系人的外部电子邮件地址不能作为 Exchange Online 邮箱的地址。


3.  单击“保存”可以创建日记规则。

## 使用命令行管理程序创建日记规则

本示例将创建日记规则 Discovery 日记收件人，记录由收件人 user1@contoso.com 发送和接收的所有邮件。

    New-JournalRule -Name "Discovery Journal Recipients" -Recipient user1@contoso.com -JournalEmailAddress "Journal Mailbox" -Scope Global -Enabled $True

## 您如何知道这有效？

要检查是否成功创建了日记规则，可进行以下操作之一：

  - 从 EAC 确认“日记规则”选项卡上是否列出了您创建的新日记规则。

  - 在命令行管理程序中，通过运行以下命令检查是否存在新日记规则（下面的示例验证了在上面的命令行管理程序示例中创建的规则）：
    
        Get-JournalRule "Discovery Journal Recipients"

返回顶部

## 查看或修改日记规则

## 使用 EAC 查看或修改日记规则

1.  在 EAC 中，转至“**合规性管理**”\>“**日记规则**”。

2.  在列表视图中，将看到组织中的所有日记规则。

3.  双击您要查看或修改的规则。

4.  在“日记规则”中修改所需的设置。有关该对话框中设置的详细信息，请参阅本主题中之前的步骤使用 EAC 创建日记规则。

## 使用命令行管理程序查看或修改日记规则

本示例显示 Exchange 组织中所有日记规则的摘要列表：

    Get-JournalRule

此示例检索“Brokerage Journal Rule”日记规则，将输出通过管道传递给 **Format-List** 命令以使用列表格式显示规则属性：

    Get-JournalRule "Brokerage Journal Rule" | Format-List

如果您希望修改特定规则的属性，则需要使用 [Set-JournalRule](https://technet.microsoft.com/zh-cn/library/bb125010\(v=exchg.150\)) cmdlet。本示例将日记规则名称从 `JR-Sales` 更改为 `TraderVault`。还会更改下列规则设置：

  - 收件人

  - JournalEmailAddress

  - 范围

<!-- end list -->

    Set-JournalRule JR-Sales -Name TraderVault -Recipient traders@woodgrovebank.com -JournalEmailAddress tradervault@woodgrovebank.com -Scope Internal

## 您如何知道这有效？

要检查是否成功修改了日记规则，可进行以下操作之一：

  - 在 EAC 中，导航到“合规管理”\>“日记规则”。双击您修改的规则并验证您的更改是否已保存。

  - 在命令行管理程序中，通过运行以下命令验证是否成功修改了日记规则。该命令将列出您修改的属性以及规则的名称（下面的示例验证了在上面的命令行管理程序示例中修改的规则）：
    
        Get-TransportRule "TraderVault" | Format-List Name,Recipient,JournalEmailAddress,Scope

返回顶部

## 启用或禁用日记规则

> [!important]
> 如果禁用日记规则，日记代理将停止记录作为规则目标的邮件。如果禁用了日记规则，则不会记录通常会记录的所有邮件。确保禁用日记规则不会违反您组织的规章或合规要求。


## 使用 EAC 启用或禁用日记规则

1.  在 EAC 中，转至“**合规性管理**”\>“**日记规则**”。

2.  在列表视图中，则规则名称旁的“开”列中，选择复选框来启用规则或清除复选框来禁用规则。

## 使用命令行管理程序启用或禁用日记规则

本示例启用规则 Contoso。

    Enable-JournalRule "Contoso Journal Rule"

本示例将禁用规则 Contoso。

    Disable-JournalRule "Contoso Journal Rule"

## 您如何知道这有效？

要检查是否成功启用或禁用了日记规则，可进行以下操作之一：

  - 在 EAC 中，查看日记规则列表，检查“开”列中复选框的状态。

  - 在命令行管理程序中，运行以下命令来返回组织中所有日记规则的列表并附带其状态：
    
        Get-JournalRule | Format-Table Name,Enabled

返回顶部

## 删除日记规则

## 使用 EAC 删除日记规则

1.  在 EAC 中，转至“**合规性管理**”\>“**日记规则**”。

2.  在列表视图中，选择您要删除的规则，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

## 使用命令行管理程序删除日记规则

本示例删除规则“代理日记规则”。

    Remove-JournalRule "Brokerage Journal Rule"

## 您如何知道这有效？

要检查是否成功删除了日记规则，可进行以下操作之一：

  - 从 EAC 确认“日记规则”选项卡上是否不再列出了您已删除的规则。

  - 在命令行管理程序中，运行以下命令检查是否不再列出您删除的规则：
    
        Get-JournalRule

返回顶部

## 启用或禁用每个邮箱数据库日记功能

> [!CAUTION]
> 在邮箱数据库上禁用邮件日记可能导致您的组织违反相应的邮件保留政策。如果在邮箱数据库上禁用邮件日记，则对通过该邮箱数据库上的邮箱收发的邮件将不再发送日记回执。


## 使用 EAC 启用或禁用每个邮箱数据库日记功能

1.  在 EAC 中，转到“服务器”\>“数据库”。

2.  在列表视图中，双击要对其启用日记的邮箱数据库。

3.  单击“维护”，然后单击“日记收件人”框旁边的“浏览”来选择日记邮箱。指定日记收件人来启用数据库的日记。
    
    若要禁用日记功能，通过单击“删除 X”删除日记收件人。

## 使用命令行管理程序启用或禁用每个邮箱数据库日记功能

该示例为邮箱数据库“销售数据库”启用日记并将“销售数据库”日记邮箱设置为日记收件人。

    Set-MailboxDatabase "Sales Database" -JournalRecipient "Sales Database Journal Mailbox"

本示例禁用“销售数据库”邮箱数据库上的每个邮箱数据库日记功能。

    Set-MailboxDatabase "Sales Database" -JournalRecipient $Null

本示例禁用 Exchange 组织中所有邮箱数据库上的每个邮箱数据日记功能。[Get-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb124924\(v=exchg.150\)) cmdlet 用于检索 Exchange 组织中的所有邮箱数据库，并且来自 cmdlet 的结果会传送至 [Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\)) cmdlet。

    Get-MailboxDatabase | Set-MailboxDatabase -JournalRecipient $Null

## 您如何知道这有效？

要检查是否成功启用或禁用了每个邮箱数据库日记功能，可进行以下操作之一：

1.  在 EAC 中，转到“服务器”\>“数据库”。

2.  双击要验证的数据库，然后选择“维护”选项卡。

3.  如果在“日记收件人”框中列出了正确的日记收件人，则为邮箱数据库成功启用了日记功能。如果未列出日记收件人，则会禁用数据库的日记功能。

<!-- end list -->

  - 在命令行管理程序中，运行以下命令来返回组织中所有邮箱数据库的列表并附带与它们关联的日记收件人：为列出了日记收件人的数据库启用日记功能，如果未列出会禁用日记。
    
        Get-MailboxDatabase | Format-Table Name,JournalRecipient

返回顶部

## 详细信息

[日记](journaling-exchange-2013-help.md)

[禁用或启用语音邮件和未接来电通知的日记功能](disable-or-enable-journaling-of-voice-mail-and-missed-call-notifications-exchange-2013-help.md)

[New-JournalRule](https://technet.microsoft.com/zh-cn/library/bb125242\(v=exchg.150\))

[Get-JournalRule](https://technet.microsoft.com/zh-cn/library/aa998866\(v=exchg.150\))

[Set-JournalRule](https://technet.microsoft.com/zh-cn/library/bb125010\(v=exchg.150\))

[Enable-JournalRule](https://technet.microsoft.com/zh-cn/library/bb123902\(v=exchg.150\))

[Disable-JournalRule](https://technet.microsoft.com/zh-cn/library/aa995925\(v=exchg.150\))

[Remove-JournalRule](https://technet.microsoft.com/zh-cn/library/bb123489\(v=exchg.150\))

[Set-MailboxDatabase](https://technet.microsoft.com/zh-cn/library/bb123971\(v=exchg.150\))

