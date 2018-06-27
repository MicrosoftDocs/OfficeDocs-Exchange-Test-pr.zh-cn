---
title: '管理用户邮箱: Exchange 2013 Help'
TOCTitle: 管理用户邮箱
ms:assetid: 957ca61c-1fa1-42ab-a0e6-8488e4782566
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123809(v=EXCHG.150)
ms:contentKeyID: 50491197
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.NewMailboxWizardForm.NewMailboxIntroductionWizardPage
ms.translationtype: HT
---

# 管理用户邮箱

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2014-05-27_

创建用户邮箱后，您可以使用 EAC 或命令行管理程序进行更改和设置其他属性。

您也可同时为多个用户邮箱更改属性。有关详细信息，请参阅批量编辑用户邮箱。

## 在开始之前，您需要知道什么？

  - 完成每个用户邮箱任务的估计时间：2 至 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

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

## 更改用户邮箱属性

## 使用 EAC 更改用户邮箱属性

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要更改其属性的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“邮箱属性”页面上，单击以下部分之一以查看或更改属性。
    
      - 常规
    
      - 邮箱用量
    
      - 联系人信息
    
      - 组织
    
      - 电子邮件地址
    
      - 邮箱功能
    
      - 成员属于
    
      - 邮件提示
    
      - 邮箱委派

## 常规

使用“常规”部分可以查看或更改有关用户的基本信息。

  - “名字”、“姓名缩写”、“姓氏”

  - “\* 姓名”   这是会在 Active Directory 中列出的姓名。如果您要更改此姓名，则它不能超过 64 个字符。

  - “\* 显示名称”此名称将会出现在组织通讯簿中的“收件人:”和“发件人：”行上以及“邮箱”列表中。此姓名不能在显示姓名之前或之后包含空格。

  - “＊ 别名” 此名称指定用户的电子邮件别名。用户的别名是电子邮件地址中 (@) 符号左侧的部分。它在林中必须是唯一的。

  - “\* 用户登录名”   这是用户用于登录邮箱和登录到域的名称。通常，用户登录名由 @ 符号左侧的用户别名以及用户帐户所在的 @ 符号右侧的域名组成。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange Online 中，此框被标记为“用户 ID”。</td>
    </tr>
    </tbody>
    </table>


  - “下次登录时需要更改密码”   如果希望用户在下次登录邮箱时重置其密码，请选中此复选框。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此复选框在 Exchange Online 中不可用。</td>
    </tr>
    </tbody>
    </table>


  - “从地址列表中隐藏”   选中此复选框可以防止收件人显示在通讯簿以及在 Exchange 组织中定义的其他地址列表中。选中此复选框后，用户仍可使用电子邮件地址向收件人发送邮件。

单击“更多选项”查看或更改以下这些额外的属性：

  - “组织单位”   此只读框显示包含用户帐户的组织单位 (OU)。必须使用 Active Directory 用户和计算机才能将此用户帐户移动到不同的 OU。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此框在 Exchange Online 中不可用。</td>
    </tr>
    </tbody>
    </table>


  - “邮箱数据库”   此只读框显示托管此邮箱的邮箱数据库的名称。若要将邮箱移动到一个不同的数据库，请在邮箱列表中选择它，然后在“详细信息”窗格中单击“将邮箱移动到其他数据库”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此选项在 Exchange Online 中不可用。</td>
    </tr>
    </tbody>
    </table>


  - “自定义属性”   此部分显示为用户邮箱定义的自定义属性。要指定自定义属性值，请单击“编辑”。最多可为收件人指定 15 个自定义属性。

## 邮箱用量

单击“邮箱使用情况”部分以查看或更改邮箱存储配额和邮箱的已删除邮件保留设置。创建邮箱时，将默认配置这些设置。它们使用为邮箱数据库配置且适用于该数据库中所有邮箱的值。您可以为每个邮箱自定义这些设置，而不是使用邮箱数据库默认设置。

  - “最近登录”   此只读框显示用户上次登录邮箱的时间。

  - “邮箱使用情况”   此区域显示邮箱的总体大小和已使用总体邮箱配额的百分比。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>为了获取前两个框中显示的信息，EAC 将查询托管邮箱的邮箱数据库。如果 EAC 无法与包含邮箱数据库的 Exchange 存储通信，这些框将为空。如果用户还没有首次登录邮箱，则会显示警告消息。</td>
</tr>
</tbody>
</table>


单击“更多选项”以查看或更改邮箱存储配额和邮箱的已删除邮件保留设置。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>这些设置在 Exchange Online 中的 EAC 中不可用。</td>
</tr>
</tbody>
</table>


  - “存储配额设置”   若要自定义邮箱的这些设置而不使用邮箱数据库默认设置，请单击“为此邮箱自定义设置”，键入一个新值，然后单击“保存”。
    
    任何存储配额设置的值范围介于 0 到 2047 千兆字节 (GB) 之间。
    
      - “在达到该限度时发出警告(GB)”   此框显示在向用户发出警告之前的最大存储限制。如果邮箱大小达到或超过指定值，Exchange 将向邮箱用户发送警告消息。
    
      - “在达到该限度时禁止发送(GB)”   此框显示邮箱的“禁止发送”限制。如果邮箱大小达到或超过指定的限制，Exchange 将阻止邮箱用户发送新邮件，并显示一条描述性错误消息。
    
      - “在达到该限度时禁止发送和接收(GB)”   此框显示此邮箱的“禁止发送和接收”限制。如果邮箱大小达到或超过指定的限制，Exchange 将阻止邮箱用户发送新邮件，并且不会将任何新邮件发送到邮箱中。发送到邮箱的任何邮件将返回给收件人，并附带一条描述性错误消息。

  - “已删除项目保留设置”   若要自定义邮箱的这些设置而不使用邮箱数据库默认设置，请单击“为此邮箱自定义设置”，键入一个新值，然后单击“保存”。
    
      - “保留已删除项目的期限(天)”   此框显示在用户永久删除并且无法恢复项目之前，已删除项目的保留时间长度。在创建邮箱后，该值基于为邮箱数据库配置的已删除项目保留设置。默认情况下，邮箱数据库配置为将已删除项目保留 14 天。此属性的值范围介于 0 到 24855 天之间。
    
      - “完成对数据库的备份之后才永久删除项目”   选中此复选框可避免在备份此邮箱所在的邮箱数据库之前永久删除邮箱和电子邮件。

## 联系人信息

使用“联系信息”部分来查看或更改用户联系信息。该页上的信息显示在通讯簿中。单击“更多选项”以显示额外框。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>可以使用“州/省”框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。</td>
</tr>
</tbody>
</table>


邮箱用户可以使用 Outlook 或 Outlook Web App 查看和更改其自己的联系人信息。但他们无法在“便笺”和“网页”框中更改此信息。

## 组织

使用此“组织”部分可以记录有关组织中用户的角色的详细信息。此信息会显示在通讯簿中。您也可以创建可从电子邮件客户端（如 Outlook）访问的虚拟组织图。

  - “职务”   使用此框可以查看或更改收件人的职务。

  - “部门”   使用此框可以查看或更改用户所在的部门。可以使用此框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。

  - “公司”   使用此框可以查看或更改用户所在的公司。可以使用此框为动态通讯组、电子邮件地址策略或地址列表创建收件人条件。

  - “经理”   若要添加经理，请单击“浏览”。在“选择经理”中，选择相应的人员，然后单击“确定”。

  - “直接下属”   您无法修改此框。“直接下属”是指向特定经理报告的用户。如果已为用户指定一个经理，则该用户将作为直接下属出现在该经理的邮箱的详细信息中。例如，Kari 是 Chris 和 Kate 的部门经理，因此 Chris 和 Kate 的邮箱的“经理”框中会指定 Kari 的邮箱，同时 Chris 和 Kate 显示在 Kari 邮箱属性的“直接下属”框中。

## 电子邮件地址

使用“电子邮件地址”部分可以查看或更改与该用户邮箱关联的电子邮件地址。这包括用户的主 SMTP 地址和任何关联代理地址。主 SMTP 地址（也称为“默认答复地址”）在地址列表中以粗体显示，大写的“SMTP” 值显示在“类型”列中。

  - “添加”   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")可为该邮箱添加新的电子邮件地址。选择以下地址类型之一：
    
      - “SMTP”   这是默认的地址类型。单击此按钮，然后在“\* 电子邮件地址”框中键入新的 SMTP 地址。
    
      - “EUM”   EUM（Exchange 统一消息）地址由 Microsoft Exchange 统一消息服务用于在 Exchange 组织中查找已启用 UM 的用户。EUM 地址包含已启用 UM 的用户的分机号和 UM 拨号计划。单击该按钮，并在“地址/扩展名”框中键入分机号。然后单击“浏览”，选择用户的拨号计划。
    
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
    
      - **将其作为回复地址**   在 Exchange Online 中，您可以选中此复选框将此新电子邮件地址设置为邮箱的主 SMTP 地址。此复选框在 Exchange 2013 中的 EAC 中不可用。

  - “基于应用到此收件人的电子邮件地址策略自动更新电子邮件地址”   选中此复选框可基于对组织中电子邮件地址策略所做的更改自动更新收件人的电子邮件地址。此框在默认情况下处于选中状态。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>此复选框在 Exchange Online 中不可用。</td>
    </tr>
    </tbody>
    </table>


  - **将其作为回复地址**

## 邮箱功能

使用“邮箱功能”部分可查看或更改下列邮箱功能和设置：

  - “共享策略”   此框显示应用于邮箱的共享策略。共享策略可以控制组织中的用户与 Exchange 组织外的用户共享日历和联系人信息的方式。在创建邮箱时就为这些邮箱分配了“默认共享策略”。要更改已分配给此用户的共享策略，请从下拉列表中选择一个不同的共享策略。

  - “角色分配策略”   此框显示已分配给邮箱的角色分配策略。角色分配策略指定分配给用户的基于角色的访问控制 (RBAC) 角色，该角色可以控制用户可以修改的特定邮箱和通讯组配置设置。要更改已分配给此用户的角色分配策略，请从下拉列表中选择一个不同的角色分配策略。

  - “保留策略”   该框显示为邮箱分配的保留策略。保留策略是一组应用至用户邮箱的保留标记。它们使您可以控制用户邮箱中各项的保留期限，并定义如何操作已达到一定期限的项目。在创建保留策略时，不会将其分配给邮箱。要将保留策略分配至用户，可从下拉列表中选择一个策略。

  - “通讯簿策略”   此框显示应用于邮箱的通讯簿策略。通过通讯簿策略可以将用户分为特定组以提供通讯簿的自定义视图。若要应用或更改应用于邮箱的通讯簿策略，请从下拉列表中选择一项。

  - “统一消息” 默认情况下禁用此功能。启用统一消息 (UM) 时，用户将能够使用组织的 UM 功能并使用一组默认的 UM 属性。单击“启用”为邮箱启用 UM。有关如何启用 UM 的信息，请参阅[为用户启用语音邮件](enable-a-user-for-voice-mail-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>必须有 UM 拨号计划以及 UM 邮箱策略方可启用 UM。</td>
    </tr>
    </tbody>
    </table>


  - “移动设备”   使用此部分可查看和更改 Exchange ActiveSync（默认情况下会启用）的设置。Exchange ActiveSync 支持从移动设备访问 Exchange 邮箱。单击“禁用 Exchange ActiveSync”可为邮箱禁用此功能。

  - “Outlook Web App” 默认情况下，已启用此功能。Outlook Web App 支持从 Web 浏览器访问 Exchange 邮箱。单击“禁用”来禁用邮箱的 Outlook Web App。单击“编辑详细信息”来添加或更改邮箱的 Outlook Web App 邮箱策略。

  - “IMAP”   默认情况下启用此功能。单击“禁用”对邮箱禁用 IMAP。

  - “POP3”   默认情况下启用此功能。单击“禁用”对邮箱禁用 POP3。

  - “MAPI” 默认情况下启用此功能。MAPI 支持从 MAPI 客户端（如 Outlook）访问 Exchange 邮箱。单击“禁用”来禁用邮箱的 MAPI。

  - “诉讼保留”   默认情况下禁用此功能。诉讼保留可以保留已删除的邮箱项目并记录对邮箱项目所作的更改。在发现搜索中可返回已删除的项目和已更改项目的所有实例。单击“启用”将邮箱置于诉讼保留。如果邮箱处于诉讼保留状态，可单击“禁用”删除诉讼保留。处于诉讼保留状态的邮箱为非活动邮箱，且不能删除。要删除邮箱，请删除诉讼保留。如果邮箱处于诉讼保留状态，可单击“编辑详细信息”来查看并更改以下诉讼保留设置：
    
      - “保留日期”   此只读邮箱指明邮箱置于诉讼保留状态的日期和时间。
    
      - “保留者”   该只读框指明将邮箱置于诉讼保留状态的用户是谁。
    
      - “注意”   使用此框可以通知用户有关诉讼保留的信息、解释将邮箱置于诉讼保留的原因，或者向用户提供其他指南，如通知用户诉讼保留不会影响他们对邮箱的日常使用。
    
      - “URL”   使用此框可以提供指向某网站的 URL，该网站提供有关邮箱上的诉讼保留的信息或指南。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>只有在使用 Outlook 2010 或更高版本时，这些框中的文本才会显示在用户的邮箱中，但不会显示在 Outlook Web App 或其他电子邮件客户端中。若要在 Outlook 中查看“说明”和 URL 框中的文本，请单击“文件”选项卡，在“信息”页上的“帐户设置”下，您将会看到诉讼保留注释。</td>
        </tr>
        </tbody>
        </table>


  - “存档”   如果用户没有存档邮箱，则禁用此功能。要启用存档邮箱，请单击“启用”。如果用户具有存档邮箱，则会显示存档邮箱的大小和使用情况统计信息。单击“编辑详细信息”来查看和更改以下存档邮箱设置：
    
      - “状态”   此只读框指示是否存在存档邮箱。
    
      - “数据库”   此只读框显示托管存档邮箱的邮箱数据库的名称。此框在 Exchange Online 中不可用。
    
      - “名称”   在此框中键入存档邮箱的名称。该名称显示在 Outlook 或 Outlook Web App 中的文件夹列表下。
    
      - **存档配额 (GB)**   该框显示存档邮箱的总大小。要更改该大小，可在框中键入新的值或从下拉列表中选择一个值。
    
      - “达到该限度时发出警告 (GB)”   该框显示在向用户发出警告之前存档邮箱的最大存储限制。如果存档邮箱大小达到或超过指定值，Exchange 将向用户发送警告消息。要更改该限制，可在框中键入新的值或从下拉列表中选择一个值。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>在 Exchange Online 中不能更改存档邮箱的存档配额和警告发出配额。</td>
        </tr>
        </tbody>
        </table>


  - “传递选项”   用于将发送给用户的电子邮件转发给另一个收件人并设置该用户可以向其发送邮件的收件人最大数目。单击“查看详细信息”可查看和更改这些设置。
    
      - “转发地址”   选择“启用转发”复选框，然后单击“浏览”来显示“选择邮箱用户和邮箱”页。使用此页选择收件人，发送到此邮箱的所有电子邮件将转发给该收件人。
    
      - **将邮件同时传递到转发地址和原始收件人的邮箱**   选中此复选框可将邮件同时传递到转发地址和用户邮箱。
    
      - “收件人限制”   该设置控制用户可向其发送信息的收件人最大数目。选择“最大收件人数”复选框以限制电子邮件的“收件人:”、“抄送:”和“密件抄送:”框中允许的最大收件人数，然后指定最大收件人数。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>对于内部部署 Exchange 组织，收件人数目不受限。对于 Exchange 在线组织，限制是 500 个收件人。</td>
        </tr>
        </tbody>
        </table>


  - “邮件大小限制”   这些设置控制用户可以发送和接收的邮件大小。单击“查看详细信息”可查看和更改发送和接收的邮件的最大大小。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange Online 中不能更改这些设置。</td>
    </tr>
    </tbody>
    </table>
    
      - “已发送消息”   要指定该用户发送的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户发送大于该指定大小的邮件，则会将该邮件返回至用户，并向其显示一条描述性的错误消息。
    
      - “已收到消息”   要指定该用户接收的消息的最大大小，可选择“最大消息大小 (KB)”复选框并在框中键入值。邮件大小必须介于 0 到 2,097,151 KB 之间。如果用户收到大于指定大小的邮件，则该邮件将返回至发件人，并向其显示一条描述性的错误消息。

  - “邮件传递限制”   这些设置控制可以向此用户发送电子邮件的人员。单击“查看详细信息”可查看和更改这些限制。
    
      - “接受来自下列发件人的邮件”   使用该部分指定谁可将邮件发送至该用户。
        
          - “所有发件人”   选择此选项可指定用户能够接受来自所有发件人的邮件。这包括 Exchange 组织中的发件人和外部发件人。此选项默认情况下处于选中状态。仅当清除了“要求所有发件人均通过身份验证”复选框时，此选项才包括外部用户。如果选中此复选框，则会拒绝来自外部用户的邮件。
        
          - “仅限以下列表中的发件人”   选择此选项可指定该用户只能接受来自 Exchange 组织中指定的一组发件人的邮件。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示“选取收件人”页面，该页面显示您 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
        
          - “要求所有发件人均通过身份验证”   选中此选项可防止匿名用户向此用户发送邮件。
    
      - “拒绝来自下列发件人的邮件”   使用该部分来阻止某些人将邮件发送至该用户。
        
          - “无发件人”   选择此选项可指定邮箱不会拒绝来自 Exchange 组织中任何发件人的邮件。此选项默认情况下处于选中状态。
        
          - “以下列表中的发件人”   选择此选项可指定该邮箱将拒绝来自 Exchange 组织中指定的一组发件人的邮件。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示“选择收件人”页面，该页面显示您 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。

## 成员属于

使用“隶属于”部分可查看该用户所属通讯组或安全组的列表。您不能在此页上更改成员信息。请注意，用户可能符合您组织中的一个或多个动态通讯组的条件。但是，动态通讯组不会显示在此页面上，因为每次使用它们时都会计算其成员资格。

## 邮件提示

使用“邮件提示”部分可添加邮件提示，以便在用户向此收件人发送邮件时告知用户潜在问题。邮件提示是在将此收件人添加到新电子邮件的“收件人”、“抄送”或“密件抄送”框中时，信息栏中显示的文本。

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


## 邮箱委派

使用“邮箱委派”部分将权限分配至其他用户（也称为“代理”）让他们登录用户邮箱或代表用户发送邮件。可以分配以下权限：

  - “发送为”   该权限可让邮箱所有者之外的用户使用邮箱来发送邮件。在将该权限分配给某个代理后，代理通过该邮箱发送的所有邮件都将显示为由邮箱所有者发送。但是该权限不会允许代理登录用户邮箱。

  - “代表发送”   该权限也允许代理使用该邮箱发送邮件。但是，在将此权限分配给代理后，代理发送的任何邮件中的“发件人：”地址将指明邮件由代理代表邮箱所有者发送。

  - “完全访问权限”   该权限允许代理登录用户邮箱并查看邮箱内容。但是，在将此权限分配给代理后，代理不能从邮箱发送邮件。为了让代理从用户邮箱发送电子邮件，您仍必须为代理分配“发送为”或“代表发送”权限。

若要向代理分配权限，请单击相应权限下面的“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")显示页面，该页面将显示 Exchange 组织内可分配该权限的所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。

## 使用命令行管理程序更改用户邮箱属性

使用 **Get-Mailbox** 和 **Set-Mailbox** cmdlet 查看和更改用户邮箱的属性。使用命令行管理程序的一个好处是，能够更改设置多个邮箱的属性。有关什么参数对应邮箱属性的信息，请参阅下列主题：

  - [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

下面是几个使用命令行管理程序更改用户邮箱属性的示例。

下例显示如何将 Pat Coleman 的电子邮件转发给 Sunil Koduri 的邮箱 (sunilk@contoso.com)。

    Set-Mailbox -Identity patc -DeliverToMailboxAndForward $true -ForwardingAddress sunilk@contoso.com

本例使用 **Get-Mailbox** 命令查找组织中的所有用户邮箱，然后使用 **Set-Mailbox** 命令将电子邮件的“收件人：”、“抄送:”和“密件抄送:”框中的收件人限制设置为允许 500 个收件人。

    Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | Set-Mailbox -RecipientLimits 500

本示例将使用 **Get-Mailbox** 命令查找 Marketing 组织单位中的所有邮箱，然后使用 **Set-Mailbox** 命令配置这些邮箱。自定义警告、禁止发送、禁止发送和接收限制分别设置为 200 MB、250 MB 和 280 MB，并且忽略邮箱数据库的默认限制。此命令可用于配置一组特定邮箱，使这些邮箱的限制大于或小于组织中的其他邮箱限制。

    Get-Mailbox -OrganizationalUnit "Marketing" | Set-Mailbox -IssueWarningQuota 209715200 -ProhibitSendQuota 262144000 -ProhibitSendReceiveQuota 293601280 -UseDatabaseQuotaDefaults $false 

本示例将使用 **Get-Mailbox** 命令查找客户服务部门中的所有用户，然后使用 **Set-Mailbox** cmdlet 将发送邮件的最大邮件大小更改为 2 MB。

    Get-Mailbox -Filter "Department -eq 'Customer Service'" | Set-Mailbox -MaxSendSize 2097152

本示例将设置法语和中文的 MailTip 转换。

    Set-Mailbox john@contoso.com -MailTipTranslations ("FR: C'est la langue française", "CHT: 這是漢語語言")

## 您如何知道这有效？

要验证是否已成功更改用户邮箱的属性，请执行以下操作：

  - 在 EAC 中，选择邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看您更改的属性或功能。根据您更改的属性，它可能显示在所选邮箱的“详细信息”窗格中。

  - 在命令行管理程序中，使用 **Get-Mailbox** cmdlet 验证更改。使用命令行管理程序的一个优势是，您可查看多个邮箱的多个属性。在上面收件人限制有所更改的示例中，运行以下命令来验证新值。
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,RecipientLimits
    
    对于上面更改邮件限制的示例，请运行此命令。
    
        Get-Mailbox -OrganizationalUnit "Marketing" | fl Name,IssueWarningQuota,ProhibitSendQuota,ProhibitSendReceiveQuota,UseDatabaseQuotaDefaults

## 批量编辑用户邮箱

可以使用 EAC 更改多个用户邮箱的属性。从 EAC 中的邮箱列表中选择两个或多个用户邮箱时，“详细信息”窗格中会显示可以批量编辑的属性。在您更改其中一个属性后，所做更改将应用到所有选定的邮箱。

下面是可以批量编辑的用户邮箱属性和功能的列表。请注意，不是每个区域的所有属性都可以更改。

  - “联系人信息”   更改共享属性，如街道、邮编和城市名称。

  - “组织”   更改共享属性，如部门名称、公司名称和选定用户的直接经理。

  - “自定义属性”   更改或添加自定义属性 1-15 的值。

  - “邮箱配额”   更改邮箱配额值和已删除项目的保留期。此功能在 Exchange Online 中不可用。

  - “电子邮件连接”   启用或禁用 Outlook Web App、POP3、IMAP、MAPI 和 Exchange ActiveSync。

  - “存档”   启用或禁用存档邮箱。

  - “保留策略、角色分配策略和共享策略”   更新上述各个邮箱功能的设置。

  - “将邮箱移动到另一个数据库”   将选定邮箱移动到其他数据库。

  - **委派权限**   为用户或组分配允许他们从其他邮箱打开或发送邮件的权限。您可以为用户或组分配“完全”、“代理发送”和“代表发送”权限。请查看[管理收件人的权限](manage-permissions-for-recipients-exchange-online-help.md)，获取详细信息。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>完成此任务估计需要 2 分钟时间，但是如果要更改多个属性或功能，时间可能会更长。</td>
</tr>
</tbody>
</table>


## 使用 EAC 批量编辑用户邮箱

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在邮箱列表中，选择两个或多个邮箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>通过按住 Shift 键的同时单击第一个邮箱，然后单击要编辑的最后一个邮箱，可以选择多个相邻的邮箱。按住 Ctrl 键的同时单击要编辑的每个邮箱，也可以选择多个不相邻的邮箱。</td>
    </tr>
    </tbody>
    </table>


3.  在“详细信息”窗格中的“批量编辑”下，选择要编辑的邮箱属性或功能。

4.  更改属性页面，然后保存所做的更改。

## 您如何知道这有效？

要验证是否已成功批量编辑用户邮箱，请执行以下操作之一：

  - 在 EAC 中，选择要批量编辑的各个邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")查看您更改的属性或功能。

  - 在 Exchange 命令行管理程序中，使用 **Get-Mailbox** cmdlet 验证更改。使用命令行管理程序的一个优势是，您可查看多个邮箱的多个属性。例如，假设您在 EAC 使用批量编辑功能来启用存档邮箱和向组织中的所有用户分配保留策略。要验证这些更改，可以运行以下命令：
    
        Get-Mailbox -ResultSize unlimited -Filter {(RecipientTypeDetails -eq 'UserMailbox')} | fl Name,ArchiveDatabase,RetentionPolicy
    
    有关 **Get-Mailbox** cmdlet 的可用参数的详细信息，请参阅 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\))。

