---
title: '通过互联网创建接收连接器接收电子邮件: Exchange 2013 Help'
TOCTitle: 通过互联网创建接收连接器接收电子邮件
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50490557
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 通过互联网创建接收连接器接收电子邮件

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-15_

此过程向您演示如何配置接收连接器以便从 Internet 接收电子邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在大多数情况下，无需显式设置接收连接器以便从 Internet 接收邮件，因此会在 Exchange 安装时隐式创建用于从 Internet 接受邮件的接收连接器。有关详细信息，请参阅<a href="receive-connectors-exchange-2013-help.md">接收连接器</a>。</td>
</tr>
</tbody>
</table>


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


## 使用 EAC 创建接收连接器以便从 Internet 接收邮件

1.  在 EAC 中，导航到“邮件流”\>“接收连接器”。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")创建一个接收连接器。

2.  在“新建接收连接器”页面上，为接收连接器指定名称，然后对于“角色”选择“前端传输”。由于在此情况下是从 Internet 接收邮件，因此建议最初将邮件路由到前端服务器以简化并合并邮件流。

3.  对于类型选择“Internet”。接收连接器将从 Internet 发件人接收邮件。

4.  对于“网络适配器绑定”，可观察到“所有可用 IPv4”会列在“IP 地址”列表中并且“端口”为 25。（简单邮件传输协议 (SMTP) 使用端口 25。）这表示此连接器可在本地服务器上分配给网络适配器的所有 IP 地址上侦听连接。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果具有多个网络适配器，则在此页面上可以添加分配给本地服务器上特定网络适配器的 IP 地址，但这不是必需的。</td>
    </tr>
    </tbody>
    </table>


5.  单击“完成”按钮以创建您的连接器。

在创建了接收连接器之后，它会出现在接收连接器列表中。如果要查看如何使用 cmdlet 创建接收连接器的示例，请参阅 [New-ReceiveConnector](https://technet.microsoft.com/zh-cn/library/bb125139\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否成功创建了接收连接器以便从 Internet 接收邮件，请测试是否可以从外部来源发送邮件并且某个用户可以接收它。如果您可以接收邮件，就可确定配置成功生效。

## 详细信息

[创建安全接收连接器以从合作伙伴接收电子邮件](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[创建接收连接器从没有运行 Exchange 的系统接收电子邮件](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

