---
title: '为负载平衡的客户端访问服务器配置 Kerberos 身份验证: Exchange 2013 Help'
TOCTitle: 为负载平衡的客户端访问服务器配置 Kerberos 身份验证
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835914
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 为负载平衡的客户端访问服务器配置 Kerberos 身份验证

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

**摘要：** 介绍在 Exchange 2013 中如何对负载平衡的客户端访问服务器进行 Kerberos 身份验证。

要对负载平衡的客户端访问服务器进行 Kerberos 身份验证，您需完成本文所述的配置步骤。

## 在 Active Directory 域服务中创建备用服务帐户凭据

所有共享同一命名空间和 URL 的客户端访问服务器都需要使用相同的备用服务帐户凭据。一般情况下，Exchange 每个版本的林中有一个帐户就足够了。*备用服务帐户凭据*或 *ASA 凭据*。

> [!IMPORTANT]  
> Exchange 2010 和 Exchange 2013 无法共享相同的 ASA 凭据。您需要为 Exchange 2013 创建新的 ASA 凭据。


> [!IMPORTANT]  
> 由于共享命名空间支持 CNAME 记录，Microsoft 建议使用 A 记录。这样可确保客户端根据共享名称（而不是服务器 FQDN）正确发出 Kerberos 票证请求。


设置 ASA 凭据时，请牢记这些准则：

  - **帐户类型。**我们建议您创建计算机帐户，而非用户帐户。计算机帐户不允许交互式登录，且安全策略可能比用户帐户简单。如果您创建了计算机帐户，实际上密码并不会过期，但是我们仍然建议您定期更新密码。您可以使用本地组策略指定计算机帐户和脚本的最长期限，达到此期限后，将定期删除不符合当前策略的计算机帐户。您的本地安全策略也决定着何时需要更改密码。我们建议您使用计算机帐户，但您也可以创建用户帐户。

  - **帐户名。**对帐户的名称没有要求。您可以根据自己的命名方案使用任何名称。

  - **帐户组。**用于 ASA 凭据的帐户不需要特殊的安全权限。如果您使用计算机帐户，则帐户只需为域计算机安全组的成员。如果您使用用户帐户，则帐户只需为域用户安全组的成员。

  - **帐户密码。**不会使用您创建帐户时提供的密码。因此当您创建帐户时，您应该使用一个复杂密码，确保密码符合您的组织的密码要求。

将 ASA 凭据创建为计算机帐户

1.  在域连接的计算机上，运行 Windows PowerShell 或 Exchange 命令行管理程序。
    
    使用 **Import-Module** cmdlet 导入 Active Directory 模块。
    
        Import-Module ActiveDirectory

2.  使用 **New-ADComputer** cmdlet 新建一个使用此 cmdlet 语法的 Active Directory 计算机帐户：
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **示例：** 
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    其中 *EXCH2013ASA* 是帐户名称，描述 *Alternate Service Account credentials for Exchange* 可以为您需要的任何内容，*SamAccountName* 参数的值（在本示例中为 *EXCH2013ASA*）在目录中必须唯一。

3.  使用以下 cmdlet 语法，通过 **Set-ADComputer** cmdlet 启用由 Kerberos 使用的 AES 256 加密密码支持：
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **示例：** 
    
        Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
    
    其中 *EXCH2013ASA* 是帐户名称，要修改的属性是十进制值为 28 的 *msDS-SupportedEncryptionTypes*，允许以下密码：RC4-HMAC、AES128-CTS-HMAC-SHA1-96、AES256-CTS-HMAC-SHA1-96。

有关这些 cmdlet 的详细信息，请参阅[导入模块](https://technet.microsoft.com/library/hh849725.aspx)和[新 ADComputer](https://technet.microsoft.com/library/ee617245.aspx)。

## 跨林方案

如果您具有跨林或资源目录林部署，并且您具有包含Exchange在Active Directory目录林之外的用户，您需要配置林在目录林之间的信任关系。同时，为每个目录林中部署中，您需要设置的路由规则，使所有名称后缀树林内和跨目录林之间存在信任关系。有关管理跨林信任关系的详细信息，请参阅[管理林信任](https://technet.microsoft.com/library/cc772440.aspx)。

## 标识与 ASA 凭据关联的服务主体名称

创建 ASA 凭据后，需要将 Exchange 服务主体名称 (SPN) 与 ASA 凭据关联。Exchange SPN 列表可能因配置而异，但至少应包括以下内容：

  - **http/**   对 Outlook 无处不在、MAPI over HTTP、Exchange Web Services、自动发现和脱机通讯簿使用此 SPN。

SPN 值必须与网络负载平衡器（而不是单个服务器）的服务名称匹配。为帮助规划应使用的 SPN 值，请考虑以下方案：

  - Single Active Directory site

  - Multiple Active Directory sites

在每种方案中，都假设已针对内部 URL、外部 URL 和客户端访问服务器成员所使用的自动发现内部 URI 而部署了负载平衡的完全限定域名 (FQDN)。有关详细信息，请参阅了解代理和重定向。

## 单个 Active Directory 站点

如果您具有单个 Active Directory 站点，您的环境可能如下图中所示：

![具有单个 AD 和 Kerberos 身份验证的 CAS 阵列](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "具有单个 AD 和 Kerberos 身份验证的 CAS 阵列")

根据上图中内部 Outlook 客户端使用的 FQDN，您需要将下列 SPN 与 ASA 凭据关联起来：

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## 多个 Active Directory 站点

如果您具有多个 Active Directory 站点，您的环境可能如下图中所示：

![具有多个 AD 网站和 Kerberos 身份验证的 CAS 阵列](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "具有多个 AD 网站和 Kerberos 身份验证的 CAS 阵列")

根据上图中 Outlook 客户端使用的 FQDN，您需要将下列 SPN 与 ADSite 1 中客户端访问服务器使用的 ASA 凭据关联起来：

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

您还需要将下列 SPN 与 ADSite 2 中客户端访问服务器使用的 ASA 凭据关联起来：

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## 配置每个客户端访问服务器上的 ASA 凭据并进行验证

创建帐户后，您需要验证帐户已复制到所有 AD DS 域控制器。具体地说，帐户需显示在将使用 ASA 凭据的每个客户端访问服务器上。接下来，在部署中的每个客户端访问服务器上将帐户配置为 ASA 凭据。

使用 Exchange 命令行管理程序配置 ASA 凭据，如下列过程之一所述：

  - 将 ASA 凭据部署到第一台 Exchange 2013 客户端访问服务器

  - 将 ASA 凭据部署到后续的 Exchange 2013 客户端访问服务器

部署 ASA 凭据的唯一受支持方法是使用 RollAlternateServiceAcountPassword.ps1 脚本。有关详细信息，请参阅[在命令行管理程序中使用 RollAlternateserviceAccountCredential.ps1 脚本](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)。脚本运行后，建议您验证是否已正确更新了所有目标服务器。

## 将 ASA 凭据部署到第一台 Exchange 2013 客户端访问服务器

1.  在 Exchange 2013 服务器上打开 Exchange 命令行管理程序。

2.  将目录更改为 *\<Exchange 2013 安装目录\>*\\V15\\Scripts。

3.  运行以下命令，将 ASA 凭据部署到第一台 Exchange 2013 客户端访问服务器：
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  当系统询问您是否要更改备用服务帐户的密码时，回答\&quot;是\&quot;。

下面是当您运行 RollAlternateServiceAccountPassword.ps1 脚本时显示的输出示例。

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## 将 ASA 凭据部署到其他 Exchange 2013 客户端访问服务器

1.  在 Exchange 2013 服务器上打开 Exchange 命令行管理程序。

2.  将目录更改为 *\<Exchange 2013 安装目录\>*\\V15\\Scripts。

3.  运行以下命令，将 ASA 凭据部署到另一台 Exchange 2013 客户端访问服务器：
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  对于要将 ASA 凭据部署到其中的每个客户端访问服务器，重复步骤 3。

下面是当您运行 RollAlternateServiceAccountPassword.ps1 脚本时显示的输出示例。

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## 验证 ASA 凭据的部署

  - 在 Exchange 2013 服务器上打开 Exchange 命令行管理程序。

  - 运行以下命令，检查客户端访问服务器上的设置。
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - 对于要验证 ASA 凭据部署的每个客户端访问服务器，重复步骤 2。

下面是当未设置之前的 ASA 凭据，运行上述 Get-ClientAccessServer 命令时显示的输出示例。

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

下面是当之前设置了 ASA 凭据，运行上述 Get-ClientAccessServer 命令时显示的输出示例。返回之前的 ASA 凭据以及设置凭据的日期和时间。

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## 将服务主体名称 (SPN) 与 ASA 凭据相关联

> [!IMPORTANT]  
> 请勿将 SPN 与 ASA 凭据关联，除非已将该凭据部署到至少一个 Exchange Server，如之前在将 ASA 凭据部署到第一个 Exchange 2013 客户端访问服务器中所述。否则，您将遇到 Kerberos 身份验证错误。


将 SPN 与 ASA 凭据相关联之前，您需确认目标 SPN 尚未与林中的其他帐户相关联。ASA 凭据必须是林中与这些 SPN 相关联的唯一帐户。可以通过从命令行运行 **setspn** 命令来验证在林中没有与 SPN 关联的其他帐户。

运行 setspn 命令，验证 SPN 尚未与林中的帐户相关联

1.  按\&quot;启动\&quot;。在\&quot;搜索\&quot;框中，键入\&quot;命令提示符\&quot;，然后在结果列表中选择\&quot;命令提示符\&quot;。

2.  在命令提示符处，键入以下命令：
    
        setspn -F -Q <SPN>
    
    其中 \<SPN\> 是您希望与 ASA 凭据相关联的 SPN。例如：
    
        setspn -F -Q http/mail.corp.tailspintoys.com
    
    该命令不应返回任何内容。如果该命令返回内容，则表明另一个帐户已与 SPN 关联。对于您希望与 ASA 凭据关联的每个 SPN，重复此步骤。

使用 setspn 命令将 SPN 与 ASA 凭据相关联

1.  按\&quot;启动\&quot;。在\&quot;搜索\&quot;框中，键入\&quot;命令提示符\&quot;，然后在结果列表中选择\&quot;命令提示符\&quot;。

2.  在命令提示符处，键入以下命令：
    
        setspn -S <SPN> <Account>$
    
    其中 \<SPN\> 是您希望与 ASA 凭据相关联的 SPN，\<Account\> 是与 ASA 凭据相关联的帐户。例如：
    
        setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
    
    对于您希望与 ASA 凭据关联的每个 SPN，运行此命令。

使用 setspn 命令确认已将 SPN 与 ASA 凭据相关联

1.  按\&quot;启动\&quot;。在\&quot;搜索\&quot;框中，键入\&quot;命令提示符\&quot;，然后在结果列表中选择\&quot;命令提示符\&quot;。

2.  在命令提示符处，键入以下命令：
    
        setspn -L <Account>$
    
    其中 \<Account\> 是与 ASA 凭据关联的帐户。例如：
    
        setspn -L tailspin\EXCH2013ASA$
    
    此命令只需运行一次。

## 为 Outlook 客户端启用 Kerberos 身份验证

1.  在 Exchange 2013 服务器上打开 Exchange 命令行管理程序。

2.  若要为 Outlook 无处不在 客户端启用 Kerberos 身份验证，请在您的客户端访问服务器上运行以下命令：
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  若要为 MAPI over HTTP 客户端启用 Kerberos 身份验证，请在 Exchange 2013 客户端访问服务器上运行以下命令：
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  对于要启用 Kerberos 身份验证的每个 Exchange 2013 客户端访问服务器，重复步骤 2 和 3。

## 验证 Exchange 客户端 Kerberos 身份验证

成功配置 Kerberos 和 ASA 凭据后，确认客户端可以按这些任务所述成功进行身份验证。

## 验证 Microsoft Exchange 服务主机服务是否正在运行

客户端访问服务器上的 Microsoft Exchange 服务主机服务 (MSExchangeServiceHost) 负责管理 ASA 凭据。如果该服务未运行，则无法进行 Kerberos 身份验证。默认情况下，该服务配置为当计算机启动时自动启动。

验证 Microsoft Exchange 服务主机服务是否已启动

1.  单击\&quot;开始\&quot;，键入\&quot;services.msc\&quot;，然后从列表中选择\&quot;services.msc\&quot;。

2.  在\&quot;服务\&quot;窗口中，在服务列表中找到\&quot;Microsoft Exchange 服务主机\&quot;。

3.  服务的状态应该为\&quot;运行中\&quot;。如果状态不为\&quot;运行中\&quot;，右键单击服务，然后单击\&quot;启动\&quot;。

## 从客户端访问服务器验证 Kerberos

在每个客户端访问服务器上配置 ASA 凭据之后，即可运行 **set-ClientAccessServer** cmdlet。运行此 cmdlet 之后，您可以使用日志验证 Kerberos 连接是否成功。

使用 HttpProxy 日志文件验证 Kerberos 是否正常运行

1.  在文本编辑器中，浏览到 HttpProxy 日志存储的文件夹。默认情况下，此日志存储在以下文件夹中：
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  打开最新的日志文件，查找 **Negotiate** 一词，日志文件中的行应如以下示例所示：
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    如果您看到 **AuthenticationType** 值为 **Negotiate**，说明服务器已成功创建经过 Kerberos 身份验证的连接。

## 维护 ASA 凭据

如果您需要定期更新 ASA 凭据的密码，请执行本文中配置 ASA 凭据的步骤。考虑设置一个计划任务来执行定期密码维护。请务必监视计划任务，以确保密码及时滚动并防止发生可能的身份验证中断。

## 关闭 Kerberos 身份验证

要将您的客户端访问服务器配置为不使用 Kerberos，请将 SPN 从 ASA 凭据取消关联或删除。如果删除了 SPN，则客户端不会尝试进行 Kerberos 身份验证，并且配置为使用协商身份验证的客户端会改为使用 NTLM。配置为仅使用 Kerberos 的客户端将无法连接。删除了 SPN 之后，您还应删除帐户。

删除 ASA 凭据

1.  在 Exchange 2013 服务器上打开 Exchange 命令行管理程序，并运行以下命令：
    
        Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials

2.  虽然您不必立即执行此操作，但您最后应重新启动所有客户端计算机，从计算机中清除 Kerberos 票证缓存。

