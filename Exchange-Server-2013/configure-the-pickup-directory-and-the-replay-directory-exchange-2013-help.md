---
title: '配置拾取目录和重播目录: Exchange 2013 Help'
TOCTitle: 配置拾取目录和重播目录
ms:assetid: c9ca7358-9a08-4f57-89d0-910e4438df8a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124549(v=EXCHG.150)
ms:contentKeyID: 50491541
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置拾取目录和重播目录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

分拣和重播目录由邮箱服务器和边缘传输服务器上的传输服务用于将邮件文件直接插入传输管道。复制到分拣目录或重播目录中的格式正确的电子邮件文件将被提交以进行传递。分拣目录可以由管理员使用来测试邮件流，也可以由必须创建并提交各自的邮件的应用程序使用。重播目录从非 SMTP 外部网关服务器中接收邮件，并重新提交您从 Microsoft Exchange 服务器队列导出的邮件。

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输服务”条目。

  - 只能使用命令行管理程序执行此过程。

  - **Set-TransportService** cmdlet 上 *PickupDirectoryMaxMessagesPerMinute* 参数的值由分拣和重播目录使用。

  - 更改分拣或重播目录的位置不会将任何现有邮件文件从旧的位置复制到新的位置。完成配置更改后，新的分拣或重播目录位置几乎会立即进入活动状态，但现有的邮件文件仍保留在旧位置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

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


## 希望执行何种操作？

## 使用命令行管理程序配置分拣目录

要配置拾取目录，请使用下面的语法。

    Set-TransportService <ServerIdentity> -PickupDirectoryPath <LocalFilePath> -PickupDirectoryMaxHeaderSize <Size> -PickupDirectoryMaxRecipientsPerMessage <Integer> -PickupDirectoryMaxMessagesPerMinute <Integer>

该示例对名为 Exchange01 的邮箱服务器上的分拣目录进行以下更改：

  - 分拣目录的位置设置为 D:\\Pickup Directory。

  - 邮件文件中允许的邮件标题的最大大小增加至 96 KB。

  - 邮件文件中允许的收件人的最大数目增加至 250 个。

  - 为分拣和重播目录处理的最大邮件速率增加到每分钟 200 个邮件。

<!-- end list -->

    Set-TransportService Exchange01 -PickupDirectoryPath "D:\Pickup Directory" -PickupDirectoryMaxHeaderSize 96KB -PickupDirectoryMaxRecipientsPerMessage 250 -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>将 <em>PickupDirectoryPath</em> 参数的值设置为 <code>$null</code> 可禁用分拣目录。</p></li>
<li><p><em>PickupDirectoryPath</em> 参数和 <em>ReplayDirectoryPath</em> 参数指定的目录不得相同。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 使用命令行管理程序配置重播目录

若要配置重播目录，请使用下面的语法。

    Set-TransportService <ServerIdentity> -ReplayDirectoryPath "C:\Replay Directory" <LocalFilePath> -PickupDirectoryMaxMessagesPerMinute <Integer>

该示例对名为 Exchange01 的邮箱服务器上的重播目录进行以下更改：

  - 重播目录位置设置为 D:\\Replay Directory。

  - 为分拣和重播目录处理的最大邮件速率增加到每分钟 200 个邮件。

<!-- end list -->

    Set-TransportService Exchange01 -ReplayDirectoryPath "D:\Replay Directory" -PickupDirectoryMaxMessagesPerMinute 200

<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>将 <em>ReplayDirectoryPath</em> 参数的值设置为 <code>$null</code> 可禁用重播目录。</p></li>
<li><p><em>PickupDirectoryPath</em> 参数和 <em>ReplayDirectoryPath</em> 参数指定的目录不得相同。</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 您如何知道这有效？

要验证是否已成功配置分拣和重播目录，请执行以下操作：

1.  运行以下命令：
    
        Get-TransportService <ServerIdentity> | Format-List Pickup*,Replay*

2.  验证显示的值是否为您配置的值。

