---
title: '主 DNS 服务器无法联系_PrimaryDNSTestFailed: Exchange 2013 Help'
TOCTitle: 主 DNS 服务器无法联系_PrimaryDNSTestFailed
ms:assetid: 5b39cb64-c8f1-4fd3-843b-ecd23f99fe3a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/ms.exch.setupreadiness.primarydnstestfailed(v=EXCHG.150)
ms:contentKeyID: 50490639
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 主 DNS 服务器无法联系\_PrimaryDNSTestFailed

 

_**适用于：**Exchange Server_

_**上一次修改主题：**2016-12-09_

此主题中的内容尚未针对 Microsoft Exchange Server 2013 进行更新。虽然尚未更新，但仍可能适用于 Exchange 2013。如果您仍需要帮助，请查看下面的社区资源。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

因为无法建立与主域名系统 (DNS) 服务器的通信，所以 Microsoft® Exchange Server 2007 安装程序无法继续进行。

Exchange 2007 安装程序要求本地计算机能够与该域的权威 DNS 数据库进行通信。

Microsoft Exchange 依靠 DNS 解析其下一个内部或外部目标服务器的 IP 地址。

与主 DNS 服务器的通信可能会由于以下原因而失败：

  - 本地 TCP/IP 配置没有指向正确的 DNS 服务器。

  - DNS 服务器停机或由于网络故障或其他原因而不可访问。

若要解决该问题，请执行下列操作：

  - 验证本地 TCP/IP 配置是否指向正确的 DNS 服务器。

**验证本地 TCP/IP 配置**

1.  查看本地 TCP/IP 配置：
    
    有关详细信息，请参阅“Configure TCP/IP to use DNS”（配置 TCP/IP 以使用 DNS）([https://go.microsoft.com/fwlink/?LinkId=68094](https://go.microsoft.com/fwlink/?linkid=68094))。

<!-- end list -->

  - 验证 DNS 服务器是否正在运行并且可以进行联系。

**验证 DNS 服务器是否正在运行并且可以进行联系**

1.  通过执行下列一项或多项检查来验证 DNS 服务器是否正在运行：
    
      - 从 DNS 服务器上的 DNS 管理程序中查看 DNS 服务器的状态。
    
      - 重新启动 DNS 服务器。
        
        有关详细信息，请参阅“Start, stop, pause, or restart a DNS server”（启动、停止、暂停或重新启动 DNS 服务器）([https://go.microsoft.com/fwlink/?LinkId=62999](https://go.microsoft.com/fwlink/?linkid=62999))。
    
      - 使用 **nslookup** 命令验证 DNS 服务器是否响应。
        
        有关详细信息，请参阅“使用 nslookup 命令验证 DNS 服务器是否响应([https://go.microsoft.com/fwlink/?LinkId=63000](https://go.microsoft.com/fwlink/?linkid=63000)) 中的说明。

