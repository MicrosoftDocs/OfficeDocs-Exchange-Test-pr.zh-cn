---
title: '启用或禁用邮件用户的电子邮件: Exchange 2013 Help'
TOCTitle: 启用或禁用邮件用户的电子邮件
ms:assetid: 1e2571d4-ff84-4fda-bb1d-825e96e1bd26
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa996598(v=EXCHG.150)
ms:contentKeyID: 50556538
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用邮件用户的电子邮件

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-11-14_

您可以在 Exchange 组织中禁用现有邮件用户的电子邮件。当禁用邮件用户的电子邮件时，它被从 Exchange 和您的组织的通讯簿。如果邮件用户通讯组的成员，用户将不再接收发送到组的邮件。此外，Exchange 属性已从 Active Directory 中的用户对象，但在 Active Directory 中保留用户对象和非 Exchange 属性 （如联系人和公司信息）。

禁用邮件用户的电子邮件后，您可以启用邮件用户再次通过在 Shell 中使用**Enable-MailUser** cmdlet。此外可以使用此 cmdlet 以启用任何活动目录的用户的邮件。

> [!NOTE]  
> 邮件用户 （也称为<em>已启用邮件的用户</em>） 是不同于组织中拥有邮箱的用户。两者的主要区别是邮件用户代表您的 Exchange 组织以外的用户具有外部电子邮件地址。他们没有在您的组织中的邮箱。用户已在您的组织中的邮箱和邮件用户之间的差异的详细信息，请参阅<a href="recipients-exchange-2013-help.md">收件人</a>。


有关邮件用户相关的其他管理任务，请参阅[管理邮件用户](https://docs.microsoft.com/zh-cn/exchange/recipients-in-exchange-online/manage-mail-users)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;邮件用户\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 为邮件用户禁用电子邮件

如上文所述，在禁用邮件用户的电子邮件时，Exchange 属性会从相应的 Active Directory 邮件用户对象，但用户会保留。从 EAC，邮件的用户的列表中删除邮件用户，但您可以查看和管理相应的 Active Directory 联系对象，通过使用 Active Directory 用户和计算机或通过在 Shell 中使用的**Get-MailUser**和**Set-Set-MailUser**的 cmdlet。

## 使用 EAC 为邮件用户禁用电子邮件

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;。

2.  在联系人列表中，单击要禁用电子邮件的邮件用户。

3.  单击\&quot;更多\&quot;![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，再单击\&quot;禁用\&quot;。

4.  如果您不确定您想要禁用用户选定的邮件，警告将显示询问。单击**是**以将其禁用。

邮件用户将从联系人列表中删除。

## 使用命令行管理程序为邮件用户禁用电子邮件

此示例将为邮件用户 Yan Li 禁用电子邮件。

```powershell
Disable-MailUser -Identity "Yan Li"
```

有关详细的语法和参数信息，请参阅 [Disable-MailUser](https://technet.microsoft.com/zh-cn/library/aa998578\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功为邮件用户禁用电子邮件，请执行下列操作之一：

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;，然后验证该邮件用户是否不再列出。

2.  在 Active Directory 用户和计算机中，用鼠标右键单击该用户，然后单击**属性**。在**常规**选项卡中，请注意**电子邮件**框中为空。这将验证邮件的用户不是已启用邮件的。

3.  在此命令行管理程序中，运行以下命令。
    
    ```powershell
    Get-MailUser
    ```
    
    由于此 cmdlet 仅返回已启用邮件的用户，因此结果中不会返回那些已禁用电子邮件的邮件用户。

4.  在此命令行管理程序中，运行以下命令。
    
    ```powershell
    Get-User
    ```
    
    由于此 cmdlet 将返回所有 Active Directory 用户对象，因此结果中将返回那些已禁用电子邮件的邮件用户。

## 使用命令行管理程序为用户启用邮件

您可以使用**Enable-MailUser** cmdlet 现有活动目录用户启用邮件。您可以启用单个用户的邮件或使用 CSV 文件启用多个用户的邮件。

## 使用命令行管理程序为单个用户启用邮件

本示例邮件启用用户 Sanjay Shah。您必须提供一个外部电子邮件地址。

```powershell
Enable-MailUser -Identity "Sanjay Shah" -ExternalEmailAddress renev@tailspintoys.com
```

## 使用命令行管理程序和 CSV 文件为多个用户启用邮件

当您在启用邮件的用户批量，首先导出的不是已启用邮件的 CSV （逗号分隔值） 文件，然后通过使用文本编辑器 （如记事本） 或电子表格应用程序，如 Microsoft Excel，然后添加到 CSV 文件的外部电子邮件地址的用户的列表。然后使用 Shell 命令中更新的 CSV 文件以启用该 CSV 文件中列出的用户的邮件。

1.  运行以下命令，将组织中未启用邮件的、或者没有邮箱的现有用户列表导出到管理员桌面上名为 UsersToMailEnable.csv 的文件中。

    ```powershell
        Get-User | Where { $_.RecipientType -eq "User" } | Out-File "C:\Users\Administrator\Desktop\UsersToMailEnable.csv"
    ```

    最终生成的文件将类似于下列文件。
    
    ```powershell
        Name            RecipientType
        ----            -------------
        Guest           User
        krbtgt          User
        RMS_SERVICE     User
        David Pelton    User
        Kim Akers       User
        Janet Schorr    User
        Jeffrey Zang    User
        Spencer Low     User
        Toni Poe        User
        ...
    ```

2.  对 CSV 文件进行以下更改：
    
      - 删除任何不想要启用邮件从 CSV 文件的用户。例如，将删除在前面的示例的前三项因为它们默认系统帐户。
    
      - 删除 **RecipientType** 列和 `User` 的所有实例。
    
      - 添加一个名为**电子邮件地址**的列标题，然后在文件中添加的每个用户的电子邮件地址。名称和每个用户的外部电子邮件地址必须用逗号分隔。
    
    更新后的 CSV 文件应类似于下列文件。
    ```powershell
        Name,EmailAddress
        David Pelton,davidp@contoso.com
        Kim Akers,kakers@tailspintoys.com
        Janet Schorr,janet.schorr@adatum.com
        Jeffrey Zang,jzang@tailspintoys.com
        Spencer Low,spencerl@fouthcoffee.com
        Toni Poe,tonip@contoso.com
        ...
    ```

3.  运行下列命令，以便使用 CSV 文件中的数据为文件中列出的用户启用邮件。
    ```powershell
        Import-CSV "C:\Users\Administrator\Desktop\UsersToMailEnable.csv" | ForEach-Object {Enable-MailUser -Identity $_.Name -ExternalEmailAddress $_.EmailAddress}
    ```

    命令结果将显示有关已启用邮件的新用户的信息。

## 您如何知道这有效？

若要验证是否已成功为 Active Directory 用户启用邮件，请执行下列操作之一：

  - 在 EAC，导航到**收件人**\>**联系人**。在联系人列表中显示新邮件用户。在**联系人类型**，该类型是**邮件用户**。
    
    > [!NOTE]  
    > 可能必须单击&amp;quot;刷新&amp;quot;<img src="images/Dd353189.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif" title="刷新图标" alt="刷新图标" />，才能显示新邮件用户。


  - 在命令行管理程序中，运行以下命令可显示有关此新邮件用户的信息。
    
    ```powershell
    Get-MailUser | Format-Table Name,RecipientTypeDetails,ExternalEmailAddress
    ```

