---
title: '使用无人参与的模式安装 Exchange 2013: Exchange 2013 Help'
TOCTitle: 使用无人参与的模式安装 Exchange 2013
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50490312
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 使用无人参与的模式安装 Exchange 2013

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-06-19_

要执行无人参与安装，您必须从命令提示符安装 Microsoft Exchange Server 2013。有关规划和部署 Exchange 2013 的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

我们建议在您组织的内部 Active Directory 林以外的外围网络中安装边缘传输角色。虽然您可以在联合域的计算机上安装边缘传输服务角色，但是这样做仅可启用 Windows 功能和设置的域管理。边缘传输角色本身不使用 Active Directory。相反，它使用 Active Directory 轻型目录服务 (AD LDS) Windows 功能存储配置和收件人信息。有关边缘传输角色的详细信息，请参阅[边缘传输服务器](edge-transport-servers-exchange-2013-help.md)。

> [!TIP]  
> 你是否曾听说过 Exchange Server 部署助理？它是一款免费的联机工具，它将询问您一些问题并专门为您创建自定义部署检查表，以帮助您在组织中快速部署 Exchange 2013。若您想要了解关于它的详细信息，请转到 <a href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 部署助理</a>。


> [!NOTE]  
> 在运行 Exchange 2013 的计算机上安装了任意服务器角色之后，不能再使用 Exchange 2013 安装向导为该计算机添加其他服务器角色。如果希望为计算机添加其他服务器角色，则必须使用“控制面板”中的“添加或删除程序”或在命令提示符窗口中使用 Setup.exe。<br />
> 边缘传输角色不能安装在与邮箱或客户端访问服务器角色相同的计算机上。


有关安装之后要完成的任务的信息，请参阅 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

以下信息适用于所有 Exchange 2013 服务器角色。

  - 确保在安装 Exchange 2013 之前阅读了发行说明。有关详细信息，请参阅[Exchange 2013 发行说明](release-notes-for-exchange-2013-exchange-2013-help.md)。

  - 安装 Exchange 2013 的计算机必须使用受支持的操作系统（如 Windows Server 2008 R2 with Service Pack 1 (SP1)、Windows Server 2012 R2 或 Windows Server 2012），拥有足够的磁盘空间，并满足其他要求。有关系统要求的信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)。

  - 要运行 Exchange 2013 设置，您必须安装 Microsoft .NET Framework 4.5、Windows Management Framework 和其他所需的软件。若要了解所有服务器角色的先决条件，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!CAUTION]  
> 在服务器上安装 Exchange 之后，不得更改服务器名称。不支持在安装了 Exchange 服务器角色之后重命名服务器。


以下信息适用于 Exchange 2013 邮箱和客户端访问服务器角色。

  - 估计完成时间：60 分钟

  - 每个组织在 Active Directory 林中都需要至少一台客户端访问服务器和一台邮箱服务器。另外，每个包含邮箱服务器的 Active Directory 站点还必须包含至少一台客户端访问服务器。如果您要分隔服务器角色，我们建议您先安装邮箱服务器角色。

  - 安装 Exchange 2013 的计算机必须是 Active Directory 域的成员。

  - 如果未提前准备 Active Directory 架构，则必须确保您使用的帐户已委派有 Schema Admins 组的成员身份。如果要在组织中安装第一台 Exchange 2013 服务器，您使用的帐户必须拥有 Enterprise Admins 组成员身份。如果您已经准备好架构，但安装的不是组织中的第一台 Exchange 2013 服务器，则使用的帐户必须是“Exchange 2013 Organization Management”管理角色组的成员。
    
    作为委派安装角色组成员的管理员可以部署组织管理角色组成员之前已经设置过的 Exchange 2013 服务器。

以下信息适用于 Exchange 2013 边缘传输服务器角色。

  - 预计完成时间：40 分钟

  - 边缘传输角色在 Exchange 2013 SP1 或更高版本中可用。

  - 您需要在计算机上配置主 DNS 后缀。例如，如果您的计算机的完全限定域名为 edge.contoso.com，计算机的 DNS 后缀是 contoso.com。有关更多信息，请参阅 [缺少主要的 DNS 后缀](primary-dns-suffix-is-missing-exchange-2013-help.md)。

  - Exchange 2007 和 Exchange 2010 中心传输服务器更新之后，您才可以在它们和 Exchange 2013 边缘传输服务器之间创建 EdgeSync 订阅。如果您不安装此更新，EdgeSync 订阅将不会正常工作。有关详细信息，请参阅 [Exchange 2013 系统要求](exchange-2013-system-requirements-exchange-2013-help.md)中的“受支持的共存方案”一节。

  - 确保您使用的帐户是您正在安装边缘传输角色的计算机上本地管理员组中的成员。

## 在无人参与模式下使用 Setup.exe 安装 Exchange 2013

> [!NOTE]  
> 若要下载 Exchange 2013 的最新版本，请参阅 <a href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013 更新</a>。


1.  登录到要安装 Exchange 2013 的计算机。

2.  导航到 Exchange 2013 安装文件的网络位置。

3.  在命令提示符下，运行组织适用的命令。
    
    > [!IMPORTANT]  
    > 如果您启用了用户访问控制 (UAC) 功能，必须从提升的命令提示符运行 <code>Setup.exe</code>。
    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  安装程序在本地将安装文件复制到要安装 Exchange 2013 的计算机。

5.  安装程序检查先决条件，包括要安装的服务器角色所有的特定先决条件。如果未能满足所有先决条件，则安装将失败并返回说明失败原因的错误消息。如果满足所有先决条件，则安装程序会安装 Exchange 2013。

6.  在 Exchange 2013 完成之后重新启动计算机。

7.  通过执行 [Exchange 2013 安装后任务](exchange-2013-post-installation-tasks-exchange-2013-help.md) 中提供的任务完成部署。

## 示例

下面是使用 Setup.exe 的示例：

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    此命令在 Active Directory 中创建名为 MyOrg 的 Exchange 2013 组织，安装客户端访问服务器角色、邮箱服务器角色和管理工具，还接受 Exchange 2013 许可条款。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    此命令在“C:\\Exchange Server”目录下安装客户端访问服务器角色、邮箱服务器角色和管理工具。此命令假设已准备好了 Exchange 2013 组织。

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    此命令在默认安装位置安装客户端访问服务器角色、邮箱服务器角色和管理工具。

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    此命令在默认位置安装边缘传输服务器角色和管理工具。

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    此命令在默认位置安装边缘传输服务器角色和管理工具。

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    此命令从服务器上完全删除 Exchange 2013，并从 Active Directory 上删除此服务器的 Exchange 配置。

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    此命令创建名为 My Org 的 Exchange 组织并为 Active Directory 准备 Exchange 2013。

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    此命令使用 D:\\amd64 作为源目录向现有 Exchange 2013 服务器添加客户端访问服务器角色。

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    此命令使用指定目录中的修补程序更新 ExchangeServer.msi，然后安装客户端访问服务器角色、邮箱服务器角色和管理工具。如果此目录中包含语言包套装，则还会安装该语言包。

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    此命令在安装客户端访问服务器角色、邮箱服务器角色和管理工具的同时，使用域控制器 DC01 对 Active Directory 进行查询并更改操作。

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    此命令使用 ExchangeConfig.txt 文件中的设置安装客户端访问服务器角色。

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    此命令从 Active Directory 删除对象 Exchange03。

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    此命令从 %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging 目录安装朝鲜语统一消息语言包。

## 您如何知道这有效？

要验证是否成功安装 Exchange 2013，请参阅 [验证 Exchange 2013 安装](verify-an-exchange-2013-installation-exchange-2013-help.md)。

遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：[Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612)、 [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542) 或 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)。

您找到所需内容了吗？请花一点时间[向我们发送反馈](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac)，告诉我们您希望找到的信息。

