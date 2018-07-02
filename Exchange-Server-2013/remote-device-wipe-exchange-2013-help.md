---
title: '远程设备擦除: Exchange 2013 Help'
TOCTitle: 远程设备擦除
ms:assetid: cd615210-cd8a-48de-b3e3-8f9ec39ca380
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124591(v=EXCHG.150)
ms:contentKeyID: 50491707
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 远程设备擦除

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-09-19_

手机、平板电脑和其他设备可以存储敏感的公司数据并访问许多公司资源。 如果移动设备丢失或被盗，数据可能存在安全风险。 通过 Microsoft Exchange 移动设备邮箱策略，可以向移动设备中添加密码要求。 这将要求用户只有输入密码后才能访问其移动设备。 我们建议除了要求提供设备密码之外，还应该将您的移动设备配置为在一段不活动时间之后自动提示输入密码。 设备密码和不活动期间锁定的结合使用将为公司数据提供更安全的保护。

除了这些功能，Exchange Server 2013 还提供了远程设备擦除功能。 可以从 Exchange 命令行管理程序或 Exchange 管理中心 (EAC) 中发出远程设备擦除命令。 用户可以从 MicrosoftOutlook Web App 用户界面发出其自己的远程设备擦除命令。

远程设备擦除功能还包括确认功能，可以将时间戳写入用户邮箱的同步状态数据中。 该时间戳会在 Outlook Web App 和 EAC 中的用户移动电话属性对话框中显示。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>远程设备擦除操作可将手机重置为出厂默认状态。 尽管 Exchange 2013 中实施的远程设备擦除协议仅需要删除个人或公司数据，但是当前的移动设备制造商都将此命令解释为擦除手机上的所有数据。 许多移动设备操作系统也会擦除任何插入移动设备的存储卡上的所有数据。 如果在自己的移动电话上执行远程设备擦除且要保留存储卡上的数据，则我们建议在启动远程设备擦除之前先拔掉存储卡。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Dd876845.Caution(EXCHG.150).gif" title="小心" alt="小心" />小心：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在进行远程设备擦除之后，数据恢复将非常困难。 但是，所有数据删除过程都无法使移动设备像新的时那样完全没有数据。 通过使用复杂的工具，仍然有可能恢复移动设备上的数据。</td>
</tr>
</tbody>
</table>


## 远程设备擦除与本地设备擦除

进行本地设备擦除时，设备会进行自我擦除，无须服务器进行请求。 如果您组织中已实施的移动设备邮箱策略指定了最大不成功密码尝试次数，并且已经超过了此最大值，则移动设备将执行本地设备擦除。 本地设备擦除的结果与远程设备擦除的结果相同。 设备将恢复为其出厂默认状态。 当移动设备执行本地设备擦除时，不会向 Exchange 服务器发送任何确认消息。

