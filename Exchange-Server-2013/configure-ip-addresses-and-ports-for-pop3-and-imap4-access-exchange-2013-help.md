---
title: '为 POP3 和 IMAP4 访问配置 IP 地址和端口: Exchange 2013 Help'
TOCTitle: 为 POP3 和 IMAP4 访问配置 IP 地址和端口
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50556616
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为 POP3 和 IMAP4 访问配置 IP 地址和端口

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-11-28_

可以使用 EAC 和命令行管理程序配置 Microsoft Exchange POP3 和 IMAP4 服务以使用不同于默认设置的 IP 地址和端口。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用 Internet 协议版本 4 (IPv4) 格式、 Internet 协议版本 6 (IPv6) 格式或同时使用这两种格式输入 IP 地址和 IP 地址范围。 Windows Server 2008 的默认安装支持 IPv4 和 IPv6。</td>
</tr>
</tbody>
</table>


有关与 POP3 和 IMAP4 相关的详细信息，请参阅[Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”和“IMAP4 设置”条目。

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

## 配置 POP3 的 IP 地址和端口

## 使用 EAC 配置 POP3 的 IP 地址和端口

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页上，单击“POP3”。

4.  在“TLS 或未加密的连接”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  在“添加 IP 地址”页上的“IP 地址”下，选择下列选项之一：
    
      - **所有可用 IPv4 地址**   使用某个服务器的所有可用 IPv4 IP 地址。
    
      - **所有可用 IPv6 地址**   使用某个服务器的所有可用 IPv6 IP 地址。
    
      - **指定 IP 地址**   使用某个特定的 IP 地址。

6.  在“端口”下输入一个端口号，或者接受默认端口。

7.  单击“保存”保存更改。

设置了 POP3 的 IP 地址和端口设置后，必须重新启动 POP3 服务使设置生效。有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令行管理程序配置 POP3 的 IP 地址和端口

此示例使用 POP3 和安全套接字层 (SSL) 设置与 Exchange 进行通信的 IP 地址和端口。

    Set-PopSettings -SSLBindings: IPaddress:Port

此示例使用没有加密的 POP3 或传输层安全性 (TLS) 加密设置与 Exchange 进行通信的 IP 地址和端口。

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

设置了 POP3 的 IP 地址和端口设置后，必须重新启动 POP3 服务使设置生效。有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作以验证是否在服务器上更改了 POP3 IP 地址和端口设置。

1.  在命令行管理程序中运行以下命令。
    
        Get-PopSettings | format-list

2.  验证 *UnencryptedOrTLSBindings* 和 *SSLBindings* 设置是否正确。

## 配置 IMAP4 的 IP 地址和端口

## 使用 EAC 配置 IMAP4 的 IP 地址和端口

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页上，单击“IMAP4”。

4.  如果要设置 TLS 或未加密的连接设置，请在“TLS 或未加密的连接”下单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。 如果要更改安全套接字层 (SSL) 连接设置，请在“安全套接字层(SSL)连接”下单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

5.  在“添加 IP 地址”页上的“IP 地址”下，选择下列选项之一：
    
      - **所有可用 IPv4 地址**   使用某个服务器的所有可用 IPv4 IP 地址。
    
      - **所有可用 IPv6 地址**   使用某个服务器的所有可用 IPv6 IP 地址。
    
      - **指定 IP 地址**   使用某个特定的 IP 地址。

6.  在“端口”下输入一个端口号，或者接受默认端口。

7.  单击“保存”保存更改。

设置了 IMAP4 的 IP 地址和端口设置后，必须重新启动 IMAP4 服务使设置生效。 有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

## 使用命令行管理程序配置 IMAP4 的 IP 地址和端口

此示例使用 IMAP4 设置与 Exchange 进行通信的 IP 地址和端口。

    Set-ImapSettings -SSLBindings: IPaddress:Port

此示例使用没有加密的 IMAP4 或 TLS 加密设置与 Exchange 进行通信的 IP 地址和端口。

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

设置了 IMAP4 的 IP 地址和端口设置后，必须重新启动 IMAP4 服务使设置生效。有关如何重新启动 IMAP4 服务的信息，请参阅[启动和停止 IMAP4 服务](start-and-stop-the-imap4-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-ImapSettings](https://technet.microsoft.com/zh-cn/library/aa998252\(v=exchg.150\))。

## 您如何知道这有效？

执行以下操作以验证是否在服务器上更改了 IMAP4 IP 地址和端口设置。

1.  在命令行管理程序中运行以下命令。
    
        Get-ImapSettings | format-list

2.  验证 *UnencryptedOrTLSBindings* 和 *SSLBindings* 设置是否正确。

## 详细信息

在配置 POP3 和 IMAP4 的 IP 地址和端口之后，您可能还需要：

[在 Exchange 2016 中启用 IMAP4](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[在 Exchange 2013 中启用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)

