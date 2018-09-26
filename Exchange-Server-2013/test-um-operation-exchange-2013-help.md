---
title: '测试 UM 操作: Exchange 2013 Help'
TOCTitle: 测试 UM 操作
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56271415
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 测试 UM 操作

 

_**适用于：** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-06-25_

本主题说明如何使用命令行管理程序测试语音邮件系统的操作。在执行以下步骤时，运行 Microsoft Exchange 统一消息服务的邮箱服务器启动一个诊断会话初始协议 (SIP) 呼叫，然后返回 UM 服务的健康状况变量。

此诊断测试只能在本地邮箱服务器上运行，而无法使用 EAC 测试邮箱服务器的操作。

有关客户端访问和邮箱服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;邮箱服务器（UM 服务）\&quot;和\&quot;客户端访问服务器（UM 呼叫路由器服务）\&quot;条目。

  - 若要执行以下过程，必须使用作为本地管理员组成员的帐户登录邮箱服务器。

  - 验证邮箱服务器是安装在与客户端访问服务器相同的计算机中，还是安装在单独的计算机中。

  - 验证客户端访问服务器是安装在与邮箱服务器相同的计算机上，还是安装在单独的计算机中。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用命令行管理程序测试统一消息服务的操作

本示例对本地邮箱服务器执行连接测试和运行测试，然后显示 IP 语音 (VoIP) 连接信息。

```powershell
Test-UMConnectivity
```

此示例将测试本地客户端访问服务器对 TCP 端口 5060 上的传入未加密 SIP 请求进行侦听的能力。

```powershell
Test-UMConnectivity -ListenPort 5060
```

此示例将测试本地客户端访问服务器对 TCP 端口 5061 上的传入加密 SIP 请求进行侦听的能力。

```powershell
Test-UMConnectivity -ListenPort 5061
```

> [!NOTE]  
> 未指定 <code>-UMIPGateway</code> 参数时，请使用模式 1。


> [!NOTE]  
> 可以将 <code>-Timeout</code> 参数设置为小于 5 秒的值。但是，建议始终将此参数的值配置为大于或等于 5 秒。

