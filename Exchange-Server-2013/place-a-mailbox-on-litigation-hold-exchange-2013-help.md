---
title: '将邮箱放到诉讼保留中: Exchange 2013 Help'
TOCTitle: 将邮箱放到诉讼保留中
ms:assetid: adee4621-3626-4aec-aa53-00b35ff0d0b0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn743673(v=EXCHG.150)
ms:contentKeyID: 62279366
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将邮箱放到诉讼保留中

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-10-18_

将邮箱置于“诉讼保留”以保留所有的邮箱内容，包括已删除项和已修改项的原始版本。当您将用户邮箱置于诉讼保留状态时，用户的存档邮箱（如果已启用）中的内容也会置于保留状态。已删除和修改的项会在指定时段内保留，或直到您将邮箱从“诉讼保留”中删除。所有此类邮箱项目均会返回到[就地电子数据展示](https://docs.microsoft.com/zh-cn/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)搜索中。

> [!IMPORTANT]  
> “诉讼保留”会保留用户邮箱中“可恢复项目”文件夹中的项。根据已删除或修改的项目的编号和大小，邮箱的“可恢复项目”文件夹的大小可能迅速增加。默认情况下，为“可恢复项目”文件夹配置了较高的配额。在 Exchange Online 中，当您将邮箱置于诉讼保留状态时，此配额会自动增加。在 Exchange Server 2013 中，我们建议您每周监视置于诉讼保留状态的邮箱，以确保它们没有达到“可恢复项目”配额的限制。


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - “诉讼保留”设置可能需要 60 分钟才能生效。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地保留”条目。

  - 要将 Exchange Online 邮箱置于诉讼保留状态，必须向其分配 Exchange Online（计划 2）许可证。如果向邮箱分配的是 Exchange Online（计划 1）许可证，必须向其分配单独的 Exchange Online 存档许可证才能将其置于保留状态。

  - 如上所述，当您将用户邮箱置于诉讼保留状态时，用户的存档邮箱中的内容也会置于保留状态。如果将 Exchange 混合部署中的内部部署主邮箱置于诉讼保留状态，则也会将基于云的存档邮箱（如果已启用）置于保留状态。

  - 在 Exchange Online 中，当您将邮箱置于诉讼保留状态时，可恢复邮件文件夹的配额会自动增加至 100 GB。此文件夹的默认大小为 30 GB。

  - “诉讼保留”会保留已删除的项目，并且还会保留修改项目的原始版本，直到该保留被删除。您可以视情况指定保留持续时间，即在指定的持续时间内保留某个邮箱项目。如果您指定保留持续时间，则从接收邮件或创建邮箱项目的日期开始计算。要保留满足指定条件的项目，请使用就地保留创建*基于查询*的保留。有关详细信息，请参阅[创建或删除就地保留](create-or-remove-an-in-place-hold-exchange-2013-help.md)。

  - 要使用命令行管理程序将 Exchange Online 邮箱置于保留状态，必须使用 Exchange Online PowerShell。 有关详细信息，请参阅[使用远程 PowerShell 连接到 Exchange Online](https://technet.microsoft.com/zh-cn/library/jj984289\(v=exchg.150\))。

  - 不支持将公用文件夹邮箱置于诉讼保留状态。必须使用就地保留来将公用文件夹置于保留状态。

## 使用 EAC 将邮箱置于诉讼保留状态

1.  转到“收件人”\>“邮箱”。

2.  在用户邮箱列表中，单击您要置于诉讼保留状态的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在邮箱属性页上，单击“邮箱功能”。

4.  在“诉讼保留: 已禁用”下，单击“启用”以将邮箱置于诉讼保留状态。

5.  在“诉讼保留”页上，输入以下可选信息：
    
      - **诉讼保留持续时间(天)**   使用此框以指定将邮箱置于诉讼保留时保留邮箱项目的时长。持续时间从接收或创建邮箱项目的日期开始计算。如果将此框留空，将无限期保留项目或保留到删除该保留。使用天指定持续时间。
    
      - **备注**   使用此框通知用户其邮箱已处于诉讼保留状态。如果您使用 Outlook 2010 或更高版本，该备注将在用户的邮箱中显示。
    
      - **URL**   使用此框将用户定向到相应网站，以便了解有关诉讼保留的详细信息。如果您使用 Outlook 2010 或更高版本，此 URL 将在用户的邮箱中显示。

6.  单击“诉讼保留”页上的**保存**，然后单击邮箱属性页上的“保存”。

返回顶部

## 使用命令行管理程序将邮箱无限期置于诉讼保留状态

此示例将邮箱 bsuneja@contoso.com 置于诉讼保留状态。邮箱中的项目将无限期保留或保留到删除该保留。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true

> [!NOTE]  
> 当您将邮箱无限期置于诉讼保留状态时（不指定持续时间），将 <em>LitigationHoldDuration</em> 属性邮箱的值设置为 <code>Unlimited</code>。


## 使用命令行管理程序将邮箱置于诉讼保留状态并将项目保留指定的持续时间

此示例将邮箱 bsuneja@contoso.com 置于诉讼保留状态，并将项目保留 2555 天（大约 7 年）。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $true -LitigationHoldDuration 2555

## 使用命令行管理程序在指定持续时间内将所有邮箱置于诉讼保留状态

您的组织可能需要将所有邮箱数据保存一段指定的时间。在您将组织中的所有邮箱置于诉讼保留状态之前，请考虑以下事项：

本示例将组织中的所有用户邮箱置于诉讼保留状态，时间为 1 年（365 天）。

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Set-Mailbox -LitigationHoldEnabled $true -LitigationHoldDuration 365

本示例使用 [Get-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123685\(v=exchg.150\)) cmdlet 检索组织中的所有邮箱，指定收件人筛选器以包含所有用户邮箱，然后将邮箱列表输出到 [Set-Mailbox](https://technet.microsoft.com/zh-cn/library/bb123981\(v=exchg.150\)) cmdlet 以启用诉讼保留和保留持续时间。

要将所有用户邮箱置于无限期保留状态，请运行以前的命令，但不包含 *LitigationHoldDuration* 参数。

请参阅详细信息部分，查看在筛选器中使用其他收件人属性以包含或排除一个或多个邮箱的示例。

## 使用命令行管理程序将邮箱从诉讼保留中删除

此示例将邮箱 bsuneja@contoso.com 从诉讼保留中删除。

    Set-Mailbox bsuneja@contoso.com -LitigationHoldEnabled $false

返回顶部

## 您如何知道这有效？

要确认已成功地将邮箱置于诉讼保留状态，请执行以下操作之一：

  - 在 EAC 中：
    
    1.  转到“收件人”\>“邮箱”。
    
    2.  在用户邮箱列表中，单击您要验证诉讼保留设置的邮箱，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    3.  在邮箱属性页上，单击“邮箱功能”。
    
    4.  在“诉讼保留”下，验证保留是否已启用。
    
    5.  单击“查看详细信息”，以验证是谁在什么时间将邮箱置于诉讼保留状态。您还可以验证或更改可选的“诉讼保留持续时间(天)”、“备注”和“URL”框中的值。

  - 在命令行管理程序中，运行以下命令之一：
    
        Get-Mailbox <name of mailbox> | FL LitigationHold*
    
    或者
    
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | FL Name,LitigationHold*
    
    如果邮箱无限期置于诉讼保留状态，则将 *LitigationHoldDuration* 邮箱属性的值设置为 `Unlimited`。

## 详细信息

  - 如果您的组织要求在特定时间段内保留所有邮箱数据，则在将组织中的所有邮箱置于诉讼保留状态之前请考虑以下事项。
    
      - 当您使用以前的命令将组织中的所有邮箱（或匹配指定收件人筛选器的邮箱子集）置于保留状态时，只有在您运行该命令时已存在的邮箱才会置于保留状态。如果您稍后创建了新的邮箱，必须再次运行该命令以将其置于保留状态。如果您频繁地创建新邮箱，您可以将该命令作为一个计划任务，按照所需的频率运行。
    
      - 将所有邮箱置于诉讼保留状态可能会对邮箱大小造成很大影响。在 Exchange Server 2013 组织中，规划充足的存储空间以满足组织的保存需求。
    
      - “可恢复的项目”文件夹自身也有存储限制，所以文件夹中的邮件不计入邮箱存储限制。如前所述，长期保存邮箱数据会导致用户邮箱和存档中的“可恢复项目”文件夹所占空间增大。在 Exchange Online 中，要适应此增加，当您将邮箱置于诉讼保留状态时，可恢复邮件文件夹的配额会从 30 GB 自动增加至 100 GB。
        
        在 Exchange Server 2013 中，“可恢复项目”文件夹的默认存储限制为 30 GB。我们建议您定期监视此文件夹，以确保不会超过此限制的大小。有关详细信息，请参阅[“可恢复的项目”文件夹](recoverable-items-folder-exchange-2013-help.md)。

  - 前面将所有邮箱置于保留状态的命令使用返回所有用户邮箱的收件人筛选器。您可以使用其他收件人属性来返回特定邮箱的列表，即您传输到 **Set-Mailbox** cmdlet 以将其置于诉讼保留状态的邮箱。
    
    下面是根据常规用户或邮箱属性，使用 **Get-Mailbox** 和 **Get-Recipient** cmdlet 返回部分邮箱的一些示例。这些示例假设已填充相关的邮箱属性（例如 *CustomAttributeN* 或 *Department*）。
    ```
        Get-Mailbox -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'CustomAttribute15 -eq "OneYearLitigationHold"'
    ```
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'Department -eq "HR"'
    ```
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'PostalCode -eq "98052"'
    ```
    ```
        Get-Recipient -RecipientTypeDetails UserMailbox -ResultSize unlimited -Filter 'StateOrProvince -eq "WA"'
    ```
    ```
        Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -ne "DiscoveryMailbox"}
    ```
    
    您可以在筛选器中使用其他用户邮箱属性来添加或排除邮箱。有关详细信息，请参阅[-Filter 参数的可筛选属性](https://technet.microsoft.com/zh-cn/library/bb738155\(v=exchg.150\))。

返回顶部

