---
title: '修改存档策略: Exchange 2013 Help'
TOCTitle: 修改存档策略
ms:assetid: 1e3002c2-801a-43ea-ae00-52ab34d76b9c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529919(v=EXCHG.150)
ms:contentKeyID: 50490026
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 修改存档策略

 

_**适用于：**Exchange Online, Exchange Server 2013_

_**上一次修改主题：**2016-02-01_

在 Exchange Server 2013 和 Exchange Online 中，可以使用存档策略自动将邮箱项目移动到个人（内部部署）或基于云的存档。存档策略是使用“移动到存档”保留操作的保留标记。

Exchange 安装程序会创建一个称为“默认 MRM 策略”的保留策略。此策略分配有一个默认策略标记 (DPT)，该标记在两年之后将项目移动到存档邮箱。此策略还包括一些个人标记，用户可以将这些标记应用于文件夹或邮箱项目以自动移动或删除邮件。如果某个邮箱在启用存档时未分配保留策略，则 Exchange 会自动将“默认 MRM 策略”应用于该邮箱。还可以创建自己的存档和保留策略并将其应用于邮箱用户。若要了解详细信息，请参阅[保留标记和保留策略](retention-tags-and-retention-policies-exchange-2013-help.md)。

可以修改默认策略中包括的保留标记以满足业务要求。例如，可以修改存档 DPT 以在三年（而不是两年）之后将项目移动到存档。还可以创建其他个人标记并将其添加到保留策略（包括“默认 MRM 策略”）或允许用户从 Outlook Web App 选项将个人标记添加到其邮箱。

有关与存档相关的其他管理任务，请参阅：

  - **Exchange Server 2013:** [在 Exchange 2013 中管理就地存档](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md)

  - **Exchange Online:** [在 Exchange Online 中启用或禁用存档邮箱](https://technet.microsoft.com/zh-cn/library/jj984357\(v=exchg.150\))

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 混合部署中，您可以为内部部署主邮箱启用基于云的存储邮箱。如果向内部部署邮箱分配存档策略，项目将移动到基于云的存档。如果将某个项目移动到存档邮箱，不会在内部部署邮箱中保留它的副本。如果将内部部署邮箱置于保留状态，存档策略仍会将项目移动到基于云的存档邮箱，项目将在其中保存保留指定的时间。</td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮件传递记录管理”条目。

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

## 使用 EAC 修改默认存档策略

1.  导航到“合规性管理”\>“保留标记”。

2.  在此列表视图中，选择标记“默认移动到存档 2 年”，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>可以单击“类型”列按类型对保留标记进行排序。默认存档策略显示为类型“默认”并且具有“存档”保留操作。或者，可以单击“名称”按名称对保留标记进行排序。</td>
    </tr>
    </tbody>
    </table>


3.  
    
    在“保留标记”中，查看或修改以下设置，然后单击“保存”：
    
      - **名称** 此框位于页面顶部，可用于查看或更改标记名称。
    
      - **保留标记类型**   这是一个只读字段，显示标记类型。
    
      - **保留操作**   不要修改此字段中的存档策略。
    
      - **保留期** 选择下列选项之一：
        
          - **从不**   单击此按钮可禁用标记。如果 DPT 已禁用，则该标记不再应用于邮箱。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>邮箱助理将不再处理应用了已禁用的保留标记的项目。如果要阻止将某个标记应用于项目，我们建议您禁用此标记，而不是将其删除。删除某个标记时，该标记配置也会从 Active Directory 中删除，且邮箱助理会处理所有邮件以删除该标记。</td>
            </tr>
            </tbody>
            </table>
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>如果用户将某个标记应用于项目，并认为此项目永不会移动，日后启用此标记可能会移动用户原本要保留在主邮箱中的项目。</td>
            </tr>
            </tbody>
            </table>
        
          - **项目达到以下期限(天)时**   单击此按钮可指定项目在特定期限之后移动到存档。默认情况下，此设置配置为在两年（730 天）之后将项目移动到存档。若要修改此设置，请在相应文本框中，键入保留期的天数。值的范围是 1 到 24,855 天。
    
      - **注释**   使用此框可键入要向 Outlook 和 Outlook Web App 用户显示的注释。

## 使用命令行管理程序修改存档策略

本示例修改`Default 2 year move to archive`标记以在 1,095 天（3 年）之后移动项目。

    Set-RetentionPolicyTag "Default 2 year move to archive" -Name "Default 3 year move to archive" -AgeLimitForRetention 1095

本示例禁用`Default 2 year move to archive`标记。

    Set-RetentionPolicyTag "Default 2 year move to archive" -RetentionEnabled $false

本示例检索所有存档 DPT 和个人标记并禁用它们。

    Get-RetentionPolicyTag | ? {$_.RetentionAction -eq "MoveToArchive"} | Set-RetentionPolicyTag -RetentionEnabled $false

有关语法和参数的详细信息，请参阅 [Set-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298042\(v=exchg.150\)) 和 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298009\(v=exchg.150\))。

## 您如何知道这有效？

使用 [Get-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298009\(v=exchg.150\)) cmdlet 检索保留标记的设置。

此命令检索 `Default 2 year move to archive` 保留标记的属性，并通过管道将输出传递给 **Format-List** cmdlet，以列表格式显示所有属性。

    Get-RetentionPolicyTag "Default 2 year move to archive" | Format-List

