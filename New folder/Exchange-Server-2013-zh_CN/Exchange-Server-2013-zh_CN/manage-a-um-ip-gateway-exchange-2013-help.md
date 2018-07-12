---
title: '管理 UM IP 网关: Exchange Online Help'
TOCTitle: 管理 UM IP 网关
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50490317
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# 管理 UM IP 网关

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-21_

创建统一邮件 (UM) IP 网关之后，可以查看或配置各种设置。例如，您可以配置的 IP 地址或完全合格的域名称 (FQDN)，配置传出呼叫设置，并启用或禁用消息等待指示符。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的\&quot;UM IP 网关\&quot;条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 查看或配置 UM IP 网关属性

1.  在 EAC，导航到**统一消息**\> **UM IP 网关**。在列表视图中，选择您想要管理的 UM IP 网关，然后单击**编辑**![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  使用**UM IP 网关**网页可查看和配置 UM IP 网关设置。您可以查看或配置以下设置 ︰
    
      - **状态**：此仅显示字段用于显示 UM IP 网关的状态。
    
      - **名称**  使用此框可以指定 UM IP 网关的唯一名称。这是出现在 EAC 显示名称。如果您需要更改显示名称 UM IP 网关，它被创建后，您必须首先删除现有 UM IP 网关，然后再创建具有相应名称的另一个 UM IP 网关。UM IP 网关名称是必需的但它使用仅用于显示目的。因为您的组织可能会使用多个 UM IP 网关，则建议使用有意义的名称，您的 UM IP 网关。UM IP 网关名称最大长度为 64 个字符，并且可以包含空格。
    
      - **地址**  您可以配置 UM IP 网关的 IP 地址或完全合格的域名称 (FQDN)。使用此框可以指定 IP 地址或配置上的 VoIP 网关、 SIP 启用 PBX、 IP PBX 或 SBC 的 FQDN。
        
        您可以在此框中输入字母和数字字符。支持 IPv4 地址，IPv6 地址和 Fqdn。如果您使用 FQDN，则还必须确保您已正确配置 DNS 主机记录的 VoIP 网关以便正确解析为 IP 地址的主机名。此外，如果您使用 FQDN 而不是 IP 地址，并且 UM IP 网关的 DNS 配置已更改，您必须禁用，然后再启用 UM IP 网关，以确保正确更新后的 UM IP 网关的配置信息。
        
        如果您想要使用相互 UM IP 网关和拨号计划中任何一种操作系统之间的传输层安全性 (相互 TLS) SIP 安全或安全模式下，您必须使用 FQDN 配置的 UM IP 网关。您还必须配置侦听端口 5061，并验证所有 IP 网关或 IP Pbx 也已都配置为侦听端口 5061 上相互 TLS 请求。要配置的 UM IP 网关，请运行下面的命令 ︰ `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`。
    
      - **通过此 UM IP 网关允许拨出电话**  选中此复选框可允许的 UM IP 网关，接受和处理的传出呼叫。此设置不影响呼叫转移或从 VoIP 网关的传入呼叫。
        
        默认情况下，当创建 UM IP 网关时，启用此设置。如果您禁用此设置，与拨号计划相关联的用户将不能拨出电话通过 VoIP 网关，IP PBX 或 SBC 在**地址**字段中定义。
    
      - **允许消息等待指示符**  选中此复选框可允许将语音邮件通知发送给用户的调用执行的 UM IP 网关。此设置使 UM IP 网关来接收和发送通知的 SIP 消息的用户。此设置默认启用的允许等待通知发送给用户的消息。
        
        消息等待指示符指示存在新的或未听过任何的消息机制可以引用。在Outlook和Outlook Web App等客户端收件箱找不到新的语音邮件已到达的指示。它可以采用短消息服务 (SMS) 或文本消息发送到已注册的移动电话、 预先配置的数目或灯亮起的桌面电话用户从 Exchange 服务器进行出站呼叫的形式。

## 使用命令行管理程序可以配置 UM IP 网关属性

此示例修改名为 `MyUMIPGateway` 的 UM IP 网关的 IP 地址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

此示例将禁止名为 `MyUMIPGateway` 的 UM IP 网关接受传入呼叫并禁止传出呼叫。

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

此示例将使 UM IP 网关能够充当 VoIP 网关模拟器，并可与 **Test-UMConnectivity** cmdlet 一起使用。

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true

> [!important]
> 在将对 UM IP 网关配置进行的所有更改复制到与 UM IP 网关同一 UM 拨号计划中的 Exchange 服务器之前，存在一个延迟期。


该示例可防止名为 `MyUMIPGateway` 的 UM IP 网关接受传入呼叫并阻止传出呼叫，可设置 IPv6 地址，并允许 UM IP 网关使用 IPv4 和 IPV6 地址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## 使用命令行管理程序可以查看 UM IP 网关属性

此示例显示 Active Directory 林中所有 UM IP 网关的格式化列表。

    Get-UMIPGateway |Format-List

此示例将显示名为 `MyUMIPGateway` 的 UM IP 网关的属性。

    Get-UMIPGateway -Identity MyUMIPGateway

此示例将显示 Active Directory 林中所有 UM IP 网关，包括 VoIP 网关模拟器。

    Get-UMIPGateway -IncludeSimulator $true

