---
title: '修改就地电子数据展示搜索: Exchange Online Help'
TOCTitle: 修改就地电子数据展示搜索
ms:assetid: 3162743c-cc12-4997-91e0-bcbfea8bcb17
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335182(v=EXCHG.150)
ms:contentKeyID: 50490274
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 修改就地电子数据展示搜索

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-08-27_

创建就地电子数据展示搜索之后，您可以对其进行修改，以更改搜索参数。例如，您可以更改要搜索的邮箱、日期范围、关键字、日志记录选项，也可以指定不同的发现邮箱来存储搜索结果。重新启动搜索时，将使用您对搜索属性所做的所有更改。

> [!CAUTION]  
> 如果就地电子数据展示搜索正在运行，您必须先停止搜索，然后才能对其进行修改。重新启动搜索时，上次运行搜索得到的结果将从发现邮箱中删除。不过，以前运行的搜索的日志将会得到保存。


## 在开始之前，您需要知道什么？

  - 估计完成时间：2-5 分钟。

  - 就地电子数据展示搜索已创建，但未在运行。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;就地电子数据展示\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 修改就地电子数据展示搜索

1.  导航到\&quot;合规性管理\&quot;\>\&quot;就地电子数据展示与保留\&quot;。

2.  在列表视图中，选择要修改的就地电子数据展示搜索，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;就地电子数据展示与保留\&quot;中，可以修改下列设置：
    
      - 在\&quot;名称\&quot;页面上，修改搜索的名称和可选说明。
    
      - 在\&quot;邮箱\&quot;页面上，修改要搜索的邮箱。您可以跨所有邮箱搜索，或选择要搜索的特定邮箱。
        
        > [!IMPORTANT]  
        > 您无法使用&amp;quot;搜索所有邮箱&amp;quot;选项以将所有邮箱放在保留的 Exchange 2013 邮箱服务器上。要创建&amp;quot;就地保留&amp;quot;，您必须选择&amp;quot;指定要搜索的邮箱&amp;quot;。有关更多详细信息，请参阅<a href="create-or-remove-an-in-place-hold-exchange-2013-help.md">创建或删除就地保留</a>。
    
      - 在\&quot;搜索查询\&quot;页面上，修改下列字段：
        
          - \&quot;包含所有用户邮箱内容\&quot;   选择此选项以保留选定邮箱中的所有内容。
        
          - \&quot;基于条件筛选\&quot;   选择此选项以指定搜索条件，包括关键词、开始和结束日期、发件人和收件人地址以及邮件类型。
    
      - 在\&quot;就地保留\&quot;页面上，选中\&quot;将与所选邮箱中的搜索查询匹配的内容置于保留状态\&quot;复选框，然后选择下列选项之一将各项设为\&quot;就地保留\&quot;：
        
          - \&quot;无限期保留\&quot;   选择该选项以无限期保留返回的项目。保留的项目将会保持，直到您从搜索中删除邮箱或删除搜索。
        
          - \&quot;指定保留项目的天数（相对于收到日期）\&quot; 使用此选项以在指定周期内保留项目。例如，如果您的组织需要将所有邮件至少保留七年，可使用此选项。可使用\&quot;基于时间\&quot;的就地保留以及保持政策，确保在七年后删除项目。
            
            > [!IMPORTANT]  
            > 当出于法律目的&amp;quot;就地保留&amp;quot;邮箱或项目时，通常建议无限期保持项目，并在完成案件或调查后删除保留。


4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序修改就地电子数据展示搜索

本示例修改了就地电子数据展示搜索 Search-Project Contoso，以搜索属于 DG-ProjectManagers 通讯组成员的邮箱。

```powershell
Set-MailboxSearch -Identity "Search-Project Contoso" -SourceMailboxes "DG-ProjectManagers"
```

## 您如何知道这有效？

要验证您是否已成功修改了就地电子数据展示搜索，请执行下列操作：

  - 使用 EAC 检查搜索的属性。

  - 使用命令行管理程序的 **Get-MailboxSearch** cmdlet 检查搜索的属性。关于如何检查邮箱搜索的属性的示例，请参阅位于 [Get-MailboxSearch](https://technet.microsoft.com/zh-cn/library/dd351021\(v=exchg.150\)) 的\&quot;示例\&quot;部分。

> [!NOTE]  
> 如果使用 Exchange Online 中的 <strong>Get-MailboxSearch</strong> 检索有关电子数据展示搜索的信息，您必须指定搜索名称，以返回搜索属性的完整列表，例如，<code>Get-MailboxSearch &quot;Contoso Legal Case&quot;</code>。如果您在不使用任何参数的情况下运行 <strong>Get-MailboxSearch</strong> cmdlet，则不会返回以下属性：
> <ul>
> <li><p>SourceMailboxes</p></li>
> <li><p>Sources</p></li>
> <li><p>SearchQuery</p></li>
> <li><p>ResultsLink</p></li>
> <li><p>PreviewResultsLink</p></li>
> <li><p>Errors</p></li>
> </ul>
> 原因是需要通过很多资源为组织中的所有电子数据展示搜索返回这些属性。

