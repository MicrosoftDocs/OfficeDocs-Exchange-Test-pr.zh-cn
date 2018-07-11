---
title: '接收连接器权限: Exchange 2013 Help'
TOCTitle: 接收连接器权限
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50490147
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 接收连接器权限

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

下表列出了各种权限类型及其说明。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>接收连接器权限</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>必须为会话授予此权限，否则会话无法将邮件提交给此接收连接器。如果会话不具备此权限，则 MAIL FROM 和 AUTH 命令将失败。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>此权限允许会话通过此连接器中继邮件。如果未授予此权限，则此连接器仅接受发送给所接受域中收件人的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>此权限允许会话绕过发件人地址欺骗检查。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>此权限允许电子邮件地址位于权威域中的发件人与该接收连接器建立会话。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>此权限允许 Exchange 2003 服务器提交来自内部发件人的邮件。Exchange 2010 将这些邮件视为内部邮件。发件人可以声明这些邮件为受信任的邮件。通过匿名提交而进入 Exchange 系统的邮件将通过 Exchange 组织进行中继，但此标志处于不受信任的状态。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>此权限允许会话提交收到的所有标头均完整无缺的邮件。如果未授予该权限，则服务器将去除所有接收的标头。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>此权限允许会话提交所有组织标头均完整无缺的邮件。组织标头均以 <strong>X-MS-Exchange-Organization-</strong> 作为开头。如果未授予该权限，则接收服务器将去除所有组织标头。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>此权限允许会话提交所有林标头均完整无缺的邮件。林头全部以 <strong>X-MS-Exchange-Forest-</strong> 作为开头。如果未授予该权限，则接收服务器将去除所有林头。</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>此权限允许会话提交含有 XEXCH50 命令的邮件。与 Exchange 2003 互操作时，需要使用此命令。XEXCH50 命令可为邮件提供诸如垃圾邮件可信度 (SCL) 等数据。</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>此权限允许会话提交大小超过为连接器配置的邮件大小限制的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>此权限允许会话绕过反垃圾邮件筛选。</p></td>
</tr>
</tbody>
</table>

