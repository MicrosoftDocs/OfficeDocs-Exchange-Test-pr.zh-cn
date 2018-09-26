---
title: '修改多值属性: Exchange 2013 Help'
TOCTitle: 修改多值属性
ms:assetid: dc2c1062-ad79-404b-8da3-5b5798dbb73b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb684908(v=EXCHG.150)
ms:contentKeyID: 50491784
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改多值属性

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-03-09_

多值属性是可以包含多个值的属性。例如，**RecipientFilterConfig** 对象上的 **BlockedRecipients** 属性可以接受如下示例中所示的多个收件人地址：

  - john@contoso.com

  - kim@northwindtraders.com

  - david@adatum.com

由于 **BlockedRecipients** 属性可以接受多个值，因此被称为多值属性。本主题说明如何使用 Exchange 命令行管理程序在对象上的多值属性中添加和删除值。

有关对象的详细信息，请参阅[结构化数据](https://technet.microsoft.com/zh-cn/library/aa996386\(v=exchg.150\))。有关命令行管理程序的详细信息，请参阅 [将 PowerShell 与 Exchange 2013 结合使用 (Exchange Management Shell)](https://technet.microsoft.com/zh-cn/library/bb123778\(v=exchg.150\))。

## 修改多值属性与修改仅接受一个值的属性

修改多值属性的方式与修改仅可以接受一个值的属性的方式稍有不同。当修改仅接受一个值的属性时，可以为其直接分配一个值，如以下命令所示。

```powershell
Set-TransportConfig -MaxSendSize 12MB
```

当使用该命令向 **MaxSendSize** 属性提供一个新值时，会覆盖存储的值。对于仅接受一个值的属性，则没有这个问题。但是，多值属性存在这个问题。例如，假定 **RecipientFilterConfig** 对象上的 **BlockedRecipients** 属性配置为具有在上一部分中列出的三个值。当运行命令 `Get-RecipientFilterConfig | Format-List BlockedRecipients` 时，将显示以下内容。

```powershell
BlockedRecipients : {david@adatum.com, kim@northwindtraders.com, john@contoso.com}
```

现在，假定您已经接收到一个向阻止的收件人列表中添加新的 SMTP 地址的请求。运行以下命令即可添加新的 SMTP 地址。

```powershell
Set-RecipientFilterConfig -BlockedRecipients chris@contoso.com
```

再次运行 `Get-RecipientFilterConfig | Format-List BlockedRecipients` 命令时，将看到以下内容。

```powershell
BlockedRecipients : {chris@contoso.com}
```

这并不是您所期望的。您希望向现有的阻止的收件人列表中添加新的 SMTP 地址，但新的 SMTP 地址覆盖了现有的阻止的收件人列表。这种意外结果展示了修改多值属性与修改仅接受一个值的属性不同之处。当修改多值属性时，必须确保附加或删除值，而不会覆盖整个值的列表。以下部分介绍如何正确执行该操作。

## 修改多值属性

修改多值属性类似于修改单值属性。只需要添加一些额外的语法告诉命令行管理程序需要添加或删除多值属性的值，而不必替换属性中存储的一切。在运行 cmdlet 时，语法与要在属性中添加或删除的值一起作为参数值包含在内。下表显示了在 cmdlet 上添加参数以修改多值属性时所需的语法。

### 多值属性语法

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Action</th>
<th>语法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>向多值属性添加一个或多个值</p></td>
<td>

```powershell
    @{Add=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}
```

</td>
</tr>
<tr class="even">
<td><p>从多值属性中删除一个或多个值</p></td>
<td>

```powershell
    @{Remove=&quot;&lt;value1&gt;&quot;, &quot;&lt;value2&gt;&quot;, &quot;&lt;value3&gt;&quot;}
```

</td>
</tr>
</tbody>
</table>


从多值属性语法表中选择的语法被指定为 cmdlet 上的一个参数值。例如，以下命令可向一个多值属性添加多个值：

```powershell
Set-ExampleCmdlet -Parameter @{Add="Red", "Blue", "Green"}
```

使用此语法时，会在属性上已有的值列表中添加或删除指定的值。参照本主题中之前的 **BlockedRecipients** 示例，现在通过使用以下命令，可以添加 chris@contoso.com 而无需覆盖此属性上的其余值：

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"}
```

如果要从值列表中删除 david@adatum.com，则要使用此命令：

```powershell
Set-RecipientFilterConfig -BlockedRecipients @{Remove="david@adatum.com"}
```

可以使用更复杂的组织，例如同时在属性中添加或删除多个值。为此，需要在 `Add` 和 `Remove` 操作之间插入一个分号 (`;`)。例如：

```powershell
    Set-RecipientFilterConfig -BlockedRecipients @{Add="carter@contoso.com", "sam@northwindtraders.com", "brian@adatum.com"; Remove="john@contoso.com"}
```

如果再次使用 `Get-RecipientFilterConfig | Format-List BlockedRecipients` 命令，则可看到添加了 Carter、Sam 和 Brian 的电子邮件地址，同时删除了 John 的地址。

```powershell
    BlockedRecipients : {brian@adatum.com, sam@northwindtraders.com, carter@contoso.com, chris@contoso.com, kim@northwindtraders.com}
```
