---
title: '在夏令时或时区更改时更新 Exchange 组织: Exchange 2013 Help'
TOCTitle: 在夏令时或时区更改时更新 Exchange 组织
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 70086927
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在夏令时或时区更改时更新 Exchange 组织

 

_**适用于：** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

如果组织或某些用户所处的国家或地区更改了其识别夏令时 (DST) 的策略，或更改了与协调世界时 (UTC) 的本地时间偏移，则您可能需要更新 Microsoft Windows、Microsoft Exchange、Microsoft Outlook 或其他程序以适应这些更改。

有关世界各地的 DST 更改的详细信息（包括链接），请参阅 [Microsoft 夏令时帮助和支持中心](https://go.microsoft.com/fwlink/p/?linkid=99640)。另请访问其他软件供应商的支持网站，以查看是否需要任何其他更新。

即使您的时区未更改，如果在全球范围内与其他计算机或用户交互，则您的计算机也需要能够针对世界上其他位置的事件执行准确的日期和时间计算。

尽快安装时区更新可尽量减少在从旧时间和日期转换到新时间和日期的过程中安排的会议或约会数。

## 您该如何做？

## 步骤 1：在所有客户端和台式计算机上安装 Windows DST 更新

因为在 DST 或时区更改时更新了 Office 365 身份验证系统，所以所有 Office 365 客户端计算机都需要进行更新，否则可能会遇到连接问题。

  - 确保所有客户端和台式计算机都安装了 Windows DST 更新。有关详细信息，请参阅[如何配置 Microsoft Windows 操作系统夏令时](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=914387)。

## 步骤 2：在所有服务器上安装 Windows DST 更新

1.  使用 Windows DST 更新来更新所有内部部署服务器。

2.  如果运行 Office 365，则更新与 Office 365 身份验证系统交互的所有服务器（如目录同步或 AD FS 服务器）。这些服务器必须进行更新以确保正常运行时间。

**注意**   如果更新服务器群集，请确保按照更新群集的常规过程来执行。首先更新被动服务器，故障转移到被动服务器（会成为活动状态），然后更新以前的活动（现在成为被动状态）服务器。有关如何更新服务器群集和高可用性服务器群集的详细信息，请参阅[Update Exchange Server Clusters and High Availability Servers](https://technet.microsoft.com/zh-cn/library/hh530052\(v=exchg.150\))和 [How to update Windows Server failover clusters](https://support.microsoft.com/en-us/kb/174799)（如何更新 Windows Server 故障转移群集）。

## 步骤 3：根据需要在客户端和台式计算机上更新 Exchange 和 Outlook

1.  如果用户使用的是 Outlook 2007 或更早版本的客户端，则使用此过程后面的表确定需要要运行的 Exchange 或 Outlook 时区工具。

2.  向需要更新其计算机的用户发送邮件，以便为其提供指向合适工具的链接。

下表显示用户应在何时运行 [Exchange 日历更新工具](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879)或 [Microsoft Office Outlook 时区数据更新工具](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667)。查找组织的服务器所运行的版本，然后确定用户所运行的客户端程序。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>客户端版本</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>组织版本</strong></p></td>
<td><p><strong>Outlook 2003 或 Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 内部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 日历工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 内部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 日历工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 内部部署</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=930879">Exchange 日历工具</a>或</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2013 本地环境</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-D (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a></p></td>
<td><p>不需要执行任何操作</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a>（Outlook 2003 不支持）</p></td>
<td><p>无需任何操作</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=931667">Microsoft Office Outlook 时区数据更新工具</a>（Outlook 2003 不支持）</p></td>
<td><p>无需任何操作</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

