---
title: '查看或配置 Outlook Web App 虚拟目录: Exchange 2013 Help'
TOCTitle: 查看或配置 Outlook Web App 虚拟目录
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50491164
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 查看或配置 Outlook Web App 虚拟目录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-08-12_

您可以使用 EAC 或命令行管理程序查看或配置 Outlook Web App 虚拟目录的属性。

> [!warning]
> 在 Exchange Online 中，管理员无法查看或配置 Outlook Web App 虚拟目录。


如果使用命令行管理程序查看 Outlook Web App 虚拟目录的属性，则返回的信息是可用信息的一个子集。例如，如果使用 **Get-OWAVirtualDirectory** cmdlet 查看属性，Exchange 会返回下列信息：

  - 虚拟目录名

  - 服务器名

  - Exchange 服务器版本

也可以使用可用参数对特定服务器上的特定虚拟目录信息进行检索。有关 **Get-OWAVirtualDirectory** cmdlet 的各项参数的详细信息，请参阅 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/aa998588\(v=exchg.150\))。

如果您使用 EAC 查看某个 Outlook Web App 虚拟目录的属性，将可以查看到该虚拟目录的大多数属性。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 位于[客户端和移动设备权限](clients-and-mobile-devices-permissions-exchange-2013-help.md)主题中的\&quot;Outlook Web App 虚拟目录\&quot;条目。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 EAC 查看或配置 Outlook Web App 虚拟目录属性

1.  在 EAC 中，单击\&quot;服务器\&quot;\>\&quot;虚拟目录\&quot;。
    
    您可以使用下拉列表选择服务器和虚拟目录类型。默认情况下，将显示所有服务器和虚拟目录。

2.  在结果窗格中，单击选择要查看或编辑的虚拟目录，然后单击\&quot;编辑\&quot;。

3.  在\&quot;常规\&quot;选项卡上，可以查看 Outlook Web App 默认网站的各项属性，还可以指定外部 URL 和内部 URL。查看或选择以下选项：
    
      - **服务器**：（只读。）\&quot;服务器\&quot;中显示托管 Outlook Web App 虚拟目录的服务器的名称。
    
      - **版本**：（只读。）\&quot;版本\&quot;中显示虚拟目录所在的 Exchange 服务器的版本。
    
      - **网站**：（只读。）\&quot;网站\&quot;中显示网站的名称。
    
      - **Outlook Web App 版本**    （只读。）\&quot;Outlook Web App 版本\&quot;中显示 Exchange 服务器版本。
    
      - **修改时间**：（只读。）\&quot;修改时间\&quot;显示上次修改虚拟目录的日期和时间。
    
      - **内部 URL**   在此文本框中，指定用于从内部网络访问此网站的 URL。在 Exchange 2013 安装过程中，将自动配置内部 URL。对于面向 Internet 或不面向 Internet 的服务器，默认的内部 URL 设置是 https://\<计算机名称\>/owa。
    
      - **外部 URL**：在此文本框中，指定用于从 Internet 访问此网站的 URL。默认情况下，\&quot;外部 URL\&quot;为空。对于面向 Internet 的客户端访问服务器，应将\&quot;外部 URL\&quot;设置为在该 Active Directory 站点的 DNS 中发布的值。对于未连接到 Internet 的 Exchange 2013 服务器，\&quot;外部 URL\&quot;设置应保留为空。

4.  在\&quot;身份验证\&quot;选项卡上，指定身份验证方法、登录格式和登录域。
    
      - **使用一个或多个标准身份验证方法**：选择此选项可以使用以下一种或多种标准身份验证方法：
        
        **集成 Windows 身份验证**   此方法要求用户拥有有效的 Windows Server 2008 或 Windows Server 2012 用户帐户名和密码来访问信息。不会提示用户输入其帐户名和密码。相反，该服务器会与客户端计算机上安装的 Windows 安全程序包进行协商。集成 Windows 身份验证使服务器在对用户进行身份验证时，不必提示用户提供信息，也不必通过网络传输未加密的信息。若要使用此方法，客户端计算机必须是运行 Exchange 的服务器所处的同一个域的成员，或是 Exchange 服务器所处的域所信任的域的成员。
        
        **Windows 域服务器的摘要式身份验证**：此方法以哈希值的形式通过网络传输密码，以提高安全性。摘要式身份验证只能在 Windows Server 2008 和 Windows Server 2012 域中用于那些帐户存储在 Active Directory 中的用户。有关摘要式身份验证的详细信息，请参阅 Windows Server 文档。
        
        **基本身份验证(密码以明文形式发送)**：此方法是 HTTP 规范定义的一种简单身份验证机制，在将用户凭据发送到服务器之前为用户的登录名和密码进行编码。为了确保密码尽可能安全，应在客户端计算机与已安装客户端访问服务器角色的服务器之间使用安全套接字层 (SSL) 加密。
    
      - **使用基于表单的身份验证**：基于表单的身份验证可为 Outlook Web App 虚拟目录提供增强的安全性。基于表单的身份验证将为 Outlook Web App 创建登录页。可以配置基于表单的身份验证所使用的登录提示类型。例如，可以将基于表单的身份验证配置为要求用户以域名\\用户名的格式在 Outlook Web App 登录页上提供域和用户名的信息。
        
        > [!important]
        > 除非启用 SSL，否则基于表单的身份验证不会提供安全通道。
        
        选择下列选项之一：
        
        **域名\\用户名**   此选项要求用户以\&quot;域名\\用户名\&quot;的格式输入域名和用户名。例如，对于在域 Contoso 中的名为 Kweku 用户，登录名将是 contoso\\kweku。
        
        **用户主体名称 (UPN)** 如果指定了用户主体名称 (UPN) 登录格式，则 Outlook Web App 登录页面上的\&quot;用户名\&quot;框将引导用户输入电子邮件地址，例如 kweku@contoso.com。如果用户的 UPN 与电子邮件地址不完全相同，用户将无法使用 **PrincipalName** 登录提示来访问 Outlook Web App。最佳做法是仅当用户的 UPN 与电子邮件地址相符时，才使用 **PrincipalName** 登录提示。
        
        **仅用户名** 用户仅输入用户名，无需输入域名，例如 Kweku。如果对基于表单的身份验证使用\&quot;仅用户名\&quot;登录提示，还必须要指定\&quot;登录域\&quot;属性。\&quot;登录域\&quot;属性决定了用户尝试登录 Outlook Web App 时要使用的默认域。例如，如果默认域为 Contoso，并且名为 Kweku 的域用户登录到 Outlook Web App，则只需输入 Kweku 作为用户名即可。服务器将使用默认的域 Contoso。如果用户不是 Contoso 域的成员，则必须输入域名和用户名。

5.  在\&quot;功能\&quot;选项卡上，指定要在虚拟目录上为 Outlook Web App 用户启用或禁用的功能。
    
    > [!NOTE]
    > 各个用户的功能设置将覆盖虚拟目录设置。通过使用 <strong>Set-CASMailbox</strong> cmdlet，或通过使用 Outlook Web App 邮箱策略，可以更改单个用户的分段设置。有关详细信息，请参阅 <a href="outlook-web-app-mailbox-policies-exchange-2013-help.md">Outlook Web App 邮箱策略</a>。
    
    使用复选框来启用或禁用功能。默认情况下，显示最常用的功能。要查看可以启用或禁用的所有功能，可单击\&quot;更多选项\&quot;。
    
    > [!NOTE]
    > 通过使用&amp;quot;高级客户端&amp;quot;复选框启用或禁用 Outlook Web App 标准版本的选项已被废除，将从设置中删除。始终启用 Outlook Web App 标准版本。


6.  在\&quot;文件访问\&quot;选项卡上，使用复选框配置用户的文件访问和查看选项。文件访问使用户可以打开或查看附加到电子邮件的文件的内容。
    
    可根据用户是否已经登录公共或私有计算机来控制文件访问。用户用于选择专用计算机访问或公用计算机访问的选项只有在使用基于表单的身份验证时才可用。所有其他形式的身份验证默认设置为私人计算机访问。
    
      - \&quot;直接文件访问\&quot;   如果要启用直接文件访问，请选中此复选框。直接文件访问，允许用户打开被附加到电子邮件的文件。
    
      - \&quot;WebReady 文档查看\&quot; 如果希望将支持的文档转换为 HTML 并且在 Web 浏览器中显示，请选中此复选框。
    
      - \&quot;转换器可用时强制进行 WebReady 文档查看\&quot;   如果希望用户在查看应用程序中打开文档前，将这些文档强制转换为 HTML 并且在 Web 浏览器中显示，请选中此复选框。只有启用了直接文件访问才能在查看应用程序中打开文档。

7.  单击\&quot;保存\&quot;更新策略。

## 使用命令行管理程序配置 Outlook Web 应用程序虚拟目录属性

本示例将针对服务器 Contoso 上的默认 Outlook Web App 虚拟目录启用基于表单的身份验证。

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

有关语法和参数的详细信息，请参阅 [Set-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/bb123515\(v=exchg.150\))。

## 使用命令行管理程序查看 Outlook Web 应用程序虚拟目录属性

本示例允许您在 Exchange 组织中所有安装了客户端访问服务器角色的计算机上，查看所有 Internet 信息访问 (IIS) 网站中的所有 Outlook Web App 虚拟目录的属性。

    Get-OWAVirtualDirectory

本示例让您查看本地 Exchange 服务器上的默认 IIS 网站中的 Outlook Web App 虚拟目录的属性。

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

本示例让您查看特定 Exchange 服务器上的某个 IIS 网站中所有 Outlook Web App 虚拟目录的属性。

    Get-OWAVirtualDirectory -server <Exchange Server Name>

本示例让您查看 Exchange 组织中所有客户端访问服务器上的所有 IIS 网站中的每个 Outlook Web App 虚拟目录的属性值。

    Get-OWAVirtualDirectory | format-list

有关语法和参数的详细信息，请参阅 [Get-OwaVirtualDirectory](https://technet.microsoft.com/zh-cn/library/aa998588\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已成功编辑了 Outlook Web App 虚拟目录：

1.  在 EAC 中，单击\&quot;服务器\&quot;\>\&quot;虚拟目录\&quot;，然后选择特定的 Outlook Web App 虚拟目录。

2.  单击\&quot;编辑\&quot;按钮查看虚拟目录的属性。

3.  单击\&quot;保存\&quot;或\&quot;取消\&quot;关闭属性页面。

