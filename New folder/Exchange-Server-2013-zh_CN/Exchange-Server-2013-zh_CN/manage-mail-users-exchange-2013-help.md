---
title: '管理邮件用户: Exchange 2013 Help'
TOCTitle: 管理邮件用户
ms:assetid: bb8b8804-f730-4ad7-9173-896a4965b90f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124381(v=EXCHG.150)
ms:contentKeyID: 50489729
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailUserWizardForm.NewMailUserIntroductionWizardPage
ms.translationtype: HT
---

# 管理邮件用户

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

邮件用户与邮件联系人类似。二者都有外部电子邮件地址，都包含有关 Exchange 或 Exchange Online 组织外部人员的信息，并且都可以显示在共享通讯簿和其他地址列表中。但是，与邮件联系人不同，邮件用户在 Exchange 或 Office 365 组织中拥有登录凭据并可以访问资源。有关详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建邮件用户

## 使用 EAC 创建邮件用户

1.  在 EAC 中，导航至“收件人”\>“联系人”\>“新建”\>“邮件用户”。

2.  在“新建邮件用户”页面中，在“\* 别名”框中键入此邮件用户的别名。别名不能超过 64 个字符，并且在林中必须是唯一的。此框是必填的。

3.  执行以下操作之一来指定邮件用户的电子邮件地址类型：
    
      - 要为此邮件用户的外部电子邮件地址指定一个 SMTP 电子邮件地址，请单击“SMTP”。
        
        > [!NOTE]
        > Exchange 可以验证 SMTP 地址的格式是否正确。如果条目与 SMTP 格式不一致，则在单击“保存”以创建邮件用户时会显示一条错误消息。
    
      - 要指定自定义地址类型，单击选项按钮，然后键入自定义地址类型。例如，可以指定 X.500 地址、GroupWise 地址或 Lotus Notes 地址。

4.  在“\* 外部电子邮件地址”框中键入此邮件用户的外部电子邮件地址。发送给此邮件用户的电子邮件将会转发到此电子邮件地址。此框是必填的。

5.  选择下列选项之一：
    
      - **现有用户**   选择该选项可为现有用户启用邮件功能。
        
        单击“浏览”打开“选择用户 – 整个林”对话框。此对话框显示组织中尚未启用邮件或没有邮箱的用户帐户列表。选择想要为其启用邮件功能的用户帐户，然后单击“确定”。如果选择此选项，则不必提供用户帐户信息，因为此信息已存在于 Active Directory 中。
    
      - **新建用户**   选择该选项可以在 Active Directory 中创建新用户帐户，并为该用户启用邮件功能。如果您选择此选项，则必须提供必需的用户帐户信息。

6.  如果在步骤 5 中选择了“新建用户”，请在“新建邮件用户”页面上填写下列各框。否则，跳转到步骤 7。
    
      - **名**   使用此框键入邮件用户的名。
    
      - **缩写**   使用此框键入邮件用户的缩写。
    
      - **姓**   使用此框键入邮件用户的姓。
    
      - “\* 显示姓名”   使用此框可以键入用户的显示姓名。这是在 EAC 的联系人列表和组织的通讯簿中列出的名称。默认情况下将使用“名字”、“缩写”和“姓氏”框中所输入的姓名填充此框。如果未使用这些框，则仍然必须在此框中键入姓名，因为这是必填的。姓名不能超过 64 个字符。
    
      - \* **姓名** 使用此框键入邮件用户的姓名。此名称会在目录服务中列出。还可使用“名字”、“缩写”和“姓氏”框中所输入的姓名填充此框。如果未使用这些框，则还必须在此框中键入姓名，因为此框是必需的。此姓名不能超过 64 个字符。
        
        > [!NOTE]
        > “姓名”框仅在 Exchange Server 2013 中可用。在 Exchange Online 中不可用。
    
      - “组织单位”   可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为域中的“用户”容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的“用户”容器。如果将收件人范围设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击“浏览”。该对话框显示林中的指定作用域内的所有 OU。选择所需的 OU，然后单击“确定”。
        
        > [!NOTE]
        > “组织单元”框仅在 Exchange Server 2013 中可用。在 Exchange Online 中不可用。
    
      - \* **用户登录名**   使用此框键入邮件用户用于登录域的名称。用户登录名由 (@) 符号左侧的用户名和右侧的后缀组成。通常，后缀是用户帐户所在域的域名。
        
        > [!NOTE]
        > 在 Exchange Online 中，此框被标记为“用户 ID”。
    
      - \* **新密码**   使用此框键入邮件用户登录域时必须使用的密码。
        
        > [!NOTE]
        > 请确保所提供的密码符合在其中创建用户帐户的域的密码长度、复杂程度和历史要求。
    
      - “\* 确认密码”   使用此框可以确认在“密码”框中键入的密码。
    
      - **下次登录时需要更改密码**   如果希望邮件用户在首次登录邮箱时重置密码，请选中此复选框。
        
        如果选中此复选框，在初次登录时，将通过对话框提示新邮件用户更改密码。在成功更改密码之前，将不允许邮件用户执行任何任务。

7.  完成后，请单击“保存”来创建邮件用户。

## 使用命令行管理程序创建邮件用户

此示例在 Exchange Server 2013 内为 Jeffrey Zeng 创建了一个启用邮件功能的用户帐户，详细信息如下：

  - 姓名和显示名是 Jeffrey Zeng。

  - 别名是 jeffreyz。

  - 外部电子邮件地址是 jzeng@tailspintoys.com。

  - 名是 Jeffrey，姓是 Zeng。

  - 登录名为 jeffreyz@contoso.com。

  - 密码为 Pa$$word1。

  - 将在默认 OU 中创建此邮件用户。若要指定不同 OU，可使用 *OrganizationalUnit* 参数。

<!-- end list -->

    New-MailUser -Name "Jeffrey Zeng" -Alias jeffreyz -ExternalEmailAddress jzeng@tailspintoys.com -FirstName Jeffrey -LastName Zeng -UserPrincipalName jeffreyz@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$word1' -AsPlainText -Force)

此示例在 Exchange Online 中为 Rene Valdes 创建了一个启用邮件功能的用户帐户。

    New-MailUser -Name "Rene Valdes" -Alias renev -ExternalEmailAddress renevaldes@fineartschool.edu -FirstName Rene -LastName Valdes -MicrosoftOnlineServicesID renev@contoso.com -Password (ConvertTo-SecureString -String 'P@ssw0rd' -AsPlainText -Force)

## 您如何知道这有效？

要验证是否成功创建了邮件用户，可执行以下操作之一：

  - 在 EAC 中，导航至“收件人”\>“联系人”。新邮件用户显示在联系人列表中。在“联系人类型”下，该类型为“邮件用户”。

  - 在命令行管理程序中，运行以下命令可显示有关此新邮件用户的信息。
    
        Get-MailUser <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## 更改邮件用户属性

创建邮件用户后，您可以使用 EAC 或命令行管理程序进行更改和设置其他属性。

您也可同时为多个用户邮箱更改属性。有关详细信息，请参阅使用 EAC 批量编辑邮件用户。

完成此任务的估计时间将会根据您要查看或更改的属性数量而异。

## 使用 EAC 更改用户邮箱属性

1.  在 EAC 中，导航至“收件人”\>“联系人”。

2.  在联系人列表中，单击您要为其更改属性的邮件用户，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“邮件用户属性”页面上，单击以下部分之一可查看或更改属性。
    
      - 常规
    
      - 联系人信息
    
      - 组织
    
      - 电子邮件地址
    
      - 邮件流设置
    
      - 成员属于
    
      - 邮件提示

## 常规

使用“常规”部分可以查看或更改有关邮件用户的基本信息。

  - **名**、**缩写**、**姓**

  - “\* 姓名”   这是会在 Active Directory 中列出的姓名。如果您要更改此姓名，则它不能超过 64 个字符。

  - “\* 显示名称”   此名称将会出现在组织通讯簿中的“收件人:”和“发件人：”电子邮件和 EAC 的联系人列表中的行。此姓名不能在显示名之前或之后包含空格。

  - \* **用户登录名**   用户使用此名可登录域。在 Exchange Online 中，这是用户用来登录 Office 365 的用户 ID。

  - **在地址列表中隐藏**   选中此复选框可以防止邮件用户显示在通讯簿以及在 Exchange 组织中定义的其他地址列表中。选中此复选框后，用户仍可使用电子邮件地址向收件人发送邮件。

  - **下次登录时需要更改密码**   如果希望用户在下次登录域时重置密码，请选中此复选框。
    
    > [!NOTE]
    > 此框在 Exchange Online 中不可用。


单击“更多选项”查看或更改以下这些额外的属性：

  - **组织单位**   此只读框显示包含邮件用户帐户的组织单位 (OU)。您必须使用 Active Directory 用户和计算机移动帐户到其他 OU。
    
    > [!NOTE]
    > 此框在 Exchange Online 中不可用。


  - **自定义属性**   此部分显示为邮件用户定义的自定义属性。要指定自定义属性值，请单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。最多可为收件人指定 15 个自定义属性。

## 联系人信息

使用“联系信息”部分来查看或更改用户联系信息。该页上的信息显示在通讯簿中。单击“更多选项”以显示额外框。

> [!tip]
> 可以使用“州/省”框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。


## 组织

使用“组织”部分可以记录有关组织中用户角色的详细信息。此信息会显示在通讯簿中。您也可以创建可从电子邮件客户端（如 Outlook）访问的虚拟组织图。

  - **职务**：使用此框可以查看或更改收件人的职务。

  - **部门**   使用此框可以查看或更改用户所在的部门。可以使用此框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。

  - **公司**   使用此框可以查看或更改用户所在的公司。可以使用此框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。

  - **经理**   若要添加经理，请单击“浏览”。在“选择经理”中，选择相应的人员，然后单击“确定”。

  - “直接下属”   您无法修改此框。直接下属是指向特定经理报告的用户。如果已为用户指定一个经理，则该用户将作为直接下属出现在该经理邮箱的详细信息中。例如，Kari 是 Chris 和 Kate 的经理，因此，Chris 和 Kate 的“经理”框中指定的是 Kari，而 Chris 和 Kate 则显示在 Kari 帐户属性中的“直接下属”框中。

## 电子邮件地址

使用“电子邮件地址”部分可以查看或更改与该邮件用户关联的电子邮件地址。这包括邮件用户的主 SMTP 地址、他们的外部电子邮件地址和任何关联的代理地址。主 SMTP 地址（也称为“默认答复地址”）在地址列表中以粗体显示，大写的 **SMTP** 值显示在“类型”列中。默认情况下，创建邮件用户之后，主 SMTP 地址与外部电子邮件地址是相同的。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。单击此按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
    
      - “自定义地址类型”   单击此按钮，然后在“\* 电子邮件地址”框中键入一个支持的非 SMTP 电子邮件地址。
        
        > [!NOTE]
        > 除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。您必须确保所指定的自定义地址符合该地址类型的格式要求。


  - **设置外部电子邮件地址**   使用此框可以更改邮件用户的外部地址。发送给此邮件用户的电子邮件将会转发到此电子邮件地址。

  - “基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址”   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。此框在默认情况下处于选中状态。
    
    > [!NOTE]
    > 此框在 Exchange Online 中不可用。


## 邮件流设置

使用“邮件流设置”部分可以查看或更改以下设置：

  - **邮件大小限制**   这些设置控制邮件用户可以发送和接收的邮件大小。单击“查看详细信息”可查看和更改发送和接收的邮件的最大大小。
    
      - “已发送消息”   要指定该用户发送的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户发送大于该指定大小的邮件，则会将该邮件返回至用户，并向其显示一条描述性的错误消息。
    
      - “已收到消息”   要指定该用户接收的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户收到大于指定大小的邮件，则该邮件将返回至发件人，并向其显示一条描述性的错误消息。

  - **邮件传递限制**   这些设置控制可以向此邮件用户发送电子邮件的人员。单击“查看详细信息”可查看和更改这些限制。
    
      - **接受来自下列发件人的邮件**   使用该部分指定谁可将邮件发送至该用户。
        
          - “所有发件人”   选择此选项可指定用户能够接受来自所有发件人的邮件。这包括 Exchange 组织中的发件人和外部发件人。此选项默认情况下处于选中状态。仅当清除了“要求所有发件人均通过身份验证”复选框时，此选项才包括外部用户。如果选中此复选框，则会拒绝来自外部用户的邮件。
        
          - “仅限以下列表中的发件人”   选择此选项可指定该用户只能接受来自 Exchange 组织中指定的一组发件人的邮件。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示“选取收件人”页面，该页面显示您 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
        
          - “要求所有发件人均通过身份验证”   选中此选项可防止匿名用户向此用户发送邮件。
    
      - “拒绝来自下列发件人的邮件”   使用该部分来阻止某些人将邮件发送至该用户。
        
          - “无发件人”   选择此选项可指定邮箱不会拒绝来自 Exchange 组织中任何发件人的邮件。此选项默认情况下处于选中状态。
        
          - “以下列表中的发件人”   选择此选项可指定该邮箱将拒绝来自 Exchange 组织中指定的一组发件人的邮件。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示“选择收件人”页面，该页面显示您 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。

## 成员属于

使用“隶属于”部分可查看该用户所属通讯组或安全组的列表。您不能在此页上更改成员信息。请注意，用户可能符合您组织中的一个或多个动态通讯组的条件。但是，动态通讯组不会显示在此页面上，因为每次使用它们时都会计算其成员资格。

## 邮件提示

使用“邮件提示”部分可添加邮件提示，以便在用户向此收件人发送邮件之前提醒用户存在潜在的问题。邮件提示是在将此收件人添加到新电子邮件的“收件人”、“抄送”或“密件抄送”行中时，信息栏中显示的文本。

> [!NOTE]
> 邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。


## 使用命令行管理程序更改邮件用户属性

邮件用户的属性存储在 Active Directory 和 Exchange 中。通常，使用 **Get-User** 和 **Set-User** cmdlet 来查看和更改组织和联系人信息属性。使用 **Get-MailUser** 和 **Set-MailUser** cmdlet 来查看或更改邮件相关的属性，例如电子邮件地址、邮件提示、自定义属性，以及是否在地址列表中隐藏邮件用户。

使用 **Get-MailUser** 和 **Set-MailUser** cmdlet 查看和更改邮件用户的属性。相关信息请参阅下列主题：

  - [Get-User](https://technet.microsoft.com/zh-cn/library/aa996896\(v=exchg.150\))

  - [Set-User](https://technet.microsoft.com/zh-cn/library/aa998221\(v=exchg.150\))

  - [Get-MailUser](https://technet.microsoft.com/zh-cn/library/aa997254\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-cn/library/aa995971\(v=exchg.150\))

此处是使用命令行管理程序更改邮件用户属性的一些示例。

此示例将设置 Pilar Pinilla 的外部电子邮件地址。

    Set-MailUser "Pilar Pinilla" -ExternalEmailAddress pilarp@tailspintoys.com

此示例在组织的通讯簿中隐藏所有邮件用户。

    Get-MailUser | Set-MailUser -HiddenFromAddressListsEnabled $true

此示例将所有邮件用户的“公司”属性设置为 Contoso。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | Set-User -Company Contoso

此示例将“公司”属性为 Contoso 的所有邮件用户的 CustomAttribute1 属性设置为 ContosoEmployee。

    Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Contoso')}| Set-MailUser -CustomAttribute1 ContosoEmployee

## 您如何知道这有效？

要验证您是否已成功更改邮件用户的属性，请执行以下操作：

  - 在 EAC 中，选择邮件用户，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 以查看您更改的属性。

  - 在命令行管理程序中，使用 **Get-User** 和 **Get-MailUser** cmdlet 验证更改。使用此命令行管理程序的一个优势是您可以查看多个邮件联系人的多个属性。
    
        Get-MailUser | Fl Name,CustomAttribute1 
    
    在上述示例中所有邮件用户的“公司”属性都设置为 Contoso，请运行以下命令验证更改：
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser')} | FL Name,Company
    
    在上述示例中所有邮件用户的 CustomAttribute1 属性都设置为 ContosoEmployee，请运行以下命令验证更改：
    
        Get-MailUser | Fl Name,CustomAttribute1 

## 批量编辑邮件用户

您还可以使用 EAC 更改多个邮件用户的已选属性。从 EAC 的联系人列表中选择两个或两个以上邮件用户后，“详细信息”窗格中将显示可以批量编辑的属性。在您更改其中一个属性后，所做更改将应用到所有选定的收件人。

批量编辑邮件用户时，您可以更改以下属性区域：

  - **联系人信息**   更改共享属性，如街道、邮编和城市名称。

  - **组织**   更改共享属性，如部门名称、公司名称和选定邮件联系人或邮件用户的直接经理。

## 使用 EAC 批量编辑邮件用户

1.  在 EAC 中，导航至“收件人”\>“联系人”。

2.  在联系人列表中，选择两个或两个以上邮件用户。无法批量编辑邮件联系人和邮件用户的组合。
    
    > [!tip]
    > 您可以选择多个相邻的邮件用户，方法是按住 Shift 键，单击要编辑的第一个邮件用户，然后单击最后一个邮件用户。您也可以按住 Ctrl 键并单击要编辑的每个联系人来选择多个邮件用户。


3.  在“详细信息”窗格的“批量编辑”下面，单击“联系人信息”或“组织”下的“更新”。

4.  更改属性页面，然后保存所做的更改。

## 您如何知道这有效？

要验证是否成功批量编辑了邮件用户，可执行以下操作之一：

  - 在 EAC 中，选择批量编辑的各邮件用户，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 以查看您更改的属性。

  - 在命令行管理程序中，使用 **Get-User** cmdlet 验证更改。例如，假设您已使用 EAC 中的批量编辑功能更改了供应商公司 A. Datum Corporation 的所有邮件用户的经理和办公室属性。要验证这些更改，可以在此命令行管理程序中运行以下命令：
    
        Get-User -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'mailuser') -and (Company -eq 'Adatum')} | fl Name,Office,Manager

## 使用目录同步管理 Exchange Online 中的邮件用户

本节提供了有关使用 Exchange Online 中的目录同步管理电子邮件用户的信息。目录同步可为混合客户以及 Active Directory 是本地的完全托管的 Exchange Online 客户提供本地和云托管的邮箱。

> [!NOTE]
> 如果您使用目录同步来管理收件人，那么您仍然可以在 Office 365 管理中心中添加和管理用户，但是他们无法与您的本地 Active Directory 同步。这是因为目录同步只能将来自本地 Active Directory 的收件人同步到云。


> [!NOTE]
> 建议将目录同步用于以下功能：
> <ul>
> <li><p><strong>Outlook 白名单和黑名单</strong> 当同步到服务时，这些列表将优先于服务中的垃圾邮件筛选。这允许用户在每个用户或每个域的基础上管理他们自己的白名单和黑名单。</p></li>
> <li><p><strong>基于目录的边缘阻止 (DBEB)</strong> 有关 DBEB 的详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/dn600322(v=exchg.150)">使用基于目录的边缘阻止拒绝发送给无效收件人的邮件</a>。</p></li>
> <li><p><strong>最终用户垃圾邮件隔离</strong> 若要访问最终用户垃圾邮件隔离邮箱，最终用户必须具有有效 Office 365 用户 ID 和密码。有本地邮箱的客户必须是有效的电子邮件用户。</p></li>
> <li><p><strong>传输规则</strong> - 在使用目录同步时，您现有的 Active Directory 用户和组将自动上传到云，而且您可以随后创建针对特定用户和/或组的传输规则，无需通过 EAC 或远程 Windows PowerShell 手动添加它们。请注意，<a href="https://go.microsoft.com/fwlink/?linkid=507569">动态通讯组</a>无法通过目录同步进行同步。</p></li>
> </ul>


**开始之前**

按[准备进行目录同步](https://go.microsoft.com/fwlink/p/?linkid=308908)中所述，获取所需权限，并准备进行目录同步。

**同步用户目录的步骤**

1.  按[激活目录同步](https://go.microsoft.com/fwlink/p/?linkid=308909)中所述，激活目录同步。

2.  按[设置目录同步计算机](http://go.microsoft.com/fwlink/p/?linkid=308911)中所述，设置您的目录同步计算机。

3.  按[使用配置向导同步目录](http://go.microsoft.com/fwlink/?linkid=308912)中所述，同步目录。
    
    > [!important]
    > 完成 Azure Active Directory 同步工具配置向导后，“MSOL_AD_SYNC”帐户即在 Active Directory 林中创建。此帐户用于读取和同步您的本地 Active Directory 信息。为了使目录同步正常工作，请确保本地目录同步服务器上的 TCP 443 处于打开状态。


4.  按[激活同步用户](http://go.microsoft.com/fwlink/p/?linkid=308913)中所述，激活同步用户。

5.  按[管理目录同步](http://go.microsoft.com/fwlink/p/?linkid=308915)中所述，管理目录同步。

6.  验证 Exchange Online 是否正确同步。在 EAC 中，转到“收件人”\>“联系人”并查看用户列表是否已从本地环境中正确同步。

