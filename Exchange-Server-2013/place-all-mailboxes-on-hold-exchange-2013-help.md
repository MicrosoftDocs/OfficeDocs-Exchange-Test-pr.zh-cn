---
title: '保留所有邮箱: Exchange 2013 Help'
TOCTitle: 保留所有邮箱
ms:assetid: 4c141604-3210-44cc-b98e-f3e0f15613b8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn767952(v=EXCHG.150)
ms:contentKeyID: 62486273
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 保留所有邮箱

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-01-18_

> [!NOTE]  
> 在 Exchange Online（Office 365 和 Exchange Online 独立计划）中新建就地保留的截止时间为 2017 年 7 月 1 日，我们已推迟了这一最后期限。不过，今年晚些时候或明年初，将无法在 Exchange Online 中新建就地保留。作为就地保留的备选方法，可以在 Office 365 安全与合规中心使用<a href="https://go.microsoft.com/fwlink/?linkid=780738">电子数据展示服务案例</a>或<a href="https://go.microsoft.com/fwlink/?linkid=827811">保留策略</a>。在我们取消新建就地保留后，仍可以修改现有就地保留，并且在 Exchange Server 2013 和 Exchange 混合部署中新建就地保留也仍将受支持。此外，也仍可以将邮箱置于诉讼保留。


您的组织可能需要将所有邮箱数据保存一段指定的时间。您可以使用诉讼保留或就地保留满足这一要求。当您将一个邮箱置于诉讼保留或就地保留状态后，修改或永久删除的邮箱邮件将保存在“可恢复邮件”文件夹中。有关详细信息，请参阅[就地保留和诉讼保留](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-and-litigation-holds)。

在您将组织中的所有邮箱置于诉讼保留或就地保留状态之前，请考虑下列问题：

  - 当您将邮箱置于保留状态时，用户的存档邮箱（如果已启用）中的内容也置于保留状态。

  - 将组织中的所有邮箱置于保留状态会大大影响邮箱的大小。在 Exchange Server 2013 部署中，规划充足的存储空间以满足组织的保存需求。在 Exchange Online 中，您的用户的[邮箱存储限制](https://go.microsoft.com/fwlink/?linkid=403645)取决于用户的订阅许可证。

  - 长期保存邮箱数据会导致用户的主邮箱和存档邮箱中的“可恢复邮件”文件夹所占空间增大。“可恢复的项目”文件夹自身也有存储限制，所以文件夹中的邮件不计入邮箱存储限制。在 Exchange Server 2013 和 Exchange Online 中，可恢复邮件文件夹的默认存储限制为 30 GB。
    
      - 在 Exchange Online 中，当您将邮箱置于保留状态时，可恢复邮件文件夹的配额会自动增加至 100 GB。
    
      - 在 Exchange Server 2013 中，我们建议您定期监视此文件夹，以确保不会超过此限制的大小。有关详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

## 在诉讼保留和就地保留之间进行选择

您在考虑将组织中的所有邮箱置于保留状态应该使用何种保留功能时需考虑以下因素。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>您想要...</th>
<th>使用诉讼保留</th>
<th>使用就地保留</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>使用 EAC</p></td>
<td><p>是</p>
<p>对于设置诉讼保留来说，EAC 最适合于快速一次性操作几个邮箱。我们建议对组织中的所有用户使用 Shell 进行诉讼保留设置。</p></td>
<td><p>是</p>
<p>但是，您不能在 EAC 中选择多于 500 个源邮箱。</p></td>
</tr>
<tr class="even">
<td><p>使用 Shell</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p>将多于 10,000 个邮箱置于保留状态</p></td>
<td><p>是</p>
<p>诉讼保留是一个邮箱属性。通过 <strong>Set-Mailbox</strong> cmdlet，您可以将组织中的所有邮箱置于保留状态。</p></td>
<td><p>是；使用多次就地保留</p>
<p>您可以使用通讯组以在单次就地保留中指定至多 10,000 个邮箱。若要将更多的邮箱置于保留状态，您必须创建更多的就地保留。这将造成额外的管理开销。使用诉讼保留，将大量邮箱置于保留状态更加简单。</p></td>
</tr>
<tr class="even">
<td><p>将许多不同的邮箱置于不同时长的保留状态。</p></td>
<td><p>是</p>
<p>诉讼保留是一个邮箱属性。您可以将每个邮箱（或邮箱集）置于不同时长的保留状态。</p>
<p>请参阅详细信息部分，了解在筛选器中使用收件人属性将部分邮箱置于诉讼保留的示例。</p></td>
<td><p>是</p>
<p>如果您要为数千个邮箱设置各自的保留，我们推荐使用诉讼保留。如果您要为指定的包含多个用户的事件创建保留，请对该用户组使用单次就地保留。</p>
<p>不建议为每个邮箱创建单独的就地保留，因为这将创建许多比诉讼保留更难管理的就地保留查询。就地保留对象过多也会导致刷新、创建或修改保留对象时 EAC 中的进程运行缓慢。</p></td>
</tr>
<tr class="odd">
<td><p>自动将新邮箱置于保留状态</p></td>
<td><p>否</p>
<p>创建新邮箱之后，您必须将其置于诉讼保留状态。您可以计划使命令或脚本按所需频率运行以取得同样的效果。</p></td>
<td><p>否</p>
<p>您必须将新的邮箱添加到就地保留，即使您在创建就地保留时指定了通讯组也是如此。您也可以计划使命令或脚本按所需频率运行以取得同样的效果。我们建议在现有的就地保留达到 10,000 个邮箱的限制时进行脚本检查，然后在需要时创建一个新的就地保留。</p></td>
</tr>
<tr class="even">
<td><p>将所有公用文件夹置于保留状态</p></td>
<td><p>否</p>
<p>在 Exchange Online 中，不支持将公用文件夹邮箱置于诉讼保留状态。必须使用就地保留。</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


## 将所有邮箱置于诉讼保留状态。

您可以通过使用 Shell 将所有邮箱置于无限期或特定时长的保留状态。此命令会将所有邮箱置于保留状态 2555 天（大约 7 年）。

```powershell
Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 2555
```

该示例使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 和收件人筛选器来检索组织中的所有用户邮箱，然后将邮箱列表输出到 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet，以启用诉讼保留并指定保留时长。有关详细信息，请参阅[将邮箱放到诉讼保留中](place-a-mailbox-on-litigation-hold-exchange-2013-help.md)。

## 将所有邮箱置于就地保留状态

您可以使用 EAC 选择多达 500 个邮箱并将其置于保留状态。有关详细信息，请参阅[创建或删除就地保留](https://technet.microsoft.com/zh-cn/library/dd979797(v=exchg.150))。

> [!TIP]  
> 要将多于 500 个用户置于就地保留状态，请使用 Shell。请参阅 <a href="https://technet.microsoft.com/zh-cn/library/dd298064(v=exchg.150)">New-MailboxSearch</a>。


## 详细信息

  - 当您将组织中的所有邮箱置于保留状态时，只有当您运行命令时已存在的邮箱将置于保留状态。如果您后续创建了新的邮箱，请再次运行该命令以将其置于保留状态。如果您频繁地创建新邮箱，您可以将该命令作为一个计划任务，按照所需的频率运行。

  - 将邮箱置于保留状态可以保留相关数据。方法是：在指定日期前阻止删除数据以及在修改邮件前保留初始版本的邮件。它不会在指定时间段后自动删除邮件。将诉讼保留或就地保留与保留策略结合起来，这可以自动删除指定时间段后的邮件，从而满足您组织的电子邮件保留要求。有关详细信息，请参阅[保留标记和保留策略](https://technet.microsoft.com/zh-cn/library/dd297955(v=exchg.150))。

  - 在本主题中用于将所有邮箱置于诉讼保留状态的 PowerShell 命令使用返回所有用户邮箱的收件人筛选器。您可以使用其他收件人属性来返回特定邮箱的列表，即您传输到 **Set-Mailbox** cmdlet 以将其置于诉讼保留状态的邮箱。
    
    下面是根据常规用户或邮箱属性，使用 **Get-Mailbox** 和 **Get-Recipient** cmdlet 返回部分邮箱的一些示例。这些示例假设已填充相关的邮箱属性（例如 *CustomAttributeN* 或 *Department*）。
    
    ```powershell
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```
    
    ```powershell
    Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    
    ```powershell
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    
    ```powershell
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    
    ```powershell
    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    ```
    
    您可以在筛选器中使用其他用户邮箱属性来添加或排除邮箱。有关详细信息，请参阅[-Filter 参数的可筛选属性](https://technet.microsoft.com/zh-cn/library/bb738155\(v=exchg.150\))。

