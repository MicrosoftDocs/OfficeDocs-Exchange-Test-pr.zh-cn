---
title: '架构主机未运行 Windows Server 2003 Service Pack 1 或更高版本'
TOCTitle: 架构主机未运行 Windows Server 2003 服务包 1 或更高版本_SchemaFSMONotWin2003SPn
ms:assetid: 644a85ca-7b36-4ed0-bd21-c64f2742df70
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.schemafsmonotwin2003spn(v=EXCHG.150)
ms:contentKeyID: 50490746
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 架构主机未运行 Windows Server 2003 服务包 1 或更高版本\_SchemaFSMONotWin2003SPn

 

_**适用于：** Exchange Server_

_**上一次修改主题：** 2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为分配有 Active Directory 目录服务架构主机角色（也称为 Flexible Single Master Operations，简称 FSMO）的域控制器没有运行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 或更高版本，所以 Microsoft Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求作为构架 FSMO 的域控制器必须运行 Windows Server 2003 SP1 或更高版本。

FSMO 控制对 Active Directory 构架的所有更新和修改。

若要解决此问题，请执行下列一项或多项操作：

  - 将 FSMO 域控制器升级到 Windows Server 2003 SP1 或更高版本，并重新运行 Microsoft Exchange 安装程序。

  - 如果 Exchange 组织中存在运行 Microsoft Windows Server 2003 Service Pack 1 (SP1) 或更高版本的 FSMO 域控制器，请使用指向该 FSMO 域控制器的 /domaincontroller 参数运行 Exchange 2007 安装程序：
    
    \[*/DomainController* 或 */dc\<FQDN of domain controller\>*\]
    
    使用 */DomainController* 参数指定用来在安装过程中从 Active Directory 读取和向其写入的域控制器。可以使用 NetBIOS 或完全限定的域名 (FQDN) 格式。

若要获取最新的 service pack，Windows Server 2003，请参阅"Windows 服务器技术中心"([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315))。

有关 Exchange Server 2007年设置参数的详细信息，请参阅 Exchange Server 2007年产品文档中的"如何为安装 Exchange 2007 以无人参与模式"([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476))。

