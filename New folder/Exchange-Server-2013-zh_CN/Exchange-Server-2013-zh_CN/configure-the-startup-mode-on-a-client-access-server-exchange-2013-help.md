---
title: '在客户端访问服务器上配置的启动模式: Exchange 2013 Help'
TOCTitle: 在客户端访问服务器上配置的启动模式
ms:assetid: 71cc9061-9e3c-4b4a-8dbe-f590ca5bcee8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673533(v=EXCHG.150)
ms:contentKeyID: 50556598
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在客户端访问服务器上配置的启动模式

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-15_

客户端访问服务器上，可以指定 Microsoft Exchange 统一消息呼叫路由器服务的启动模式。默认情况下，客户端访问服务器在 TCP 模式中，将启动，但如果您使用传输层安全性 (TLS) 加密语音通信 (VoIP) 上，您必须配置客户端访问服务器使用 TLS 或双重模式。我们建议将客户端访问服务器配置为使用双启动模式。这是因为所有的客户端访问和邮箱服务器可以将传入呼叫应答所有 um 拨号计划，和那些拨号计划可以有不同的安全设置。如果您更改启动模式，您必须重新启动 Microsoft Exchange 统一消息呼叫路由器服务以使更改生效。

> [!important]
> 默认情况下，客户端访问服务器都可用来应答传入呼叫。您不必为 UM 拨号计划处理 UM 调用，除非您正在集成 UM 和 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 添加客户端访问服务器。


有关与统一消息和客户端访问服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;客户端访问服务器（UM 呼叫路由器服务）\&quot;条目。

  - 验证客户端访问服务器是安装在与邮箱服务器相同的计算机上还是安装在单独的计算机上。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 配置客户端访问服务器上的启动模式

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在此列表视图中，选择要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange Server\&quot;页上单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 电话路由器设置\&quot;\>\&quot;UM 启动模式\&quot;下，从下拉列表中选择下列选项之一：
    
      - **TCP**   如果不使用 mTLS 而仅使用\&quot;不安全\&quot;拨号计划，则使用此选项。
    
      - **TLS**   如果使用 mTLS 且仅使用\&quot;SIP 安全\&quot;或\&quot;安全\&quot;拨号计划，则使用此选项。
    
      - **DUAL**   如果使用 mTLS 且使用\&quot;不安全\&quot;、\&quot;SIP 安全\&quot;或\&quot;安全\&quot;拨号计划，则使用此选项。

5.  选择 UM 启动模式后，单击\&quot;保存\&quot;。

## 使用命令行管理程序配置客户端访问服务器上启动模式

此示例将名为 `UMCallRouter1` 的客户端访问服务器的启动模式设置为 Dual 模式。

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode Dual

此示例将名为 `UMCallRouter1` 的客户端访问服务器的启动模式设置为 TLS 模式。

    Set-UMCallRouterSettings -Server UMCallRouter1 -UMStartUpMode TLS

