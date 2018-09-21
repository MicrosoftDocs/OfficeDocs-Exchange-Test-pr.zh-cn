---
title: '禁用或删除邮箱: Exchange 2013 Help'
TOCTitle: 禁用或删除邮箱
ms:assetid: 31ad25d6-2942-4fd9-aecb-cdf9654163d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ863434(v=EXCHG.150)
ms:contentKeyID: 50556551
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 禁用或删除邮箱

 

_**适用于：** Exchange Server 2013 SP1_

_**上一次修改主题：** 2015-03-09_

您可以使用 EAC 或命令行管理程序来禁用或删除 Exchange 2013 中的邮箱。禁用或删除邮箱后，Exchange 会将相应邮箱保留在邮箱数据库中，然后将此邮箱切换到禁用状态。禁用和删除的邮箱保留在邮箱数据库中，直到已删除的邮箱保留期过期（默认为 30 天）。此保留期过期后，邮箱将永久删除或“清除”。

如果您需要删除 Exchange Online 中的邮箱，请参阅[在 Exchange Online 中删除或还原用户邮箱](https://technet.microsoft.com/zh-cn/library/dn186233\(v=exchg.150\))。

> [!NOTE]  
> 禁用或删除的邮箱称为“断开连接的邮箱”。


删除邮箱和禁用邮箱之间的主要差异在于：禁用邮箱之后，Exchange 属性将从对应的 Active Directory 用户帐户中删除，但用户帐户将保留。而删除邮箱之后，Exchange 属性和 Active Directory 用户帐户均会删除。此差异还将确定您是选择重新连接、还是选择恢复已禁用和删除的邮箱。

下表列出了您可以禁用和删除的 Exchange 邮箱类型。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>邮箱类型</th>
<th>禁用？</th>
<th>删除？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>存档邮箱</p></td>
<td><p>是</p></td>
<td><p>否*</p></td>
</tr>
<tr class="even">
<td><p>链接邮箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>资源邮箱（会议室或设备）</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p>共享邮箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>用户邮箱</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


\* 如果存档邮箱已启用，则它将在主邮箱删除时一并删除。有关禁用存档邮箱的信息，请参阅[在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)。

如果管理员删除带有邮箱的用户帐户，Exchange 信息存储最终将检测到此邮箱不再连接到用户帐户，将此邮箱标记为删除，即使邮箱处于保留状态也是如此。如果您想保留此邮箱，则必须执行以下操作：

1.  禁用用户帐户，而不是删除用户帐户。

2.  更改邮箱的属性以限制邮箱的使用和对它的访问。例如，将发送和接收配额设置为 1，阻止可以将邮件发送到邮箱的用户，限制可以访问邮箱的用户。

3.  保留此邮箱，直到擦除所有数据或直到不再需要保留为止。

有关与断开连接的邮箱相关的其他管理任务，请参阅以下主题：

  - [断开连接的邮箱](disconnected-mailboxes-exchange-2013-help.md)

  - [连接禁用的邮箱](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [连接或还原已删除的邮箱](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [永久删除邮箱](permanently-delete-a-mailbox-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“收件人设置权限”部分。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 禁用邮箱

如上所述，当您禁用邮箱之后，Exchange 属性将从对应的 Active Directory 用户帐户中删除，但该用户帐户将保留下来。

## 使用 EAC 禁用邮箱

以下步骤说明了如何禁用用户邮箱。导航至 EAC 中的适当页面之后，使用相同的过程可禁用其他邮箱类型。

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要禁用的邮箱。

3.  单击“更多”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，再单击“禁用”。

4.  此时会显示一条警告，询问您是否确实要禁用邮箱。单击“是”以禁用邮箱。

邮箱将从邮箱列表中删除。

## 使用命令行管理程序禁用邮箱

使用以下命令禁用用户邮箱、链接的邮箱、资源邮箱和共享邮箱。

```powershell
Disable-Mailbox <identity>
```

运行此命令时，系统将显示一条消息，要求您确认是否要禁用邮箱。

以下是一些禁用邮箱的命令示例。
```
```powershell
Disable-Mailbox danj
```
```
```
    Disable-Mailbox "Conf Room 31/1234 (12)"
```
```
```powershell
Disable-Mailbox sharedmbx@contoso.com
```
```

## 您如何知道这有效？

若要验证是否已成功禁用邮箱，请执行下列操作之一：

  - 在 EAC 中，单击“收件人”，导航至要禁用的邮箱类型的相应页面，然后验证此邮箱是否不再列出。

  - 在 Active Directory 用户和计算机中，右键单击已禁用邮箱的用户帐户，然后单击“属性”。在“常规”选项卡上，请注意“电子邮件”字段为空。这表明该邮箱已禁用，但用户帐户仍然存在。

  - 在此命令行管理程序中，运行以下命令。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 属性中的 `Disabled` 值表明邮箱已禁用。
    
    > [!NOTE]  
    > 删除邮箱时，<em>DisconnectReason</em> 属性中的值也为 <code>Disabled</code>。但是，对应的 Active Directory 用户帐户将会删除。


  - 在此命令行管理程序中，运行以下命令。
    
    ```powershell
Get-User <identity>
```
    
    请注意，*RecipientType* 属性的值为 `User`，而不是已禁用邮箱的用户值 `UserMailbox`。这也表明该邮箱已禁用，但用户帐户仍然存在。

## 删除邮箱

如上所述，删除邮箱之后，Exchange 属性和 Active Directory 用户帐户均会删除。邮箱（和存档邮箱（如果已启用））将在邮箱保留期过期后从邮箱数据库中永久删除。

## 使用 EAC 删除邮箱

以下步骤说明了如何删除用户邮箱。导航至 EAC 中的适当页面之后，使用相同的过程可删除其他邮箱类型。

1.  在 EAC 中，导航到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击要删除的邮箱，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

3.  此时会显示一条警告，询问您是否确实要删除邮箱。单击“是”删除邮箱。

邮箱将从邮箱列表中删除。

## 使用命令行管理程序删除邮箱

使用以下命令删除用户邮箱、链接的邮箱、资源邮箱和共享邮箱。

```powershell
Remove-Mailbox <identity>
```

运行此命令时，系统将显示一条消息，要求您确认是否要删除邮箱和对应的 Active Directory 用户帐户。

以下是一些删除邮箱的命令示例。

```
```powershell
Remove-Mailbox pilarp@contoso.com
```
```
```
    Remove-Mailbox "Fleet Van (16)"
```
```
```powershell
Remove-Mailbox corpprint
```
```

## 您如何知道这有效？

若要验证是否已成功删除邮箱，请执行以下一系列验证步骤之一。

1.  在 EAC 中，单击“收件人”，导航至要删除的邮箱类型的相应页面，然后验证此邮箱是否不再列出。

2.  在 Active Directory 用户和计算机中，验证相应的用户帐户是否不再列出。

或

1.  运行以下命令来验证邮箱是否已删除。
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisconnectReason,DisconnectDate
    
    *DisconnectReason* 属性中的 `Disabled` 值表明邮箱已删除。
    
    > [!NOTE]  
    > 删除邮箱时，<em>DisconnectReason</em> 属性中的值也为 <code>Disabled</code>。但是，对应的 Active Directory 用户帐户将会保留下来。


2.  运行以下命令，验证 Active Directory 用户帐户是否已删除。
    
    ```powershell
Get-User <identity>
```
    
    该命令将返回错误，指出找不到用户，从而验证帐户已删除。

