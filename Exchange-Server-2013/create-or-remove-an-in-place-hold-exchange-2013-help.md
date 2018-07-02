﻿---
title: '创建或删除就地保留: Exchange 2013 Help'
TOCTitle: 创建或删除就地保留
ms:assetid: 9d5d8d37-a053-4830-9cb1-6e1ede25e963
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd979797(v=EXCHG.150)
ms:contentKeyID: 50491226
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建或删除就地保留

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2017-01-18_

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange Online（Office 365 和 Exchange Online 独立计划）中新建就地保留的截止时间为 2017 年 7 月 1 日，我们已推迟了这一最后期限。不过，今年晚些时候或明年初，将无法在 Exchange Online 中新建就地保留。作为就地保留的备选方法，可以在 Office 365 安全与合规中心使用<a href="https://go.microsoft.com/fwlink/?linkid=780738">电子数据展示服务案例</a>或<a href="https://go.microsoft.com/fwlink/?linkid=827811">保留策略</a>。在我们取消新建就地保留后，仍可以修改现有就地保留，并且在 Exchange Server 2013 和 Exchange 混合部署中新建就地保留也仍将受支持。此外，也仍可以将邮箱置于诉讼保留。</td>
</tr>
</tbody>
</table>


就地保留将保留所有邮箱内容，包括已删除项目和已修改项目的原始版本。所有此类邮箱项目均会返回到[就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)搜索中。将用户的邮箱置于就地保留时，相应的存档邮箱（如果已启用）中的内容也将置于保留状态，并在电子数据展示搜索中返回。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“就地保留”条目。

  - 要将 Exchange Online 邮箱置于就地保留状态，必须向其分配 Exchange Online（计划 2）许可证。如果向邮箱分配的是 Exchange Online（计划 1）许可证，必须向其分配单独的 Exchange Online 存档许可证才能将其置于保留状态。

  - 根据您的 Active Directory 拓扑和复制延迟设置，就地保留可能需要一个小时才会生效。

  - 如上所述，当您将用户邮箱置于就地保留状态时，用户的存档邮箱中的内容也会置于保留状态。如果将 Exchange 混合部署中的内部部署主邮箱置于就地保留状态，则也会将基于云的存档邮箱（如果已启用）置于保留状态。

  - 如果将用户放在多个就地保留，来自任何基于查询的搜索查询将合并（使用 **OR** 运算符）。在这种情况下，放在一个邮箱中的所有基于查询的保留中关键字的最大数量为 500。如果超过 500 个关键字，则邮箱中的所有内容都将置于保留状态（而不只是符合搜索条件的内容）。将保留所有内容，直到关键字总数减少到 500 或更少。

  - 在 Exchange Online 中，当您将邮箱置于就地保留状态时，可恢复邮件文件夹的配额会自动增加至 100 GB。“可恢复的项目”文件夹的默认大小为 30 GB。

  - 在 Exchange Online 中，您可以将 Office 365 组置于就地保留状态。当您将 Office 365 组置于保留状态时，组邮箱将置于保留状态，但组成员的邮箱不会置于保留状态。有关 Office 365 组的信息，请参阅[了解 Office 365 组](https://go.microsoft.com/fwlink/p/?linkid=724066)。

## 创建就地保留

**使用 EAC 创建就地保留**

1.  导航到“合规性管理”\>“就地电子数据展示与保留”。

2.  单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在“就地电子数据展示与保留”中的“名称和描述”页面上键入搜索名称和可选描述，然后单击“下一步”。

4.  在“**邮箱和公用文件夹**”页上，选择要置于保留状态的内容位置，然后单击“**下一步**”。
    
    ![选择将其置于保留状态的内容位置](images/Dd979797.bbe76c50-a93b-4e5e-acd2-78e0d747ea19(EXCHG.150).png "选择将其置于保留状态的内容位置")  
    
    1.  **搜索所有邮箱**   创建就地保留时，不能选择此选项。可以选择此选项用于就地电子数据展示搜索，但若要创建就地保留，必须选择要置于保留状态的特定邮箱。
    
    2.  **不要搜索任何邮箱**   专为公用文件夹创建就地保留时，请选择此选项。
    
    3.  **指定要搜索的邮箱**   选中此选项，然后单击“**添加**”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")以选择要置于保留状态的邮箱或通讯组。在 Exchange Online 中，还可以选择要置于保留状态的 Office 365 组。
    
    4.  **搜索所有公用文件夹**   在 Exchange Online 中，可以选中此复选框将组织中的所有公用文件夹置于保留状态。如上文所述，若要仅为公用文件夹创建就地保留，请务必选择“**不要搜索任何邮箱**”选项。

5.  在“搜索查询”页面上，完成下列字段，然后单击“下一步”：
    
      - “包含所有用户邮箱内容”   单击此按钮以保留选定邮箱中的所有内容。
    
      - **基于条件筛选**   单击此按钮以指定搜索条件，包括关键词、开始和结束日期、发件人和收件人地址以及邮件类型。创建基于查询的保留时，只会保留与搜索条件相匹配的项。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>将公用文件夹置于就地保留状态时，还保留了与公用文件夹层次结构同步过程相关的电子邮件。这可能会导致保存数千个与层次结构同步相关的电子邮件项。这些邮件可能会填满公用文件夹邮箱上可恢复项目文件夹的存储配额。为了防止发生此状况，可以创建一个基于查询的就地保留，并将下列 <code>property:value</code> 对添加到搜索查询：<br />
        <code>NOT(subject:HierarchySync*)</code><br />
        其结果是，主题行中包含短语“HierarchySync”的任何邮件（与公用文件夹层次结构的同步相关）都不会置于保留状态。</td>
        </tr>
        </tbody>
        </table>


6.  在“就地保留设置”页面上，选中“将与所选邮箱中的搜索查询匹配的内容置于保留状态”复选框，然后选择以下选项之一：
    
      - **无限期保留**   单击此按钮以无限期保留搜索返回的项目。保留的项目将会保持，直到您从搜索中删除邮箱或删除搜索。
    
      - **指定保留项目的天数（相对于收到日期）**   单击此按钮以在指定周期内保留项目。例如，如果您的组织需要将所有邮件至少保留七年，可使用此选项。可使用“基于时间”的就地保留以及保持政策，确保在七年后删除项目。有关保留策略的详细信息，请参阅[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)。

**使用命令行管理程序创建的就地保留**

下例将创建一个名为 Hold-CaseId012 的就地保留并将邮箱 joe@contoso.com 添加到其中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>如果没有指定就地保留的其他搜索参数，指定源邮箱中的所有项目会放于保留中。如果未指定 <em>ItemHoldPeriod</em> 参数，项目将无限期保留或保留到邮箱从保留中删除或保留被删除。</td>
</tr>
</tbody>
</table>


    New-MailboxSearch "Hold-CaseId012"-SourceMailboxes "joe@contoso.com" -InPlaceHoldEnabled $true

有关语法和参数的详细信息，请参阅 [New-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd298064\(v=exchg.150\))。

**您如何知道这有效？**

要检查是否成功创建了就地保留，可进行以下操作之一：

  - 使用 EAC 验证就地保留是否位于“就地电子数据展示与保留”选项卡的列表视图中。

  - 使用 **Get-MailboxSearch** cmdlet 检索邮箱搜索并检查搜索参数。有关如何检索邮箱搜索的示例，请参阅 [Get-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351021\(v=exchg.150\)) 中的示例。

返回顶部

## 删除就地保留

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，邮箱搜索用于就地保留和就地电子数据展示。您无法删除用于就地保留的邮箱搜索。必须先禁用就地保留，操作方法为清除“就地保留设置”页面的“将与所选邮箱中的搜索查询匹配的内容置于保留状态”复选框或者在命令行管理程序中将 <em>InPlaceHoldEnabled</em> 参数设置为 <code>$false</code>。也可以使用搜索中指定的 <em>SourceMailboxes</em> 参数删除邮箱。</td>
</tr>
</tbody>
</table>


**使用 EAC 删除就地保留**

1.  导航到“合规性管理”\>“就地电子数据展示与保留”。

2.  在此列表视图中，选择您要删除的就地保留，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“就地电子数据展示与保留”属性中的“就地保留”页面上，清除“将与所选邮箱中的搜索查询匹配的内容置于保留状态”复选框，然后单击“保存”。

4.  再次从此列表视图中选择就地保留，然后单击“删除”![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")。

5.  在警告对话框中，单击“是”删除搜索。

**使用命令行管理程序删除就地保留**

下例首先禁用名为 Hold-CaseId012 的就地保留，然后删除邮箱搜索。

    Set-MailboxSearch "Hold-CaseId012"  -InPlaceHoldEnabled $false
    Remove-MailboxSearch "Hold-CaseId012"

有关语法和参数的详细信息，请参阅 [Set-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd335145\(v=exchg.150\))。

**您如何知道这有效？**

要验证是否成功删除了就地保留，请执行以下操作之一：

  - 使用 EAC 验证就地保留未出现在“就地电子数据展示与保留”选项卡的列表视图中。

  - 使用 **Get-MailboxSearch** cmdlet 检索所有邮箱搜索并检查已删除的搜索是否不再列出。有关如何检索邮箱搜索的示例，请参阅 [Get-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351021\(v=exchg.150\)) 中的示例。

返回顶部

