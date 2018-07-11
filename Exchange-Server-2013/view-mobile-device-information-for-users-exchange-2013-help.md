---
title: '查看用户移动设备信息: Exchange 2013 Help'
TOCTitle: 查看用户移动设备信息
ms:assetid: 4fd263c0-ad61-416c-bd68-339bf66605cf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997974(v=EXCHG.150)
ms:contentKeyID: 50490532
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 查看用户移动设备信息

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-29_

用户可以将多个移动设备配置为与 Microsoft Exchange Server 2013 同步。可以使用 EAC 或命令行管理程序查看与特定用户关联的移动设备的列表。

有关与移动设备相关的更多管理任务，请参阅 [Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“移动设备邮箱策略”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 EAC 查看用户的移动设备信息

EAC 显示当前与用户邮箱同步的移动设备列表。您可以按产品系列、型号、电话号码或状态查看移动设备。

1.  在 EAC 中，单击“收件人”\>“邮箱”，然后选择一个邮箱。

2.  在“详细信息”窗格中，滚动到“电话和语音功能”，然后单击“查看详请”，将显示“移动设备详情”屏幕。

## 使用命令行管理程序查看用户的移动设备信息

您可以使用 Get-MobileDevice cmdlet 查看特定用户的移动设备列表。

1.  运行以下命令。
    
        Get-MobileDevice -Mailbox useralias

