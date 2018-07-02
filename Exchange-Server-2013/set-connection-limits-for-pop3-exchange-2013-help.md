---
title: '设置 POP3 的连接限制: Exchange 2013 Help'
TOCTitle: 设置 POP3 的连接限制
ms:assetid: 512d61c2-2a34-4813-92a9-875339d3388b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997988(v=EXCHG.150)
ms:contentKeyID: 50556579
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 设置 POP3 的连接限制

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-11-28_

您可以使用 EAC 或命令行管理程序来管理组织的 POP3 连接限制。

在指定 POP3 的连接限制时，可以选择针对服务器、IP 地址或特定用户的连接限制。

有关与 POP3 相关的其他信息，请参阅 [Exchange Server 2013 中的 POP3 和 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的“POP3 设置”条目。

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

## 使用 EMC 设置服务器、IP 地址或用户的 POP3 连接限制

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“POP3”。

4.  向下滚动并单击“更多选项”。

5.  在“连接限制”下，使用以下设置：
    
      - **最大连接数**   指定所指定的服务器将接受的连接总数。 这包括通过身份验证和未通过身份验证的连接。默认值为 2,147,483,647。可能的值从 1 到 2,147,483,647。
    
      - **来自单个 IP 地址的最大连接数** 指定此服务器将接受的来自单个 IP 地址的连接数。默认值为 2,147,483,647。可能的值从 1 到 2,147,483,647。
    
      - **来自单个用户的最大连接数** 指定此服务器将接受的来自特定用户的最大连接数。默认值为 16。可能的值从 1 到 2,147,483,647。
    
      - **最大命令大小(字节)**   指定单个命令的最大大小。默认大小为 512。可能的值从 40 到 1,024。

6.  单击“应用”，然后单击“确定”保存更改。

设置了连接限制之后，必须重新启动 POP3 服务。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

## 使用命令行管理程序设置服务器、IP 地址或用户的 POP3 连接限制

此示例设置服务器的连接限制。

    Set-PopSettings -Identity CAS01 -MaxConnections Value

此示例设置 IP 地址的连接限制。

    Set-PopSettings -Identity CAS01 -MaxConnectionsFromSingleIP Value

此示例设置用户的连接限制。

    Set-PopSettings -MaxConnectionsPerUser Value 

此示例设置了最大命令大小。

    Set-PopSettings -MaxCommandSize Value

设置了连接限制之后，必须重新启动 POP3 服务。 有关如何重新启动 POP3 服务的信息，请参阅[启动和停止 POP3 服务](start-and-stop-the-pop3-services-exchange-2013-help.md)。

有关语法和参数的详细信息，请参阅 [Set-PopSettings](https://technet.microsoft.com/zh-cn/library/aa997154\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否成功设置了连接限制，请执行以下操作之一：

1.  在 EAC 中，导航到“服务器”**\>**“服务器”。

2.  在服务器列表中，选择客户端访问服务器，然后单击“编辑”![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在服务器属性页面上，单击“POP3”。

4.  向下滚动并单击“更多选项”。

5.  根据“连接限制”，验证连接设置是否正确。

或

1.  在命令行管理程序中运行以下命令。
    
        Get-PopSettings | format-list

2.  验证连接设置是否正确。

## 详细信息

在为服务器、IP 地址或用户设置 POP3 连接限制之后，您可能还需要：

[在 Exchange 2013 中启用 POP3](enable-pop3-in-exchange-2013-exchange-2013-help.md)

[设置 POP3 的连接超时限制](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

