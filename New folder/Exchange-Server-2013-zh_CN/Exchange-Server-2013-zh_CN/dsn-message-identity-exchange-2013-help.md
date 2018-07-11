---
title: 'DSN 邮件标识: Exchange 2013 Help'
TOCTitle: DSN 邮件标识
ms:assetid: 70ffba22-e4fd-4cd3-98f5-8bfca2df89e4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998835(v=EXCHG.150)
ms:contentKeyID: 50490815
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# DSN 邮件标识

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

您可以基于自定义发送状态通知 (DSN) 邮件的语法对其进行标识。此标识是自定义 DSN 邮件的 GUID 或由以下值组成的字符串：

  - **Locale**   此变量指定显示 DSN 邮件所使用的语言的区域设置。有关 **New-SystemMessage** 命令可以使用的区域设置代码的列表，请参阅[系统邮件支持的语言](supported-languages-for-system-messages-exchange-2013-help.md)。

  - **Internal 或 External**   此变量指定将 DSN 邮件只发送给属于内部 Microsoft Exchange Server 2013 组织的发件人还是同时发送给 Exchange 组织外部的发件人。如果希望在发送给内部发件人的 DSN 邮件中加入特定的电子邮件联系人或解决方案，但是不希望将这些信息透露给组织外部的发件人，则可以使用 Internal 选项。

  - **DSN code**   此变量指定自定义 DSN 邮件的 DSN 代码。

DSN 邮件标识的语法为 `<Locale>\<Internal or External>\<DSN code>`。

可以为每个 DSN 代码创建多个自定义 DSN 邮件（这些邮件可以发送给内部发件人或外部发件人）以及不同的区域设置。例如，下表显示了 DSN 代码 5.1.2 一些可能的配置及相应的 DSN 邮件标识。

### DSN 配置和标识示例

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>DSN 配置</th>
<th>DSN 标识</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>向区域设置为英语 (en) 的内部发件人显示 DSN 邮件</p></td>
<td><p>En\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>向区域设置为英语 (en) 的外部发件人显示 DSN 邮件</p></td>
<td><p>En\External\5.1.2</p></td>
</tr>
<tr class="odd">
<td><p>向区域设置为日语 (ja) 的内部发件人显示 DSN 邮件</p></td>
<td><p>Ja\Internal\5.1.2</p></td>
</tr>
<tr class="even">
<td><p>向区域设置为日语 (ja) 的外部发件人显示 DSN 邮件</p></td>
<td><p>Ja\External\5.1.2</p></td>
</tr>
</tbody>
</table>

