---
title: '从队列导出邮件: Exchange 2013 Help'
TOCTitle: 从队列导出邮件
ms:assetid: 688b342c-f380-4fe0-afce-7e38cf490627
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998625(v=EXCHG.150)
ms:contentKeyID: 51408231
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 从队列导出邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-05-05_

将邮件从队列中导出到文件时，不会从队列中删除该邮件。将在指定位置创建一份纯文本文件形式的邮件副本。可以在诸如文本编辑器或电子邮件客户端应用程序之类的应用程序中查看结果文件，也可以通过使用 Exchange 组织内外的任何其他邮箱服务器或边缘传输服务器上的重播目录重新提交邮件文件。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;队列\&quot;条目。

  - 要使导出过程成功，邮件必须处于已挂起状态。您可以将邮件从传递队列、无法到达队列或带毒邮件队列中导出。带毒邮件队列中的邮件已处于挂起状态。不能挂起或导出提交队列中的邮件。

  - 不能使用 Exchange Toolbox 中的队列查看器导出邮件。但在使用命令行管理程序导出邮件之前，可以使用队列查看器查找、标识和挂起邮件。

  - 验证与邮件文件目标目录位置有关的下列信息：
    
      - 导出任何邮件之前，目标目录必须存在。系统不创建该目录。如果未指定绝对路径，则使用当前的 Exchange 命令行管理程序工作目录。
    
      - 该路径可以是 Exchange 服务器上的本地路径，也可以是指向远程服务器上共享位置的通用命名约定 (UNC) 路径。
    
      - 帐户必须拥有对目标目录的**写入**权限。
    
      - 指定导出邮件的文件名时，请确保其中包含 .eml 文件扩展名，以便可以通过电子邮件客户端应用程序轻松地打开文件，或通过重播目录正确地处理文件。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序从特定队列中导出特定邮件

若要从特定队列中导出特定邮件，请运行下列命令：

    Export-Message -Identity <MessageIdentity> | AssembleMessage -Path <FilePath>\<FileName>.eml

本示例将位于服务器 Mailbox01 上 contoso.com 传递队列中的 **InternalMessageID** 值为 1234 的邮件副本导出至路径 D:\\Contoso Export 中的 export.eml 文件中。

    Export-Message -Identity Exchange01\Contoso.com\1234 | AssembleMessage -Path "D:\Contoso Export\export.eml"

## 使用命令行管理程序从特定队列中导出所有邮件

若要从特定队列导出所有邮件，并将各邮件的 **InternetMessageID** 值用作文件名，可以使用下列语法。

    Get-Message -Queue <QueueIdentity> | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

注意，**InternetMessageID** 值包含尖括号（\> 和 \<），由于文件名中不允许出现这些尖括号，所以需要删除它们。

此示例将所有邮件的副本从服务器 Mailbox01 上的 contoso.com 传递队列导出至 D:\\Contoso Export 的本地目录中。

    Get-Message -Queue Mailbox01\Contoso.com | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

## 使用命令行管理程序从服务器上的所有队列中导出某些特定邮件

若要从一个服务器上的所有队列中导出特定邮件，并将各邮件的 **InternetMessageID** 值用作文件名，可以使用下列语法。

    Get-Message -Filter {<MessageFilter>} [-Server <ServerIdentity>] | ForEach-Object {$Temp=<Path>+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

注意，**InternetMessageID** 值包含尖括号（\> 和 \<），由于文件名中不允许出现这些尖括号，所以需要删除它们。

此示例将所有来自 contoso.com 域中发件人的邮件副本从服务器 Mailbox01 上所有队列导出至 D:\\Contoso Export 的本地目录中。

    Get-Message -Filter {FromAddress -like "*@contoso.com"} -Server Mailbox01 | ForEach-Object {$Temp="D:\Contoso Export\"+$_.InternetMessageID+".eml";$Temp=$Temp.Replace("<","_");$Temp=$Temp.Replace(">","_");Export-Message $_.Identity | AssembleMessage -Path $Temp}

> [!NOTE]  
> 如果省略 <em>Server</em> 参数，此命令会在本地服务器上运行。

