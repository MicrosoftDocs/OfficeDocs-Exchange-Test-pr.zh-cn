---
title: '管理客户端访问服务器上的 UM 设置: Exchange 2013 Help'
TOCTitle: 管理客户端访问服务器上的 UM 设置
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50556521
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理客户端访问服务器上的 UM 设置

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-04-09_

在安装运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器之后，可以配置几个选项，包括并发呼叫数、TCP 和传输层安全性 (TLS) 侦听端口、状态和启动模式。

> [!NOTE]  
> 在客户端访问服务器可以处理统一消息 (UM) 呼叫之前，不需要将客户端访问服务器添加到 UM 拨号计划中，但在集成 UM 和 Microsoft Office Communications Server 2007 R2 或 Microsoft Lync Server 时除外。默认情况下，组织中的所有客户端访问服务器都可用于应答传入呼叫。


有关与统一消息和客户端访问服务器相关的其他任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;客户端访问服务器（UM 呼叫路由器服务）\&quot;条目。

  - 验证是否已在与邮箱服务器相同的计算机上或单独的计算机上安装客户端访问服务器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用命令行管理程序在客户端访问服务器上配置统一消息属性

此示例将从所有会话初始协议 (SIP) 拨号计划中删除名为 `MyClientAccessServer` 的客户端访问服务器。

```powershell
Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer
```

本示例在名为 `MySIPDialPlan` 的 SIP 拨号计划中添加名为 `MyClientAccessServer` 的客户端访问服务器，还设置了传入语音呼叫的最大次数。

```powershell
Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer
```

此示例在名为 `MyClientAccessServer` 的客户端访问服务器上将 SIP TCP 侦听端口设置为 5077，将启动模式设置为\&quot;双重\&quot;模式。

```powershell
Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 
```

## 使用命令行管理程序查看客户端访问服务器属性

此示例显示所有客户端访问服务器的列表。

```powershell
Get-UMCallRouterSettings
```

此示例显示客户端访问服务器属性的格式化列表。

```powershell
Get-UMCallRouterSettings | Format-List
```

