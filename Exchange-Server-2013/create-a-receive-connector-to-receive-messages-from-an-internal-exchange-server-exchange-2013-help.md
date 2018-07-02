---
title: '通过 Internal Exchange Server 创建接收连接器接收邮件: Exchange 2013 Help'
TOCTitle: 通过 Internal Exchange Server 创建接收连接器接收邮件
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50490569
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通过 Internal Exchange Server 创建接收连接器接收邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-03_

在需要从 Exchange 服务器接收邮件时创建“内部”类型的接收连接器。使用此类型的连接器控制组织中的邮件路由：例如，当要将邮件从邮箱服务器上的传输服务路由到特定边缘传输服务器，或是从一个邮箱服务器路由到另一个邮箱服务器时。

对本程序使用的方案感兴趣？请参阅下列主题：

  - [配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“接收连接器”条目。

  - 如果开始安装，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。在安装之后，可以使用本主题中的步骤创建接收连接器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 通过 Internal Exchange Server 创建接收连接器接收邮件

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 可以新建接收连接器。

2.  在“新建接收连接器”页面上，为接收连接器指定名称，然后对于“角色”选择“集线器传输”。在此情况下，假设您要在您的网络内部路由邮件，而不出入组织。

3.  对于类型选择“内部”。连接器使用 Exchange 服务器身份验证进行配置。

4.  如果远程网络设置页面列出 0.0.0.0-255.255.255.255（这表示接收连接器从所有 IP 地址接收连接），则单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 以删除它。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")，为要从其接收邮件的服务器添加 IP 地址（如 192.168.1.1），然后单击“保存”。

5.  单击“完成”创建此连接器。

在创建了接收连接器之后，它会出现在接收连接器列表中。如果要查看如何使用 cmdlet 创建接收连接器的示例，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功创建了接收连接器以便从内部服务器接收邮件，请测试来自发送服务器的邮件是否可成功到达收件人服务器。执行此操作的一个方法是使用 Exchange 命令行管理程序，通过 [Set-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125140\(v=exchg.150\)) cmdlet 将所创建的接收连接器的 *ProtocolLoggingLevel* 设置为 `Verbose`，然后检查日志以确保邮件传递。

## 详细信息

[通过互联网创建接收连接器接收电子邮件](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[创建安全接收连接器以从合作伙伴接收电子邮件](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

