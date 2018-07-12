---
title: 'Outlook Web App 中的信息权限管理: Exchange 2013 Help'
TOCTitle: Outlook Web App 中的信息权限管理
ms:assetid: 60a49dab-17ac-4d2c-9b41-7d87250d6c00
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876891(v=EXCHG.150)
ms:contentKeyID: 50490691
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Web App 中的信息权限管理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

信息工作者越来越多地使用电子邮件交换敏感信息。为帮助保护此类信息的安全，组织可以使用信息权限管理 (IRM) 对邮件内容应用持久保护。在 Microsoft Exchange Server 2010 之前，对 IRM 保护的有效使用仅限于 Outlook 客户端。Exchange Server 2007 中，Microsoft Outlook Web Access 用户需要下载 Microsoft Internet Explorer 的权限管理外接程序才能访问受 IRM 保护的内容。

在 Exchange 2013 中，Outlook Web App 中的 IRM 允许用户访问 Exchange 提供的丰富 IRM 功能来对邮件内容应用持久 IRM 保护。

在 Outlook Web App 中提供了以下 IRM 功能：

  - **发送受 IRM 保护的邮件**   如下图所示，Outlook Web App 用户可以使用权限下拉列表，选择要应用于邮件的权限策略模板。这可以使用户从 Outlook Web App 中发送受 IRM 保护的邮件。客户端访问服务器将对邮件进行 IRM 保护。
    
    ![从 OWA 发送受 IRM 保护的邮件](images/Dd876891.fa8cabb5-c049-46dc-8b29-9d9957dbfd3e(EXCHG.150).gif "从 OWA 发送受 IRM 保护的邮件")  

  - **受 IRM 保护的附件**   用户从 Outlook Web App 中发送受 IRM 保护的邮件时，邮件中附加的任何文件也会受到相同的 IRM 保护，并且使用与邮件相同的权限策略模板进行保护。在 Exchange 2013 中，IRM 保护应用于与 Microsoft OfficeWord、Excel 和 PowerPoint 相关联的文件，以及 .xps 文件和电子邮件。仅当附件尚未受 IRM 保护时，可将 IRM 保护应用于该附件。若要了解有关 Active Directory 权限管理服务 (AD RMS) 权限策略模板的详细信息，请参阅[信息权限管理](information-rights-management-exchange-2013-help.md)。
    
    > [!NOTE]
    > Outlook Web App 中的 IRM 仅保护此节中提到的受支持文件附件。使用不支持的文件格式的附件将不受保护。当 Outlook Web App 用户要保护某封邮件但附加的文件类型不受支持时，系统将显示通知，告知用户仅可保护受支持的文件类型。
    
    > [!important]
    > IRM 保护不可应用于已使用 S/MIME 签名或加密的邮件。若要应用 IRM 保护，必须从邮件中删除 S/MIME 签名和加密。对于受 IRM 保护的邮件，此规则同样适用；用户不能使用 S/MIME 对这些邮件进行签名或加密。


  - **读取受 IRM 保护的邮件**   发件人使用组织的 AD RMS 群集保护的邮件呈现在 Outlook Web App 的预览窗格中。无需安装任何外接程序，且计算机无需在 AD RMS 部署中注册。在用户打开邮件或在预览窗格中查看邮件时，将使用由预许可代理添加的使用许可证解密该邮件。解密后，邮件将显示在预览窗格中。如果预许可不可用，Outlook Web App 将从 AD RMS 服务器申请一个许可证，然后呈现该邮件。在 Outlook Web App 中读取受 IRM 保护的附件时，Web-Ready 文档查看不可用。
    
    > [!NOTE]
    > Outlook Web App 中的 IRM 不能阻止用户以 Outlook 和其他 Office 应用程序的方式使用打印屏幕功能捕捉屏幕。这会影响“提取”权限，如果在 AD RMS 权限策略模板中指定，该权限可阻止对邮件内容进行复制。


  - **跨浏览器多平台 IRM 支持**Outlook Web App 中的 IRM 提供跨浏览器的多平台 IRM 支持。Outlook Web App 支持的所有浏览器都支持 Exchange 2013 中的 IRM，包括 Apple Macintosh 和 Linux 操作系统。若要了解有关支持的浏览器和操作系统的详细信息，请参阅[支持 Outlook Web App 的浏览器](https://go.microsoft.com/fwlink/p/?linkid=129362)。

  - **WebReady 文档查看**   在 Exchange 2013 中，用户可以使用 WebReady 文档查看来查看支持的受 IRM 保护的附件。这使用户可以使用关联应用程序查看受支持的附件，而不必下载附件。

若要了解与管理 IRM 相关的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 启用 Outlook Web App 中的 IRM

若要启用 Outlook Web App 中的 IRM，必须将联合邮箱（由 Exchange 2013 安装程序创建的系统邮箱）添加到 AD RMS 中的超级用户组。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。这使 Exchange 2013 服务器可以访问受 IRM 保护的邮件。

还必须使用 Outlook Web App 命令行管理程序中的 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet 启用 Exchange 中的 IRM。这将为 Outlook Web App 组织启用 Exchange 2013 中的 IRM。可以为 Outlook Web App 虚拟目录禁用或启用 Outlook Web App 中的 IRM。还可以将 Outlook Web App 中的 IRM 控制在以下粒度级别：

  - **每个 Outlook Web App 虚拟目录：** 若要为 Outlook Web App 虚拟目录启用或禁用 Outlook Web App 中的 IRM，请使用 **Set-OWAVirtualDirectory** cmdlet 并将 *IRMEnabled* 参数设置为 `$false` 或 `$true`（默认）。此操作可以为 Exchange 2013 客户端访问服务器上的一个虚拟目录禁用 Outlook Web App 中的 IRM，同时保持其他客户端访问服务器上的另一个虚拟目录上的 IRM 为启用状态。

  - **每个 Outlook Web App 邮箱策略：** 若要为 Outlook Web App 邮箱策略启用或禁用 Outlook Web App 中的 IRM，请使用 **Set-OWAMailboxPolicy** cmdlet 并将 *IRMEnabled* 参数设置为 `$false` 或 `$true`（默认）。此操作通过为用户组分配不同的 Outlook Web App 邮箱策略，可以对一组用户启用 Outlook Web App 中的 IRM，而同时对另一组用户禁用 IRM。

有关详细信息，请参阅[启用或禁用客户端访问服务器上的信息权限管理](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md)。

