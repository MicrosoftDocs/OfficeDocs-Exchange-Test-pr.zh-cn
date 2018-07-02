---
title: '移动电话和平板电脑功能: Exchange 2013 Help'
TOCTitle: 移动电话和平板电脑功能
ms:assetid: ad54d9e6-7a1c-4fb0-b5a9-0b042b98ada3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb232162(v=EXCHG.150)
ms:contentKeyID: 50556654
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 移动电话和平板电脑功能

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

用户可以通过 Microsoft Exchange ActiveSync，在移动电话、平板电脑及其他便携设备上访问其电子邮件、日历、联系人和任务信息。他们还可以使用 Microsoft Exchange ActiveSync 设置自己的签名和自动回复。多种移动电话和设备可与 Exchange ActiveSync 配合使用。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>尽管我们一贯地将访问 Exchange Server 2013 的设备视为移动电话，但是有许多可以访问 Exchange 2013 的设备没有移动电话功能。本文档中的术语“移动电话”也指这些设备。</td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 兼容设备

用户可以通过选择与 Exchange ActiveSync 兼容的移动电话利用 Exchange ActiveSync 的丰富功能。许多制造商和电信运营商都提供这些移动电话。有关详细信息，请参阅具体的移动电话文档。

与 Microsoft Exchange 兼容的移动电话包括：

  - **Apple** Apple iPhone、iPod Touch 和 iPad 全都支持 Exchange ActiveSync。

  - **Windows Phone**   Windows Phone 8、Windows Phone 7 及更早版本都支持 Exchange ActiveSync。

  - **Android**   许多采用 Android 操作系统的移动电话和平板电脑都支持 Exchange ActiveSync。但是，这些移动设备可能不支持所有可用的移动设备邮箱策略。有关详细信息，请参阅[移动设备邮箱策略](mobile-device-mailbox-policies-exchange-2013-help.md)。

## WWindows Phone 软件功能

将 Windows Phone 软件作为其操作系统的移动电话在与 Exchange 2013 同步时可提供最为强大的功能。下表列出了可用于 Windows Phone 8 和 Windows Phone 7 的移动设备邮箱策略。

### Windows Phone 7 和 8 的功能

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作系统</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Windows Phone 8</p></td>
<td><p>Windows Phone 8 支持以下移动设备邮箱策略：</p>
<ul>
<li><p>允许简单设备密码</p></li>
<li><p>必须是字母数字密码</p></li>
<li><p>启用设备密码</p></li>
<li><p>设备密码过期</p></li>
<li><p>启用 IRM</p></li>
<li><p>最大设备密码尝试失败次数</p></li>
<li><p>最大不活动设备时间锁定</p></li>
<li><p>最小设备密码复杂字符数</p></li>
<li><p>最短设备密码长度</p></li>
<li><p>要求设备加密</p></li>
<li><p>远程擦除</p></li>
</ul>
<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果组织使用其他移动设备邮箱策略设置，则需要将“允许不可设置的设备”策略设置为 true。这对组织有安全上的意义，因为将允许不符合所有移动设备策略设置要求的其他移动电话和设备进行同步。有关详细信息，请参阅<a href="mobile-device-mailbox-policies-exchange-2013-help.md">移动设备邮箱策略</a>。</td>
</tr>
</tbody>
</table>

</td>
</tr>
<tr class="even">
<td><p>Windows Phone 7</p></td>
<td><p>Windows Phone 7 移动电话仅支持部分 Exchange ActiveSync 邮箱策略设置：</p>
<ul>
<li><p>需要使用密码</p></li>
<li><p>最短密码长度</p></li>
<li><p>最大不活动时间锁定</p></li>
<li><p>最大设备密码尝试失败次数</p></li>
<li><p>允许简单密码</p></li>
<li><p>密码有效期</p></li>
<li><p>密码历史记录</p></li>
<li><p>禁用可移动存储</p></li>
<li><p>禁用 IrDA</p></li>
<li><p>禁用桌面同步</p></li>
<li><p>阻止远程桌面</p></li>
<li><p>阻止 Internet 共享</p></li>
</ul></td>
</tr>
</tbody>
</table>

