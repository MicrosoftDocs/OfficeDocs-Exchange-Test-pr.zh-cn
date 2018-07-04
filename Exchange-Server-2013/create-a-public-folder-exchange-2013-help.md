---
title: '创建公用文件夹: Exchange Online Help'
TOCTitle: 创建公用文件夹
ms:assetid: 6d252e60-c8d0-4efd-b9d7-ba5284a6f8ab
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb691104(v=EXCHG.150)
ms:contentKeyID: 50490886
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.PublicFolders.NewPublicFolderWizardForm.NewPublicFolderWizardPage
ms.translationtype: MT
---

# 创建公用文件夹

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-02-24_

公用文件夹专为共享访问设计，为收集、组织信息及与您的工作组或组织中的其他人共享信息提供了一种轻松、有效的方式。

默认情况下，公用文件夹继承其父文件夹的设置，包括权限设置。

> [!NOTE]
> 有关存储配额和公用文件夹的限制的详细信息，请参阅以下主题：
> <ul>
> <li><p>若要了解 Office 365 中的公用文件夹，请参阅 <a href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 限制</a>。</p></li>
> <li><p>有关本地 Exchange Server 2013 中的公用文件夹的信息，请参阅<a href="limits-for-public-folders-exchange-2013-help.md">公用文件夹的限制</a>。</p></li>
> </ul>


有关管理公用文件夹相关的更多管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的\&quot;公用文件夹\&quot;条目。

  - 除非您已首先创建了公用文件夹邮箱，否则无法创建公用文件夹。有关如何创建公用文件夹邮箱的详细信息，请参阅[创建公用文件夹邮箱](create-a-public-folder-mailbox-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

## 您想执行什么操作？

## 使用 EAC 创建公用文件夹

使用 EAC 创建公用文件夹时，您只能设置公用文件夹的名称和路径。若要配置其他设置，需要在创建公用文件夹后进行编辑。

1.  导航至\&quot;公用文件夹\&quot;\>\&quot;公用文件夹\&quot;。

2.  如果要创建此公用文件夹作为现有公用文件夹的子级，请在列表视图中单击现有公用文件夹。如果要创建顶级公用文件夹，请跳过此步骤。

3.  单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

4.  在\&quot;公用文件夹\&quot;中，键入公用文件夹的名称。
    
    > [!important]
    > 在创建公用文件夹时，不要在名称内使用反斜线 (\)。


5.  在\&quot;路径\&quot;框中，验证公用文件夹的路径。如果不是所需路径，请单击\&quot;取消\&quot;并按照此过程的步骤 2 操作。

6.  单击\&quot;保存\&quot;。

## 使用命令行管理程序创建公用文件夹

本示例在路径 Marketing\\2013 中创建一个名为 Reports 的公用文件夹。

    New-PublicFolder -Name Reports -Path \Marketing\2013

> [!important]
> 在创建公用文件夹时，不要在名称内使用反斜线 (\)。


有关语法和参数的详细信息，请参阅 [New-PublicFolder](https://technet.microsoft.com/zh-cn/library/aa996405\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功创建了公用文件夹，请执行以下操作：

  - 在 EAC 中，单击\&quot;刷新\&quot;以刷新公用文件夹的列表。新的公用文件夹应该会显示在该列表中。

  - 在命令行管理程序中，运行以下任何命令：
    
        Get-PublicFolder -Identity \Marketing\2013\Reports | Format-List
    
        Get-PublicFolder -Identity \Marketing\2013 -GetChildren
    
        Get-PublicFolder -Recurse

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。

