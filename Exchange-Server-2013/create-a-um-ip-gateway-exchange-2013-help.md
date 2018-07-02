---
title: '创建 UM IP 网关: Exchange 2013 Help'
TOCTitle: 创建 UM IP 网关
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50490566
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: HT
---

# 创建 UM IP 网关

 

_**适用于：**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：**2013-04-16_

创建统一消息 (UM) IP 网关时，启用 Exchange 服务器以连接到新 Voice Over IP (VoIP) 网关、针对会话初始协议 (SIP) 启用的专用交换机 (PBX)、IP PBX 或会话边界控制器 (SBC)。创建 UM IP 网关之后，应当立即创建新的 UM 智能寻线，然后将此 UM 智能寻线与 UM IP 网关进行关联。通过创建一个或多个 UM 智能寻线，可以将 UM IP 网关与一个或多个 UM 拨号计划进行关联。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：3 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM IP 网关”条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用 EAC 创建 UM IP 网关

1.  
    
    在 EAC 中，导航至“统一消息”\>“UM IP 网关”，然后单击“新建”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建 UM IP 网关”页上，输入以下信息：
    
      - “名称”   使用此框指定 UM IP 网关的唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM IP 网关之后必须更改其显示名，则必须先删除现有的 UM IP 网关，然后再创建另一个具有所需名称的 UM IP 网关。必须提供 UM IP 网关名，但是该名称仅用于显示。因为组织可能会使用多个 UM IP 网关，所以，建议您为该 UM IP 网关使用有意义的名称。UM IP 网关名称的最大长度为 64 个字符，并且可以包含空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - “地址”   您可配置具有 IP 地址和完全限定域名 (FQDN) 的 UM IP 网关。使用该框指定在 VoIP 网关、启用了 SIP 的 PBX、IP PBX 或 SBC 或 FQDN 上配置的 IP 地址。此框只接受有效并且格式正确的 FQDN。
        
        您可以在此框中输入字母和数字字符。支持 IPv4 地址、IPv6 地址和 FQDN。若要在 UM IP 网关与在 SIP 安全或安全模式下运行的拨号计划之间使用相互传输层安全性（相互 TLS），则必须使用 FQDN 配置 UM IP 网关。还必须将其配置为在端口 5061 上侦听，并确保所有 VoIP 网关或 IP PBX 都已配置为在端口 5061 上侦听相互 TLS 请求。若要配置 UM IP 网关，请运行以下命令：`Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        如果使用 FQDN，必须还要确保已为该 VoIP 网关正确地配置了 DNS 主机记录，以便可以正确地将主机名解析为 IP 地址。如果使用 FQDN 而不是 IP 地址，并更改了 UM IP 网关的 DNS 配置，则必须先禁用 UM IP 网关然后再启用它，以确保 UM IP 网关的配置信息已正确更新。
    
      - “UM 拨号计划”   单击“浏览”选择要与 UM IP 网关关联的 UM 拨号计划。选择要与 UM IP 网关关联的 UM 拨号计划时，还会创建默认 UM 智能寻线并将其与所选的 UM 拨号计划关联。如果未选择 UM 拨号计划，则必须手动创建 UM 智能寻线并将该 UM 智能寻线与所创建的 UM IP 网关关联。

3.  
    
    单击“保存”。

## 使用命令行管理程序创建 UM IP 网关

此示例创建名为 `MyUMIPGateway` 的 UM IP 网关，该网关使 Exchange 服务器可以开始接受来自 IP 地址为 10.10.10.1 的 VoIP 网关、针对 SIP 启用的 PBX、IP PBX 或 SBC 的呼叫。

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

此示例创建名为 `MyUMIPGateway` 的 UM IP 网关，该网关使 Exchange 服务器可以开始接受来自 FQDN 为 MyUMIPGateway.contoso.com 的 VoIP 网关、针对 SIP 启用的 PBX、IP PBX 或 SBC 的呼叫并在端口 5061 侦听。

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

此示例创建名为 `MyUMIPGateway` 的 UM IP 网关，并阻止 UM IP 网关接受传入呼叫或发送传出呼叫，设置 IPv6 地址，并允许 UM IP 网关使用 IPv4 和 IPV6 地址。

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

