---
title: '将公用文件夹移动到不同的公用文件夹的邮箱: Exchange 2013 Help'
TOCTitle: 将公用文件夹移动到不同的公用文件夹的邮箱
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51408268
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 将公用文件夹移动到不同的公用文件夹的邮箱

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-11-16_

如果公用文件夹邮箱的内容开始超过邮箱配额，您可能需要将公用文件夹移动到不同的公用文件夹的邮箱。有几种方法来执行此操作。若要移动一个或多个不包含子文件夹的公用文件夹，您可以使用**PublicFolderMoveRequest** cmdlet。如果您需要移动整个公用文件夹分支 （其中包括父公用文件夹和所有子文件夹），可以使用`Move-PublicFolderBranch.ps1`脚本，当您安装 Exchange 2013 时才可用。

有关与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间取决于公用文件夹的大小。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的\&quot;公用文件夹\&quot;条目。

  - 您不能使用 EAC 要执行这些过程。您必须使用外壳程序。

  - 如果正在移动的文件夹包含子文件夹，这些子文件夹将不会移动，默认情况。如果您想要移动公用文件夹和所有子文件夹，请使用**Move-PublicFolderBranch.ps1**脚本。

  - 移动公用文件夹只会移动公用文件夹的物理内容，不会改变逻辑层次结构。

  - 根据公用文件夹和其包含的内容量的大小，移动可能需要几小时才能完成。在此期间，用户将无法访问公用文件夹。但是，用户不能在短时间内访问的公用文件夹，而该文件夹是在"完成正在进行中"状态。

  - 您可以一次执行一个公用文件夹移动请求。您必须使用**Remove-PublicFolderMoveRequest** cmdlet 完成后删除该请求。

  - 若要检查正在进行的公用文件夹移动请求的状态，请运行 [Get-PublicFolderMoveRequest](https://technet.microsoft.com/zh-cn/library/jj878076\(v=exchg.150\)) cmdlet。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 移动单个公用文件夹

此示例开始进行将公用文件夹 \\CustomerEnagagements 从公用文件夹邮箱 DeveloperReports 移动到 DeveloperReports01 的移动请求

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01

> [!NOTE]
> 移动请求处于活动状态时，将锁定目标公用文件夹的邮箱。


有关语法和参数的详细信息，请参阅 [New-PublicFolderMoveRequest](https://technet.microsoft.com/zh-cn/library/jj878081\(v=exchg.150\))。

## 移动多个公用文件夹

本示例开始移动请求到目标公用文件夹邮箱 DeveloperReports01 \\Dev 公用文件夹分支下的公用文件夹。此示例不会移动公用文件夹 \\Dev。

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01

> [!NOTE]
> 移动请求处于活动状态时，将锁定目标公用文件夹的邮箱。


有关语法和参数的详细信息，请参阅 [New-PublicFolderMoveRequest](https://technet.microsoft.com/zh-cn/library/jj878081\(v=exchg.150\))。

## 移动一个公用文件夹分支

此示例使用`Move-PublicFolderBranch.ps1`脚本移动公用文件夹的一个分支。这将启动移动请求公用文件夹 \\Dev 和其所有子文件夹为公用文件夹邮箱 DeveloperReports01。该脚本位于脚本文件夹中，必须从该位置运行。

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## 您如何知道操作成功？

若要验证是否成功创建了公用文件夹移动请求，可以运行以下命令：

    Get-PublicFolderMoveRequest | Format-List Status

`Completed` 状态表示该移动请求已成功完成。

如果移动请求未成功时，您可能需要还原公用文件夹或其内容。有关详细信息，请参阅[恢复失败的移动公用文件夹和公用文件夹的邮箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

