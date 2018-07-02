---
title: '创建共享邮箱: Exchange 2013 Help'
TOCTitle: 创建共享邮箱
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50491729
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建共享邮箱

 

_**适用于：**Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**上一次修改主题：**2016-12-09_

**估计完成时间：5 分钟**

共享邮箱可让贵组织中的人员组方便地通过共用帐户（例如 info@contoso.com 或 support@contoso.com）监视和发送电子邮件。如果组中有人回复发送至共享邮箱的邮件，则该电子邮件看起来是由共享邮箱发送而不是从单个用户发送的。

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果你使用的是 Office 365 企业版，则应在 Office 365 管理中心创建共享邮箱。
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=834766">在 Office 365 管理中心创建共享邮箱</a></p></li>
</ul></td>
</tr>
</tbody>
</table>


如果组织使用的是混合 Exchange 环境，则应使用本地 Exchange 管理中心 (EAC) 创建和管理共享邮箱。若要了解有关共享邮箱的详细信息，请参阅 [共享邮箱](shared-mailboxes-exchange-2013-help.md)。

## 使用 EAC 创建共享邮箱

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“用户邮箱”条目。

1.  转到“收件人”\>“共享”\>“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  填写必填字段：
    
      - **显示名称**
    
      - **电子邮件地址**

3.  若要授予“完全访问”或“代理发送”权限，可单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，然后选择要对其授予权限的用户。您可以使用 **CTRL** 键来选择多个用户。不清楚要使用什么权限？请参阅本主题后面部分中的您应使用哪些权限？。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>“完全访问”权限允许用户打开邮箱，以及创建和修改其中的项目。“代理发送”权限允许除邮箱所有者以外的任何人从该共享邮箱发送电子邮件。这两个权限是成功操作共享邮箱所必需的。</td>
    </tr>
    </tbody>
    </table>


4.  单击“保存”保存您的更改，并创建共享邮箱。

## 使用 EAC 编辑共享邮箱委派

1.  转到“收件人”\>“共享”\>“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  单击“邮箱委派”

3.  若要授予或移除“完全访问”和“代理发送”权限”，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 或“移除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")，然后选择您想要授予权限的用户。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>“完全访问”权限允许用户打开邮箱，以及创建和修改其中的项目。“代理发送”权限允许除邮箱所有者以外的任何人从该共享邮箱发送电子邮件。这两个权限是成功操作共享邮箱所必需的。</td>
    </tr>
    </tbody>
    </table>


4.  单击“保存”保存更改。

## 使用共享邮箱

为了解用户如何访问和使用共享邮箱，请查看以下内容：

  - [在 Outlook 2016 和 Outlook 2013 中打开和使用共享邮箱](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [在面向企业的 Outlook 网页版中打开和使用共享邮箱](https://go.microsoft.com/fwlink/p/?linkid=834766)

## 使用命令行管理程序创建共享邮箱

该示例可创建共享的邮箱销售部门，并对安全组 MarketingSG 授予“完全访问权限”和“代表发送”权限。将对属于安全组成员的用户授予邮箱的权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>该示例假定您已经创建了安全组 MarketingSG，并且该安全组已启用邮件。请参阅<a href="manage-mail-enabled-security-groups-exchange-2013-help.md">管理启用邮件的安全组</a>。</td>
</tr>
</tbody>
</table>


    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

有关语法和参数的详细信息，请参阅 [New-Mailbox](https://technet.microsoft.com/zh-cn/library/aa997663\(v=exchg.150\))。

## 您应使用哪些权限？

您可以使用共享邮箱的以下权限。

  - **完全访问权限** 完全访问权限允许用户登录共享邮箱并作为该邮箱的所有者。访问共享邮箱后，用户可以创建日历项目；读取、查看、删除和更改电子邮件消息；创建任务和日历联系人。然而，具有完全访问权限的用户无法从共享邮箱发送电子邮件，除非他们同时拥有“发送为”或“代表发送”权限。

  - **发送为**   “发送为”权限允许用户在发送邮件时模仿共享邮箱。例如，如果 Kweku 登录共享邮箱“Marketing Department”并发送电子邮件，这将显示为是“Marketing Department”发送的邮件。

  - **代表发送**   “代表发送”权限允许用户代表共享邮箱发送电子邮件。例如，如果 John 登录共享邮箱“Reception Building 32”并发送电子邮件，邮件将显示为由“John 代表 Reception Building 32”发送。您不能使用 EAC 来授予“代表发送”权限，您必须结合使用 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 和 *GrantSendonBehalf* 参数。

## 详细信息

若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>

