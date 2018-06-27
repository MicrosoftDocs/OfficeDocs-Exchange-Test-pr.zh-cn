---
title: '创建接收连接器从没有运行 Exchange 的系统接收电子邮件: Exchange 2013 Help'
TOCTitle: 创建接收连接器从没有运行 Exchange 的系统接收电子邮件
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50490967
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建接收连接器从没有运行 Exchange 的系统接收电子邮件

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-03_

您可能会遇到要从未运行 Exchange 的系统接收邮件的情况。例如，如果您有一个网络设备用来执行策略检查然后将邮件路由到 Exchange 服务器。我们假定在这种情况下，该设备使用 SMTP。如果不是这样，则应使用外部连接器或传递代理连接器。

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


## 使用 EAC 创建接收连接器以便从邮件设备接收邮件

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")创建一个接收连接器。

2.  在“新建接收连接器”页上，为接收连接器指定名称，然后为“角色”选择“集线器传输”。在这种情况下，您希望运行传输服务的邮箱服务器从设备接收邮件。

3.  选择“自定义”作为类型，因为接收连接器将从未运行 Microsoft Exchange Server 2013 的设备接收邮件。

4.  对于“网络适配器绑定”，可观察到“所有可用 IPv4”会列在“IP 地址”列表中。单击“下一步”。

5.  对于“远程网络设置”，单击“删除”![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标") 从“IP 地址”列表中删除“0.0.0.0-255.255.255.255”，因为您希望指定连接器接受来自特定设备的邮件。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标") 添加新 IP 地址，并在“添加 IP 地址”窗口中添加您设备的 IP 地址。单击“保存”。

6.  单击“完成”按钮以创建您的连接器。

在创建了接收连接器之后，它会出现在接收连接器列表中。如果要查看如何使用 cmdlet 创建接收连接器的示例，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否成功创建了接收连接器以便从邮件设备接收邮件，请测试您是否可以从该设备接收邮件。如果您可以接收邮件，就可确定配置成功生效。

## 详细信息

[通过互联网创建接收连接器接收电子邮件](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

