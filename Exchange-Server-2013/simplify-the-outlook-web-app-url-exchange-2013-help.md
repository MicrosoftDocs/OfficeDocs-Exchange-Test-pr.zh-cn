---
title: '简化 Outlook Web App 的 URL: Exchange 2013 Help'
TOCTitle: 简化 Outlook Web App 的 URL
ms:assetid: 5fb6a873-f3cf-4f82-87d1-2ff6e47a0080
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa998359(v=EXCHG.150)
ms:contentKeyID: 54652285
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 简化 Outlook Web App 的 URL

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-07-16_

**摘要：**使用本文中的过程简化你的组织用户用于访问 Exchange 2013 中的 OWA 的 URL。

你可以简化用户用于访问其 Exchange Server 2013 邮箱的 MicrosoftOutlook Web App URL。

若要简化用户对 Outlook Web App 的访问，可能需要配置 Outlook Web App 网页（通常是采用 IIS 的默认网站），以便将用户自动重定向到 https。\&quot;使用 IIS 管理器简化 Outlook Web App URL 并强制执行到 SSL 的重定向\&quot;部分的步骤可将对 http://*服务器* 的请求重定向到 https://*服务器*/owa。为了帮助保护客户端与服务器之间发送的信息，默认网站在安装时设置为需要安全套接字层 (SSL)。

在 Windows Server 2008 中配置来自顶级目录的重定向时，设置将传播到低级别目录。例如，当您将默认网站配置为重定向到 /owa 虚拟目录时，您配置的设置也会出现在所有虚拟目录（如 /Autodiscover、/Exchange 和 /Public）的 HTTP 重定向页面上。因此，除了希望重定向的虚拟目录之外，您必须从所有虚拟目录中删除重定向。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题\&quot;Outlook Web App 权限\&quot;部分中的\&quot;IIS 管理器\&quot;条目。

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


## 步骤 1：使用 IIS 管理器简化 Outlook Web App URL 并强制重定向到 SSL

1.  启动 IIS 管理器。

2.  依次展开本地计算机、\&quot;站点\&quot;，然后单击\&quot;默认网站\&quot;。

3.  在\&quot;默认网站主页\&quot;窗格底部，单击\&quot;功能视图\&quot;（如果此选项尚未选中）。

4.  在\&quot;IIS\&quot;部分中，双击\&quot;HTTP 重定向\&quot;。

5.  选中\&quot;将请求重定向到此目标\&quot;复选框。

6.  键入 /owa 虚拟目录的绝对路径。例如，键入 **https://mail.contoso.com/owa**。

7.  在\&quot;重定向行为\&quot;下，选中\&quot;仅将请求重定向到此目录(非子目录)中的内容\&quot;复选框。

8.  在\&quot;状态代码\&quot;列表中，单击\&quot;已找到 (302)\&quot;。

9.  在\&quot;操作\&quot;窗格中，单击\&quot;应用\&quot;。

10. 单击\&quot;默认网站\&quot;。

11. 在\&quot;默认网站主页\&quot;窗格中，双击\&quot;SSL 设置\&quot;。

12. 在\&quot;SSL 设置\&quot;中，清除\&quot;要求 SSL\&quot;。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>如果不清除&amp;quot;要求 SSL&amp;quot;，则用户在输入不安全的 URL 时不会进行重定向。而是会收到拒绝访问错误。</td>
    </tr>
    </tbody>
    </table>


## 步骤 2：从虚拟目录中删除重定向

若要从虚拟目录中删除重定向，请执行以下步骤：

1.  打开命令提示符窗口。

2.  导航到 \<*窗口目录*\>\\System32\\Inetsrv。

3.  运行以下命令：
    
    1.  `appcmd set config "Default Web Site/autodiscover" /section:httpredirect /enabled:false -commit:apphost`
    
    2.  `appcmd set config "Default Web Site/ecp" /section:httpredirect /enabled:false -commit:apphost`
    
    3.  `appcmd set config "Default Web Site/ews" /section:httpredirect /enabled:false -commit:apphost`
    
    4.  `appcmd set config "Default Web Site/owa" /section:httpredirect /enabled:false -commit:apphost`
    
    5.  `appcmd set config "Default Web Site/oab" /section:httpredirect /enabled:false -commit:apphost`
    
    6.  `appcmd set config "Default Web Site/powershell" /section:httpredirect /enabled:false -commit:apphost`
    
    7.  `appcmd set config "Default Web Site/rpc" /section:httpredirect /enabled:false -commit:apphost`
    
    8.  `appcmd set config "Default Web Site/rpcwithcert" /section:httpredirect /enabled:false -commit:apphost`
    
    9.  `appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:httpredirect /enabled:false -commit:apphost`

4.  通过运行命令 `iisreset/noforce` 来完成。

在通过顶级目录配置重定向时，可能会在 \<*驱动器*\>\\Program Files\\Microsoft\\Exchange Server\\\<*版本*\>\\ClientAccess\\oab 下创建 web.config 文件。如果发生这种情况并且将来删除重定向，则在用户单击\&quot;发送和接收\&quot;时，Outlook 可能会冻结。若要避免删除重定向之后发生这种情况，请在 \<*驱动器*\>\\Program Files\\Microsoft\\Exchange Server\\\<*版本*\>\\ClientAccess\\oab 中删除 web.config 文件。

## 您如何知道操作成功？

为了验证您已成功简化 Outlook Web App URL 并将其重定向到 SSL 连接，请执行以下操作：

1.  打开 Web 浏览器，并按照格式 http://\<*URL*\> 输入 Outlook Web App 的新 URL。

2.  您应该通过 SSL 连接重定向到 Outlook Web App 登录页。

