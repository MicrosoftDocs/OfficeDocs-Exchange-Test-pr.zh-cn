---
title: '添加或删除邮箱的电子邮件地址: Exchange 2013 Help'
TOCTitle: 添加或删除邮箱的电子邮件地址
ms:assetid: 93e2d9a4-7558-4509-8641-8381a7eb674f
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123794(v=EXCHG.150)
ms:contentKeyID: 50556640
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 添加或删除邮箱的电子邮件地址

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

您可以为同一个邮箱配置多个电子邮件地址。这些附加地址称为“*代理地址*”。用户可以使用代理地址接收发送给其他电子邮件地址的电子邮件。任何发送到用户的代理地址的电子邮件都会传递给其主电子邮件地址，该地址也称为“*主 SMTP 地址*”或者“*默认答复地址*”。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果你使用的是 Office 365 企业版，则应按照以下文章中的说明添加或删除用户邮箱的电子邮件地址：<a href="https://go.microsoft.com/fwlink/p/?linkid=8347775">Office 365 管理中心：在 Office 365 中向用户添加更多电子邮件别名</a></td>
</tr>
</tbody>
</table>


有关与收件人管理相关的其他管理任务，请参阅[收件人](recipients-exchange-2013-help.md)中的“收件人文档”表。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

本主题中的过程将展示如何添加或删除用户邮箱的电子邮件地址。可以使用类似的过程添加或删除其他收件人类型的电子邮件地址。

## 您想执行什么操作？

## 向用户邮箱添加电子邮件地址

## 使用 EAC 添加电子邮件地址

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要向其添加电子邮件地址的邮箱，然后单击“**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")”。

3.  在邮箱属性页上，单击“**电子邮件地址**”。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在“<strong>电子邮件地址</strong>”页上，主 SMTP 地址以黑体字显示在地址列表中，“<strong>类型</strong>”列中是大写的 <strong>SMTP</strong> 值。</td>
    </tr>
    </tbody>
    </table>


4.  单击“**添加**![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")”，然后单击 **SMTP** 将 SMTP 电子邮件地址添加到此邮箱。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>SMTP 是默认的电子邮件地址类型。也可以向邮箱添加 Exchange 统一消息 (EUM) 地址或自定义地址。有关详细信息，请参阅<a href="manage-user-mailboxes-exchange-2013-help.md">管理用户邮箱</a>主题中的“更改用户邮箱属性”。</td>
    </tr>
    </tbody>
    </table>


5.  在“**电子邮件地址**”框中键入新的 SMTP 地址，然后单击“**确定**”。
    
    该新地址显示在选定邮箱的电子邮件地址列表中。

6.  单击“**保存**”以保存所做的更改。

## 使用命令行管理程序添加电子邮件地址

与邮箱关联的电子邮件地址包含在邮箱的 *EmailAddresses* 属性中。因为 *EmailAddresses* 属性可以包含多个电子邮件地址，因此称为*多值*属性。下列示例展示了修改多值属性的各种不同方式。

此示例展示了如何向 Dan Jump 的邮箱添加 SMTP 地址。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com"}

此示例展示了如何向邮箱添加多个 SMTP 地址。

    Set-Mailbox "Dan Jump" -EmailAddresses @{add="dan.jump@northamerica.contoso.com","danj@tailspintoys.com"}

有关如何使用此方法添加和删除多值属性值的详细信息，请参阅[修改多值属性](modifying-multivalued-properties-exchange-2013-help.md)。

此示例展示了向邮箱添加电子邮件地址的另一种方法：指定与邮箱关联的所有地址。在此示例中，danj@tailspintoys.com 是要添加的新电子邮件地址。另两个电子邮件地址是现有的地址。包含区分大小写的限定符 `SMTP` 的地址是主 SMTP 地址。在使用此命令语法时，必须包含邮箱的所有电子邮件地址。否则，在命令中指定的地址将覆盖现有的地址。

    Set-Mailbox "Dan Jump" -EmailAddresses SMTP:dan.jump@contoso.com,dan.jump@northamerica.contoso.com,danj@tailspintoys.com

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道操作成功？

若要验证是否成功地向邮箱添加了电子邮件地址，请执行下列操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，单击相应的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

  - 在邮箱属性页上，单击“**电子邮件地址**”。

  - 在邮箱的电子邮件地址列表中，验证是否包含新电子邮件地址。

或

  - 在命令行管理程序中运行以下命令。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 验证结果中是否包含新电子邮件地址。

## 从用户邮箱中删除电子邮件地址

## 使用 EAC 删除电子邮件地址

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要向从中删除电子邮件地址的邮箱，然后单击“**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")”。

3.  在邮箱属性页上，单击“**电子邮件地址**”。

4.  在电子邮件地址列表中，选择要删除的地址，然后单击“**删除**![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")”。

5.  单击“**保存**”以保存所做的更改。

## 使用命令行管理程序删除电子邮件地址

此示例展示了如何从 Janet Schorr 的邮箱中删除电子邮件地址。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janets@corp.contoso.com"}

此示例展示了如何从邮箱中删除多个地址。

    Set-Mailbox "Janet Schorr" -EmailAddresses @{remove="janet.schorr@corp.contoso.com","janets@tailspintoys.com"}

有关如何使用此方法添加和删除多值属性值的详细信息，请参阅[修改多值属性](modifying-multivalued-properties-exchange-2013-help.md)。

通过在设置邮箱的电子邮件地址的命令中省略某个电子邮件地址，也可以将其删除。例如，假设 Janet Schorr 的邮箱有三个电子邮件地址：janets@contoso.com（主 SMTP 地址）、janets@corp.contoso.com 和 janets@tailspintoys.com。若要删除地址 janets@corp.contoso.com，要运行以下命令。

    Set-Mailbox "Janet Schorr" -EmailAddresses SMTP:janets@contoso.com,janets@tailspintoys.com

因为在上一个命令中省略了 janets@corp.contoso.com，因此将其从邮箱中删除了。

有关语法和参数的详细信息，请参阅 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))。

## 您如何知道操作成功？

若要验证是否成功地从邮箱中删除了电子邮件地址，请执行下列操作之一：

  - 在 EAC 中，导航到“收件人”\>“邮箱”，单击相应的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

  - 在邮箱属性页上，单击“**电子邮件地址**”。

  - 在邮箱的电子邮件地址列表中，验证是否包含相应的电子邮件地址。

或

  - 在命令行管理程序中运行以下命令。
    
        Get-Mailbox <identity> | fl EmailAddresses

  - 验证结果中是否包含相应的电子邮件地址。

## 使用命令行管理程序向多个邮箱添加电子邮件地址

使用命令行管理程序以及逗号分隔值 (CSV) 文件，可以一次性向多个邮箱添加新电子邮件地址。

此示例从 C:\\Users\\Administrator\\Desktop\\AddEmailAddress.csv 导入数据，该文件具有以下格式。

    Mailbox,NewEmailAddress
    Dan Jump,danj@northamerica.contoso.com
    David Pelton,davidp@northamerica.contoso.com
    Kim Akers,kima@northamerica.contoso.com
    Janet Schorr,janets@northamerica.contoso.com
    Jeffrey Zeng,jeffreyz@northamerica.contoso.com
    Spencer Low,spencerl@northamerica.contoso.com
    Toni Poe,tonip@northamerica.contoso.com
    ...

运行以下命令可使用 CSV 文件中的数据将电子邮件地址添加到 CSV 文件中指定的每个邮箱。

    Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Set-Mailbox $_.Mailbox -EmailAddresses @{add=$_.NewEmailAddress}}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>该 CSV 文件第一行中的列名 (<code>Mailbox,NewEmailAddress</code>) 可以是任意值。无论你使用的列名如何，请确保在 Shell 命令中使用相同的列名。</td>
</tr>
</tbody>
</table>


## 您如何知道操作成功？

若要验证是否成功地向多个邮箱添加了电子邮件地址，请执行下列操作之一：

  - 在 EAC 中，导航到“**收件人**”\>“**邮箱**”，单击向其添加了地址的邮箱，然后单击“**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")”。

  - 在邮箱属性页上，单击“**电子邮件地址**”。

  - 在邮箱的电子邮件地址列表中，验证是否包含新电子邮件地址。

或

  - 在命令行管理程序中运行以下命令，并使用用于添加新电子邮件地址的同一个 CSV 文件。
    
        Import-CSV "C:\Users\Administrator\Desktop\AddEmailAddress.csv" | ForEach {Get-Mailbox $_.Mailbox | fl Name,EmailAddresses}

  - 验证每个邮箱的结果中是否包含新电子邮件地址。

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

