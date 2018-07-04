---
title: '启用或禁用电子邮件发送的邮件联系人: Exchange 2013 Help'
TOCTitle: 启用或禁用电子邮件发送的邮件联系人
ms:assetid: ca47441f-1aa4-4958-aba5-18d51e59837e
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124552(v=EXCHG.150)
ms:contentKeyID: 50556660
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用电子邮件发送的邮件联系人

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-12-05_

您可以在 Exchange 组织中禁用现有邮件联系人的电子邮件。禁用邮件联系人的电子邮件时，它将从交换和您的组织的通讯簿中删除。如果邮件联系人通讯组的成员，该联系人将不再接收发送到组的邮件。此外，Exchange 属性已从 Active Directory 中的已启用邮件的联系人对象，但联系人和非 Exchange 属性 （如联系人和组织信息） 会保留在 Active Directory 中。

禁用邮件联系人的电子邮件后，您可以启用邮件联系人再次通过在 Shell 中使用**Enable-MailContact** cmdlet。您还可以使用此 cmdlet 以启用任何 Active Directory 联系人的邮件。

有关与邮件联系人相关的其他管理任务，请参阅[管理邮件联系人](manage-mail-contacts-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮件联系人\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 禁用邮件联系人的电子邮件

如上文所述，当禁用邮件联系人的电子邮件时，Exchange 属性会从相应的 Active Directory 联系对象，但保留联系人。邮件联系人从联系人列表中邮件中 EAC，但您可以查看和管理相应的 Active Directory 联系对象，通过使用 Active Directory 用户和计算机或通过在 Shell 中使用的**Get-Contact**和**Set-Contact**的 cmdlet。

## 使用 EAC 禁用邮件联系人的电子邮件

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;。

2.  在联系人列表中，单击要禁用其电子邮件的邮件联系人。

3.  单击\&quot;更多\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，然后单击\&quot;禁用\&quot;。

4.  如果您不确定您想要禁用选定的邮件联系人，将显示一条警告询问。单击**是**以将其禁用。

此时将从联系人列表中删除邮件联系人。

## 使用命令行管理程序禁用邮件联系人的电子邮件

此示例禁用邮件联系人 Neil Black 的电子邮件。

    Disable-MailContact -Identity "Neil Black"

有关详细的语法和参数信息，请参阅[Disable-MailContact](https://technet.microsoft.com/zh-cn/library/aa997465\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功禁用了邮件联系人的电子邮件，请执行以下操作之一：

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;，然后验证是否不再列出邮件联系人。

2.  在 Active Directory 用户和计算机，用鼠标右键单击联系人，然后单击**属性**。在**常规**选项卡中，请注意**电子邮件**框中为空。这将验证该联系人不是已启用邮件的。

3.  在此命令行管理程序中，运行以下命令。
    
        Get-MailContact
    
    结果中不会返回禁用了电子邮件的联系人，因为此 cmdlet 仅返回启用了邮件联系人。

4.  在此命令行管理程序中，运行以下命令。
    
        Get-Contact
    
    结果中会返回禁用了电子邮件的联系人，因为此 cmdlet 返回所有 Active Directory 联系人对象。

## 使用命令行管理程序为联系人启用邮件

您可以使用**Enable-MailContact** cmdlet 启用 Active Directory 的现有联系人的邮件。您可以启用一个联系人的邮件或使用 CSV 文件启用多个联系人的邮件。

## 使用命令行管理程序为单个联系人启用邮件

本示例邮件启用联系人廖廖。您必须提供一个外部电子邮件地址。

    Enable-MailContact -Identity "Rene Valdes" -ExternalEmailAddress renev@tailspintoys.com

## 使用命令行管理程序和 CSV 文件为多个联系人启用邮件

当您在启用邮件的联系人批量，首先导出联系人，不是已启用邮件的 CSV （逗号分隔值） 文件，然后通过使用文本编辑器 （如记事本） 或电子表格应用程序，如 Microsoft Excel，然后添加到 CSV 文件的外部电子邮件地址的列表。然后使用 Shell 命令中更新的 CSV 文件以启用该 CSV 文件中列出的联系人的邮件。

1.  运行以下命令可将未启用邮件的现有联系人列表导出到管理员桌面上的 Contacts.csv 文件。
    
        Get-Contact | Where { $_.RecipientType -eq "Contact" } | Out-File "C:\Users\Administrator\Desktop\Contacts.csv"
    
    生成的文件将类似于以下文件。
    
        Name
        Walter Harp
        James Alvord
        Rainer Witt
        Susan Burk
        Ian Tien
        ...

2.  添加一个名为**电子邮件地址**的列标题，然后在文件中添加的每个联系人的电子邮件地址。必须用逗号分隔的名称和外部电子邮件地址为每个联系人。更新的 CSV 文件应类似于下面的文件。
    
        Name,EmailAddress
        James Alvord,james@contoso.com
        Susan Burk,sburk@tailspintoys.com
        Walter Harp,wharp@tailspintoys.com
        Ian Tien,iant@tailspintoys.com
        Rainer Witt,rainerw@fourthcoffee.com
        ...

3.  运行以下命令可使用 CSV 文件中的数据为其中列出的联系人启用邮件。
    
        Import-CSV C:\Users\Administrator\Desktop\Contacts.csv | ForEach-Object {Enable-MailContact -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    
    命令结果将显示有关启用邮件的新联系人的信息。

## 您如何知道这有效？

若要验证是否成功地为 Active Directory 联系人启用了邮件，请执行以下操作之一：

  - 在 EAC，导航到**收件人**\>**联系人**。新的邮件联系人将显示在联系人列表中。在**联系人类型**，类型为**邮件联系**。
    
    > [!NOTE]
    > 可能需要单击&amp;quot;刷新&amp;quot;<img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="刷新图标" alt="刷新图标" /> 才能显示新邮件联系人。


  - 在命令行管理程序中，运行以下命令可显示有关新邮件联系人的信息。
    
        Get-MailContact | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress

