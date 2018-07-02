---
title: '配置邮箱的邮件传递限制: Exchange 2013 Help'
TOCTitle: 配置邮箱的邮件传递限制
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50556655
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置邮箱的邮件传递限制

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2012-11-29_

可以使用 EAC 或命令行管理程序对是否将邮件传递给单个收件人进行限制。 邮件传递限制可用于控制谁可以向组织中的用户发送邮件。 例如，可以将邮箱配置为接受或拒绝特定用户发送的邮件，或者配置为仅接受来自 Exchange 组织中的用户的邮件。

本主题中介绍的邮件传递限制适用于所有类型收件人。 有关不同收件人类型的详细信息，请参阅[收件人](recipients-exchange-2013-help.md)。

有关与收件人相关的其他管理任务，请参阅下列主题：

  - [管理用户邮箱](manage-user-mailboxes-exchange-2013-help.md)

  - [创建和管理通讯组](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [管理动态通讯组](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [管理邮件用户](manage-mail-users-exchange-2013-help.md)

  - [管理邮件联系人](manage-mail-contacts-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

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

## 使用 EAC 配置邮件传递限制

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要为其配置邮件传递限制的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击“邮箱功能”。

4.  在“邮件传递限制”下，单击“查看详情”以查看并更改以下传递限制：
    
      - **接受来自下列发件人的邮件**   使用该部分指定谁可将邮件发送至该用户。
        
          - **所有发件人**   此选项指定用户能够接受来自所有发件人的邮件。这包括 Exchange 组织中的发件人和外部发件人。这是默认选项。 仅当清除了“要求所有发件人均通过身份验证”复选框时，此选项才包括外部用户。如果选中此复选框，则会拒绝来自外部用户的邮件。
        
          - **仅限以下列表中的发件人**   此选项指定该用户只能接受来自 Exchange 组织中指定的一组发件人的邮件。 单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可显示 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。
        
          - **要求所有发件人均通过身份验证**   此选项可阻止匿名用户向此用户发送邮件。其中包括 Exchange 组织外部的用户。
    
      - “拒绝来自下列发件人的邮件”   使用该部分来阻止某些人将邮件发送至该用户。
        
          - **无发件人**   此选项指定邮箱不会拒绝来自 Exchange 组织中任何发件人的邮件。这是默认选项。
        
          - **以下列表中的发件人**   此选项指定该邮箱将拒绝来自 Exchange 组织中特定的一组发件人的邮件。 单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可显示 Exchange 组织中所有收件人的列表。选择所需的收件人，将其添加至列表，然后单击“确定”。也可以通过在搜索框中键入该收件人的姓名，然后单击“搜索”![搜索图标](images/Dn750895.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "搜索图标")，搜索特定的收件人。

5.  单击“确定”关闭“邮件传递限制”页面，然后单击“保存”保存所做的更改。

## 使用命令行管理程序配置邮件传递限制

以下示例展示了如何使用命令行管理程序为邮箱配置邮件传递限制。 对于其他收件人类型，可使用相应的带有相同参数的 **Set-** cmdlet。

此示例将 Robin Wood 的邮箱配置为仅接受来自用户 Lori Penor、Jeff Phillips 以及通讯组 Legal Team 1 的成员的邮件。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要将邮箱配置为仅接受来自个别发件人的邮件，则必须使用 <em>AcceptMessagesOnlyFrom</em> 参数。 如果要将邮箱配置为仅接受来自作为特定通讯组成员的发件人的邮件，则必须使用 <em>AcceptMessagesOnlyFromDLMembers</em> 参数。</td>
</tr>
</tbody>
</table>


此示例将用户 David Pelton 添加到 Robin Wood 的邮箱接受其邮件的用户列表中。

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

此示例将 Robin Wood 的邮箱配置为需要对所有发件人进行身份验证。 这意味着该邮箱将仅接受来自 Exchange 组织中的其他用户的邮件。

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

此示例将 Robin Wood 的邮箱配置为仅拒绝来自用户 Joe Healy、Terry Adams 以及通讯组 Legal Team 2 的成员的邮件。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

此示例将 Robin Wood 的邮箱配置为也拒绝通讯组 Legal Team 3 的成员发送的邮件。

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果要将邮箱配置为拒绝来自个别发件人的邮件，则必须使用 <em>RejectMessagesFrom</em> 参数。 如果要将邮箱配置为拒绝来自作为特定通讯组成员的发件人的邮件，则必须使用 <em>RejectMessagesFromDLMembers</em> 参数。</td>
</tr>
</tbody>
</table>


有关与配置不同类型的收件人的传递限制相关的详细语法和参数信息，请参阅下列主题：

  - [Set-DistributionGroup](https://technet.microsoft.com/zh-cn/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/zh-cn/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/zh-cn/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/zh-cn/library/aa995971\(v=exchg.150\))

## 您如何知道这有效？

若要验证是否为用户邮箱成功配置了邮件传递限制，请执行下列操作之一：

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要为其验证邮件传递限制的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击“邮箱功能”。

4.  在“邮件传递限制”下，单击“查看详情”以验证邮箱的传递限制。

或

在命令行管理程序中运行以下命令。

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

