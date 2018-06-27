---
title: '配置跨林发送连接器: Exchange 2013 Help'
TOCTitle: 配置跨林发送连接器
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52061516
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 配置跨林发送连接器

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2013-02-21_

在 Active Directory 中，*林*表示目录服务的外边界。可以创建发送连接器以启用林间的通信。在此示例中，连接器使用基本身份验证。

有关配置连接器相关的其他管理任务，请参阅[连接器](connectors-exchange-2013-help.md)。

对本程序使用的方案感兴趣？请参阅以下主题：

  - [在跨林拓扑中部署 Exchange 2013](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：20 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“发送连接器”和“接收连接器”条目。

  - 如果开始安装，请参阅[部署 Exchange 2013 的新安装](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)。在安装之后，可以使用本主题中的步骤创建连接器以配置跨林拓扑。

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


## 您想执行什么操作？

## 在每个林中创建一个用户帐户

必须在每个林中创建一个用于基本身份验证的用户帐户。在每个林中创建一个帐户，将每个帐户添加到用于通信的 Exchange Server 的通用安全组。发送连接器使用该帐户向其他林中接收邮件的服务器进行身份验证。例如，提供一个用户主体名称 (UPN) 为 FourthCoffee@Contoso.com 的用户帐户作为凭据，向 Contoso 域中的 Exchange 服务器发送邮件时，Fourth Coffee 域中的 Exchange 服务器必须使用这些凭据进行身份验证。

## 使用 EAC 可创建将电子邮件路由到另一个 Exchange 2013 林的发送连接器

使用基本身份验证建立跨林邮件流。

1.  在 EAC 中，导航到“邮件流”\>“发送连接器”。单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新发送连接器”向导中，指定发送连接器的名称，然后选择“内部”作为“类型”。单击“下一步”。

3.  选择“通过智能主机路由邮件”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加智能主机”窗口中，在第二个林中指定目标服务器的 IP 地址，例如 64.4.6.100。单击“保存”，然后单击“下一步”。
    
    对于“智能主机身份验证”，选择“基本身份验证”，并提供用户名和密码。在此处，可以选择“仅在启动 TLS 后提供基本身份验证”以确保 TLS 上通信的安全。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果在 TLS 上使用基本身份验证，则目标服务器必须配置为使用 X.509 证书。</td>
    </tr>
    </tbody>
    </table>


4.  在“地址空间”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加域”窗口中，确保 SMTP 作为“类型”列出。对于“完全限定域名 (FQDN)”，输入接收域，例如 fourthcoffee.com。单击“保存”，然后单击“下一步”。

5.  对于“源服务器”，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“选择服务器”窗口中，选择要使用的服务器，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。单击“确定”。

6.  单击“完成”。连接器显示在发送连接器列表中。

创建发送连接器后，在第二个林中创建发送连接器以将邮件发送到原始林。在此情况下，您指定的完全限定域名 (FQDN) 将成为第一个林的域名。例如，contoso.com。

## 使用命令行管理程序设置发送连接器上的权限

此示例在命令行管理程序中使用 Enable-CrossForestConnector.ps1 脚本来设置要在跨林拓扑中使用的发送连接器上的权限。

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## 您如何知道操作成功？

要验证是否已成功创建将电子邮件路由到第二个林的发送连接器，请将来自您组织中的用户的邮件（可以使用 Outlook Web App）发送到为“地址空间”指定的域。如果收件人收到了此邮件，那么您已成功配置发送连接器。

## 详细信息

[为发送到 Internet 的电子邮件创建发送连接器](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[发送连接器](send-connectors-exchange-2013-help.md)

