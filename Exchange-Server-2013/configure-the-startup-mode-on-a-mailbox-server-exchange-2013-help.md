---
title: '在邮箱服务器上配置的启动模式: Exchange 2013 Help'
TOCTitle: 在邮箱服务器上配置的启动模式
ms:assetid: 4457d6a0-52bd-4269-8cb5-d34d7fe9bfc3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ee423544(v=EXCHG.150)
ms:contentKeyID: 50556570
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 在邮箱服务器上配置的启动模式

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-15_

在邮箱服务器上，可以指定 Microsoft Exchange 统一消息服务的启动模式。默认情况下，邮箱服务器在 TCP 模式中，将启动，但是如果您使用传输层安全性 (TLS) 加密语音通信 (VoIP) 上，您必须配置邮箱服务器使用 TLS 或双重模式。我们建议将邮箱服务器配置为使用双启动模式。这是因为所有的客户端访问服务器和邮箱服务器可以将传入呼叫应答所有 um 拨号计划，和那些拨号计划可以有不同的安全设置 （无安全机制、 安全的或 SIP 安全）。如果您更改启动模式，您必须重新启动 Microsoft Exchange 统一消息服务以使更改生效。

> [!IMPORTANT]  
> 默认情况下，邮箱服务器都可用来应答传入呼叫。您不必为 UM 拨号计划处理 UM 调用，除非您正在集成 UM 和 Microsoft Office 通信服务器 2007 R2 或 Microsoft Lync Server 添加的邮箱服务器。


有关统一消息和邮箱服务器相关的其他管理任务，请参阅 [UM 服务过程](um-services-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;邮箱服务器（UM 服务）\&quot;条目。

  - 验证邮箱服务器是安装在与客户端访问服务器相同的计算机中，还是安装在单独的计算机中。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 在邮箱服务器上配置启动模式

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange 服务器\&quot;页上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 服务设置\&quot;\>\&quot;UM 启动模式\&quot;下，从下拉列表中选择以下项之一：
    
      - **TCP**   如果您没有使用 mTLS 而是仅使用了不安全的拨号计划，则使用该选项。
    
      - **TLS**   如果您使用 mTLS 并且仅使用了 SIP 安全或安全的拨号计划，则使用该选项。
    
      - **DUAL**   如果您使用 mTLS 并且使用不安全、SIP 安全以及安全拨号计划，请使用此选项。

5.  选择 UM 启动模式后，单击\&quot;保存\&quot;。

## 使用命令行管理程序在邮箱服务器上配置启动模式

此示例将名为 `MyUMServer1` 的邮箱服务器的启动模式设置为双协议模式。

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode Dual
```

此示例将名为 `MyUMServer1` 的邮箱服务器的启动模式设置为 TLS 模式。

```powershell
Set-UMService -Identity MyUMServer1 -UMStartUpMode TLS
```

