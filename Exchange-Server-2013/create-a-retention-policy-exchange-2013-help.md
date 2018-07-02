---
title: '创建保留策略: Exchange 2013 Help'
TOCTitle: 创建保留策略
ms:assetid: d8806c98-fea5-492f-906d-f514e25361b2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150573(v=EXCHG.150)
ms:contentKeyID: 50491654
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建保留策略

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

在 Exchange Online 和 Exchange Server 2013 中，可以使用保留策略来管理电子邮件生命周期。通过创建保留标记，将它们添加至保留策略，并将策略应用至邮箱用户来应用保留策略。

下面的[视频](https://go.microsoft.com/fwlink/?linkid=825854)介绍如何创建保留策略并将其应用到 Exchange Online 中的邮箱。

有关与保留策略相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：30 分钟。

  - 本主题中的过程需要特定权限。请参阅每个过程，以了解其权限信息。

  - 向其应用保留策略的邮箱必须驻留于 Exchange Server 2010 或版本更高的服务器上。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您该如何做？

## 步骤 1：创建保留标记

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮件传递记录管理”条目。

**使用 EMC 创建保留标记**

1.  导航至“合规性管理”\>“保留标记”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")

2.  选择下列选项之一：
    
      - **已自动应用于整个邮箱(默认)**   选择此选项可创建默认策略标记 (DPT)。可以使用 DPT 创建默认删除策略和默认存档策略，这些策略适用于邮箱中的所有项目。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>不能使用 EAC 创建 DPT 以删除语音邮件项目。有关如何创建 DPT 以删除语音邮件项目的详细信息，请参见下面的命令行管理程序示例。</td>
        </tr>
        </tbody>
        </table>
    
      - **已自动应用于特定文件夹**   选择此选项可为默认的文件夹（如“收件箱”或“已删除的邮件”等）创建保留策略标记 (RPT)。
        
        <table>
        <thead>
        <tr class="header">
        <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
        </tr>
        </thead>
        <tbody>
        <tr class="odd">
        <td>您只能使用“删除并允许恢复”或“永久删除”操作创建 RPT。</td>
        </tr>
        </tbody>
        </table>
    
      - **已由用户应用于项目和文件夹(个人)**   选择此选项可创建个人标记。这些标记允许 Outlook 和 Outlook Web App 用户将不同于应用于父文件夹或整个邮箱的设置的存档或删除设置应用于邮件或文件夹。

3.  “**新建保留标记**”页标题和选项会因为选择的标记类型不同而有差异。填写以下字段：
    
      - **名称**   输入保留标记的名称。标记名称用于显示，对应用标记的文件夹或项目没有任何影响。请注意，为用户配置的个人标记在 Outlook 和 Outlook Web App 中可用。
    
      - **将此标记应用于以下默认文件夹**   此选项仅在选择了“已自动应用于特定文件夹”时可用。
    
      - **保留操作”**   从下面选择要在项目抵达保留期限后要执行的操作：
        
          - **删除但允许恢复**   选择该操作可删除项目，但是允许用户在 Outlook 或 Outlook Web App 中使用“**恢复已删除邮件**”选项恢复它们。在到达为邮箱数据库或邮箱用户配置的删除邮件的保留期限之前，将邮件保留。
        
          - **永久删除**   选择该选项从邮箱数据库永久删除项目。
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>将会保留遵从就地保留或诉讼保留的邮箱或项目并在就地电子数据展示搜索中返回。有关详细信息，请参阅<a href="in-place-hold-and-litigation-hold-exchange-2013-help.md">就地保留和诉讼保留</a>。</td>
            </tr>
            </tbody>
            </table>
        
          - **移动到存档**   该操作仅在创建 DPT 或个人标记时有用。选择此操作可将邮件移到用户的就地存档。
    
      - **保留期** 选择下列选项之一：
        
          - **从不**   选择此选项可指定应永远不删除邮件或将其移到存档。
        
          - **项目达到以下期限(天)时**   选择此选项并指定在移动或删除邮件之前的邮件保留天数。将自收到或创建项目的日期起计算除了日历和任务之外所有支持的项目的保留期限。对于日历和任务项目的保留期限将自结束日期起计算。
    
      - **注释**   使用此可选字段可输入管理性的说明或注释。该字段不向用户显示。

**使用命令行管理程序创建保留标记**

使用 **New-RetentionPolicyTag** cmdlet 可以创建保留标记。cmdlet 中可用的不同选项可让你创建不同类型的保留标记。使用 *Type* 参数创建 DPT (`All`)、RPT（指定默认文件夹类型，如 `Inbox`）或个人标记 (`Personal`)。

此示例创建一个 DPT，以便在 7 年（2,556 天）后删除邮箱中的所有邮件。

    New-RetentionPolicyTag -Name "DPT-Corp-Delete" -Type All -AgeLimitForRetention 2556 -RetentionAction DeleteAndAllowRecovery

此示例创建一个 DPT，以便在 2 年（730 天）后将所有邮件移到就地存档。

    New-RetentionPolicyTag -Name "DPT-Corp-Move" -Type All -AgeLimitForRetention 730 -RetentionAction MoveToArchive

此示例创建一个 DPT，以便在 20 天后删除语音邮件。

    New-RetentionPolicyTag -Name "DPT-Corp-Voicemail" -Type All -MessageClass Voicemail -AgeLimitForRetention 20 -RetentionAction DeleteAndAllowRecovery

此示例创建一个 RPT，以便在 30 天后删除“垃圾电子邮件”文件夹中的所有邮件。

    New-RetentionPolicyTag -Name "RPT-Corp-JunkMail" -Type JunkEmail -AgeLimitForRetention 30 -RetentionAction PermanentlyDelete

此示例创建一个个人标记，以便永远不删除邮件。

    New-RetentionPolicyTag -Name "Never Delete" -Type Personal -RetentionAction DeleteAndAllowRecovery -RetentionEnabled $false

## 步骤 2：创建保留策略

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的“邮件传递记录管理”条目。

**使用 EAC 创建保留策略**

1.  导航至“合规性管理”\>“保留策略”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")

2.  在“新建保留策略”中完成下列字段：
    
      - **名称**   输入保留策略的名称。
    
      - **保留标记**   单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可选择要添加至该保留策略的标记。
        
        保留策略可以包含以下标记：
        
          - 一个具有“移动到存档”操作的 DPT
        
          - 一个具有“删除但允许恢复”或“永久删除”操作的 DPT
        
          - 一个具有“删除但允许恢复”或“永久删除”操作的语音邮件的 DPT
        
          - 每个默认文件夹（例如“收件箱”）一个 RPT 以删除项目
        
          - 任意数量的个人标记
            
            <table>
            <thead>
            <tr class="header">
            <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
            </tr>
            </thead>
            <tbody>
            <tr class="odd">
            <td>尽管可以将任意数量的个人标记添加到保留策略，但是过多使用不同保留设置的个人标记可能会使用户混淆。建议链接到保留策略的个人标记不要超过 10 个。</td>
            </tr>
            </tbody>
            </table>
        
        可以创建保留策略但不向其添加任何保留标记，但不会移动或删除应用该策略的邮箱中的邮件。也可以在创建保留策略后在保留策略中添加和删除保留标记。

**使用命令行管理程序创建保留策略**

此示例创建了保留策略 RetentionPolicy-Corp，并使用 *RetentionPolicyTagLinks* 参数将五个标记与该策略关联。

    New-RetentionPolicy "RetentionPolicy-Corp"  -RetentionPolicyTagLinks "DPT-Corp-Delete","DPT-Corp-Move","DPT-Corp-Voicemail","RPT-Corp-JunkMail","Never Delete"

有关语法和参数的详细信息，请参阅 [New-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd297970\(v=exchg.150\))。

## 步骤 3：将保留策略应用于邮箱用户

在创建保留策略后，必须将其应用至邮箱用户。可以将不同的保留策略应用至不同的用户组。有关详细说明，请参阅[将保留策略应用于邮箱](apply-a-retention-policy-to-mailboxes-exchange-2013-help.md)。

## 您如何知道此任务有效？

在创建保留标记后，将它们添加至保留策略，并将策略应用至邮箱用户，下次 MRM 邮箱助手处理邮箱时，会根据您在保留标记中配置的设置移动或删除邮件。

要验证是否已应用保留策略，请执行以下操作：

1.  运行以下命令行管理程序命令以手动对单个邮箱运行 MRM 助手。
    
        Start-ManagedFolderAssistant -Identity <mailbox identity>

2.  使用 Outlook 或 Outlook Web App 登录邮箱，并验证是否已根据策略配置删除邮件或将其移动至存档。

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

