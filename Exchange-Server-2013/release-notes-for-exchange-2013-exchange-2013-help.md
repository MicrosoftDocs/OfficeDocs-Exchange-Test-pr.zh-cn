---
title: 'Exchange 2013 发行说明: Exchange 2013 Help'
TOCTitle: Exchange 2013 发行说明
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50490101
ms.date: 04/17/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 发行说明

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2018-04-16_

欢迎使用 Microsoft Exchange Server 2013！本主题包含您要成功部署 Exchange 2013 而需要了解的重要信息。在开始部署之前，请完整阅读本主题。

本主题包含以下各部分：

  - 安装和部署

  - Exchange 命令行管理程序

  - 邮箱

  - 公用文件夹

  - 邮件流

  - 客户端连接

  - Exchange 2010 共存

## 安装和部署

  - **msExchProductId 不会反映已安装的 Exchange 2013 的版本：** 在 Exchange 扩展您的 Active Directory 架构并准备 Exchange Active Directory 后，系统会更新若干个属性，以便显示准备工作已完成。其中一个属性就是 *msExchangeProductId*，它位于 `Configuration` 命名上下文中的 `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` 容器下。如果您要安装的 Exchange 2013 版本中没有引入 Active Directory 架构更改，则此属性不会进行更新，或可能会显示一个非预期的值。如果此值与要安装的 Exchange 2013 的版本不相符，则可能会产生混淆。
    
    发生这种行为属情理之中，因为 *msExchProductId* 的值不会反映要安装的 Exchange 2013 的版本。此属性反映的是最后更改 Active Directory 架构的 Exchange 2013 版本。为了避免混淆，我们建议您按照[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)的[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)部分中的步骤操作，验证您的 Active Directory 是否已更新且已为要安装的 Exchange 2013 版本做好了准备。

  - **安装程序错误地要求安装 .NET Framework 4.0**   如果您在计算机未安装 .NET Framework 的情况下安装 Exchange 2013，安装程序会错误地要求您安装 .NET Framework 4.0，而实际上需要安装的是 .NET Framework 4.5 或更高版本。
    
    要解决此问题，请安装 .NET Framework 4.5 或更高版本。您不需要安装 .NET Framework 4.0。有关先决条件的完整列表，请参阅 [Exchange 2013 先决条件](exchange-2013-prerequisites-exchange-2013-help.md)。

  - **Exchange XML 应用程序配置文件在累积更新安装过程中会被覆盖**   当您安装 Exchange 累积更新或 Service Pack 时，您在 Exchange XML 应用程序配置文件中对每个服务器进行的任何自定义设置（例如，客户端访问服务器上的 web.config 文件或邮箱服务器上的 EdgeTransport.exe.config 文件）都将被覆盖。请确保保存此信息，以便在安装后可轻松地重新配置服务器。安装 Exchange 累积更新或 Service Pack 后，您必须重新配置这些设置。

  - **使用委派管理权限安装 Exchange 会导致安装程序失败** 仅当委派安装角色组成员的用户尝试在预先设置的服务器上安装 Exchange 时，安装程序失败。之所以发生这种情况，是因为委派安装组缺少在 Active Directory 中创建和配置特定对象所需的权限。
    
    要解决该问题，请执行下列操作之一：
    
      - 将安装 Exchange 的用户添加到 Domain Admins Active Directory 安全组。
    
      - 通过属于组织管理角色组成员的用户安装 Exchange。

有关如何安装 Exchange 2013 的详细信息，请参阅[规划和部署](planning-and-deployment-for-exchange-2013-installation-instructions.md)。

## Exchange 命令行管理程序

  - **命令行管理程序意外加载 Exchange 2007 或 Exchange 2010 cmdlet** 以前，在 Exchange 2013 服务器上打开命令行管理程序将导致该命令行管理程序打开到本地服务器或者运行 Exchange 2013 的另一台服务器的连接。当进行连接时，将加载 Exchange 2013 cmdlet。启动 Exchange 2013 CU11 时，命令行管理程序将连接到登录用户邮箱所在的 Exchange 服务器。如果登录用户没有邮箱，命令行管理程序将连接到 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 仲裁邮箱所在的服务器。目标服务器可以是任何受支持的 Exchange 版本。这意味着如果登录用户的邮箱（或者如果用户没有邮箱，则是仲裁邮箱）位于 Exchange 2010 服务器上，则命令行管理程序将连接到该服务器并加载 Exchange 2010 cmdlet。这可能会阻止您执行某些任务，因为 Exchange 2013 cmdlet 不能管理 Exchange 2010 配置或服务器。
    
    从 Exchange 2013 CU11 开始，此行为是经过设计的。若要确保命令行管理程序加载 Exchange 2013 cmdlet，请将登录用户的邮箱移动到 Exchange 2013。如果登录用户没有邮箱，则将 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 仲裁邮箱移动到 Exchange 2013 服务器。
    
    有关如何移动仲裁邮箱的详细信息，请参阅 Exchange 团队博客上的 [Exchange 命令行管理程序和邮箱定位](https://go.microsoft.com/fwlink/?linkid=717722)。

## 邮箱

  - **运行不同版本的 Exchange 的邮箱服务器可以添加到同一个数据库可用性组** **Add-DatabaseAvailabilityGroupServer** cmdlet 和 Exchange 管理员中心错误地允许 Exchange 2013 服务器添加到基于 Exchange 2016 的数据库可用性组 (DAG)，反之亦然。Exchange 仅支持将运行相同版本的邮箱服务器（例如 Exchange 2013 与 Exchange 2016）添加到 DAG。此外，Exchange 管理员中心会在可添加到 DAG 的服务器列表中同时显示 Exchange 2013 和 Exchange 2016。这将允许管理员无意中将运行不兼容版本的 Exchange 的服务器添加到 DAG（例如，将 Exchange 2013 服务器添加到基于 Exchange 2016 的DAG）。
    
    目前，此问题没有解决办法。管理员在向 DAG 添加邮箱服务器时必须用心。仅将 Exchange 2013 服务器添加到基于 Exchange 2013 的 DAG，仅将 Exchange 2016 服务器添加到基于 Exchange 2016 的 DAG。您可以通过查看 Exchange 管理中心的服务器列表中的“版本”列，来区分每个 Exchange 版本。下面是针对 Exchange 2013 和 Exchange 2016 的服务器版本：
    
      - **Exchange 2013** 15.0 (Build xxx.xx)
    
      - **Exchange 2016** 15.1 (Build xxx.xx)

  - **从以前的 Exchange 版本迁移时邮箱增大**   将邮箱从上一版本的 Exchange 移到 Exchange 2013 时，报告的邮箱大小可能会增大 30% 到 40%。邮箱数据库所使用的磁盘空间尚未增大，仅每个邮箱所使用的空间属性增大。邮箱增大的原因是：在配额计算中包括了所有项的属性，从而更准确地计算邮箱内各项所用的空间。邮箱增大可能会导致某些用户在将其邮箱移到 Exchange 2013 时超出邮箱大小配额。
    
    要防止用户超出其邮箱大小配额，请增大数据库或邮箱的配额值以适应新的配额计算。要配置数据库或邮箱的配额值，请分别对 **Set-MailboxDatabase** 和 **Set-Mailbox** cmdlet 使用 *IssueWarningQuota*、*ProhibitSendQuota* 和 *ProhibitSendReceiveQuota* 参数。

  - **Outlook 2007 和 Outlook 2010 客户端可能无法下载脱机通讯簿**   如果无法从 Internet 访问脱机通讯簿 (OAB) 内部 URL，Outlook 2007 和 Outlook 2010 客户端可能无法下载 OAB。
    
    要为 Outlook 2007 和 Outlook 2010 客户端解决此问题，需使 OAB 内部 URL 可从 Internet 访问。Outlook 2013 不受此问题影响。

  - **在现有 Exchange 组织中安装 Exchange 2013 可能会导致所有客户端下载 OAB**   将第一台 Exchange 2013 服务器安装到现有 Exchange 2007 或 Exchange 2010 组织可能会导致组织中的所有客户端下载 OAB 的新副本，从而导致网络饱和和服务器性能问题。发生此问题的原因在于 Exchange 2013 在组织中创建了新的默认 OAB，取代了 Exchange 2007 或 Exchange 2010 OAB。未分配特定 OAB 的邮箱，或位于未分配特定 OAB 的邮箱数据库中的邮箱，会下载新的默认 OAB。
    
    安装 Exchange 2013 时，若要阻止客户端下载 OAB 的新副本，为每个邮箱或邮箱所在的邮箱数据库分配 OAB。此操作必须在 Exchange 2013 安装到组织中之前执行。

  - **用户可能会被路由到不负责所请求 OAB 的 OAB 生成邮箱**   Exchange 2013 CU5 及更高版本的 CU 已更改 OAB 链接到 OAB 生成邮箱的方式。此更改使用户可以路由到不负责用户所请求 OAB 的 OAB 生成邮箱。符合下列所有条件时会发生这种问题：
    
      - 您的组织中有多个 OAB 生成邮箱。
    
      - 在升级客户端访问服务器之前升级承载 OAB 生成邮箱的邮箱服务器。
    
      - 您正在将 Exchange 2013 服务器从 CU5 之前的版本升级到更高版本（例如，从 Exchange 2013 CU3 升级到 Exchange 2013 CU6）。
    
      - 您的客户端访问服务器正在运行 CU5 之前的版本。
    
    要解决此问题，请确保在升级邮箱服务器之前将客户端访问服务器升级到 Exchange 2013 CU6 或更高版本。这可以确保客户端访问服务器知道如何将请求代理到负责生成用户 OAB 的 OAB 生成邮箱。
    
    要了解有关 Exchange 2013 CU5 中的 OAB 更改的详细信息，请参阅 [Exchange 2013 累积更新 5 中的 OAB 改进](https://go.microsoft.com/fwlink/p/?linkid=400642)。

## 公用文件夹

  - **未经授权的发件人不再能够向启用了邮件功能的公用文件夹发送邮件**   在 Exchange 2013 CU6 之前，未经授权的发件人可以向启用了邮件功能的公用文件夹发送邮件。这允许不管公用文件夹上设置的权限如何，外部发件人都可以向启用了邮件功能的公用文件夹发送邮件。
    
    从 Exchange 2013 CU6 开始，如果您想要让外部发件人向启用了邮件功能的公用文件夹发送邮件，则至少需要向“匿名”用户授予“创建项目”权限。如果您已经设置启用了邮件功能的公用文件夹而尚未进行此操作，外部发件人将收到一封传递失败通知，邮件将不会传递到启用了邮件功能的公用文件夹。
    
    可以使用命令行管理程序或 Outlook 设置匿名用户的权限。要了解如何设置匿名用户的权限，请参阅[对公用文件夹启用或禁用邮件](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)。

  - 可以从旧版 Exchange 服务器迁移到 Exchange 2013 的公用文件夹的最大数目是 500000。有关公用文件夹复制的详细信息，请参阅[使用批处理迁移将公用文件夹从以前版本迁移到 Exchange 2013](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)。

## 邮件流

  - **客户端访问服务器上的 TransportAgent cmdlet 需要本地 Windows PowerShell**   **\*-TransportAgent** cmdlet 存在一个问题，阻止这些 cmdlet 使用 Exchange Management Shell 在客户端访问服务器上安装、卸载和管理传输代理。要在客户端访问服务器上安装、卸载和管理传输代理，您必须手动加载 ExchangeWindows PowerShell 管理单元，然后运行 **\*-TransportAgent** cmdlet。如果您尝试使用 Exchange 命令行管理程序安装、卸载或管理传输代理，则您所做更改将应用于连接到的 Exchange 2013 邮箱服务器。
    
    要在客户端访问服务器上安装、卸载或管理传输代理，请在要管理的客户端访问服务器上执行以下操作：
    
    > [!CAUTION]
    > 不支持加载 <code>Microsoft.Exchange.Management.PowerShell.SnapIn</code>Windows PowerShell 管理单元并运行 <strong>*-TransportAgent</strong> cmdlet 以外的 cmdlet，因为这可能会对 Exchange 部署造成无法修复的损坏。<br />
    > 您必须是要在其中安装、卸载或管理传输代理的客户端访问服务器上的本地管理员。我们不支持修改 Exchange 文件、目录或 Active Directory 对象的访问控制列表 (ACL)。
    
    > [!important]
    > 仅在客户端访问服务器上执行下面的过程。如果要在邮箱服务器上管理传输代理，则不需要加载 ExchangeWindows 管理单元。
    
    1.  打开一个新的 Windows PowerShell 窗口。
    
    2.  运行以下命令。
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  执行正常传输代理管理任务。
    
    4.  在要管理的每个客户端访问服务器上重复此过程。

## 客户端连接

  - **非域联合客户端的 NTLM 身份验证失败**   如果满足下列条件，客户端（如 Windows Live Mail）和 Exchange 2013 之间的身份验证可能会失败：
    
      - 客户端使用的身份验证方法是 NTLM。
    
      - 计算机未加入到域中。
    
    要解决此问题，可以执行以下任一操作：
    
      - 将运行客户端的计算机加入到域中。
    
      - 将客户端使用的身份验证类型从 NTLM 更改为通过 TLS 的基本身份验证。

  - **当与 Send-MailMessage cmdlet 一起使用时，GSSAPI 身份验证失败**   当包含在 Windows PowerShell 默认安装中的 **Send-MailMessage** cmdlet 用于发送身份验证邮件至 Exchange 2013 时，通用安全服务应用程序编程接口 (GSSAPI) 身份验证可能会失败。当发生这种情况时，您将看到在接受连接的 Exchange 2013 客户端访问服务器上的“应用程序”事件日志中的一个条目显示以下信息：
    
      - **源** MSExchangeFrontEndTransport
    
      - **事件 ID**   1035
    
      - **说明**   入站身份验证失败，接收连接器客户端前端 \<*服务器名称*\> 显示错误 `IllegalMessage`。身份验证机制是 Gssapi。尝试向 Exchange 进行身份验证的客户端的源 IP 地址是 \[\<*客户端 IP 地址*\>\]。
    
    要解决此问题，您需要在 Exchange 2013 客户端访问服务器上从客户端接收连接器中删除 `Integrated` 身份验证方法。要从客户端接收连接器中删除 `Integrated` 身份验证方法，请在可从运行 **Send-MailMessage** cmdlet 的计算机接收连接的每台 Exchange 2013 客户端访问服务器上运行以下命令：
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **当您升级到 Exchange 2013 SP1 时，MAPI over HTTP 可能会遇到性能不佳的问题**   如果您从 Exchange 2013 累积更新升级到 Exchange 2013 SP1 并启用 MAPI over HTTP，使用该协议连接到 Exchange 2013 SP1 服务器的客户端可能遇到性能不佳的问题。这是因为在从累积更新升级到 Exchange 2013 SP1 的过程中未配置所需设置。如果您从 Exchange 2013 RTM 升级到 Exchange 2013 SP1，或者安装新的 Exchange 2013 SP1 或更高版本服务器，则不会出现此问题。
    
    > [!NOTE]
    > 这只是 MAPI over HTTP 协议在客户端访问服务器上是否启用的问题。默认情况下它处于禁用状态。如果 MAPI over HTTP 禁用，客户端将转为使用 RPC over HTTP 协议。
    
    要解决此问题，请执行下列步骤：
    
    1.  在运行客户端访问服务器角色的服务器上，在 Windows 命令提示符中运行以下命令：
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  在运行邮箱服务器角色的服务器上，在 Windows 命令提示符中运行以下命令：
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Exchange 2010 共存

  - **通过 Exchange 2013 客户端访问服务器代理时，访问 Exchange 2010 邮箱的请求可能无法正常工作**   在某些情况下，如果没有安装任何更新汇总，Exchange 2013 和 Exchange 2010 Service Pack 3 (SP3) 客户端访问服务器之间的代理请求可能无法正常工作并出现错误。符合下列所有条件时会发生这种问题：
    
      - 拥有 Exchange 2013 邮箱的用户尝试使用以下方法之一打开 Exchange 2010 邮箱：
        
          - Outlook Web App 中的“打开另一个邮箱”选项 **-或者-**
        
          - Exchange 管理中心中的“另一个用户”选项
    
      - 用户连接的客户端访问服务器运行的是 Exchange 2013。
    
      - Exchange 2010 客户端访问服务器从 Exchange 2010 RTM 版或先前的 Exchange 2010 Service Pack 升级到 Exchange 2010 SP3。
    
    如果符合上述所有条件，用户将无法访问其他用户的 Exchange 2010Outlook Web App 选项，并将显示空白页。
    
    要解决此问题，请在每台 Exchange 2010 服务器上安装 Exchange 2010 SP3 更新汇总 1 或更高版本。

