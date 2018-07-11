---
title: '配置 VoIP 安全设置: Exchange Online Help'
TOCTitle: 配置 VoIP 安全设置
ms:assetid: b5335654-c766-4f3f-883c-f31263e1d9c1
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb201721(v=EXCHG.150)
ms:contentKeyID: 50491386
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置 VoIP 安全设置

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2014-10-16_

您可以为统一消息 (UM) 拨号计划启用 IP 语音 (VoIP) 安全性。默认情况下，创建 UM 拨号计划时，该拨号计划将使用不安全模式，或者不使用加密。Exchange 服务器可以对单个或多个 UM 拨号计划的呼叫进行应答，也可以对具有不同 VoIP 安全设置的拨号计划的呼叫进行应答。在 Office 365 和 Exchange Online 中要求使用安全模式并且不能将其禁用。

在对 UM 拨号计划进行配置以使用会话初始协议 (SIP) 安全或安全模式时，应答 UM 拨号计划呼叫的 Exchange 服务器将对 SIP 信号通信（适用于 SIP 安全模式）或同时对实时传输协议 (RTP) 媒介通道和 SIP 信号通信（适用于安全模式）进行加密。

> [!important]
> 对于内部部署和混合部署，在运行 Microsoft Exchange 统一消息呼叫路由器服务的客户端访问服务器或运行 Microsoft Exchange 统一消息服务的邮箱服务器上配置 SipTCPListeningPort、SipTLSListeningPort 或 UMStartUpMode 时，需要正确地配置 Windows 防火墙规则以允许 SIP 和 RTP 网络通信。


有关与 UM 拨号计划相关的其他管理任务，请参阅[UM 拨号计划过程](um-dial-plan-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：小于 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM 拨号计划\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 在 UM 拨号计划中配置 VoIP 安全性

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;，选择要对其更改 VoIP 安全性的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。

3.  在\&quot;常规\&quot;的\&quot;VoIP 安全模式\&quot;下，选择下列选项之一:
    
      - **SIP 安全**
    
      - **不安全**（默认）
    
      - **安全**

4.  单击\&quot;保存\&quot;。

## 使用命令行管理程序在 UM 拨号计划中配置 VoIP 安全性

此示例配置名为 `MySecureDialPlan` 的 UM 拨号计划，以对 SIP 和 RTP 通信进行加密。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Secured

此示例配置名为 `MySecureDialPlan` 的 UM 拨号计划，以对 SIP 通信进行加密，但不对 RTP 通信进行加密。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity SIPsecured

此示例配置名为 `MySecureDialPlan` 的 UM 拨号计划，但不对 SIP 和 RTP 通信进行加密。

    Set-UMDialPlan -identity MySecureDialPlan -VoIPSecurity Unsecured

