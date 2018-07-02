---
title: '管理内部部署移动: Exchange 2013 Help'
TOCTitle: 管理内部部署移动
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 50489961
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 管理内部部署移动

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-02-25_

移动请求是将邮箱从一个邮箱数据库移动到另一个邮箱数据库的过程。本地移动请求是在单林内发生的邮箱移动。在 Microsoft Exchange Server 2013 中，邮箱和个人存档邮箱可以驻留在单独的数据库中。使用移动请求功能，可以将主邮箱及其关联的存档移动到同一数据库或分别移动到单独的数据库中。本主题中的过程将有助于进行内部部署邮箱移动。

使用以下过程在内部部署组织中移动邮箱。这些过程使用 Exchange 命令行管理程序和 Exchange 中心 (EAC)。

使用移动请求移动邮箱时，以下两个服务将对移动请求进行处理：

  - Microsoft Exchange 邮箱复制服务

  - Microsoft Exchange 邮箱复制代理

有关邮箱复制服务器和代理的详细信息，请参阅[了解有关 MRS 代理的详细信息](https://technet.microsoft.com/zh-cn/library/jj156451\(v=exchg.150\))。

有关邮箱移动的详细信息，请参阅 [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：20 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)中的“邮箱移动和迁移权限”条目。

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


## 您想执行什么操作？

## 测试邮箱是否可以移动

此示例使用 *WhatIf* 开关测试是否可以将 Tony Smith 的邮箱移动到新的数据库 DB01，以及在此命令中是否存在任何错误。使用 *WhatIf* 开关时，系统将对邮箱执行检查。如果邮箱不可以移动，将出现错误。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 创建本地移动请求

## 使用 EAC 创建本地移动请求

若要创建本地移动请求，请登录 EAC 并执行以下步骤：

1.  在 EAC 中，导航至“收件人”\>“迁移”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建本地邮箱移动”向导中，选择要移动的用户并单击“确定”，然后单击“下一步”。

3.  在“移动配置”页面上，为新的批次指定名称。选择您需要存档邮箱的哪些选项以及邮箱数据位置，然后单击“新建”。

## 使用命令行管理程序创建本地移动请求

有关如何创建本地移动请求的示例，请参阅 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\)) 中的示例 2。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 在 EAC 中，导航到“收件人”\>“迁移”。

  - 通过单击“所有批次状态”检查您在 EAC 中的移动是否成功。

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 创建批移动请求

## 使用 EAC 创建批处理移动请求

登录 EAC 并执行下列步骤：

1.  在 EAC 中，导航至“收件人”\>“迁移”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建本地邮箱移动”向导中，选择要移动的用户并单击“确定”，然后单击“下一步”。

3.  在“移动配置”页面上，为新的批次指定名称。选择您需要存档邮箱的哪些选项以及邮箱数据位置，然后单击“新建”。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>确保不要将“错误项限制”设置为超过 50 个项目。如果超过 50 项，移动可能会失败。如果要将“错误项限制”设置为超过 50 个项目，必须使用 Exchange 命令行管理程序并将 <em>AcceptLargeDataLoss</em> 参数设置为 True。</td>
</tr>
</tbody>
</table>


## 使用命令行管理程序创建批处理移动请求

此示例创建了一个本地移动迁移批处理，其中指定 .csv 文件中的邮箱将迁移到一个不同的邮箱数据库。此 .csv 文件包含单个列，列中包含要移动的每个邮箱的电子邮件地址。此列的标题必须命名为 **EmailAddress**。此示例中的迁移批处理必须使用 **Start-MigrationBatch** cmdlet 或 Exchange 管理中心 (EAC) 手动启动。或者，也可以使用 *AutoStart* 参数自动启动该迁移批次。

    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"

    Start-MigrationBatch -Identity LocalMove1

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [Start-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219165\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 通过单击“所有批次状态”检查您在 EAC 中的移动是否成功。

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 显示迁移批处理

有关使用命令行管理程序显示迁移批处理的示例，请参阅 [Get-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219164\(v=exchg.150\)) 中的示例 2。

## 仅移动用户的主邮箱

## 使用 EAC 仅移动用户的主邮箱

1.  在 EAC 中，导航至“收件人”\>“迁移”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建本地邮箱移动”向导中，选择要移动其主邮箱的用户并单击“确定”，然后单击“下一步”。

3.  在“移动配置”页面上，为新的批次指定名称。选择“仅移动主邮箱”，选择要用于邮箱数据库位置的选项，然后单击“新建”。

## 使用命令行管理程序仅移动用户的主邮箱

本示例仅将 Tony Smith 的主邮箱移动到 DB01。不移动存档。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"

有关语法和参数的详细信息，请参阅 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 在 EAC 中，单击“所有批处理的状态”。

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 使用 .csv 批处理文件创建跨林移动

此示例配置迁移终结点，然后使用 .csv 文件创建一个从源林到目标林的跨林批处理移动。

    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"

有关为跨林移动准备好林的详细信息，请参阅下列主题：

  - [为跨林移动请求准备邮箱](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [使用示例代码准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [在命令行管理程序中使用 Prepare-MoveRequest.ps1 脚本准备跨林移动的邮箱](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 仅移动存档邮箱

## 使用 EAC 仅移动存档邮箱

1.  在 EAC 中，导航至“收件人”\>“迁移”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建本地邮箱移动”向导中，选择要移动其存档邮箱的用户并单击“确定”，然后单击“下一步”。

3.  在“移动配置”页面上，为新的批次指定名称。选择“仅移动存档邮箱”，选择要用于邮箱数据库位置的选项，然后单击“新建”。

## 使用命令行管理程序仅移动存档邮箱

本示例仅将 Tony Smith 的存档邮箱移动到 DB03。不移动主邮箱。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 将用户的主邮箱和存档邮箱分别移动到单独的数据库

本示例将 Ayla 的主邮箱和存档邮箱移动到单独的数据库。主数据库移动到 DB01，存档移动到 DB03。

    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

## 移动用户的主邮箱并允许较大的错误项限制

## 使用 EAC 移动用户的主邮箱并允许较大的错误项限制

1.  在 EAC 中，导航至“收件人”\>“迁移”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建本地邮箱移动”向导中，选择要移动其主邮箱的用户并单击“确定”，然后单击“下一步”。

3.  在“移动配置”页面上，为新的批次指定名称。选择“仅移动主邮箱”，然后选择要用于邮箱数据库位置的选项。

4.  单击“更多选项”![更多选项图标](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "更多选项图标")，输入错误项限制，然后单击“确定”。

## 使用命令行管理程序移动用户的主邮箱并允许较大的错误项限制

此示例将 Lisa 的主邮箱移动到邮箱数据库 DB01，并将错误项限制设置为 `100`。若要设置较大的错误项限制，必须使用 *AcceptLargeDataLoss* 参数。

    New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss

有关语法和参数的详细信息，请参阅 [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\)) 和 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 您如何知道这有效？

要验证您是否已成功完成迁移，请执行下列操作：

  - 从命令行管理程序执行以下命令，检索邮箱移动信息。
    
        Get-MigrationUserStatistics -Identity BatchName -Status | Format-List

有关详细信息，请参阅 [Get-MigrationUserStatistics](https://technet.microsoft.com/zh-cn/library/jj218695\(v=exchg.150\))。

