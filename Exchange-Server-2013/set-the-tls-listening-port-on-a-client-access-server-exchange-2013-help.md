---
title: '设置客户端访问服务器的 TLS 的侦听端口: Exchange 2013 Help'
TOCTitle: 设置客户端访问服务器的 TLS 的侦听端口
ms:assetid: f4401923-61fa-4dc5-95f8-c0d2f515b2ea
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673576(v=EXCHG.150)
ms:contentKeyID: 50556686
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 设置客户端访问服务器的 TLS 的侦听端口

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-17_

您可以配置用于侦听的 SIP 请求运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器上的传输层安全性 (TLS) 端口。默认情况下，当您安装客户端访问服务器，SIP TLS 的侦听端口号设置为 5061。

如果要执行以下操作，则可能还必须将 TLS 侦听端口配置为 5061：

  - 将 UM 拨号计划中的 VoIP 安全设置设为\&quot;SIP 安全\&quot;。

  - 将 UM 拨号计划中的 VoIP 安全设置设为\&quot;安全\&quot;。

  - 与 MicrosoftOffice Communications Server 2007 R2 或 Microsoft Lync Server 集成。

  - 使用相互传输层安全性（相互 TLS）对客户端访问服务器、运行 Microsoft Exchange 统一消息服务的邮箱服务器以及 VoIP 网关、为会话初始协议 (SIP) 启用的专用交换机 (PBX)、IP PBX 或会话边界控制器 (SBC) 之间的网络数据加密。

如果您要在 UM IP 网关和在\&quot;SIP 安全\&quot;模式或\&quot;安全\&quot;模式下运行的拨号计划之间使用相互 TLS，则在您创建 UM IP 网关时，必须使用完全限定域名 (FQDN) 对其进行配置，然后配置 UM IP 网关，以侦听 TLS 端口 5061。您还必须验证任何 VoIP 网关、为 SIP 启用的 PBX、IP PBX 或 SBC 是否也配置为可侦听端口 5061 上的相互 TLS 请求。

您仅可以配置客户端访问服务器 TCP 和 TLS 端口。不能配置为 2013年的 Exchange 邮箱服务器的端口。但是，可以使用**Set-UMService** cmdlet 将 Exchange 2010 UM 服务器 TCP 和 TLS 的侦听端口配置。

有关与统一消息和客户端访问服务器相关的其他任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;客户端访问服务器（UM 呼叫路由器服务）\&quot;条目。

  - 验证是否已正确安装客户端访问和邮箱服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置客户端访问服务器上的 TLS 侦听端口

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择您要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange Server\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 服务设置\&quot;下的\&quot;TLS 侦听端口\&quot;下，输入 TLS 端口号，然后单击\&quot;保存\&quot;。

## 使用命令行管理程序配置客户端访问服务器上的 TLS 侦听端口

此示例将客户端访问服务器上名为 `MyClientAccessServer` 的 TLS 侦听端口设置为 5561。

```powershell
Set-UMCallRouterSettings -Server MyClientAccessServer -SipTlsListeningPort 5561
```

