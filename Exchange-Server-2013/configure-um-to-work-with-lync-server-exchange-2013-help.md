---
title: '将 UM 配置为与 Lync Server 配合使用: Exchange 2013 Help'
TOCTitle: 将 UM 配置为与 Lync Server 配合使用
ms:assetid: 29bdddbf-75d5-4c92-988e-c8506ecc7a1c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ966276(v=EXCHG.150)
ms:contentKeyID: 52061490
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 将 UM 配置为与 Lync Server 配合使用

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-06-11_

集成 Microsoft Lync Server 和 Exchange 统一消息时，必须在命令行管理程序中运行 ExchUcUtil.ps1 脚本。ExchUcUtil.ps1 脚本会执行下列操作：

  - 为每个 Lync Server 池创建一个 UM IP 网关。
    
    > [!important]
    > ExchUcUtil.ps1 脚本会创建一个或多个 UM IP 网关。除该脚本创建的一个网关外，必须禁用所有 UM IP 网关上的传出呼叫。这包括禁用在运行该脚本之前创建的 UM IP 网关上的传出呼叫。若要禁用 UM IP 网关上的传出呼叫，请参阅<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">禁用 UM IP 网关的传出呼叫</a>。


  - 为每个 UM IP 网关创建一个 UM 智能寻线。每个智能寻线的引导标识符指定与 UM IP 网关关联的 Lync Server 前端池或 Standard Edition 服务器所使用的 UM SIP URL 拨号计划。

  - 授予 Lync Server 权限，以读取 Active Directory UM 容器对象，例如 UM 拨号计划、自动助理、UM IP 网关和 UM 智能寻线。

> [!important]
> 必须将每个 UM 林配置为信任部署了 Lync Server 2013 的林，并且必须将部署了 Lync Server 2013 的林配置为信任每个 UM 林。如果在多个林中安装了 Exchange UM，则必须为每个 UM 林执行 Exchange Server 集成步骤，否则将需要指定 Lync Server 域。例如，<em>ExchUcUtil.ps1 –Forest:&lt;lync-domain-controller-fqdn&gt;</em>。


有关与集成 Lync Server 和统一消息相关的其他管理任务，请参阅[部署 Exchange 2013 UM 和 Lync Server 概述](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[Exchange 2013 cmdlet](https://technet.microsoft.com/zh-cn/library/bb124413\(v=exchg.150\)) 主题中的“权限 Cmdlet”条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序运行 ExchUcUtil.ps1 脚本

在与 Microsoft Lync Server 位于同一拓扑的组织中的任意 Exchange 服务器上运行 ExchUcUtil.ps1 脚本。您可以使用命令行管理程序从邮箱服务器运行此脚本，也可以使用客户端访问服务器上的远程 Windows PowerShell 运行此脚本。如果在组织中的客户端访问服务器上运行此脚本，则客户端访问服务器会将远程 Windows PowerShell 会话代理到组织中的邮箱服务器。

> [!important]
> ExchUcUtil.ps1 脚本会创建一个或多个 UM IP 网关。除该脚本创建的一个网关外，必须禁用所有 UM IP 网关上的传出呼叫。这包括禁用在运行该脚本之前创建的 UM IP 网关上的传出呼叫。若要禁用 UM IP 网关上的传出呼叫，请参阅<a href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">禁用 UM IP 网关的传出呼叫</a>。


> [!important]
> 您必须具有 Exchange Organization Management 角色的权限，或是 Exchange Organization Administrators 安全组成员，才能运行此脚本。


1.  打开 Exchange 命令行管理程序。

2.  在 `C:\Windows\System32` 提示符下，键入 **cd "\<drive letter\>\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts\>.ExchUcUtil.ps1"**，然后按 Enter 键。

## 您如何知道这有效？

若要验证是否已成功完成 ExchUcUtul.ps1 脚本，请执行以下操作：

  - 使用 **Get-UMIPGateway** cmdlet 或 EAC 查看新 UM IP 网关或已创建的网关。

  - 使用 **Get-UMHuntGroup** cmdlet 或 EAC 查看新 UM 智能寻线或已创建的智能寻线。

