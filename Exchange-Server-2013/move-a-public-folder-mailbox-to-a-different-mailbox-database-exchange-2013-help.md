---
title: '将公用文件夹邮箱移动至不同的邮箱数据库中: Exchange 2013 Help'
TOCTitle: 将公用文件夹邮箱移动至不同的邮箱数据库中
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51408236
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将公用文件夹邮箱移动至不同的邮箱数据库中

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2015-07-21_

为了实现负载平衡或使资源更靠近地理位置，您可能需要将公用文件夹邮箱移动至不同的邮箱数据库中。与移动常规邮箱类似，您可以使用 **MoveRequest** cmdlet 来移动公用文件夹邮箱。有关移动邮箱的详细信息，请参阅 [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间取决于公用文件夹邮箱的大小。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[收件人权限](recipients-permissions-exchange-2013-help.md)主题中的“邮箱移动和迁移权限”部分。

  - 您无法在 EAC 中执行此过程。您只能在命令行管理程序中执行此过程。

  - 根据公用文件夹邮箱的大小，可能需要几个小时才能完成该移动过程。在移动过程中，用户将无法访问公用文件夹。当文件夹处于“完成正在进行中”状态时，用户短时间内也无法访问公用文件夹。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 创建移动请求

**New-MoveRequest** cmdlet 将公用文件夹邮箱排入 Microsoft Exchange 邮箱复制服务队列中。当 Microsoft Exchange 邮箱复制服务可用时，它会拣选该移动请求，然后开始移动该公用文件夹邮箱。它会从头至尾完成整个请求。

此示例开始执行移动请求，将公用文件夹邮箱 PF\_SanFrancisco 移动至邮箱数据库 MBX\_DB01。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

有关语法和参数的详细信息，请参阅 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

## 创建一个稍后完成的移动请求。

在移动请求的最后阶段，即 `CompletionInProgress` 状态时，该公用文件夹邮箱会将用户锁定。如果需要，您可以在到达该阶段之前暂停该移动请求，然后在用户不受影响时恢复请求。

此示例开始执行移动请求，将公用文件夹邮箱 PF\_SanFrancisco 移动至邮箱数据库 MBX\_DB01，然后在即将完成时暂停该移动请求。

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

有关语法和参数的详细信息，请参阅 [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))。

此示例检索公用文件夹邮箱 PF\_SanFrancisco 正在进行的邮箱移动的状态。

    Get-MoveRequest -Identity "PF_SanFrancisco"

有关语法和参数的详细信息，请参阅 [Get-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd335227\(v=exchg.150\))。

当该移动请求达到暂停状态时，您可以恢复该请求。此示例恢复了公用文件夹邮箱 PF\_SanFrancisco 的移动请求。

    Resume-MoveRequest -Identity "PF_SanFrancisco"

有关语法和参数的详细信息，请参阅 [Resume-MoveRequest](https://technet.microsoft.com/zh-cn/library/ee332320\(v=exchg.150\))。

## 您如何知道操作成功？

若要验证是否成功创建了移动请求，请运行以下命令：

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

`Completed` 状态表示该移动请求已成功完成。

如果移动不成功，您可能需要恢复该公用文件夹。有关详细信息，请参阅[恢复失败的移动公用文件夹和公用文件夹的邮箱](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md)。

