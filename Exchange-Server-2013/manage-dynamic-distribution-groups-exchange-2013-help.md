---
title: '管理动态通讯组: Exchange Online Help'
TOCTitle: 管理动态通讯组
ms:assetid: 8ef85d0a-41df-4b5c-b8e7-ca8d09c048ca
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123722(v=EXCHG.150)
ms:contentKeyID: 50489699
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDynamicGroupWizardForm.CreateDynamicGroupInformationWizardPage
ms.translationtype: MT
---

# 管理动态通讯组

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

动态通讯组是启用了邮件的 Active Directory 组对象，创建它们的目的是为了加快 Microsoft Exchange 组织中电子邮件以及其他信息的批量发送速度。

与包含一组已定义成员的常规通讯组不同，每次向动态通讯组发送邮件时，都将根据所定义的筛选器和条件来计算该组的成员列表。电子邮件发送到动态通讯组时，将被传递到组织中所有与为该动态通讯组定义的条件匹配的收件人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>动态通讯组包含 Active Directory 中属性值与组筛选器匹配的所有收件人。如果修改收件人属性以与筛选器匹配，该收件人可能会无意中成为组成员而开始接收发送给组的邮件。定义良好、一致的帐户设置过程可以降低发生此问题的机率。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [收件人权限](recipients-permissions-exchange-2013-help.md)主题中的\&quot;动态通讯组\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 创建动态通讯组

## 使用 EAC 创建动态通讯组

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;\>\&quot;新建\&quot;\>\&quot;动态通讯组\&quot;。

2.  
    
    在\&quot;新建动态通讯组\&quot;页面上，填写下列各框：
    
      - **\* 显示名称**   使用此框键入显示名称。此名称将出现在共享的通讯簿中、\&quot;收件人:\&quot;行中（电子邮件发送到该组时），以及 EAC 的\&quot;组\&quot;列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。它在林中必须也是唯一的。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>组命名策略不会应用于动态通讯组。</td>
        </tr>
        </tbody>
        </table>
    
      - **\* 别名**   使用此框可以键入组的别名。别名不能超过 64 个字符，并且在林中必须是唯一的。当用户在电子邮件的\&quot;收件人:\&quot;行中键入别名时，它将解析为该组的显示名称。
    
      - **描述**   使用此框可以对组进行说明，以便用户了解组的用途。此描述将显示在共享通讯簿中。
    
      - **组织单位**   可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为域 Active Directory 中的\&quot;用户\&quot;容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的\&quot;用户\&quot;容器。如果将收件人范围设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击\&quot;浏览\&quot;。该对话框显示林中的指定作用域内的所有 OU。选择所需的 OU，然后单击\&quot;确定\&quot;。
    
      - **所有者**  动态通讯组的所有者为可选项。你可以单击\&quot;**浏览**\&quot;，然后从列表中选择用户来添加所有者。

3.  
    
    使用\&quot;**成员**\&quot;部分指定动态通讯组的收件人类型，然后设置用于确定成员身份的规则。选择下列各框之一：
    
      - **所有收件人类型**   选择此选项，可向所有收件人类型发送与该组所定义的条件相符的邮件。
    
      - **仅以下收件人类型**   符合为该组所定义的条件的邮件将发送至下列一个或多个收件人类型：
        
          - **具有 Exchange 邮箱的用户**   如果要包括拥有 Exchange 邮箱的用户，请选中此复选框。拥有 Exchange 邮箱的用户是指在 Exchange 组织中具有用户域帐户和邮箱的用户。
        
          - **具有外部电子邮件地址的用户**   如果要包括拥有外部电子邮件地址的用户，请选中此复选框。拥有外部电子邮件帐户的用户在 Active Directory 中有用户域帐户，但是使用位于组织外部的电子邮件帐户。这使他们能够包括在全局地址列表 (GAL) 中，并被添加到通讯组列表。
        
          - **资源邮箱**   如果要包含 Exchange 资源邮箱，请选中此复选框。资源邮箱允许你通过邮箱管理公司资源，如会议室或公司交通工具。
        
          - **具有外部电子邮件地址的联系人**   如果要包括拥有外部电子邮件地址的联系人，请选中此复选框。拥有外部电子邮件地址的联系人在 Active Directory 中没有用户域帐户，但是外部电子邮件地址在 GAL 中可用。
        
          - **已启用邮件的组**   如果要包含已启用邮件的安全组或通讯组，请选中此复选框。已启用邮件的组与通讯组相似。发送到启用了邮件的组帐户的电子邮件将传递给多个收件人。

4.  
    
    单击\&quot;添加规则\&quot;为该组中的成员身份定义条件。

5.  从下拉列表中选择下列收件人属性之一，然后提供一个值。如果选定属性的值与你定义的值相符，收件人将收到一封发送到该组的邮件。
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>属性</th>
    <th>需要向收件人发送邮件的情况</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>&amp;quot;收件人&amp;quot;容器</strong></p></td>
    <td><p>收件人对象位于指定的域或 OU 中。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>省/市/自治区</strong></p></td>
    <td><p>指定的值与收件人的&amp;quot;省/市/自治区&amp;quot;属性相符。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Company</strong></p></td>
    <td><p>指定的值与收件人的&amp;quot;公司&amp;quot;属性相符。</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Department</strong></p></td>
    <td><p>指定的值与收件人的&amp;quot;部门&amp;quot;属性相符。</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>自定义属性 N</strong>（其中 N 是从 1 到 15 的数字）</p></td>
    <td><p>指定的值与收件人的&amp;quot;自定义属性 N&amp;quot;属性相符。</p></td>
    </tr>
    </tbody>
    </table>
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>你为选定属性输入的值必须与收件人相应属性中显示的值完全相符。例如，如果为&amp;quot;<strong>省/市/自治区</strong>&amp;quot;输入&amp;quot;<strong>Washington</strong>&amp;quot;，但收件人的属性值为&amp;quot;<strong>WA</strong>&amp;quot;，则不会满足条件。另外，你指定的基于文本的值不区分大小写。例如，如果你为&amp;quot;<strong>公司</strong>&amp;quot;属性指定了 <strong>Contoso</strong>，邮件将发送给该值为 <strong>contoso</strong> 的收件人。</td>
    </tr>
    </tbody>
    </table>


6.  在\&quot;**指定词语或短语**\&quot;窗口中，在文本框中键入值。单击\&quot;**添加**\&quot;，然后单击\&quot;**确定**\&quot;。

7.  要添加另一条规则来定义成员身份的条件，请在创建的前一条规则下单击\&quot;添加规则\&quot;。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果要添加多条规则来定义成员身份，收件人必须满足每条规则的条件才能收到发送给组的邮件。换言之，每条规则都以布尔操作符 <strong>AND</strong> 相连。</td>
    </tr>
    </tbody>
    </table>


8.  完成后，单击\&quot;保存\&quot;创建动态通讯组。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果希望为除了 EAC 中的可用属性以外的属性指定规则，必须使用 Shell 创建动态通讯组。请注意，具有自定义收件人筛选器的动态通讯组的筛选器和条件设置只能通过使用 Shell 进行管理。有关如何使用自定义查询创建动态通讯组的示例，请参阅下面一节的&amp;quot;使用 Shell 创建动态通讯组&amp;quot;。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序创建动态通讯组

本示例将创建仅包含邮箱用户的动态通讯组\&quot;Mailbox Users DDG\&quot;。

    New-DynamicDistributionGroup -IncludedRecipients MailboxUsers -Name "Mailbox Users DDG" -OrganizationalUnit Users

此示例创建具有自定义收件人筛选器的动态通讯组。该动态通讯组包含名为 Server1 的服务器上的所有邮箱用户。

    New-DynamicDistributionGroup -Name "Mailbox Users on Server1" -OrganizationalUnit Users -RecipientFilter {((RecipientTypeDetails -eq 'UserMailbox' -and ServerName -eq 'Server1'))}

此示例创建具有自定义收件人筛选器的动态通讯组。该动态通讯组包含\&quot;**CustomAttribute10**\&quot;的属性值为\&quot;FullTimeEmployee\&quot;的所有邮箱用户。

    New-DynamicDistributionGroup -Name "Full Time Employees" -RecipientFilter {(RecipientTypeDetails -eq 'UserMailbox') -and (CustomAttribute10 -eq 'FullTimeEmployee')}

有关语法和参数的详细信息，请参阅 [New-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb125127\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功创建了动态通讯组，请执行下列操作之一：

  - 在 EAC 中，导航到\&quot;**收件人**\&quot;\>\&quot;**组**\&quot;。新的动态通讯组将显示在组列表中。在\&quot;**组类型**\&quot;下，类型为\&quot;**动态通讯组**\&quot;。

  - 在命令行管理程序中，运行下列命令显示关于新动态通讯组的信息。
    
        Get-DynamicDistributionGroup | FL Name,RecipientTypeDetails,RecipientFilter,PrimarySmtpAddress

## 更改动态通讯组的属性

## 使用 EAC 更改动态通讯组的属性

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;组\&quot;。

2.  在组列表中，单击要查看或更改的动态通讯组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在组的属性页面上，单击下列部分之一查看或更改属性。
    
      - General
    
      - Ownership
    
      - Membership
    
      - Delivery management
    
      - Message approval
    
      - Email options
    
      - MailTip
    
      - Group delegation

## 常规

使用此部分可以查看或更改有关组的基本信息。

  - **\* 显示名称**   此名称将会出现在通讯簿中、电子邮件中的\&quot;收件人:\&quot;行中（电子邮件发送到该组时），以及\&quot;组\&quot;列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。显示名称在域中还必须是唯一的。

  - \&quot;\* 别名\&quot;   这是电子邮件地址中出现在 (@) 符号左侧的部分。如果更改别名，组的主 SMTP 地址也会更改，并包含新的别名。同时，带有之前别名的电子邮件地址将作为该组的代理地址保留。

  - \&quot;描述\&quot;   使用此框可以对组进行说明，以便用户了解组的用途。此说明出现在通讯簿和 EAC 的\&quot;详细信息\&quot;窗格中。

  - \&quot;在地址列表中隐藏此组\&quot; 如果您不希望用户在通讯簿中看到此组，则选中此复选框。若要将电子邮件发送到该组，发件人必须在\&quot;收件人:\&quot;或\&quot;抄送:\&quot;行上键入组的别名或电子邮件地址。

  - **组织单位**   此只读框显示包含动态通讯组的组织单位 (OU)。必须使用 Active Directory 用户和计算机将组移动到不同的 OU。

## 所有权

使用此部分可以指定组的所有者。动态通讯组只能有一个所有者。组的所有者显示在 Active Directory 用户和计算机中的对象的\&quot;**管理者**\&quot;选项卡上。

你可以单击\&quot;**浏览**\&quot;，然后从列表中选择添加所有者。要删除所有者，请单击\&quot;**清除**\&quot;，然后单击\&quot;**保存**\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

## 成员身份

使用此部分可以更改用于确定组成员身份的条件。你可以删除或更改现有的成员身份规则和添加新规则。有关说明如何执行此操作的步骤，请参阅在使用 EAC 新建动态通讯组时配置成员身份步骤中的步骤 3。

## 传递管理

使用此部分可以管理谁将电子邮件发送到该组。

  - **仅属于你所在组织的发件人**   选择此选项可以仅允许组织中的发件人向此组发送邮件。这意味着如果组织外部的某个人向此组发送电子邮件，邮件将被拒绝。这是默认设置。

  - **允许组织内外的发件人**   选择此选项可以允许任何人向此组发送邮件。
    
    您可以通过仅允许特定发件人向此组发送邮件，来进一步限制可以将邮件发送到此组的发件人。单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择一个或多个收件人。向此列表中添加发件人后，这些发件人将是唯一能够向此组发送邮件的人员。不在此列表中的任何人发送的邮件都将被拒绝。
    
    若要从列表中删除个人或组，请从列表中选择相应的个人或组，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果您已将此组配置为只允许组织内部的发件人向此组发送邮件，则从邮件联系人发送的电子邮件将被拒绝，即使这些联系人已添加到此列表中也是如此。</td>
    </tr>
    </tbody>
    </table>


## 邮件审批

使用此部分可以设置用于仲裁组的选项。审阅人可以在发送到此组的邮件到达组成员之前批准或拒绝邮件。

  - \&quot;发送到此组的邮件必须由审阅人批准\&quot;   默认情况下未选中此复选框。如果选中此复选框，则在传递传入邮件之前将由组审阅人检查邮件。组审阅人可以批准或拒绝传入邮件。

  - \&quot;组仲裁人\&quot;   若要添加组仲裁人，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。若要删除仲裁人，请选择仲裁人，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。如果已经选中\&quot;发送到此组的邮件必须由审阅人批准\&quot;，但未选择审阅人，则发送到此组的邮件将会发送到组所有者进行审批。

  - \&quot;不要求进行邮件审批的发件人\&quot;   若要添加可以绕过组审阅的个人或组，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。若要删除个人或组，请选择相应项目，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

  - **选择审阅通知** 使用此部分可以设置如何通知用户有关邮件审批的情况。
    
      - \&quot;当发件人的邮件未得到批准时，通知所有发件人\&quot;   这是默认设置。当组织内部和外部发件人的邮件未得到批准时，通知所有发件人。
    
      - **仅当组织中发件人的邮件未得到批准时，通知这些发件人**如果选择此选项，当组织中的个人或组发送到此组的邮件未得到审阅人批准时，仅通知这些发件人。
    
      - \&quot;某邮件未通过批准时，不通知任何人\&quot;   如果选择此选项，则不会向组审阅人未批准其邮件的邮件发件人发送通知。

## 电子邮件选项

使用此部分可以查看或更改与该组关联的电子邮件地址。这包括组的主 SMTP 地址和任何关联的代理地址。主 SMTP 地址（也称为\&quot;回复地址\&quot;）在地址列表中以粗体显示，大写的 **SMTP** 值显示在\&quot;类型\&quot;列中。

  - \&quot;添加\&quot;   单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - \&quot;SMTP\&quot;   这是默认的地址类型。单击此按钮，然后在\&quot;\* 电子邮件地址\&quot;框中键入新的 SMTP 地址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要让新地址称为该组的主 SMTP 地址，请选中&amp;quot;将其作为回复地址&amp;quot;复选框。</td>
        </tr>
        </tbody>
        </table>
    
      - \&quot;自定义地址类型\&quot;   单击此按钮，然后在\&quot;\* 电子邮件地址\&quot;框中键入一个支持的非 SMTP 电子邮件地址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>除 X.400 地址以外，Exchange 不验证自定义地址的格式是否正确。您必须确保所指定的自定义地址符合该地址类型的格式要求。</td>
        </tr>
        </tbody>
        </table>


  - **编辑**   要更改与组关联的电子邮件地址，请从列表中选择该地址，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要让现有地址成为该组的主 SMTP 地址，请选中&amp;quot;将其作为回复地址&amp;quot;复选框。</td>
    </tr>
    </tbody>
    </table>


  - **移除**   要删除与组关联的电子邮件地址，请从列表中选择该地址，然后单击\&quot;移除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

  - \&quot;基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址\&quot;   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。此框在默认情况下处于选中状态。

## MailTip

使用此部分可以添加邮件提示，以便在用户向该组发送邮件时提醒用户存在潜在的问题。邮件提示是在将该组添加到新电子邮件的\&quot;收件人\&quot;、\&quot;抄送\&quot;或\&quot;密件抄送\&quot;行时，信息栏中显示的文本。例如，对于较大的组，可添加邮件提示来提醒潜在的发送人：他们的邮件将会发送给很多人。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>邮件提示可包含 HTML 标记，但不允许包含脚本。自定义邮件提示的长度不能超过 175 个显示的字符。此字符限制不计入 HTML 标记。</td>
</tr>
</tbody>
</table>


## 组代理

使用此部分可以向用户分配权限（称为\&quot;代理\&quot;），允许他们以组身份发送邮件或代表组发送邮件。可以分配以下权限：

  - \&quot;发送身份\&quot;   此权限允许代理以组身份发送邮件。分配此权限后，代理可选择将组添加到\&quot;发件人\&quot;行以指示该邮件由组发送。

  - **代表以下用户发送**   此权限也允许代理代表组发送邮件。在分配该选项后，代理可选择在\&quot;**发件人**\&quot;行中添加组。邮件将显示为由组发送，并将说明该邮件由代理代表组发送。

若要向代理分配权限，请单击相应权限下面的\&quot;添加\&quot;显示\&quot;选择收件人\&quot;页面，该页面将显示 Exchange 组织内可分配该权限的所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击\&quot;确定\&quot;。也可以通过在搜索框中键入该收件人的姓名，然后单击\&quot;搜索\&quot;，搜索特定的收件人。

## 使用命令行管理程序更改动态通讯组的属性

使用 **Get-DynamicDistributionGroup** 和 **Set-DynamicDistributionGroup** cmdlet 查看和更改动态通讯组的属性。使用命令行管理程序的优势在于不但可以更改 EAC 中不可用的属性，而且可以更改多个组的属性。有关与通讯组属性对应的参数的信息，请参阅下列主题：

  - [Get-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124762\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb123796\(v=exchg.150\))

下面是一些使用命令行管理程序更改动态通讯组属性的示例：

本示例更改组织中的所有动态通讯组的下列参数：

  - 在通讯簿中隐藏所有动态通讯组

  - 将可发送至组的最大邮件大小设置为 5MB

  - 启用审阅

  - 指派管理员作为组审阅人

<!-- end list -->

    Get-DynamicDistributionGroup -ResultSize unlimited | Set-DynamicDistributionGroup -HiddenFromAddressListsEnabled $true -MaxReceiveSize 5MB -ModerationEnabled $true -ModeratedBy administrator

本示例将代理 SMTP 的电子邮件地址 Seattle.Employees@contoso.com 添加到\&quot;All Employees\&quot;组。

    Set-DynamicDistributionGroup -Identity "All Employees" -EmailAddresses SMTP:All.Employees@contoso.com, smtp:Seattle.Employees@contoso.com

## 您如何知道这有效？

要验证您是否已成功更改了动态通讯组的属性，请执行下列操作：

  - 在 EAC 中选择组，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看已更改的属性或功能。根据所更改的属性，它可能显示在选定组的\&quot;详细信息\&quot;窗格中。

  - 在 Shell 中，使用 **Get-DynamicDistributionGroup** cmdlet 验证各项更改。使用 Shell 的一个优点是可查看多个组的多个属性。在第一个示例中，你可以运行下列命令来验证新值。
    
        Get-DynamicDistributionGroup -ResultSize unlimited | fl Name,HiddenFromAddressListsEnabled,MaxReceiveSize,ModerationEnabled,ModeratedBy
    
    对于上面更改邮件限制的示例，请运行此命令。
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

