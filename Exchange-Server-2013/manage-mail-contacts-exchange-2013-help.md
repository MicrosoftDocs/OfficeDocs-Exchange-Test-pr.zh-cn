---
title: '管理邮件联系人: Exchange Online Help'
TOCTitle: 管理邮件联系人
ms:assetid: 74c72aed-e9ff-4927-8eb7-c08a86e79ae0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998858(v=EXCHG.150)
ms:contentKeyID: 50489760
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailContactWizardForm.NewMailContactIntroductionWizardPage
ms.translationtype: MT
---

# 管理邮件联系人

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-10-04_

邮件联系人都包含有关人或组织交换或Exchange Online组织之外存在的已启用邮件的目录服务对象。每个邮件联系人具有外部电子邮件地址。有关邮件联系人的详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;收件人设置权限\&quot;部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 创建邮件联系人

## 使用 EAC 创建邮件联系人

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;。

2.  单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") \>\&quot;邮件联系人\&quot;。

3.  完成\&quot;新建邮件联系人\&quot;页上的以下框：
    
      - **名**：使用此框可以键入联系人的名。
    
      - **缩写**：使用此框可以键入联系人的缩写。
    
      - **姓**：使用此框可以键入联系人的姓。
    
      - **\* 显示姓名**   使用此框可以键入联系人的显示姓名。这是将在 EAC 的联系人列表和组织的通讯簿中列出的名称。默认情况下将使用\&quot;名\&quot;、\&quot;缩写\&quot;和\&quot;姓\&quot;框中所输入的姓名填充此框。如果未使用这些框，则还必须在此框中键入姓名，因为姓名是必需的。姓名不能超过 64 个字符。
    
      - **\* 姓名**   使用此框可以键入联系人的姓名。此姓名会在目录服务中列出。与显示姓名一样，默认情况下将使用\&quot;名\&quot;、\&quot;缩写\&quot;和\&quot;姓\&quot;框中所输入的姓名填充此框。如果未使用这些框，则还必须在此框中键入姓名，因为姓名是必需的。姓名不能超过 64 个字符。
    
      - **\* 别名**使用此文本框可以键入别名 (64 个字符或更少) 的联系人。此框是必需的。
    
      - **\* 外部电子邮件地址**   使用此框可以键入联系人的外部电子邮件帐户。此框是必填的。发送给此联系人的电子邮件将会转发到此电子邮件地址。
    
      - **组织单位**   可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为域中的\&quot;用户\&quot;容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的\&quot;用户\&quot;容器。如果将收件人作用域设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击\&quot;浏览\&quot;。该对话框显示林中的指定作用域内的所有 OU。选择所需的 OU，然后单击\&quot;确定\&quot;。
        
        > [!NOTE]  
        > &amp;quot;组织单元&amp;quot;框仅在 Exchange Server 2013 中可用。在 Exchange Online 中不可用。


4.  完成后，请单击\&quot;保存\&quot;。

## 使用命令行管理程序创建邮件联系人

此示例将在 Exchange Server 2013 中为 Debra Garcia 创建邮件联系人。

    New-MailContact -Name "Debra Garcia" -ExternalEmailAddress dgarcia@tailspintoys.com -OrganizationalUnit Users

此示例将在 Exchange Online 中为 Alan Shen 创建邮件联系人。

    New-MailContact -Name "Alan Shen" -ExternalEmailAddress alans@fourthcoffee.com

此示例将在 Exchange Server 2013 中对名为 Karen Toh 的现有联系人启用邮件。

    Enable-MailContact -Identity "Karen Toh" -ExternalEmailAddress ktoh@tailspintoys.com

## 您如何知道这有效？

要验证是否成功创建了邮件联系人，请执行以下操作之一：

  - 在 EAC 中，导航到\&quot;收件人\&quot; \> \&quot;联系人\&quot;。联系人列表中将显示新的邮件联系人。在\&quot;联系人类型\&quot;下，该类型是\&quot;邮件联系人\&quot;。

  - 在命令行管理程序中，运行以下命令可显示有关新邮件联系人的信息：
    
        Get-MailContact <Name> | FL Name,RecipientTypeDetails,ExternalEmailAddress

## 更改邮件联系人属性

## 使用 EAC 更改邮件联系人属性

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;。

2.  在邮件联系人和邮件用户的列表中，单击要更改其属性的邮件联系人，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;邮件联系人属性\&quot;页上，单击以下部分之一以查看或更改属性。
    
      - General
    
      - Contact Information
    
      - Organization
    
      - Email Options（在 Exchange Online 中不可用）
    
      - MailTip

## 常规

使用\&quot;常规\&quot;部分查看或更改有关邮件联系人的基本信息。

  - **名字**、**姓名缩写**、**姓氏**

  - \&quot;\* 姓名\&quot;   这是会在 Active Directory 中列出的姓名。如果您要更改此姓名，则它不能超过 64 个字符。

  - **\* 显示名称**   此名称将会出现在组织通讯簿中的\&quot;收件人\&quot;和\&quot;发件人\&quot;行上以及\&quot;邮箱\&quot;列表中。此名称不能在显示名称之前或之后加上空格。

  - **\* 别名**   这是邮件联系人的别名。如果更改别名，则它必须在组织中唯一且必须为 64 个字符或更少。

  - **\* 外部电子邮件地址**   这是邮件联系人的主 SMTP 地址及其外部电子邮件帐户。发送给此联系人的电子邮件将会转发到此电子邮件地址。

  - 单击\&quot;更多选项\&quot;可显示包含邮件联系人帐户的 OU。必须使用 Active Directory 用户和计算机将联系人移动到其他 OU。

## 联系人信息

使用\&quot;联系人信息\&quot;部分可以查看或更改收件人的联系信息，例如邮件地址和电话号码。此信息会显示在通讯簿中。

## 组织

使用\&quot;组织\&quot;部分可以记录有关组织中邮件联系人的角色的详细信息。此信息会显示在通讯簿中。也可以创建可从电子邮件客户端（如 Outlook）访问的虚拟组织图。

  - **职务**   使用此框可以查看或更改联系人的职务。

  - **部门**   使用此框可以查看或更改联系人所在的部门。可以使用此框为动态通讯组和通讯簿创建收件人条件。

  - **公司**   使用此框可以查看或更改联系人所在的公司。还可以使用此框为动态通讯组创建收件人条件。

  - **经理**   若要添加经理，请单击\&quot;浏览\&quot;。在\&quot;选择经理\&quot;中，选择相应的人员，然后单击\&quot;确定\&quot;。

  - **直接下属**   无法修改此框。*直接下属*是指向特定经理报告的收件人。如果已为收件人指定一个经理，则该收件人将作为直接下属出现在该经理的邮箱的详细信息中。例如，Toby 管理邮件联系人 Ann 和 Spencer，因此在 Ann 和 Spencer 的组织属性的\&quot;经理\&quot;框中指定 Toby，而 Ann 和 Spencer 出现在 Toby 的邮箱属性的\&quot;直接下属\&quot;框中。

## 电子邮件选项

使用\&quot;电子邮件选项\&quot;部分可以添加或删除邮件联系人的代理地址或编辑现有的代理地址。邮件联系人的主 SMTP 地址也显示在此部分中，但无法更改它。要更改它，必须在\&quot;常规\&quot;部分更改联系人的外部电子邮件地址。

> [!NOTE]  
> <strong>电子邮件选项</strong>部分只是在Exchange Server 2013中可用。不在Exchange Online中可用。


## 邮件提示

使用\&quot;邮件提示\&quot;部分可添加邮件提示，以便在用户向此收件人发送邮件之前提醒用户存在潜在的问题。邮件提示是在将此收件人添加到新电子邮件的\&quot;收件人\&quot;、\&quot;抄送\&quot;或\&quot;密件抄送\&quot;行中时，信息栏中显示的文本。

> [!NOTE]  
> 邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。


## 使用命令行管理程序更改邮件联系人属性

邮件联系人的属性存储在 Active Directory 和 Exchange 中。通常，使用 **Get-Contact** 和 **Set-Contact** cmdlet 查看和更改组织和联系人信息属性。使用 **Get-MailContact** 和 **Set-MailContact** cmdlet 查看或更改邮件相关属性（例如电子邮件地址、邮件提示、自定义属性以及是否在地址列表中隐藏联系人）。

有关详细信息，请参阅下列主题：

  - [Get-Contact](https://technet.microsoft.com/zh-cn/library/aa998258\(v=exchg.150\))

  - [Set-Contact](https://technet.microsoft.com/zh-cn/library/bb124535\(v=exchg.150\))

  - [Get-MailContact](https://technet.microsoft.com/zh-cn/library/bb124717\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-cn/library/aa995950\(v=exchg.150\))

下面是使用命令行管理程序更改邮件联系人属性的一些示例。

此示例配置邮件联系人 Kai Axford 的\&quot;职务\&quot;、\&quot;部门\&quot;、\&quot;公司\&quot;和\&quot;经理\&quot;属性。

    Set-Contact "Kai Axford" _-Title Consultant -Department "Public Relations" -Company Fabrikam -Manager "Karen Toh"

此示例将所有邮件联系人的 CustomAttribute1 属性设置为值 PartTime 并在组织的通讯簿中隐藏这些联系人。

    Get-MailContact | Set-MailContact -CustomAttribute1 PartTime -HiddenFromAddressListsEnabled $true

此示例将 Public Relations 部门中所有邮件联系人的 CustomAttribute15 属性设置为值 TemporaryEmployee。

    Get-Contact -Filter "Department -eq 'Public Relations'" | Set-MailContact -CustomAttribute15 TemporaryEmployee

## 您如何知道这有效？

要验证是否已成功更改邮件联系人的属性，请执行以下操作：

  - 在 EAC 中，选择邮件联系人，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 查看您更改的属性。

  - 在外壳程序中，使用**Get-Contact**和**Get-MailContact** cmdlet 以验证所做的更改。使用外壳程序的优点之一是您可以查看多个邮件联系人的多个属性。在所有邮件联系人有 CustomAttribute1 属性设置为 PartTime 何地被从通讯簿中隐藏上面的示例，运行以下命令以验证所做的更改。
    
        Get-MailContact | Fl Name,CustomAttribute1,HiddenFromAddressListsEnabled
    
    在上面的示例中，为 Public Relations 部门中的所有邮件联系人设置了 CustomAttribute15，运行以下命令来验证所做的更改：
    
        Get-Contact -Filter "Department -eq 'Public Relations'" | Get-MailContact | FL Name,CustomAttribute15

## 批量编辑邮件联系人

可以使用 EAC 更改多个邮件联系人的所选属性。在 EAC 中从联系人列表中选择两个或更多邮件联系人时，可以批量编辑的属性会显示在\&quot;详细信息\&quot;窗格中。在更改其中一个属性后，所做更改将应用到所有选定的收件人。

批量编辑邮件联系人时，可以更改以下属性区域：

  - **联系人信息**   更改共享属性，如街道、邮编和城市名称。

  - **组织**   更改共享属性，如部门名称、公司名称和选定邮件联系人或邮件用户的直接经理。

## 使用 EAC 批量编辑邮件联系人

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;联系人\&quot;。

2.  在联系人列表中，选择两个或更多邮件联系人。无法批量编辑邮件联系人和邮件用户的组合。
    
    > [!TIP]  
    > 按住 Shift 键并单击第一个邮件联系人，然后单击最后一个要编辑的邮件联系人，可以选择多个相邻的邮件联系人。按住 Ctrl 键并单击每个要编辑的邮件联系人，也可以选择多个邮件联系人。


3.  在\&quot;详细信息\&quot;窗格中的\&quot;批量编辑\&quot;下，单击\&quot;联系人信息\&quot;或\&quot;组织\&quot;下的\&quot;更新\&quot;。

4.  更改属性页面，然后保存所做的更改。

## 您如何知道这有效？

要验证是否成功批量编辑了邮件联系人，请执行以下操作之一：

  - 在 EAC 中，选择批量编辑的每个邮件联系人，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标") 查看已更改的属性。

  - 在 Shell 中使用**Get-Contact** cmdlet 以验证所做的更改。例如，假设您用于批量编辑功能中 EAC 更改名为百达公司的供应商公司的经理和所有邮件联系人的办公室。若要验证这些更改，无法在外壳程序中运行以下命令。
    
        Get-Contact -ResultSize unlimited -Filter {(Company -eq 'Adatum')} | fl Name,Office,Manager


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="&amp;quot;领英学习&amp;quot;短图标" alt="&amp;quot;领英学习&amp;quot;短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

