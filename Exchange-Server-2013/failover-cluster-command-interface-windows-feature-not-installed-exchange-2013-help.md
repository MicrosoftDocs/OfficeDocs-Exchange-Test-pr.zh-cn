---
title: '故障转移群集命令界面 Windows 功能未安装: Exchange 2013 Help'
TOCTitle: 故障转移群集命令界面 Windows 功能未安装
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51408194
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 故障转移群集命令界面 Windows 功能未安装

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2014-12-03_

Microsoft Exchange Server 2013 安装程序无法继续，因为本地计算机上缺少所需的 Windows 功能。您将需要安装此 Windows 功能，然后 Exchange 2013 才能继续运行。

Exchange 2013 安装程序要求首先在计算机上安装“故障转移群集命令界面”Windows 功能，然后才能继续安装。

执行下列操作以在此计算机上安装 Windows 功能。如果此项更新要求重新启动以完成安装，则需要退出 Exchange 2013 安装程序，重新启动，然后再启动安装程序。

> [!NOTE]  
> 可能需要安装其他 Windows 功能或更新，Exchange 2013 安装程序才能继续运行。有关所需的 Windows 功能和更新的完整列表，请查看 <a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 先决条件</a>。


1.  在本地计算机上打开 Windows PowerShell。

2.  运行以下命令，安装必需的 Windows 功能。
    
    ```powershell
    Install-WindowsFeature RSAT-Clustering-CmdInterface
    ```

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

