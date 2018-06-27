---
title: '从移动邮箱策略添加或删除用户: Exchange 2013 Help'
TOCTitle: 从移动邮箱策略添加或删除用户
ms:assetid: 4ca8e395-c074-4165-b788-16fae3e2ccab
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997929(v=EXCHG.150)
ms:contentKeyID: 50490501
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 从移动邮箱策略添加或删除用户

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-07-16_

通过移动设备邮箱策略可以将一组通用的安全和移动设备设置应用于一组用户。可以创建多个移动设备邮箱策略。

<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安装 Microsoft Exchange Server 2013 时，将创建默认的移动设备邮箱策略，并且该策略会自动分配给所有用户。</td>
</tr>
</tbody>
</table>


有关与移动设备邮箱策略相关的更多管理任务，请参阅[移动设备邮箱策略](mobile-device-mailbox-policies-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备邮箱策略”条目。

  - 在 EAC 的“移动”\>“移动设备邮箱策略”中必须有一个可用的移动设备邮箱策略。

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

## 更改用户的移动设备邮箱策略

您可以使用 EAC 或命令行管理程序来更改用户的移动设备邮箱策略。

## 使用 EAC 更改用户的移动设备邮箱策略

使用 EAC 更改单个用户的移动设备邮箱策略。

1.  在 EAC 中，单击“收件人”\>“邮箱”，然后选择一个邮箱。

2.  在“详细信息”窗格中，滚动到“电话和语音功能”，然后选择“查看详请”，将显示“移动设备详情”屏幕。

3.  显示当前分配的移动设备邮箱策略。要更改移动设备邮箱策略，请单击“浏览”。

4.  从列表中选择合适的移动设备邮箱策略，单击“确定”，然后单击“保存”。

## 使用命令行管理程序将用户添加到移动设备邮箱策略

您可以在命令行管理程序中使用 **Get-CASMailbox** cmdlet 来更改单个用户的移动设备邮箱策略。

1.  在此命令行管理程序中，运行以下命令。
    
        Get-CASMailbox -Identity tony@contoso.com -ActiveSyncMailboxPolicy "Sales" 

## 您如何知道这有效？

若要验证是否已成功更改了用户的移动设备邮箱策略，请执行以下操作之一：

1.  在 EAC 中，单击“收件人”\>“邮箱”，然后选择一个特定收件人。在“详细信息”窗格中，向下滚动到“电话和语音功能”，然后单击“查看详细信息”。

2.  在此命令行管理程序中，运行以下命令。
    
        Get-CASMailbox -Identity tony@contoso.com 

## 在同一时间为多个用户更改移动设备邮箱策略

如果您想同时为多个用户更改移动设备邮箱策略，您可以使用 EAC 中的批量编辑功能，或者使用命令行管理程序为筛选的一组用户更改移动设备邮箱策略。

## 使用 EAC 中的批量编辑工具为多个用户更改移动设备邮箱策略

您可以使用批量编辑功能一次为多个用户更新移动设备邮箱策略。

1.  在 EAC 中，单击“收件人”\>“邮箱”。

2.  选择多个用户。

3.  在“详细信息”窗格中，向下滚动到“Exchange ActiveSync”，然后单击“更新策略”。

4.  单击“浏览”，选择移动设备邮箱策略。

5.  单击“确定”，然后单击“保存”。

## 使用命令行管理程序为筛选的一组用户更改移动设备邮箱策略

您可以使用命令行管理程序为筛选的一组用户更改移动设备邮箱策略。您可以按各种属性筛选用户。

1.  在此命令行管理程序中，运行以下命令。
    
        Get-Mailbox | where { $_.CustomAttribute1 -match "Manager"
         } | Set-CASMailbox -activesyncmailboxpolicy(Get-ActiveSyncMailboxPolicy "Contoso").Identity
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可以用 <code>CustomAttribute1</code> 替换 <strong>Get-Mailbox</strong> 对象的任何属性。若要查看完整列表，请键入：<code>Get-Mailbox username |fl</code>.</td>
    </tr>
    </tbody>
    </table>


## 您如何知道这有效？

若要验证是否已成功更改了用户的移动设备邮箱策略，请执行以下操作之一：

1.  在 EAC 中，单击“收件人”\>“邮箱”，然后选择一个特定收件人。在“详细信息”窗格中，向下滚动到“电话和语音功能”，然后单击“查看详细信息”。

2.  在此命令行管理程序中，运行以下命令。
    
        Get-CASMailbox -Identity tony@contoso.com

