---
title: '设置客户端访问服务器上的 TCP 侦听端口: Exchange 2013 Help'
TOCTitle: 设置客户端访问服务器上的 TCP 侦听端口
ms:assetid: 5f48f21a-d8d4-48b2-868f-9a3647693841
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673530(v=EXCHG.150)
ms:contentKeyID: 50556587
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置客户端访问服务器上的 TCP 侦听端口

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-09_

您可以配置一个 TCP 端口，使其用来侦听客户端访问服务器（运行 Microsoft Exchange 统一消息呼叫路由器服务）中的 SIP 请求。默认情况下，安装客户端访问服务器时，SIP TCP 侦听端口号将设置为 5060，且客户端访问服务器以 TCP 模式启动。SIP TCP 侦听端口无法使用 EAC 进行配置。必须使用 **Set-UMCallRouterSettings** cmdlet 来配置 SIP TCP 侦听端口号。

如果 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 配置为使用除 SIP 标准 5060 以外的 TCP 端口，则可能必须将 TCP 侦听端口配置为 5061。

只能配置客户端访问服务器 TCP 和 TLS 端口。无法为 Exchange 2013 邮箱服务器配置端口。但可以使用 **Set-UMService** cmdlet 为 Exchange 2010 UM 服务器配置 TCP 和 TLS 侦听端口。

有关与统一消息和客户端访问服务器相关的其他任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“客户端访问服务器（UM 呼叫路由器服务）”条目。

  - 验证是否已正确安装客户端访问和邮箱服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 在客户端访问服务器中配置 TCP 侦听端口

1.  在 EAC 中，导航到“服务器”\>“服务器”。

2.  在列表视图中，选择要修改的 Exchange 服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在“Exchange Server”页面上，单击“统一消息”。

4.  在“UM 呼叫路由器设置”的“TCP 侦听端口”下，输入 TCP 端口号，然后单击“保存”。

## 使用命令行管理程序在客户端访问服务器中配置 TCP 侦听端口

本示例将名为 `MyClientAccessServer` 的客户端访问服务器中的 TCP 侦听端口设置为 5566。

    Set-UMCallRouterSettings -Server MyClientAccessServer -SipTCPListeningPort 5566

