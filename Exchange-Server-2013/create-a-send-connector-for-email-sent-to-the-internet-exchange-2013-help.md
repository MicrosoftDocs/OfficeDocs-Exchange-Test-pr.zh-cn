---
title: '为发送到 Internet 的电子邮件创建发送连接器: Exchange 2013 Help'
TOCTitle: 为发送到 Internet 的电子邮件创建发送连接器
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50490887
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 为发送到 Internet 的电子邮件创建发送连接器

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-01-23_

默认情况下，Microsoft Exchange Server 2013 不允许您将邮件发送到域外部。要将邮件发送到域外部，您需要创建发送连接器。下图显示了创建发送连接器以向 Internet 发送邮件时的邮件流。

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

对本程序使用的方案感兴趣？请参阅下列主题：

  - [配置邮件流和客户端访问](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 在开始之前，您需要知道什么？

  - 估计完成时间：15 分钟

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


## 您想执行什么操作？

## 使用 EAC 为发送到 Internet 的电子邮件创建发送连接器

1.  在 EAC 中，导航到“邮件流”\>“发送连接器”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新发送连接器”向导中，指定发送连接器的名称，然后选择“Internet”作为“类型”。单击“下一步”。

3.  验证是否选择了“与收件人域关联的 MX 记录”，这可指定连接器使用域名系统 (DNS) 路由邮件。单击“下一步”。

4.  在“地址空间”下，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“添加域”窗口中，确保 SMTP 作为“类型”列出。对于“完全限定域名(FQDN)”，输入 \*，指示此发送连接器应用于发送到任何域的邮件。单击“保存”。

5.  确保“作用域发送连接器”未选中，然后单击“下一步”。

6.  对于“源服务器”，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在“选择服务器”窗口中，选择将用于通过客户端访问服务器将邮件发送到 Internet 的邮箱服务器，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在选择了服务器之后，单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。单击“确定”。

7.  单击“完成”。

创建发送连接器后，它会出现在发送连接器列表中。

## 使用命令行管理程序通过客户端访问服务器路由邮件

在 Exchange 2013 中，可以使用 **Set-SendConnector** cmdlet 的 *FrontendProxyEnabled* 参数通过客户端访问服务器路由出站邮件。默认情况下，此参数不设置为 `$true`，但在许多情况下，它可合并并简化邮件流，尤其是在您使用的环境包含大量消息服务器时。

此示例在发送连接器上将 *FrontendProxyEnabled* 参数设置为 `$true`。

    Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true

## 您如何知道这有效？

要验证是否已成功为发送到 Internet 的电子邮件创建发送连接器，通过您的某个用户将邮件发送给外部收件人并验证该邮件是否成功到达。

## 详细信息

[发送连接器](send-connectors-exchange-2013-help.md)

[创建发送连接器以通过智能主机路由出站电子邮件](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

