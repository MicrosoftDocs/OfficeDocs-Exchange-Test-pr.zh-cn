---
title: '创建和管理通讯组: Exchange 2013 Help'
TOCTitle: 创建和管理通讯组
ms:assetid: c4c43493-55e1-46d2-bd4b-d6f6cecd747f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124513(v=EXCHG.150)
ms:contentKeyID: 50491668
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.CreateDistributionGroupWizardForm.CreateDistributionGroupIntroductionWizardPage
ms.translationtype: HT
---

# 创建和管理通讯组

 

_**适用于：** Exchange Online, Exchange Server 2016, Office 365_

_**上一次修改主题：** 2016-12-09_

使用 Exchange 管理中心 (EAC) 或 Exchange 命令行管理程序在 Exchange 组中新建通讯组或为 Active Directory 中的现有组启用邮件。

有两类组可用于分发邮件：

  - “已启用邮件的通用通讯组”（也称为“通讯组”）仅用于分发邮件。

  - “已启用邮件的通用安全组”（也称为“安全组”）可用于分发邮件，还可用于授予对 Active Directory 中资源的访问权限。有关详细信息，请参阅[管理启用邮件的安全组](manage-mail-enabled-security-groups-exchange-2013-help.md)。

请务必注意 Active Directory 与 Exchange 之间的术语差异。在 Active Directory 中，通讯组是指任何不具有安全上下文的组，而无论它是否已启用邮件。与之相反，在 Exchange 中，所有的已启用邮件组都称为通讯组，而无论它们是否具有安全上下文。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“通讯组”条目。

  - 如果您的组织已配置了组命名策略，则只对用户创建的组应用组命名策略。当您或其他管理员使用 EAC 创建通讯组时，组命名策略将被忽略，并且不会应用于组名称。但是，如果您使用命令行管理程序创建或重命名通讯组，也将会应用策略，除非您使用 *IgnoreNamingPolicy* 参数覆盖该组命名策略。有关详细信息，请参阅：
    
      - [创建通讯组命名策略](create-a-distribution-group-naming-policy-exchange-2013-help.md)
    
      - [重命名策略的通讯组](override-the-distribution-group-naming-policy-exchange-2013-help.md)

## 您想执行什么操作？

## 创建通讯组

## 使用 EAC 创建通讯组

1.  在 EAC 中，导航到“收件人”\>“组”。

2.  单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")\>“通讯组”。

3.  
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><img src="images/Bb124513.3ea82c95-9dda-450f-823b-cd0772249d81(EXCHG.150).png" title="新增 Office 365 组试用" alt="新增 Office 365 组试用" /><br />
    如果具有 Office 365 企业版计划或 Exchange Online 计划，现在就可以创建 Office 365 组来取代通讯组。Office 365 组具有通讯组的功能及和其他更多功能。具备了 Office 365 组，你可以向某个组发送电子邮件、共享公用日历，还拥有一个保存和处理组文件和文件夹的库。单击“<strong>新建</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="添加图标" alt="添加图标" />”&gt;“<strong>Office 365 组</strong>”，开始使用并查看 <a href="https://go.microsoft.com/fwlink/p/?linkid=800653">Office 365 组 - 管理员帮助</a>。<br />
    如果有想要迁移到 Office 365 组的现有通讯组，请查看<a href="https://go.microsoft.com/fwlink/p/?linkid=824756">将通讯组列表迁移到 Office 365 组 - 管理员帮助</a>。<br />
    如果仍然想要创建一个通讯组，可以单击或点击“<strong>新建通讯组</strong>”向导。</td>
    </tr>
    </tbody>
    </table>


4.  
    
    在“新建通讯组”页上，填写下列框：
    
      - “\* 显示名”   使用此框可以键入显示名。此名称将出现在组织的通讯簿中、电子邮件中的“收件人:”行中（电子邮件发送到该组时），以及 EAC 的“组”列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。它在林中必须也是唯一的。
    
      - “\* 别名”   使用此框可以键入组的别名。别名不能超过 64 个字符，并且在林中必须是唯一的。当用户在电子邮件的“收件人:”行中键入别名时，它将解析为该组的显示名称。
    
      - **组织单位**   （将仅在 Exchange 2013 本地中看到此选项）可选择非默认的组织单位 (OU)（属于收件人作用域）。如果将收件人作用域设置为林，则默认值设置为 Active Directory 域中的“用户”容器，该域包含运行 EAC 的计算机。如果将收件人作用域设置为特定域，则将默认选择该域中的“用户”容器。如果将收件人范围设置为某个特定 OU，则默认情况下，将选择该 OU。
        
        若要选择一个不同的 OU，请单击“浏览”。该对话框显示林中的指定作用域内的所有 OU。选择所需的 OU，然后单击“确定”。
    
      - **\* 所有者**   默认情况下，创建组的人即为所有者。所有组都必须至少有一个所有者。可以通过单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")来添加所有者。
    
      - “成员”   使用此部分可以添加成员并指定是否需要对人员加入或退出此组进行审批。
        
        组所有者不必是组的成员。使用“将组所有者添加为成员”可以将所有者添加为成员，或删除所有者的成员身份。
        
        若要向组中添加成员，请单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。添加完成员之后，单击“确定”以返回到“新建通讯组”页。
        
        在“选择是否需要所有者批准才能加入组”下，指定对于要加入组的人是否需要批准。选择下列设置之一：
        
          - **打开：任何人都可以加入而不需要该组的所有者审批** 这是默认设置。
        
          - **关闭：只能由组所有者添加成员。只有组的所有者才能添加成员**
        
          - “所有者审批：所有请求都必须由组所有者进行手动批准或拒绝”   如果选择此选项，则组所有者将会收到加入组的审批请求电子邮件。
        
        在“选择组是否允许自由离开”下，指定对于要离开组的人是否需要批准。选择下列设置之一：
        
          - **开放:任何人都可以离开而不需要组所有者批准** 这是默认设置。
        
          - “关闭：** 只能组所有者才能删除成员。将自动拒绝所有离开请求   **

5.  完成后，请单击“保存”创建通讯组。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>默认情况下，新通讯组都要求对所有发件人进行身份验证。这样可防止外部发件人将邮件发送到通讯组。要将通讯组配置为接受来自所有收件人的邮件，您必须修改该通讯组的邮件传递限制设置。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序创建通讯组

该示例创建具有别名 **itadmin** 和名称 **IT Administrators** 的通信组。通讯组在默认 OU 中创建，任何人都可以不经组拥有者批准加入该组。

    New-DistributionGroup -Name "IT Administrators" -Alias itadmin -MemberJoinRestriction open

有关使用命令行管理程序的详细信息，请参阅[New-DistributionGroup](https://technet.microsoft.com/zh-cn/library/aa998856\(v=exchg.150\))。

## 您如何知道这有效？

要检查是否成功创建了通讯组，可进行以下操作之一：

  - 在 EAC 中，导航到“收件人”\>“组”。新通讯组显示在组列表中。在“组类型”下，该类型是“通讯组”。

  - 在命令行管理程序中运行以下命令来显示有关新通讯组的信息。
    
        Get-DistributionGroup <Name> | FL Name,RecipientTypeDetails,PrimarySmtpAddress

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>只能创建通用通讯组或对其启用邮件。若要将本地域或全局组转换为通用组，可以使用命令行管理程序中的 <a href="https://technet.microsoft.com/zh-cn/library/bb123770(v=exchg.150)">Set-Group</a> cmdlet。可以具有从早期版本的 Exchange 中迁移来的、并非通用组的启用邮件组。可以使用 EAC 或命令行管理程序管理这些组</td>
</tr>
</tbody>
</table>


## 更改通讯组属性

## 使用 EAC 更改通讯组属性

1.  在 EAC 中，导航到“收件人”\>“组”。

2.  在此组列表中，单击您要查看或更改的通讯组，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在组属性页面上，单击以下部分之一来查看或更改属性。
    
      - 常规
    
      - 所有权
    
      - 成员身份
    
      - 成员身份审批
    
      - 传递管理
    
      - 邮件审批
    
      - 电子邮件选项
    
      - MailTip
    
      - 组代理

## 常规

使用此部分可以查看或更改有关组的基本信息。

  - **\* 显示名称**   此名称将会出现在通讯簿中、电子邮件中的“收件人:”行中（电子邮件发送到该组时），以及“组”列表中。显示名称是必需的，并且应当是用户友好的，以便用户可以识别它。显示名称在域中还必须是唯一的。
    
    如果您已实现了一个组命名策略，则显示名称必须符合此策略定义的命名格式。

  - “\* 别名”   这是电子邮件地址中出现在 (@) 符号左侧的部分。如果更改别名，组的主 SMTP 地址也会更改，并包含新的别名。同时，带有之前别名的电子邮件地址将作为该组的代理地址保留。

  - “描述”   使用此框可以对组进行说明，以便用户了解组的用途。此说明出现在通讯簿和 EAC 的“详细信息”窗格中。

  - “在地址列表中隐藏此组” 如果您不希望用户在通讯簿中看到此组，则选中此复选框。若要将电子邮件发送到该组，发件人必须在“收件人:”或“抄送:”行上键入组的别名或电子邮件地址。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>应考虑隐藏安全组，原因是这些组通常用于向组成员分配权限，而不是用于发送电子邮件。</td>
    </tr>
    </tbody>
    </table>


  - “组织单位”   该只读框显示包含通讯组的组织单位 (OU)。必须使用 Active Directory 用户和计算机将组移动到不同的 OU。

## 所有权

使用此部分可以分配组所有者。组所有者可以向此组中添加成员、批准或拒绝加入或退出此组的请求以及批准或拒绝发送给此组的邮件。默认情况下，创建组的人即为所有者。所有组都必须至少有一个所有者。

可以通过单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")来添加所有者。通过选中一个所有者然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")，可以删除该所有者。

## 成员身份

使用此部分可以添加或删除成员。组所有者不必是组的成员。在“成员”下，可通过单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")来添加成员。可通过在成员列表中选择一个用户然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")来删除成员。

## 成员身份审批

使用此部分可以指定是否需要对用户加入或离开该组进行审批。

  - “选择是否需要所有者批准才能加入组”   选择以下设置之一：
    
      - “开放：任何人都可以加入此组，而无需经组的所有者批准”
    
      - **关闭：只有组所有者才能添加成员。只有组的所有者才能添加成员**
    
      - “所有者审批：所有请求都必须由组所有者手动批准或拒绝”   如果选择此选项，则组所有者将会收到加入组的审批请求电子邮件。

  - **选择是否将组保留为打开状态   **选择以下设置之一：
    
      - “开放：任何人都可以离开此组，而无需经组的所有者批准”
    
      - “关闭：** 只有组所有者才能删除成员。将自动拒绝所有离开请求   **

## 传递管理

使用此部分可以管理谁将电子邮件发送到该组。

  - **仅属于您所在组织的发件人**   选择此选项可以仅允许组织中的发件人向此组发送邮件。这意味着如果组织外部的某个人向此组发送电子邮件，邮件将被拒绝。这是默认设置。

  - **允许组织内外的发件人**   选择此选项可以允许任何人向此组发送邮件。
    
    您可以通过仅允许特定发件人向此组发送邮件，来进一步限制可以将邮件发送到此组的发件人。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择一个或多个收件人。向此列表中添加发件人后，这些发件人将是唯一能够向此组发送邮件的人员。不在此列表中的任何人发送的邮件都将被拒绝。
    
    若要从列表中删除个人或组，请从列表中选择相应的个人或组，然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。
    
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

  - “发送到此组的邮件必须由审阅人批准”   默认情况下未选中此复选框。如果选中此复选框，则在传递传入邮件之前将由组审阅人检查邮件。组审阅人可以批准或拒绝传入邮件。

  - “组仲裁人”   若要添加组仲裁人，请单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。若要删除仲裁人，请选择仲裁人，然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。如果已经选中“发送到此组的邮件必须由审阅人批准”，但未选择审阅人，则发送到此组的邮件将会发送到组所有者进行审批。

  - “不要求进行邮件审批的发件人”   若要添加可以绕过组审阅的个人或组，请单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。若要删除个人或组，请选择相应项目，然后单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

  - **选择审阅通知** 使用此部分可以设置如何通知用户有关邮件审批的情况。
    
      - “当发件人的邮件未得到批准时，通知所有发件人”   这是默认设置。当组织内部和外部发件人的邮件未得到批准时，通知所有发件人。
    
      - “当组织中发件人的邮件未得到批准时，通知这些发件人”如果选择此选项，则在审阅人未批准组织中的个人或组发送到此组的邮件时仅通知相应的发件人。
    
      - “某邮件未通过批准时，不通知任何人”   如果选择此选项，则不会向组审阅人未批准其邮件的邮件发件人发送通知。

## 电子邮件选项

使用此部分可以查看或更改与该组关联的电子邮件地址。这包括组的主 SMTP 地址和任何关联的代理地址。主 SMTP 地址（也称为“回复地址”）在地址列表中以粗体显示，大写的 **SMTP** 值显示在“类型”列中。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。单击此按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>若要让新地址称为该组的主 SMTP 地址，请选中“将其作为回复地址”复选框。</td>
        </tr>
        </tbody>
        </table>
    
      - “自定义地址类型”   单击此按钮，然后在“\* 电子邮件地址”框中键入一个支持的非 SMTP 电子邮件地址。
        
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


  - “编辑”   要更改与组关联的电子邮件地址，在列表中选择该地址，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>若要让现有地址成为该组的主 SMTP 地址，请选中“将其作为回复地址”复选框。</td>
    </tr>
    </tbody>
    </table>


  - “移除”   要删除与组关联的电子邮件地址，在列表中选择该地址，然后单击“移除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

  - “基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址”   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。此框在默认情况下处于选中状态。

## MailTip

使用此部分可以添加邮件提示，以便在用户向该组发送邮件时提醒用户存在潜在的问题。邮件提示是在将该组添加到新电子邮件的“收件人”、“抄送”或“密件抄送”行时，信息栏中显示的文本。例如，对于较大的组，可添加邮件提示来提醒潜在的发送人：他们的邮件将会发送给很多人。

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

使用此部分可以向用户分配权限（称为“代理”），允许他们以组身份发送邮件或代表组发送邮件。可以分配以下权限：

  - “发送身份”   此权限允许代理以组身份发送邮件。分配此权限后，代理可选择将组添加到“发件人”行以指示该邮件由组发送。

  - “代表以下用户发送”   此权限也允许代理代表组发送邮件。在分配该选项后，代理可选择在“发件人”行中添加组。邮件将显示为由组发送，并将说明该邮件由代理代表组发送。

若要向代理分配权限，请单击相应权限下面的“添加”显示“选择收件人”页面，该页面将显示 Exchange 组织内可分配该权限的所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”，搜索特定的收件人。

## 使用命令行管理程序更改通讯组属性

使用 **Get-DistributionGroup** 和 **Set-DistributionGroup** cmdlet 查看和更改通讯组属性。使用命令行管理程序的优点是能够更改在 EAC 中不可用的属性以及更改多个组的属性。有关什么参数对应通讯组属性的信息，请参阅下列主题：

  - [Get-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124755\(v=exchg.150\))

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\))

这里是一些使用命令行管理程序更改通讯组属性的示例。

该示例将西雅图员工通讯组的主要 SMTP 地址（也称为回复地址）从 employees@contoso.com 更改为 sea.employees@contoso.com。此外，之前的回复地址将保留为代理地址。

    Set-DistributionGroup "Seattle Employees" -EmailAddresses SMTP:sea.employees@contoso.com,smtp:employees@contoso.com

该示例将可以发送给组织内所有通讯组的最大邮件大小限制为 10 MB。

    Get-DistributionGroup -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'MailUniversalDistributionGroup')} | Set-DistributionGroup -MaxReceiveSize 10MB

以下示例启用对通讯组 Customer Support 的裁决，并将审查方设置为 Amy。此外，如果从组织内部发送邮件的发件人的邮件未获批准，这一经过裁决的通讯组还会通知发件人。

    Set-DistributionGroup -Identity "Customer Support" -ModeratedBy "Amy" -ModerationEnabled $true -SendModerationNotifications 'Internal'

以下示例将用户创建的通讯组 Dog Lovers 更改为需要组管理者批准用户加入组的请求。此外，通过 *BypassSecurityGroupManagerCheck* 参数，将不会通知组管理者已对该通讯组设置进行了更改。

    Set-DistributionGroup -Identity "Dog Lovers" -MemberJoinRestriction 'ApprovalRequired' -BypassSecurityGroupManagerCheck

## 您如何知道这有效？

要检查是否成功更改了通讯组的属性，可进行以下操作之一：

  - 在 EAC 中选择组，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看已更改的属性或功能。根据所更改的属性，它可能显示在选定组的“详细信息”窗格中。

  - 在命令行管理程序中，使用 **Get-DistributionGroup** cmdlet 验证更改。使用命令行管理程序的一个优点是可查看多个组的多个属性。在上面收件人限制有所更改的示例中，运行以下命令来验证新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    对于上面更改邮件限制的示例，请运行此命令。
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

