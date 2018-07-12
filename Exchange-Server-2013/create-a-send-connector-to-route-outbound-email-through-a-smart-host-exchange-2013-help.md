---
title: '创建发送连接器以通过智能主机路由出站电子邮件: Exchange 2013 Help'
TOCTitle: 创建发送连接器以通过智能主机路由出站电子邮件
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50490481
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 创建发送连接器以通过智能主机路由出站电子邮件

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-07_

在某些情况下，可能需要通过第三方智能主机路由电子邮件，例如，当您有一个网络设备，并希望对出站邮件执行策略检查。

> [!NOTE]  
> 第三方智能主机必须使用 SMTP 进行传输。如果不是这样，则应使用外部连接器或传递代理连接器。


对本程序使用的方案感兴趣？请参阅下列主题：

  - [配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“发送连接器”条目。

  - 如果开始安装，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。在安装之后，可以使用本主题中的步骤创建出站连接器。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 可以使用 EAC 创建通过智能主机路由出站电子邮件的发送连接器

1.  在 EAC 中，导航到“邮件流”\>“发送连接器”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建发送连接器”向导中，指定发送连接器的名称，然后对“类型”选择“自定义”。通常在要将邮件路由到未运行 Microsoft Exchange Server 2013 的计算机时进行此选择。单击“下一步”。

3.  选择“通过智能主机路由邮件”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加智能主机”窗口中，指定 IP 地址（如 192.168.100.1）或完全限定域名 (FQDN)，如 contoso.com。单击“保存”。
    
    对于“智能主机身份验证”，选择智能主机所需的身份验证类型。如果选择“基本身份验证”，则必须提供用户名和密码。
    
    > [!NOTE]  
    > 如果选择基本身份验证，我们建议您使用加密连接，因为基本身份验证将以明文方式发送用户名和密码。


4.  在“地址空间”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加域”窗口中，确保 SMTP 作为“类型”列出。对于“完全限定域名 (FQDN)”，输入 \* 指定将此发送连接器应用到发送给任何域的邮件。单击“保存”。

5.  对于“源服务器”，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“选择服务器”窗口中，选择将用于通过客户端访问服务器将邮件发送到 Internet 的邮箱服务器，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。选择服务器后，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。单击“确定”。

6.  单击“完成”。

创建发送连接器后，它会出现在发送连接器列表中。

## 您如何知道这有效？

要验证是否已成功创建可通过智能主机路由出站电子邮件的发送连接器，请将来自您组织中的用户的邮件发送（可以使用 Outlook Web App）到为“地址空间”指定的域。如果收件人收到了此邮件，那么您已成功配置发送连接器。

## 详细信息

[为发送到 Internet 的电子邮件创建发送连接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[发送连接器](send-connectors-exchange-2013-help.md)

