---
title: '配置 IP 地址: Exchange 2013 Help'
TOCTitle: 配置 IP 地址
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50489930
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置 IP 地址

 

_**适用于：** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2012-11-11_

在创建统一消息 (UM) IP 网关之前，您必须先在所用的 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 上设置 IP 地址或完全限定域名 (FQDN)。随后在创建 UM IP 网关时，设置 IP 地址或 FQDN。可以在以后更改 IP 地址或 FQDN。

可以使用 EAC 或命令行管理程序配置 IP 地址或 FQDN。在 EAC 中，“UM IP 网关”页面上的“地址”框可以接受 IPv4 IP 地址、IPv6 地址或 FQDN。还可以在命令行管理程序中对 **Set-UMIPGateway** cmdlet 使用 *Address* 参数，以设置 IPv4 IP 地址、IPv6 地址或 FQDN。如果使用 FQDN 创建 UM IP 网关，则必须在 DNS 正向查找区域中创建合适的 HOST A 记录。如果更改了 UM IP 网关的 DNS 配置，则必须先禁用 UM IP 网关，然后再启用它，以确保其配置信息正确更新。

有关 UM IP 网关的更多管理任务，请参阅[UM IP 网关过程](um-ip-gateway-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：2 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“UM IP 网关”条目。

  - 在执行这些步骤之前，先确认已创建 UM 拨号计划。有关详细步骤，请参阅[创建 UM 拨号计划](create-a-um-dial-plan-exchange-2013-help.md)。

  - 在执行这些步骤之前，请确认已创建 UM IP 网关。有关详细步骤，请参阅[创建 UM IP 网关](create-a-um-ip-gateway-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 在 UM IP 网关上配置 IP 地址

1.  在 EAC 中，导航到“统一消息”\>“UM IP 网关”，选择要修改的 UM IP 网关，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在“UM IP 网关”页面上的“地址”框中，输入 VoIP 网关、IP PBX 或会话边界控制器 (SBC) 的 IP 地址。

3.  单击“保存”保存更改。

> [!IMPORTANT]  
> 如果在 UM IP 网关上使用 FQDN 而不是 IP 地址，请验证已创建正确的 DNS 记录。


## 使用命令行管理程序在 UM IP 网关上配置 IP 地址

此示例使用 IP 地址 10.10.10.1 配置名为 `MyUMIPGateway` 的 UM IP 网关。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

此示例使用 IP 地址 10.10.10.10 配置名为 `MyUMIPGateway` 的 UM IP 网关，并侦听 TCP 端口 5061 上的 SIP 请求。

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

此示例可防止名为 `MyUMIPGateway` 的 UM IP 网关接受传入和传出呼叫，设置 IPv6 地址，并允许 UM IP 网关使用 IPv4 和 IPV6 地址。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

