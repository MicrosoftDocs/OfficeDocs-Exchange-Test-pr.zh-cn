---
title: '创建“发送连接器”以发送电子邮件给合作伙伴，应用传输层安全性 (TLS): Exchange 2013 Help'
TOCTitle: 创建“发送连接器”以发送电子邮件给合作伙伴，应用传输层安全性 (TLS)
ms:assetid: ff2abefc-dd3e-4431-b947-df942fbf82d9
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657514(v=EXCHG.150)
ms:contentKeyID: 50492058
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建“发送连接器”以发送电子邮件给合作伙伴，应用传输层安全性 (TLS)

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2012-10-15_

如果希望确保与合作伙伴进行安全、加密通信，您可以创建发送连接器，该连接器配置为对发送给合作伙伴域的邮件代理强制执行传输层安全性 (TLS)。TLS 通过互联网提供安全通信。

对本程序使用的方案感兴趣？请参阅下列主题：

  - [配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“发送连接器”条目。

  - 如果开始安装，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。在安装之后，可以使用本主题中的步骤创建出站连接器。

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


## 使用 EAC 创建发送连接器以通过应用的 TLS 发送电子邮件到合作伙伴

要为此情况创建发送连接器，登录 EAC 并执行以下步骤：

1.  在 EAC 中，导航到“邮件流”\>“发送连接器”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建发送连接器”向导中，指定发送连接器的名称，然后为“类型”选择“合作伙伴”。当选择“合作伙伴”时，连接器被配置为仅允许连接到使用 TLS 证书验证。单击“下一步”。

3.  验证是否选择了“与收件人域关联的 MX 记录”，这可指定连接器使用域名系统 (DNS) 路由邮件。单击“下一步”。

4.  在“地址空间”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加域”窗口中，确保 SMTP 作为“类型”列出。在“完全限定的域名 (FQDN)”中，输入您的合作伙伴域的名称。单击“保存”。

5.  对于“源服务器”，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“选择服务器”窗口中，选择将用于通过客户端访问服务器将邮件发送到 Internet 的邮箱服务器，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在选择了服务器之后，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。单击“确定”。

6.  单击“完成”。

在创建了发送连接器之后，它会出现在发送连接器列表中。

## 您如何知道这有效？

要验证您已成功创建发送连接器以发送电子邮件给合作伙伴，通过应用的 TLS 发送贵组织中的用户的邮件给合作伙伴组织的收件人。如果收件人收到邮件，连接器将成功创建。

## 详细信息

[为发送到 Internet 的电子邮件创建发送连接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[创建发送连接器以通过智能主机路由出站电子邮件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

