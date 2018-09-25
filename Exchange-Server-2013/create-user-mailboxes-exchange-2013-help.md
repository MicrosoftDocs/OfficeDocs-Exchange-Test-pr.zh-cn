---
title: '创建用户邮箱: Exchange 2013 Help'
TOCTitle: 创建用户邮箱
ms:assetid: 51a8b4c6-a53e-41c5-8bb1-ea4c0eaa0174
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ991919(v=EXCHG.150)
ms:contentKeyID: 52061509
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建用户邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2013-04-12_

邮箱是 Exchange 组织中信息工作人员最常用的收件人类型。每个邮箱都与一个 Active Directory 用户帐户关联。用户可以使用邮箱发送和接收邮件，并可以存储邮件、约会、任务、便笺和文档。使用 EAC 或命令行管理程序创建用户邮箱。

也可为具有 Active Directory 用户帐户但是没有相应邮箱的现有用户创建用户邮箱。这称为*启用邮箱*的现有用户。

## 在开始之前，您需要知道什么？

  - 完成每个用户邮箱任务的估计时间：2 至 5 分钟。

  - 创建新用户邮箱时，不能在别名或用户登录名中使用撇号 (') 或引号 (")，因为不支持这些字符。尽管在使用不受支持的字符创建新邮箱时可能不会收到错误，但这些字符以后可能会导致问题。例如，针对使用不受支持的字符创建的邮箱，已分配访问权限的用户可能会遇到问题或意外行为。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建用户邮箱

## 使用 EAC 创建用户邮箱

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  单击“新建”\>“用户邮箱”。

3.  在“新建用户邮箱”页面的“别名”框中，键入用户别名，这可为用户指定电子邮件别名。用户的别名是电子邮件地址中 (@) 符号左侧的部分。它在林中必须是唯一的。
    
    > [!NOTE]  
    > 如果您将此框保留为空，则会对电子邮件别名使用“用户登录名称”的用户名部分中的值。


4.  选择下列选项之一：
    
      - **现有用户**   选择此选项可为现有用户启用邮件功能并创建邮箱。
        
        单击“浏览”打开“选择用户 – 整个林”对话框。此对话框显示尚未启用邮件功能或没有 Exchange 邮箱的林中的 Active Directory 用户帐户的列表。选择想要为其启用邮件功能的用户帐户，然后单击“确定”。如果选择此选项，则不必提供用户帐户信息，因为这些信息已存在于 Active Directory 中。
    
      - **新建用户**   选择此选项可在 Active Directory 中创建一个新的用户帐户，并为此用户创建一个邮箱。如果您选择此选项，则必须提供必需的用户帐户信息。
    
    > [!NOTE]  
    > 与用户邮箱关联的 Active Directory 帐户必须与 Exchange 服务器驻留在相同的林中。要为受信任的林中驻留的用户帐户创建邮箱，必须创建一个链接邮箱。请参阅<a href="manage-linked-mailboxes-exchange-2013-help.md">管理链接的邮箱</a>。


5.  如果在步骤 4 中选择了“新建用户”，请填写“新建用户邮箱”页面上的以下框。否则，跳转到步骤 7。
    
      - **名**   使用此框可以键入用户的名。
    
      - **缩写**   使用此框可以键入用户的缩写。
    
      - **姓**   使用此框可以键入用户的姓。
    
      - \* **显示姓名**   使用此框可以键入用户的显示姓名。此姓名将在 EAC 中的邮箱列表中和共享通讯簿中列出。默认情况下将使用“名”、“缩写”和“姓”框中所输入的姓名填充此框。如果未使用这些框，则还必须在此框中键入姓名，因为这是必填的。姓名不能超过 64 个字符。
    
      - \* **姓名**   使用此框可以键入用户的姓名。此姓名会在 Active Directory 中列出。此外，还将使用“名”、“缩写”和“姓”框中所输入的姓名填充此框。如果未使用这些框，则还必须在此框中键入姓名，因为此框是必需的。此姓名不能超过 64 个字符。
    
      - **组织单位**   可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为 Active Directory 域中的“用户”容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的“用户”容器。如果将收件人作用域设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击“浏览”。该对话框显示林中的指定作用域内的所有 OU。选择所需 OU，然后单击“确定”。
    
      - \* **用户登录名**   使用此框键入用户将用于登录邮箱和登录到域的名称。用户登录名由 (@) 符号左侧的用户名和右侧的后缀组成。通常，后缀是用户帐户所在域的域名。请注意，不能在用户登录名中使用撇号 (') 或引号 (")，因为不支持这些字符。
        
        > [!NOTE]  
        > 如果用户姓名的值与“别名”框中使用的值不同，则用户的电子邮件地址和用户登录名将不同。
    
      - \* **新密码**   使用此框可以键入用户登录其邮箱必须使用的密码。
        
        > [!NOTE]  
        > 请确保所提供的密码符合在其中创建用户帐户的域的密码长度、复杂程度和历史要求。
    
      - \* **确认密码**   使用此框可以确认在“密码”框中键入的密码。
    
      - **下次登录时需要更改密码**   如果希望用户在首次登录邮箱时重置密码，请选中此复选框。
        
        如果选中此复选框，在初次登录时，将通过对话框提示新用户更改密码。在成功更改密码之前，将不允许用户执行任何任务。

6.  单击“更多选项”配置以下框。否则，请跳到步骤 7 以保存新的用户邮箱。
    
      - **指定邮箱数据库**   使用此选项可指定邮箱数据库，而不是让 Exchange 为您选择数据库。单击“浏览”打开“选择邮箱数据库”对话框。此对话框列出 Exchange 组织中的所有邮箱数据库。默认情况下，按名称对邮箱数据库进行排序。还可以单击相应列标题，按服务器名称或版本对数据库进行排序。选择要使用的邮箱数据库，然后单击“确定”。
    
      - **为此用户创建本地存档存储**   选中此复选框可为邮箱创建存档邮箱。如果创建存档邮箱，则邮箱项目将基于默认保留策略设置（或定义的这些内容）自动从主邮箱移动到存档。
        
        单击“浏览”以选择位于本地林中的数据库，用于存储存档邮箱。
        
        若要了解更多信息，请参阅[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通讯簿策略**   使用此选项可为邮箱指定通讯簿策略 (ABP)。ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。在分配给邮箱用户时，ABP 使这些用户可以访问 Outlook 和 Outlook Web App 中的自定义 GAL。若要了解更多信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。
        
        在下拉列表中，选择要与此邮箱关联的策略。

7.  完成后，请单击“保存”创建邮箱。

## 使用命令行管理程序创建用户邮箱

本示例为 Pilar Pinilla 创建一个新用户帐户和邮箱，详细信息如下:

  - 别名是 pilarp

  - 名是 Pilar，姓是 Pinilla

  - 名称和显示名是 Pilar Pinilla

  - 用户登录名是 pilarp@contoso.com

  - 密码是 Pa$$word1

  - 将在默认的 OU 中创建邮箱。若要指定不同 OU，可使用 *OrganizationalUnit* 参数。

<!-- end list -->

    New-Mailbox -Alias pilarp -Name "Pilar Pinilla" -FirstName Pilar -LastName Pinilla -DisplayName "Pilar Pinilla" -UserPrincipalName pilarp@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

有关语法和参数的信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您如何知道操作成功？

要检查是否成功创建了用户邮箱，可进行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”。邮箱列表中将显示新的用户邮箱。在“邮箱类型”下，该类型是“用户”。

  - 在命令行管理程序中，运行下面的命令以显示有关新用户邮箱的信息。
    
    ```powershell
      Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```

## 为现有用户创建邮箱

也可为具有 Active Directory 用户帐户但是没有相应邮箱的现有用户创建用户邮箱。这称为*启用邮箱*的现有用户。为现有用户启用邮箱功能后，该用户便可以发送和接收电子邮件。

## 使用 EAC 为现有用户创建邮箱

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  单击“新建”\>“用户邮箱”。

3.  在“新建用户邮箱”页面的“别名”框中，键入用户别名，这可为用户指定电子邮件别名。用户的别名是电子邮件地址中 (@) 符号左侧的部分。它在林中必须是唯一的。
    
    > [!NOTE]  
    > 如果您将此框保留为空，则会对电子邮件别名使用“用户登录名称”的用户名部分中的值。


4.  单击“现有用户”。

5.  单击“浏览”打开“选择用户 – 整个林”对话框。此对话框显示尚未启用邮件功能或没有 Exchange 邮箱的林中的 Active Directory 用户帐户的列表。选择想要为其启用邮件功能的用户帐户，然后单击“确定”。
    
    为现有用户创建邮箱后，不必提供帐户信息，因为此信息已存在于 Active Directory 中。
    
    > [!NOTE]  
    > 与用户邮箱关联的 Active Directory 帐户必须与 Exchange 服务器驻留在相同的林中。要为受信任的林中驻留的用户帐户创建邮箱，必须创建一个链接邮箱。请参阅<a href="manage-linked-mailboxes-exchange-2013-help.md">管理链接的邮箱</a>。


6.  单击“更多选项”配置以下框。否则，请跳到步骤 7 以保存新的用户邮箱。
    
      - **指定邮箱数据库**   使用此选项可指定邮箱数据库，而不是让 Exchange 为您选择数据库。单击“浏览”打开“选择邮箱数据库”对话框。此对话框列出 Exchange 组织中的所有邮箱数据库。默认情况下，按名称对邮箱数据库进行排序。还可以单击相应列标题，按服务器名称或版本对数据库进行排序。选择要使用的邮箱数据库，然后单击“确定”。
    
      - **为此用户创建本地存档存储**   选中此复选框可为邮箱创建存档邮箱。如果创建存档邮箱，则邮箱项目将基于默认保留策略设置（或定义的这些内容）自动从主邮箱移动到存档。
        
        单击“浏览”以选择位于本地林中的数据库，用于存储存档邮箱。
        
        若要了解更多信息，请参阅[Exchange 2013 中的就地存档](in-place-archiving-in-exchange-2013-exchange-2013-help.md)。
    
      - **通讯簿策略**   使用此选项可为邮箱指定通讯簿策略 (ABP)。ABP 包含一个全局地址列表 (GAL)、一个脱机通讯簿 (OAB)、一个会议室列表以及一组地址列表。在分配给邮箱用户时，ABP 使这些用户可以访问 Outlook 和 Outlook Web App 中的自定义 GAL。若要了解更多信息，请参阅[通讯簿策略](address-book-policies-exchange-2013-help.md)。
        
        在下拉列表中，选择要与此邮箱关联的策略。

7.  完成后，请单击“保存”创建邮箱。

## 使用命令行管理程序为现有用户创建邮箱

本示例在名为 UsersMailboxDatabase 的 Exchange 数据库上为现有用户创建一个 estherv@contoso.com 邮箱。

```powershell
  Enable-Mailbox estherv@contoso.com -Database UsersMailboxDatabase
```

还可以使用 **Enable-Mailbox** cmdlet 为多个用户启用邮件。这可以通过将 **Get-User** cmdlet 的结果经管道传递给 **Enable-Mailbox** cmdlet 来实现。运行 **Get-User** cmdlet 时，必须仅返回尚未为其启用邮件的用户。为此，需要指定具有 *RecipientTypeDetails* 参数的值用户。还可以限制返回的结果，方法是通过使用 *Filter* 参数仅请求符合指定条件的用户。然后将结果通过管道传递给 **Enable-Mailbox** cmdlet。

例如，下面的命令将为尚未启用邮件功能的用户启用具有 **UserPrincipalName** 属性值的邮箱功能，以确保您不会无意中将系统帐户转换为邮箱。

```powershell
  Get-User -RecipientTypeDetails User -Filter { UserPrincipalName -ne $Null } | Enable-Mailbox
```

有关语法和参数的信息，请参阅 [Enable-Mailbox](https://technet.microsoft.com/zh-cn/library/aa998251\(v=exchg.150\)) 和 [Get-User](https://technet.microsoft.com/zh-cn/library/aa996896\(v=exchg.150\))。

有关管道传输的详细信息，请参阅[管道传输](https://technet.microsoft.com/zh-cn/library/aa998260\(v=exchg.150\))。

## 您如何知道操作成功？

若要验证是否成功为现有用户创建了邮箱，请执行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”。邮箱列表中将显示新启用邮箱功能的用户。在“邮箱类型”下，该类型是“用户”。

  - 在命令行管理程序中，运行下面的命令以显示有关新启用邮箱功能的用户的信息。
    
    ```powershell
      Get-Mailbox <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress
    ```
    
    请注意，*RecipientTypeDetails* 属性的值是 `UserMailbox`。

