---
title: '远程域支持的字符集: Exchange 2013 Help'
TOCTitle: 远程域支持的字符集
ms:assetid: 66023a62-1fd3-4019-be2b-4e7147db148a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998600(v=EXCHG.150)
ms:contentKeyID: 52061367
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 远程域支持的字符集

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2015-03-09_

对于发送到远程域的邮件，可以指定以下字符集。

  - 在 Exchange 管理中心 (EAC) 的“远程域”设置页面上，从“MIME 字符集”和“非 MIME 字符集”下拉列表中选择名称。

  - 在命令行管理程序中，对 [Set-RemoteDomain](https://technet.microsoft.com/zh-cn/library/aa997857\(v=exchg.150\)) cmdlet 中的 *CharacterSet* 参数或 *NonMimeCharacterSet* 参数使用下表中“名称”列中的值。

### 远程域配置的受支持字符集

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>名称</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>big5</p></td>
<td><p>繁体中文(Big5)</p></td>
</tr>
<tr class="even">
<td><p>DIN_66003</p></td>
<td><p>德语 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>euc-jp</p></td>
<td><p>日语(EUC)</p></td>
</tr>
<tr class="even">
<td><p>euc-kr</p></td>
<td><p>朝鲜语(EUC)</p></td>
</tr>
<tr class="odd">
<td><p>GB18030</p></td>
<td><p>简体中文(GB18030)</p></td>
</tr>
<tr class="even">
<td><p>gb2312</p></td>
<td><p>简体中文(GB2312)</p></td>
</tr>
<tr class="odd">
<td><p>hz-gb-2312</p></td>
<td><p>简体中文(HZ)</p></td>
</tr>
<tr class="even">
<td><p>iso-2022-jp</p></td>
<td><p>日语(JIS)</p></td>
</tr>
<tr class="odd">
<td><p>iso-2022-kr</p></td>
<td><p>朝鲜语 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-1</p></td>
<td><p>西欧语 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-2</p></td>
<td><p>中欧字符 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-3</p></td>
<td><p>拉丁语 3 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-4</p></td>
<td><p>波罗的海字符 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-5</p></td>
<td><p>塞瑞利克字符 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-6</p></td>
<td><p>阿拉伯语 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-7</p></td>
<td><p>希腊语 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-8</p></td>
<td><p>希伯来语 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-9</p></td>
<td><p>土耳其语 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>iso-8859-13</p></td>
<td><p>爱沙尼亚语 (ISO)</p></td>
</tr>
<tr class="even">
<td><p>iso-8859-15</p></td>
<td><p>拉丁文 9 (ISO)</p></td>
</tr>
<tr class="odd">
<td><p>koi8-r</p></td>
<td><p>塞瑞利克字符 (KOI8-R)</p></td>
</tr>
<tr class="even">
<td><p>koi8-u</p></td>
<td><p>塞瑞利克字符 (KOI8-U)</p></td>
</tr>
<tr class="odd">
<td><p>ks_c_5601-1987</p></td>
<td><p>朝鲜语 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>NS_4551-1</p></td>
<td><p>挪威语 (IA5)</p></td>
</tr>
<tr class="odd">
<td><p>SEN_850200_B</p></td>
<td><p>瑞典语 (IA5)</p></td>
</tr>
<tr class="even">
<td><p>shift_jis</p></td>
<td><p>日语(Shift-JIS)</p></td>
</tr>
<tr class="odd">
<td><p>utf-8</p></td>
<td><p>Unicode (UTF-8)</p></td>
</tr>
<tr class="even">
<td><p>windows-1250</p></td>
<td><p>中欧字符 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1251</p></td>
<td><p>塞瑞利克字符 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1252</p></td>
<td><p>西欧字符 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1253</p></td>
<td><p>希腊语 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1254</p></td>
<td><p>土耳其语 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1255</p></td>
<td><p>希伯来语 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1256</p></td>
<td><p>阿拉伯语 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-1257</p></td>
<td><p>波罗的海字符 (Windows)</p></td>
</tr>
<tr class="even">
<td><p>windows-1258</p></td>
<td><p>越南语 (Windows)</p></td>
</tr>
<tr class="odd">
<td><p>windows-874</p></td>
<td><p>泰语 (Windows)</p></td>
</tr>
</tbody>
</table>

