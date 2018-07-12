---
title: '删除公用文件夹: Exchange 2013 Help'
TOCTitle: 删除公用文件夹
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 50490169
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除公用文件夹

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-11-16_

你可能需要删除组织中不再使用的公用文件夹。若要了解如何确定应删除哪些公用文件夹，请参阅[查看公用文件夹和公用文件夹项目的统计信息](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md)。

有关管理公用文件夹相关的更多管理任务，请参阅[公用文件夹程序](public-folder-procedures-exchange-2013-help.md)。

有关与公用文件夹相关的其他管理任务，请参阅[Office 365 和 Exchange Online 中的公用文件夹程序](https://technet.microsoft.com/zh-cn/library/jj966272\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[共享和协作权限](sharing-and-collaboration-permissions-exchange-2013-help.md)主题中的“公用文件夹”条目。

  - 无法删除启用邮件的公用文件夹。必须先针对相应公用文件夹禁用电子邮件，然后才能删除它。有关详情，请参阅[对公用文件夹启用或禁用邮件](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用 EAC 删除公用文件夹

1.  导航到“公用文件夹”\>“公用文件夹”。

2.  在列表视图中，选择要删除的公用文件夹。请注意，单击文件夹名称即可显示相应文件夹内的子文件夹（若有）。此时，可以单击选择要删除的特定子文件夹。
    
    若要删除文件夹或子文件夹，请依次单击文件夹所在行上的任意位置（带下划线的文件夹名称除外）和“**删除**![删除图标](images/JJ657511.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "删除图标")”。如果单击带下划线的文件夹名称，则无法选择“**删除**”选项。
    
    ![选择要删除的公用文件夹](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "选择要删除的公用文件夹")  

3.  系统会显示警告框，询问你是否确定要删除相应公用文件夹。单击“**是**”即可继续。

## 使用命令行管理程序删除公用文件夹

此示例删除了公用文件夹 Help Desk\\Resolved。此命令假定 Resolved 公用文件夹不含任何子文件夹。

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

此示例测试上一个命令（未做任何修改）。

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

此示例将删除公用文件夹 Marketing 及其全部子文件夹（因为该命令以递归方式运行）。

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

有关语法和参数的详细信息，请参阅 [Remove-PublicFolder](https://technet.microsoft.com/zh-cn/library/bb124894\(v=exchg.150\))。

