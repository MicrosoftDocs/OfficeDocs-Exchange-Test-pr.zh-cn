---
title: '安装服务器角色时发生安装失败_InstallWatermark: Exchange 2013 Help'
TOCTitle: 安装服务器角色时发生安装失败_InstallWatermark
ms:assetid: ad89ebd5-f9bb-40c1-8811-09b145c2b341
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.installwatermark(v=EXCHG.150)
ms:contentKeyID: 50491295
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安装服务器角色时发生安装失败\_InstallWatermark

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为在安装服务器角色时曾发生安装失败，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求先成功地重新安装之前安装失败的服务器角色或者将其从安装进程中删除，才能继续执行任何其他安装任务。

若要解决此问题，要么重新安装失败的服务器角色，要么删除该服务器角色。

**从命令行重新安装失败的服务器角色**

1.  打开命令提示符窗口，然后导航到安装文件。

2.  运行以下命令：
    
        Setup /roles:<Failed Server Role>
    
    在逗号分隔的列表中选择下列一个或多个角色：
    
    ClientAccess（或 CA，或 C）
    
    EdgeTransport（或 ET，或 E）
    
    > [!NOTE]  
    > 边缘传输服务器角色无法在同一台计算机上与任何其他服务器角色共存。
    
    > [!NOTE]  
    > 必须在外围网络中和 Active Directory 林外部部署边缘传输服务器角色。
    
    HubTransport（或 HT，或 H）
    
    Mailbox（或 MB，或 M）
    
    UnifiedMessaging（或 UM，或 U）
    
    ManagementTools（或 MT，或 T）
    
    > [!NOTE]  
    > 如果指定 ManagementTools，则将安装 Exchange 管理控制台、Exchange 命令行管理程序的 Exchange cmdlet、Exchange 帮助文件、Exchange 最佳实践分析工具和 Exchange 疑难解答助理。如果安装任何其他服务器角色，将自动安装管理工具。
    
    例如，要将集线器传输服务器角色添加到现有的邮箱服务器上，请键入以下内容：** %LocalExchangeInstallationDir%\\bin\\Setup.com /role:HubTransport /Mode:Install**

> [!NOTE]  
> 如果之前曾成功安装了任何 Exchange Server 2007 服务器角色，则安装向导将以维护模式运行。如果之前未成功安装任何 Exchange 2007 服务器角色，则安装向导将从它所停止的位置开始。


**以维护模式使用 Exchange Server 2007 安装向导来重新安装失败的服务器角色**

1.  登录到要为其重新安装服务器角色的服务器。

2.  打开“控制面板”，然后双击“添加或删除程序”。

3.  在“更改或删除程序”页上，选择“Microsoft Exchange Server”，再单击“更改”。

4.  在 Exchange Server 2007 安装向导中的“Exchange 维护模式”页上，单击“下一步”。

5.  在“服务器角色选择”页上，选中要安装的服务器角色的复选框，再单击“下一步”。
    
    > [!NOTE]  
    > 边缘传输服务器角色无法在同一台计算机上与任何其他服务器角色共存。
    
    > [!NOTE]  
    > 必须在外围网络中和 Active Directory 林外部部署边缘传输服务器角色。
    
    > [!NOTE]  
    > 如果选择管理工具，将安装 Exchange 管理控制台、用于 Exchange 命令行管理程序的 Exchange cmdlet、以及 Exchange 帮助文件。如果安装任何其他服务器角色，将自动安装管理工具。


6.  如果选择“集线器传输角色”，并且是在包含现有 Exchange Server 2003 或 Exchange 2000 Server 组织的林中安装 Exchange 2007，那么，请在“邮件流设置”页上，在现有组织中选择属于 Exchange 2003 或 Exchange 2000 路由组成员的桥头服务器，以在其中创建路由组连接器。

7.  在“**准备情况检查**”页上，查看状态以确定是否成功完成了组织和服务器角色先决条件检查。如果已成功完成检查，请单击“**安装**”以安装 Exchange 2007。

8.  在“完成”页上，单击“完成”。

**在之前未成功安装任何其他服务器角色的情况下使用 Exchange Server 2007 安装向导重新安装失败的服务器角色**

1.  按照 Exchange Server 2007 产品文档中“如何使用 Exchange Server 2007 安装程序执行自定义安装”([https://go.microsoft.com/fwlink/?LinkId=86648](https://go.microsoft.com/fwlink/?linkid=86648)) 的指导操作。

**删除失败的服务器角色**

1.  按照 Exchange Server 2007 产品文档中“如何删除 Exchange 2007 服务器角色”([https://go.microsoft.com/fwlink/?LinkId=86649](https://go.microsoft.com/fwlink/?linkid=86649)) 的指导操作。

## 详细信息

有关如何以无人值守模式安装 Exchange 2007 的详细信息，请参阅“如何以无人值守模式安装 Exchange 2007”([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))。

