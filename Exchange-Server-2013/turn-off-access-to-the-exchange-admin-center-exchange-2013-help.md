---
title: '关闭对 Exchange 管理中心的访问: Exchange 2013 Help'
TOCTitle: 关闭对 Exchange 管理中心的访问
ms:assetid: 49f4fa77-1722-4703-81c9-8724ae0334fb
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ218639(v=EXCHG.150)
ms:contentKeyID: 50490490
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 关闭对 Exchange 管理中心的访问

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-05-20_

为了安全起见，一些组织可能需要限制用户通过 Internet 访问 Exchange 管理中心 (EAC)。此过程展示了如何禁用对 EAC 的访问权限。此过程不会阻止用户访问 Outlook Web App 中的选项。

> [!NOTE]  
> 此过程在适用以下步骤的情况下，在 CAS 服务器上完全禁用 EAC 管理员访问权限。如果要为内部用户启用 EAC 管理员，应该单独安装 CAS 服务器，然后使用以下命令将其配置为仅处理内部请求：<br />
> <code>Set-ECPVirtualDirectory -Identity &quot;InternalCAS\ecp (default web site)&quot; -AdminEnabled $True</code>


> [!CAUTION]  
> 此过程仅适用于 Exchange Server 2013 的内部部署。


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [Exchange 和命令行管理程序基础结构权限](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md)主题中的\&quot;Exchange 管理中心连接\&quot;条目。

  - 无法使用 EAC 执行此过程。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令行管理程序关闭对 EAC 的 Internet 访问

此示例关闭了对服务器 CAS01 上的 EAC 的访问。

    Set-ECPVirtualDirectory -Identity "CAS01\ecp (default web site)" -AdminEnabled $false

有关语法和参数的详细信息，请参阅 [Set-EcpVirtualDirectory](https://technet.microsoft.com/zh-cn/library/dd297991\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功关闭对 EAC 的访问，请执行以下操作：

1.  使用 Internet 浏览器，键入用于访问 Outlook Web App 的组织内部或外部 URL，但要将 **/owa** 标识符替换为 **/ecp**。例如，如果用于访问 Outlook Web App 的外部 URL 是 https://primary.tailspintoys.com/owa，请使用 https://primary.tailspintoys.com/ecp。

2.  如果访问已关闭，则将收到\&quot;404 – 找不到网站\&quot;错误。

