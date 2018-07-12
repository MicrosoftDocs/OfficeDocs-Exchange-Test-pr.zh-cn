---
title: '创建安全接收连接器以从合作伙伴接收电子邮件: Exchange 2013 Help'
TOCTitle: 创建安全接收连接器以从合作伙伴接收电子邮件
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50489863
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建安全接收连接器以从合作伙伴接收电子邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

此过程向您演示如何配置接收连接器以便从合作伙伴接收安全电子邮件。在需要对您与受信任合作伙伴之间的通信进行加密时可使用此过程。此连接器配置为仅接受来自使用传输层安全性 (TLS) 进行身份验证的服务器的连接。

对本程序使用的方案感兴趣？请参阅下列主题：

  - [配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接收连接器”条目。

  - 如果开始安装，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。在安装之后，可以使用本主题中的步骤创建接收连接器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用 EAC 创建接收连接器以便从合作伙伴接收安全邮件

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可以新建接收连接器。

2.  在“新建接收连接器”页面上，为接收连接器指定名称，然后对于“角色”选择“前端传输”。由于在此情况下是从合作伙伴接收邮件，因此建议最初将邮件路由到前端服务器以简化并合并邮件流。

3.  对于类型选择“合作伙伴”。接收连接器会从受信任第三方接收邮件。

4.  对于“网络适配器绑定”，可观察到“所有可用 IPv4”会列在“IP 地址”列表中并且“端口”为 25。（简单邮件传输协议使用端口 25。）这表示此连接器可在本地服务器上分配给网络适配器的所有 IP 地址上侦听连接。单击“下一步”。

5.  如果远程网络设置页面列出 0.0.0.0-255.255.255.255（这表示接收连接器从所有 IP 地址接收连接），则单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以删除它。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，添加合作伙伴服务器的 IP 地址，然后单击“保存”。
    
    > [!NOTE]
    > 还可以使用 CIDR 表示法指定 IP 地址范围，如 64.4.6.100/24。


6.  单击“完成”创建此连接器。

在创建了接收连接器之后，它会出现在接收连接器列表中。如果要查看如何使用 cmdlet 创建接收连接器的示例，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功创建了接收连接器以便从合作伙伴接收邮件，请测试合作伙伴是否可以向您的某个用户发送邮件以及该用户是否可成功接收邮件。如果可以接收加密邮件（可以通过检查邮件头来验证是否使用了 TLS），便知道配置是否成功生效。

## 详细信息

[接收连接器](receive-connectors-exchange-2013-help.md)

