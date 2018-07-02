---
title: '客户端访问服务器: Exchange 2013 Help'
TOCTitle: 客户端访问服务器
ms:assetid: 87e206ab-7a7b-4b4f-be1a-5035713c74d2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298114(v=EXCHG.150)
ms:contentKeyID: 50490980
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 客户端访问服务器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2014-07-02_

对于 Microsoft Exchange 2013，对 Exchange 服务器角色进行了主要的体系结构更改。过去 Exchange 2010 和 Exchange 2007 中存在五个服务器角色，而在 Exchange 2013 中，服务器角色的数目减少为三个：客户端访问服务器和邮箱服务器以及 Service Pack 1 的边缘传输服务器角色。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 也能使用 Exchange 2010 边缘传输服务器角色。</td>
</tr>
</tbody>
</table>


Exchange 2013 邮箱服务器包括 Exchange 2010 中所有的服务器组件：客户端访问协议、传输服务、邮箱数据库和统一消息服务（客户端访问服务器将从传入呼叫生成的 SIP 通信重定向至邮箱服务器）。有关 Exchange 2013 邮箱服务器的详细信息，请参阅[邮箱服务器](mailbox-server-exchange-2013-help.md)。

客户端访问服务器提供身份验证、代理和有限重定向服务，并提供所有常见的客户端访问协议：HTTP、POP、IMAP 和 SMTP。客户端访问服务器是无状态的瘦服务器，不执行任何数据渲染。客户端访问服务器上从不会排队或存储任何内容。有关新 Exchange 2013 体系结构的详细信息，请参阅 [Exchange 2013 中的新增功能](what-s-new-in-exchange-2013-exchange-2013-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/JJ898581.warning(EXCHG.150).gif" title="警告" alt="警告" />警告：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>客户端访问服务器在外围网络中不受支持，并且必须部署在您的内部 Active Directory 环境中。每个包含邮箱服务器的 Active Directory 站点还必须包含客户端访问服务器。</td>
</tr>
</tbody>
</table>


因为存在这些体系结构更改，所以对客户端连接进行了一些更改。首先，RPC/TCP 不再是受支持的直接访问协议。这意味着所有 Outlook 连接必须通过 RPC over HTTPS（也称为 Outlook 无处不在）实现；Exchange 2013 SP1 和 Outlook 2013 SP1 则必须通过 MAPI over HTTP 实现连接。这些变更的结果是无需在客户端访问服务器上具有 RPC 客户端访问服务。此外，站点恢复解决方案所需的命名空间数比 Exchange 2010 中所需的少，并且不再需要提供 RPC 客户端访问服务相关性。另外，Outlook 客户端不再连接到服务器的完全限定域名 (FQDN)（在所有以前版本的 Exchange 中都这样做）。使用自动发现功能，Outlook 找到一个新的连接点，该连接点由用户的邮箱 GUID + @ + 用户主 SMTP 地址的域部分组成。经过这种更改，用户不太可能会看到“管理员更改了您的邮箱。请重新启动。”这样的消息。Exchange 2013 仅支持 Outlook 2007 和更高版本。

## 客户端访问服务器功能

Exchange 2013 中客户端访问服务器的功能非常类似于前门，允许所有客户端请求并将它们路由到正确的活动邮箱数据库。客户端访问服务器提供网络安全功能（如安全套接字层 (SSL) 和客户端身份验证），并通过重定向和代理功能管理客户端连接。客户端访问服务器会验证客户端连接，并且在大多数情况下，将代理对保存数据库（包含用户邮箱）当前活动副本的邮箱服务器的请求。在某些情况下，客户端访问服务器可能会将请求重定向到不同位置或运行 Exchange Server 的更新版本的更适合的客户端访问服务器。

客户端访问服务器具有以下功能：

  - **无状态服务器** 在早期版本的 Exchange 中，许多客户端访问协议都需要会话相关性。例如，Outlook Web App 要求来自特定客户端的所有请求都由负载平衡的客户端访问服务器数组中的特定客户端访问服务器处理。在 Exchange 2013 中，客户端访问服务器是无状态的。也就是说，由于对邮箱的所有处理都是在邮箱服务器上进行的，因此客户端访问服务器数组中的哪个客户端访问服务器接收每个客户端请求无关紧要。功能上的这种更改意味着负载平衡器级别不再需要会话相关性。这允许使用负载平衡技术（如 DNS 轮循机制）提供的简单技术平衡到客户端访问服务器的入站连接。还允许硬件负载平衡设备显著支持更多并发连接。

  - **连接池** 客户端访问服务器处理客户端身份验证并将身份验证数据发送到邮箱服务器。客户端访问服务器用来连接到邮箱服务器的帐户是属于 Exchange Server 组成员的特权帐户。这使得客户端访问服务器能够有效地通过池连接到邮箱服务器。一个数组的客户端访问服务器可以处理来自 Internet 的数百万计的客户端连接，但与早期版本的 Exchange 相比，用于代理对邮箱服务器的请求的连接数要少的多。这提高了处理效率并减少了端到端的延迟。

## 客户端访问服务器上的管理任务

在 Exchange 2013 中，可以在客户端访问服务器上执行几项关键任务。数字证书管理主要在客户端访问服务器上执行，Exchange ActiveSync、POP3 和 IMAP4 的一些客户端协议管理也在客户端访问服务器上处理。

