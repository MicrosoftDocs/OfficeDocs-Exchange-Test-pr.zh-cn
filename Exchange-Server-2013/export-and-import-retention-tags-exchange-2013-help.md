---
title: '导出和导入保留标记: Exchange Online Help'
TOCTitle: 导出和导入保留标记
ms:assetid: 18405ea2-7ccc-475e-bd84-8b040e17bf44
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ907307(v=EXCHG.150)
ms:contentKeyID: 51408199
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 导出和导入保留标记

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2017-11-15_

有几个可能要导出或导入保留标记的方案，包括：

  - 跨多目录林Exchange组织中的所有服务器应用相同的保留策略

  - 在某些邮箱驻留在内部部署 Exchange 组织中而某些邮箱驻留在 Exchange Online 中的混合部署中应用相同保留策略。

  - 应用保留策略，在Exchange存档方案中，其中内部Exchange 2010或更高版本的邮箱与用户具有的基于云的存档。

在这些方案中，托管文件夹助理可以在项目或邮箱移动到其他组织之后，正确处理应用了保留标记的项目。

> [!CAUTION]  
> 若要使保留标记和保留策略在两个组织之间保持同步，每次在源组织中更改保留标记或策略时，必须执行此过程以从源组织导出保留标记和策略并将其导入目标组织。
> 您不能选择特定的保留标记或要导出的策略。导出 RetentionTags.ps1 脚本从组织导出所有保留标记和策略。


有关与邮件记录管理相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

  - 本主题中的过程取决于在Exchange服务器上的`%ExchangeInstallPath%Scripts`文件夹中这三个文件：
    
      - Export-RetentionTags.ps1
    
      - Import-RetentionTags.ps1
    
      - MigrateRetentionTags.strings.psd1

  - 您不能选择特定的保留标记或导出或导入的策略。导出 RetentionTags.ps1 脚本从组织导出所有保留标记和策略。导入 RetentionTags.ps1 脚本中导入所有保留标记和策略的 XML 文件中导入，替换所有的现有保留标记和Exchange的组织中的策略。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 步骤 1： 从内部 Exchange 组织中导出保留标记

1.  运行此Exchange 命令行管理程序命令，将目录更改到**脚本**Exchange安装路径中的子目录。
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  运行 Export-RetentionTags.ps1 脚本可将保留标记导出到 XML 文件。
    
    > [!IMPORTANT]  
    > 如果要导入或导出到Exchange Online的保留标记和保留策略，您必须连接到Exchange Online的 Windows PowerShell 会话。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj984289(v=exchg.150)">使用远程 PowerShell 连接到 Exchange Online</a>。
    
        .\Export-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 您如何知道操作成功？

若要验证是否已成功导出保留标记和保留策略，执行以下操作：

1.  导航到在导出命令中指定的路径，并验证您指定名称的 XML 文件已创建。

2.  或者，也可以在文本编辑器中打开 XML 文件以查看其内容。

## 步骤 2： 将保留标记导入到 Exchange 组织

1.  运行此Exchange 命令行管理程序命令，将目录更改到**脚本**Exchange安装路径中的子目录。
    
        Cd $Env:ExchangeInstallPath\Scripts

2.  运行 Import-RetentionTags.ps1 脚本可从以前导出的 XML 文件导入保留标记。
    
    > [!IMPORTANT]  
    > 如果要导入或导出到Exchange Online的保留标记和保留策略，您必须连接到Exchange Online的 Windows PowerShell 会话。有关详细信息，请参阅<a href="https://technet.microsoft.com/zh-cn/library/jj984289(v=exchg.150)">使用远程 PowerShell 连接到 Exchange Online</a>。
    
    > [!NOTE]  
    > 针对Exchange Online运行此脚本时, 可能提示您确认您想要运行来自不受信任的发行者的软件。验证发布者的名称显示为<code>CN=Microsoft Corporation, OU=MOPR, O=Microsoft Corporation, L=Redmond, S=Washington, C=US</code>，然后单击<strong>R</strong>键允许脚本运行一次或<strong>一个</strong>始终运行。
    
        .\Import-RetentionTags.ps1 "c:\docs\ExportedRetentionTags.xml"

## 您如何知道操作成功？

若要验证是否已成功导入保留标记和保留策略，执行以下操作：

1.  在 EAC，导航到**法规遵从性管理**\>**保留标记**，并验证是否成功导出保留标记。导航到**法规遵从性管理**\>**保留策略**，并验证是否已成功导的保留策略。

2.  使用**Get-RetentionPolicy**和**Get-RetentionPolicyTag** cmdlet 来验证已创建的标记和策略。有关如何检索保留标记和保留策略的示例，请参阅[Get-RetentionPolicyTag](https://technet.microsoft.com/zh-cn/library/dd298009\(v=exchg.150\))和[Get-RetentionPolicy](https://technet.microsoft.com/zh-cn/library/dd298086\(v=exchg.150\))中的示例。

