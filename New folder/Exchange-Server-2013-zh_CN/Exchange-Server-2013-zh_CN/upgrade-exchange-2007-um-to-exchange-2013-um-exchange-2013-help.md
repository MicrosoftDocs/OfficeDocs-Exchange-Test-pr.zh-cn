---
title: '升级到 Exchange 2013 UM 的 Exchange 2007 UM: Exchange 2013 Help'
TOCTitle: 升级到 Exchange 2013 UM 的 Exchange 2007 UM
ms:assetid: 642c922d-7e85-40f0-bb9b-0f20da692be3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn169227(v=EXCHG.150)
ms:contentKeyID: 54652277
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 升级到 Exchange 2013 UM 的 Exchange 2007 UM

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

当您要升级到 Exchange 统一消息 2013年的 Microsoft Exchange 2007 组织的统一邮件 (UM) 时，没有所需的步骤和其他步骤已经完成 Exchange 2007 UM 部署过程中的。根据您的电话环境和创建并配置为在 Exchange 2007 中支持统一消息的 UM 组件，您可能需要部署包括语音 (VoIP) IP 网关，IP 专用分组交换机 (Pbx)，在其他电话服务设备或传统或 SIP 启用 Pbx 然后创建和配置 Exchange 2013 UM 要求的任何其他 UM 组件。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：45-90 分钟。

  - 检查是否已在 Exchange 2007 和 Exchange 2013 组织中使用了适当的权限，以创建和配置所有必需的组件。

  - 检查是否已部署并正确配置了电话组件，包括 VoIP 网关和 PBX、IP PBX，或启用了会话初始协议 (SIP) 的 PBX。

  - 检查是否已正确安装和配置了运行 Microsoft Exchange 统一消息呼叫路由器（UM 呼叫路由器）服务的客户端访问服务器以及运行 Microsoft Exchange 统一消息服务 (UM) 的邮箱服务器。有关 UM 服务的详细信息，请参阅 [UM 服务](um-services-exchange-2013-help.md)。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!tip]
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您该如何做？

## 步骤 1：下载并安装必需的 UM 语言包

UM 语言包允许呼叫者和 Outlook Voice Access 用户能够用多种语言与语音邮件系统交互。在 Exchange 2013 邮箱服务器上新安装一种语言后，呼叫者和 Outlook Voice Access 用户可以使用该语言收听电子邮件以及与语音邮件系统交互。然而，若要使该语言对所有的传入呼叫都有效，则必须在所有 Exchange 2013 邮箱服务器上都安装所需的 UM 语言包。这是因为每个 Exchange 2013 邮箱服务器都可以对统一消息的传入呼叫做出应答。

默认情况下，当您安装 Exchange 2013 邮箱服务器时，会安装\&quot;美国英语\&quot;(en-US) 语言包。这是您的拨号计划的唯一可用语言选项，除非您安装了另一个 UM 语言包。（不能删除美国英语，除非要从计算机中删除邮箱服务器。）在 Exchange 2013 邮箱服务器上安装 UM 语言包后，当您配置拨号计划的默认语言时，与该语言包关联的语言将被列为可用选项。在默认情况下，由于创建自动助理时将 UM 自动助理关联到 UM 拨号计划，所以将使用关联的 UM 拨号计划的默认语言设置。但是，创建 UM 自动助理后，可以更改此设置。

> [!NOTE]
> 如果美国英语是要为您的拨号计划提供的唯一语言，则可以跳过此步骤并转到步骤 2。


通过使用 setup.exe 命令或运行*\<UMLanguagePack\>*.exe 安装程序已下载从[Exchange Server 2013 UM 语言包](https://go.microsoft.com/fwlink/p/?linkid=266542)UM 语言包后，您可以添加 UM 语言包。有关详细信息，请参阅[安装 UM 语言包](install-a-um-language-pack-exchange-2013-help.md)。

此示例使用 setup.exe 来安装日语 (ja-JP) UM 语言包。

    setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

## 步骤 2︰ 将 Exchange 2007 自定义问候语、 公告、 菜单和提示移动到 Exchange 2013 系统邮箱

统一邮件拨号计划和自动助理使用自定义的问候、 公告、 菜单和提示。安装 Exchange 2007 或 Exchange 2013 和用于支持功能，如消息审批和多邮箱搜索时将创建名为 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 系统邮箱。此系统邮箱还用于存储拨号计划和自动助理自定义问候语、 公告、 菜单和提示。如果系统邮箱不存在，可以使用**安装程序 /PrepareAD**命令来创建它。

在默认情况下，系统邮箱在 Exchange 管理中心 (EAC) 中不可见。可以通过运行以下命令之一获得系统邮箱列表：

此命令返回所有系统邮箱的列表。

    Get-Mailbox -Arbitration

此命令返回系统邮箱及其各自属性或设置的列表。

    Get-Mailbox -Arbitration |fl

当您正在导入自定义的问候、 公告、 菜单和提示从 Exchange 2007 到 Exchange 2013 时，您必须使用 MigrateUMCustomPrompts.ps1 脚本。不能使用 EAC 导入自定义的问候、 公告、 菜单和提示。MigrateUMCustomPrompts.ps1 脚本迁移到 Exchange 2013 UM 一份所有 UM 上 Exchange Server 2007年自定义问候语、 公告、 菜单和提示。默认情况下，MigrateUMCustomPrompts.ps1 脚本位于 2013年的 Exchange 邮箱服务器上的*\<Program Files\>*\\Microsoft\\Exchange Server\\V15\\Scripts 文件夹中，并且必须从 2013年的 Exchange 邮箱服务器运行。若要运行该脚本︰

1.  单击\&quot;开始\&quot;\>\&quot;所有程序\&quot;\>\&quot;Microsoft Exchange Server 2013\&quot;\>\&quot;Exchange 命令行管理程序\&quot;。

2.  在 Exchange 管理外壳程序，在提示符下，键入脚本的路径。例如，键入**cd"D:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts"**，，然后按 enter 键。

3.  在命令行管理程序提示符处，键入 **".\\MigrateUMCustomPrompt"**，然后按 Enter。

> [!NOTE]
> 此外可以使用<strong>Import-UMPrompt</strong> cmdlet 单独导自定义提示。Exchange 2007 UM <strong>Copy-UMCustomPrompt</strong> cmdlet 不支持复制到 Exchange 2013 UM 的自定义提示。


从 Exchange 2013 服务器上运行 MigrateUMCustomPrompts.ps1 脚本，该脚本将执行 GUID 或对象标识符查找拨号计划或自动助理在 Active Directory 中并将查询它来确定是否有任何自定义问候语、 公告、 菜单或提示。如果找到，自定义的问候、 公告、 菜单和提示将被导入到名为 {e0dc1c29-89c3-4034-b678-e6c29d823ed9} 系统邮箱。

通过使用该系统邮箱，自定义问候语、通知、菜单和提示可以与数据库中的其他邮箱一起备份和还原。这可减少所需的资源量。存储系统邮箱中的自定义问候语、通知、菜单以及和提示可删除任何可能发生的不一致状况。若要了解有关邮箱移动的详细信息，请参阅 [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)。

## 步骤 3︰ 导出和导入证书

如果您正在使用 SIP 安全或 Exchange 2007 组织中的安全拨号计划，将需要导出和导入到您的 Exchange 客户端访问 2013年和邮箱服务器的所使用的证书。双方使用传输层安全性 (相互 TLS) 对 VoIP 网关，IP Pbx 和 Exchange 2013 服务器之间发送的数据进行加密和 SIP 启用 Pbx。 证书绑定到一个电子密钥 （公钥和私钥） 对证书所有者的身份用来加密和数字签名的信息。您可以使用下列证书之一的 UM 和 UM 呼叫路由器的服务︰

  - 自签名 (Exchange) 证书

  - 内部公钥基础结构 (PKI) 证书

  - 第三方商业证书

在默认情况下，当安装 Exchange 2013 时，会创建两个自签名证书：** Microsoft Exchange Server 身份验证证书**和 **Microsoft Exchange**。\&quot;Microsoft Exchange\&quot;自签名证书用于 UM 加密数据，但您必须要为 UM 和 UM 呼叫路由器服务分配证书。该自签名证书可以被复制，然后在导入到 VoIP 网关、IP PBX、以及启用 SIP 的 PBX 上。然而，将 UM 与 Microsoft Lync Server 集成时，该证书不可用。

若要使 UM 加密在 Exchange 2013 服务器与 VoIP 网关、IP PBX 以及启用 SIP 的 PBX 间传递的数据，需要执行以下操作：

  - 使用现有自签名 UM 证书，创建一个新的自签名 Exchange 证书，并向内部证书颁发机构提交证书请求以获取 PKI 证书，或购买可用于 Exchange 2013 邮箱和客户端访问服务器与 VoIP 网关、IP PBX 以及启用 SIP 的 PBX 之间相互 TLS 的第三方商业证书。
    
    使用 EAC 创建一个 Exchange 自签名证书，如下所示：
    
    1.  在 EAC 中，导航至\&quot;服务器\&quot;\>\&quot;证书\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。
    
    2.  在\&quot;新建 Exchange 证书\&quot;页面，选择\&quot;创建自签名证书\&quot;，然后选择\&quot;下一步\&quot;。
    
    3.  为证书输入一个友好名称，然后选择\&quot;下一步\&quot;。
    
    4.  单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")选择要应用此证书的 Exchange 服务器，然后选择\&quot;下一步\&quot;。
    
    5.  指定您想包含在证书中的域，然后选择\&quot;下一步\&quot;。如果想为服务添加一个域，则单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    6.  验证所包含的域是否正确，然后选择\&quot;完成\&quot;。
    
    > [!important]
    > 当使用 EAC 创建证书时，系统不会提示您为证书启用服务。证书创建完成之后，可以使用 EAC 启用服务。有关如何为服务启用证书的详细信息，请参阅<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">将证书分配给该 UM 和 UM 呼叫路由器服务</a>。
    
    在命令行管理程序中运行以下命令来创建 Exchange 自签名证书。
    
        New-ExchangeCertificate -Services 'UM, UMCallRouter' -DomainName '*.northwindtraders.com' -FriendlyName 'UMSelfSigned' -SubjectName 'C=US,S=WA,L=Redmond,O=Northwindtraders,OU=Servers,CN= Northwindtraders.com' -PrivateKeyExportable $true
    
    > [!tip]
    > 如果通过使用 <em>Services</em> 参数指定想启用的服务，系统会提示您为创建的证书启用服务。在此示例中，系统会提示您为统一消息和统一消息呼叫路由器服务启用证书。有关如何为服务启用证书的详细信息，请参阅<a href="assign-a-certificate-to-the-um-and-um-call-router-services-exchange-2013-help.md">将证书分配给该 UM 和 UM 呼叫路由器服务</a>。


  - 导入组织中的所有 Exchange 客户端访问 2013年和邮箱服务器将使用的证书。如果使用 Exchange 2013 自签名的证书，需要复制该证书，然后将其导入的 VoIP 网关，IP Pbx 或 SIP 启用 Pbx。如果使用 Exchange 2007 中的自签名的证书，主题备用名称 (SAN) 必须包含所有 Exchange 2013 服务器的计算机名。如果您有在您的组织中的 Exchange 2007 统一消息服务器，您可以使用 Exchange 2013 自签名的证书，但必须将 Exchange 2007 UM 服务器的计算机名添加到 SAN 中的 Exchange 2013 证书。

  - 启用或分配用于组织中客户端访问服务器和邮箱服务器上 UM 和 UM 呼叫路由器服务的证书。
    
    使用 EAC 启用 Exchange 2013 服务器上的 UM 服务和 UM 呼叫路由器服务，以使用 Exchange 自签名证书，如下所示：
    
    1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;证书\&quot;，选择要启用服务的证书，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。
    
    2.  在\&quot;步骤\&quot;页上，选择\&quot;服务\&quot;，选择\&quot;统一消息\&quot;，再选择\&quot;统一消息呼叫路由器\&quot;。
    
    在命令行管理程序中运行以下命令来启用 Exchange 自签名证书。
    
        Enable-ExchangeCertificate -Thumbprint 5113ae0233a72fccb75b1d0198628675333d010e -Services 'UM, UMCallRouter'

  - 将任何新的或现有 UM 拨号计划配置为 SIP 安全或安全。

  - 在您组织中的客户端访问服务器和邮箱服务器上将 UM 启动模式配置为 TLS 或双协议模式。

  - 使用完全限定的域名 (FQDN) 创建并配置新的或现有 UM IP 网关。

  - 将 UM IP 网关上的侦听端口配置为使用 TLS 端口 5061。

  - 重新启动所有 Exchange 2013 客户端访问服务器上的 UM 呼叫路由器服务，并重新启动所有 Exchange 2013 邮箱服务器上的 UM 服务。有关 UM 服务的详细信息，请参阅 [UM 服务](um-services-exchange-2013-help.md)。

## 步骤 4︰ 在所有的 Exchange 2013 客户端访问服务器上配置 UM 启动模式

如果您正在使用 SIP 安全或安全拨号计划，必须在 Exchange 2013 客户端访问服务器上配置 UM 启动模式。通过 EAC 或外壳，可以在 Exchange 2013 客户端访问服务器上指定 UM 呼叫路由器服务的 UM 启动模式。默认情况下，Exchange 2013 客户端访问服务器在 TCP 模式中，将启动，但是如果您使用传输层安全性 (TLS) 加密语音通信 (VoIP) 上，您必须配置 Exchange 2013 客户端访问服务器使用 TLS 或双重模式。我们建议所有 Exchange 2013 客户端访问服务器被都配置为双用作 UM 启动模式。这是因为所有 Exchange 2013 客户端访问服务器可以将传入呼叫应答所有 um 拨号计划，和那些拨号计划可以都有不同的安全设置。如果您更改 UM 启动模式下，您必须重新启动 UM 呼叫路由器服务以使更改生效。UM 服务的详细信息，请参阅[UM 服务](um-services-exchange-2013-help.md)。

使用 EAC 在 Exchange 2013 客户端访问服务器上配置 UM 启动模式，如下所示：

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange Server\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 呼叫路由器设置\&quot;\>\&quot;UM 启动模式\&quot;下，从下拉列表中选择以下项之一：
    
      - **TCP**   如果您没有使用 mTLS 而且仅使用不安全的拨号计划，请使用此选项。
    
      - **TLS**   如果您使用 mTLS 而且仅使用 SIP 安全或安全拨号计划，请使用此选项。
    
      - **双协议模式**   如果您正在使用 mTLS 和不安全、SIP 安全以及安全拨号计划，请使用此选项。

5.  选择 UM 启动模式后，单击\&quot;保存\&quot;。

在命令行管理程序中运行以下命令，以在 Exchange 2013 客户端访问服务器上配置 UM 启动模式。

    Set-UMCallRouterSettings -Server MyUMCallRouter.northwindtraders.com -UMStartupMode Dual

## 步骤 5: 2013年的 Exchange 邮箱中的所有服务器上配置的 UM 启动模式

如果正在使用 SIP 安全或安全拨号计划，您必须在 Exchange 2013 邮箱服务器上配置 UM 启动模式。可以使用 EAC 或命令行管理程序为 Exchange 2013 邮箱服务器上的 UM 服务指定 UM 启动模式。默认情况下，Exchange 2013 邮箱服务器将以 TCP 模式启动，但如果使用传输层安全性 (TLS) 加密 Voice over IP (VoIP) 通信，则必须将 Exchange 2013 邮箱服务器配置为使用 TLS 或双协议模式。建议将所有 Exchange 2013 邮箱服务器配置为使用双协议模式作为 UM 的启动模式。这是因为所有 Exchange 2013 邮箱服务器都可以应答所有 UM 拨号计划的传入呼叫，而且那些拨号计划可以具有不同的安全设置。如果更改 UM 启动模式，则必须重新启动 UM 服务，以使更改生效。有关 UM 服务的详细信息，请参阅 [UM 服务](um-services-exchange-2013-help.md)。

使用 EAC 配置 Exchange 2013 邮箱服务器上的 UM 启动模式，如下所示：

1.  在 EAC 中，导航到\&quot;服务器\&quot;\>\&quot;服务器\&quot;。

2.  在列表视图中，选择要修改的 Exchange 服务器，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;Exchange Server\&quot;页面上，单击\&quot;统一消息\&quot;。

4.  在\&quot;UM 服务设置\&quot;\>\&quot;UM 启动模式\&quot;下，从下拉列表中选择以下项之一：
    
      - **TCP**   如果您没有使用 mTLS 而且仅使用不安全的拨号计划，请使用此选项。
    
      - **TLS**   如果您使用 mTLS 而且仅使用 SIP 安全或安全拨号计划，请使用此选项。
    
      - **双协议模式**   如果您正在使用 mTLS 和不安全、SIP 安全以及安全拨号计划，请使用此选项。

5.  选择 UM 启动模式后，单击\&quot;保存\&quot;。

在命令行管理程序中运行以下命令，以在 Exchange 2013 邮箱服务器上配置 UM 启动模式。

    Set-UMService -Identity MyUMServer -ExternalHostFqdn host.external.contoso.com -IPAddressFamily Any -UMStartupMode Dual

## 第 6 步︰ 创建或配置现有 UM 拨号计划

这取决于您现有的 Exchange 2007 部署，您可能需要创建新的 UM 拨号计划或配置您现有的拨号计划。UM 拨号计划代表了一套传统或 SIP 启用专用分组交换机 (Pbx)，IP Pbx 或 SIP 启用 Pbx，共享公共用户分机号码。拨号计划中承载传统或 SIP 启用 Pbx 或 IP Pbx 上的所有用户的扩展包含相同数量的数字。用户可以无需扩展到附加特殊号码或拨打的完整的电话号码拨另一个的电话分机。

统一消息中使用 UM 拨号计划，以确保用户电话分机是唯一。在一些电话网络中，多个 IP Pbx、 传统 Pbx 或启用了 SIP 的 Pbx 存在。在这些电话网络中，可能有两个具有相同的电话分机号码的用户。UM 拨号计划解决此问题。将两个用户放入两个单独的 UM 拨号计划使其扩展的唯一。有关详细信息，请参阅[UM 拨号计划](um-dial-plans-exchange-2013-help.md)。

如果需要，可以使用 EAC 创建 UM 拨号计划：

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;，然后单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;新建 UM 拨号计划\&quot;页面上，填写下列内容：
    
      - **名称**   键入拨号计划的名称。UM 拨号计划名称是必需的，并且必须是唯一的。但是，键入的名称在 EAC 和命令行管理程序中仅用于显示目的。UM 拨号计划名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
        
        尽管拨号计划名称的框可以接受 64 个字符，但是拨号计划的名称不得超过 49 个字符。如果尝试创建的拨号计划名称包含的字符数超过 49 个，将收到错误消息。该消息称不能生成 UM 邮箱策略，因为 UM 拨号计划的名称太长。这是因为创建拨号计划时，还创建了名为 *\<DialPlanName\>***Default Policy** 的默认 UM 邮箱策略。当向拨号计划的名称中添加默认策略中的 15 个字符时，总字符数就会超出限制。UM 拨号计划和 UM 邮箱策略的 *name* 参数都可以是 64 个字符。但是，如果拨号计划的名称超过 49 个字符，默认 UM 邮箱策略的名称将超过 64 个字符，这是系统所不允许的。
    
      - **分机号码长度(位)**   输入拨号计划中分机号码的位数。分机号码位数基于在 PBX 上创建的电话拨号计划。例如，如果与电话拨号计划关联的用户拨打 4 位的分机号码来呼叫同一电话拨号计划中的另一个用户，则应选择 4 作为分机号码中的位数。
        
        这是一个必填框，该字段的值范围为 1 到 20。典型的分机号码长度为 3 到 7 位。如果现有电话环境包含分机号码，则必须指定一个与这些分机号码的位数相匹配的位数。
        
        在创建电话分机拨号计划时，将需要在用户关联到电话分机拨号计划时输入用户的分机号码。当启用了 UM 的用户与 SIP URI 或 E.164 拨号计划关联时，对于会话初始协议 (SIP) 拨号计划或 E.164 拨号计划，也需要分机号码。当 Outlook Voice Access 用户访问其 Exchange 邮箱时使用此分机号码。
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_URI 类型)
    
      - UNRESOLVED\_TOKENBLOCK\_VAL(UI\_VoIP 安全)
    
      - \&quot;国家/地区代码\&quot;：使用此框可以键入用于拨出电话的国家/地区代码数字。将在所拨打的电话号码前面加拨此号码。此框可接受 1 到 4 位数。例如，美国的国家/地区代码为 1，英国的为 44。

3.  单击\&quot;保存\&quot;。

如果需要，可以在命令行管理程序中运行以下命令，以创建 UM 拨号计划。

    New-UMDialplan -Name MyUMDialPlan -URIType E164 -NumberOfDigitsInExtension 5 -VoIPSecurity Secured

如果需要，可以使用 EAC 配置现有的 UM 拨号计划：

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。

2.  在此列表视图中，选择要查看或修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;UM 拨号计划\&quot;页上，单击\&quot;配置\&quot;。使用配置选项查看指定的拨号计划设置并启用或禁用功能。

如果需要，可以在命令行管理程序中运行以下命令，以配置现有的 UM 拨号计划。

    Set-UMDialplan -Identity MyDialPlan -AccessTelephoneNumbers 4255551234 -AudioCodec Wma -CallAnsweringRulesEnabled $false -OutsideLineAccessCode 9 -VoIPSecurity SIPSecured

当您部署 Exchange 2007 统一消息时，您就需要统一消息服务器添加到 UM 拨号计划以使它能够应答传入呼叫。这不再是必需的。在 Exchange 2013，客户端访问和邮箱服务器无法将链接与电话分机或 E.164 拨号计划，但必须链接到 SIP URI 拨号计划。客户端访问和邮箱服务器将应答所有传入呼叫的拨号计划的所有类型。

## 第 7 步︰ 创建或配置现有 UM IP 网关

这取决于您现有的 Exchange 2007 部署，您可能需要创建新的 UM IP 网关或配置您现有的。如果您正在使用 SIP 安全或安全拨号计划，必须使用 FQDN 创建 UM IP 网关并使用外壳程序将其配置为侦听端口 5061。现有 UM IP 网关，请验证它们正在配置 FQDN，并正在侦听端口 5061。如果 UM IP 网关不能使用 FQDN，使用 EAC 或外壳可更改地址。如果 UM IP 网关不能使用端口 5061，使用外壳程序更改的端口。您可以使用**Get-UMIPGateway** cmdlet 查看 UM IP 网关的设置。

UM IP 网关代表物理 Voice over IP (VoIP) 网关、IP PBX 或启用 SIP 的 PBX。必须先在目录服务中创建 UM IP 网关，才能使用 VoIP 网关、IP PBX 或启用 SIP 的 PBX 应答语音邮件用户的传入呼叫和发送他们的传出呼叫。

结合使用 UM IP 网关与 UM 智能寻线功能，可以在 VoIP 网关、IP PBX 或启用 SIP 的 PBX 与 UM 拨号计划之间建立关联。通过创建多个 UM 智能寻线，可以将一个 UM IP 网关与多个 UM 拨号计划关联。有关详细信息，请参阅 [UM IP 网关](um-ip-gateways-exchange-2013-help.md)。

如果需要，可以使用 EAC 创建 UM IP 网关，如下所示：

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，然后单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在\&quot;新建 UM IP 网关\&quot;页上，输入以下信息：
    
      - **名称**   使用此框指定 UM IP 网关的唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM IP 网关之后必须更改其显示名，则必须先删除现有的 UM IP 网关，然后再创建一个具有相应名称的 UM IP 网关。必须提供 UM IP 网关名，但是该名称仅用于显示。因为组织可能会使用多个 UM IP 网关，所以，建议您为该 UM IP 网关使用有意义的名称。UM IP 网关名称的最大长度为 64 个字符，并且可以包含空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **地址**   可以使用 IPv4 或 IPv6 地址或 FQDN 配置 UM IP 网关。使用该框指定在 VoIP 网关、IP PBX 或 启用 SIP 的 PBX 上配置的 IP 地址或 FQDN。此框只接受有效并且格式正确的 FQDN。
        
        您可以输入字母和数字字符。支持 IPv4 地址，IPv6 地址和 Fqdn。如果您想要使用相互 TLS 之间一个 UM IP 网关和拨号计划在操作 SIP 安全或者安全模式，您必须使用 FQDN 配置 UM IP 网关。您还必须配置侦听端口 5061，并验证所有 VoIP 网关或 IP Pbx 也已都配置为侦听端口 5061 上相互 TLS 请求。若要配置的 UM IP 网关，请运行下面的命令外壳程序中︰ `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`
        
        如果使用 FQDN，必须还要确保已为该 VoIP 网关、IP PBX 或启用 SIP 的 PBX 正确地配置了 DNS 主机记录，以便可以正确地将主机名解析为 IP 地址。另外，如果使用 FQDN 而不是 IP 地址，并更改了 UM IP 网关的 DNS 配置，则必须先禁用 UM IP 网关然后再启用它，以确保 UM IP 网关的配置信息已正确更新。
    
      - **UM 拨号计划**   单击\&quot;浏览\&quot;选择要与 UM IP 网关关联的 UM 拨号计划。选择要与 UM IP 网关关联的 UM 拨号计划时，还会创建默认 UM 智能寻线并将其与所选的 UM 拨号计划关联。如果未选择 UM 拨号计划，则必须手动创建 UM 智能寻线并将该 UM 智能寻线与所创建的 UM IP 网关关联。

3.  单击\&quot;保存\&quot;。

如果需要，可以在命令行管理程序中运行以下命令，以创建 UM IP 网关。

    New-UMIPGateway -Identity MyUMIPGateway -Address "MyUMIPGateway.contoso.com"

如果需要，可以使用 EAC 配置现有的 UM IP 网关：

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM IP 网关\&quot;，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM IP 网关\&quot;页上，单击\&quot;配置\&quot;。使用配置选项来查看指定的 UM IP 网关设置并启用或禁用功能。

如果需要，可以在命令行管理程序中运行以下命令，以配置现有的 UM IP 网关。

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## 第 8 步︰ 创建 UM 查寻组

根据现有 Exchange 2007 部署，您可能需要创建新的 UM 查寻组。电话查寻组使您能够分发到多个扩展名从一个单一的数字电话呼叫或电话号码。在统一消息，UM 查寻组的逻辑表示形式电话查寻组，并且它链接到 UM 拨号计划的 UM IP 网关。

对每个 IP PBX 或 PBX 智能寻线，您需要拥有至少一个 UM 智能寻线。完成以下步骤后，将默认创建一个 UM 智能寻线。如果您拥有一个以上的 IP PBX 或 PBX 智能寻线，则需要创建更多 UM 智能寻线。若要了解有关 UM 智能寻线的详细信息，请参阅 [UM 智能寻线](um-hunt-groups-exchange-2013-help.md)。

如果需要，可以使用 EAC 创建 UM 智能寻线：

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上的\&quot;UM 智能寻线\&quot;下，单击\&quot;新建\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在\&quot;新建 UM 智能寻线\&quot;页上，输入以下信息：
    
      - **名称**   使用此文本框可创建 UM 智能寻线的显示名。UM 智能寻线名是必需的，并且必须是唯一的，但是该名称在 EAC 和命令行管理程序中仅用于显示目的。如果在创建智能寻线后必须更改其显示名，则必须首先删除现有的智能寻线，然后创建另一个具有适当名称的智能寻线。如果您的组织使用多个智能寻线，那么，建议对您的智能寻线使用有意义的名称。UM 智能寻线名的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：" / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **UM IP 网关**   使用此框选择 UM IP 网关。此框显示将要与 UM 智能寻线相关联的 UM IP 网关的名称。若要将 UM IP 网关与 UM 智能寻线相关联，请单击\&quot;浏览\&quot;。
    
      - **引导标识**   使用此框可指定一个字符串，该字符串唯一标识在 PBX 或 IP PBX 上配置的引导标识符。在此框中可以使用分机号码或 SIP 统一资源标识符 (URI)。此框可接受字母数字字符。对于旧版 PBX，数字值将用作引导标识符。但是，一些 IP PBX 和启用 SIP 的 PBX 可以使用 SIP URI。

4.  单击\&quot;保存\&quot;。

如果需要，可以在命令行管理程序中运行以下命令，以创建 UM 智能寻线。

    New-UMHuntGroup -Name MyUMHuntGroup -PilotIdentifier 5551234,55555 -UMDialPlan MyUMDialPlan -UMIPGateway MyUMIPGateway

> [!tip]
> 您不可以配置或更改 UM 智能寻线的设置。如果要更改 UM 智能寻线的配置设置，则必须将其删除并使用正确设置添加新的 UM 智能寻线。


## 第 9 步︰ 创建或配置 UM 自动助理

这取决于您现有的 Exchange 2007 部署，您可能需要创建新的 UM 自动助理。您可以使用 UM 自动助理创建语音菜单系统，让外部和内部调用方使用 UM 自动助理的菜单系统以查找人员并放置或转移求助电话公司用户或组织中的部门。有关详细信息，请参阅[自动回答和路由传入呼叫](automatically-answer-and-route-incoming-calls-exchange-2013-help.md)。

在较小的部署中，您可能只想部署 UM，以使调用方可以将用户的语音邮件。在这些部署中，不需要创建自动助理。但是，在大多数情况下，使用自动助理是非常有用的外部调用方为您的组织拨打电话时。

如果需要，可以使用 EAC 创建 UM 自动助理，如下所示：

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。选择您想要在其中添加自动助理的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标").

2.  在\&quot;UM 拨号计划\&quot;页上，在\&quot;UM 自动助理\&quot;下，单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

3.  在\&quot;新建 UM 自动助理\&quot;页上，填写以下框：
    
      - **名称**   使用此框可以创建 UM 自动助理的显示名。UM 自动助理名称是必需的，并且必须是唯一的。但是，此名称在 EAC 和命令行管理程序中仅用于显示目的。如果在已创建自动助理之后必须更改它的显示名，则必须首先删除现有 UM 自动助理，然后创建另一个有合适名称的自动助理。如果您的组织使用多个 UM 自动助理，则建议您的 UM 自动助理使用有意义的名称。UM 自动助理名称的最大长度是 64 个字符，并且可以包括空格。
        
        虽然您可以命名一个新的 UM 自动助理以包含空格，但是，如果将统一消息与 Lync Server 集成，则自动助理的名称不能包含空格。因此，如果您创建的自动助理的显示名称中包含空格，但要与 Lync Server 集成，则必须先删除该自动助理，然后另外创建一个显示名称中不包含空格的自动助理。
    
      - **将此自动助理创建为已启用**   完成 UM 自动助理的创建后，选中此复选框可使自动助理能够应答传入呼叫。默认情况下，新建的自动助理为禁用状态。如果决定创建被禁用的 UM 自动助理，可以在完成创建之后使用 EAC 或命令行管理程序启用自动助理。
    
      - **设置此自动助理以响应语音命令**   选中此复选框来对 UM 自动助理启用语音。通过对自动助理启用语音，呼叫者可以通过使用按键或语音输入来响应 UM 自动助理所使用的系统或自定义提示。默认情况下，自动助理在创建时不会启用语音。为了让呼叫者使用语言为美国英语 (en-US) 以外的启用语音的自动助理，必须安装合适的 UM 语言包，并将自动助理的属性配置为使用此语言。默认情况下，当您安装 Exchange 2013 邮箱服务器时，会安装 en-US UM 语言包。
    
      - **访问号码**   输入呼叫者将用于联系自动助理的分机或电话号码。请在该框中键入分机号码或电话号码，然后单击\&quot;添加\&quot;，将号码添加到列表中。您提供的分机号码的位数或电话号码无需与在关联的 UM 拨号计划中配置的分机号码的位数匹配。这是因为允许直接呼叫 UM 自动助理。
        
        输入的分机号码或访问号码的数目不受限制。但是，可以新建自动助理，而不列出分机号码或电话号码。分机号码或电话号码并非必需。可以编辑或删除现有分机号码或引导标识符。若要编辑现有分机号码或电话号码，请单击\&quot;编辑\&quot;。若要从列表中删除现有分机号码或电话号码，请单击\&quot;删除\&quot;。

4.  单击\&quot;保存\&quot;。

如果需要，可以在命令行管理程序中运行以下命令，以创建 UM 自动助理。

    New-UMAutoAttendant -Name MyUMAutoAttendant -UMDialPlan MyUMDialPlan -PilotIdentifierList 56000,56100 -SpeechEnabled $true -Status Enabled

如果需要，可以使用 EAC 配置现有的自动助理：

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 自动助理\&quot;下，选择要查看或配置的 UM 自动助理，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。使用配置选项来查看指定的自动助理设置并启用或禁用功能。

如果需要，可以在命令行管理程序中运行以下命令，以配置现有的自动助理。

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA -OperatorExtension 50100 -AfterHoursTransferToOperatorEnabled $true -StaroutToDialPlanEnabled $true

## 第 10 步︰ 创建或配置 UM 邮箱策略

这取决于您现有的 Exchange 2007 部署，您可能需要创建新的 UM 邮箱策略或配置现有 UM 邮箱策略。当您启用统一消息的用户时，UM 邮箱策略是必需的。每个已启用 UM 的用户的邮箱必须链接到单个 UM 邮箱策略。创建 UM 邮箱策略后，您将链接到该 UM 邮箱策略的一个或多个启用 UM 的邮箱。这使您能够控制针安全性设置，例如最小小数位数的 PIN 或链接到该 UM 邮箱策略的已启用 UM 的用户的登录尝试的最大数目。有关详细信息，请参阅[UM 邮箱策略](um-mailbox-policies-exchange-2013-help.md)。

如果需要，可以使用 EAC 创建 UM 邮箱策略：

1.  在 EAC 中，导航到\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;。在此列表视图中，选择您要修改的 UM 拨号计划，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页上的\&quot;UM 邮箱策略\&quot;下，单击\&quot;添加\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

3.  在\&quot;新建 UM 邮箱策略\&quot;页面上，在\&quot;名称\&quot;框中，输入新的 UM 邮箱策略的名称。
    
    > [!NOTE]
    > 使用此框可为 UM 邮箱策略指定唯一名称。此名称是 EAC 中出现的显示名。如果在创建 UM 邮箱策略后必须要更改其显示名，则必须首先删除现有的 UM 邮箱策略，然后创建具有相应名称的其他 UM 邮箱策略。如果有任何启用 UM 的用户关联了 UM 邮箱策略，那么您不可以删除该 UM 邮箱策略。UM 邮箱策略名称是必需的，但其仅用于显示目的。由于您的组织可能使用多个 UM 邮箱策略，因此建议您使用对 UM 邮箱策略有意义的名称。UM 邮箱策略名称的最大长度为 64 个字符，可以包括空格。但是，不能包括下列任何字符：&quot; / \ [ ] : ; | = , + * ? &lt; &gt;.


4.  单击\&quot;保存\&quot;。
    
    > [!NOTE]
    > 保存该 UM 邮箱策略时，将启用所有默认设置，包括 PIN 策略、 语音邮件功能，以及受保护的语音邮件设置。如果您想要自定义或更改任何默认设置为您刚刚创建的 UM 邮箱策略，使用<strong>Set-UMMailbox</strong> cmdlet 或 EAC。


如果需要，可以运行以下命令，在命令行管理程序中创建 UM 邮箱策略。

    New-UMMailboxPolicy -Name MyUMMailboxPolicy -UMDialPlan MyUMDialPlan

如果需要，可以使用 EAC 配置现有的 UM 邮箱策略：

1.  在 EAC 中，导航至\&quot;统一消息\&quot;\>\&quot;UM 拨号计划\&quot;，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。

2.  在\&quot;UM 拨号计划\&quot;页面的\&quot;UM 邮箱策略\&quot;下，选择要查看或配置的 UM 邮箱策略，然后单击\&quot;编辑\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标")。使用配置选项来查看指定的 UM 邮箱策略设置并启用或禁用功能。

如果需要，可以在命令行管理程序中运行以下命令，以配置现有的 UM 邮箱策略。

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

## 第 11 步︰ 将现有的已启用 UM 的邮箱移动到 Exchange 2013

在 Exchange 2007 统一消息之后您启用了用户在组织内使用语音邮件，默认的 UM 属性集, 将应用于用户以便他们可以使用 UM 功能。有关详细信息，请参阅[用户的语音邮件](voice-mail-for-users-exchange-2013-help.md)。

在升级的过程中，将会有一段时间，在此期间您必须同时在 Exchange 2007 邮箱服务器上和 2013年的 Exchange 邮箱服务器上启用 UM 的邮箱。但是，如果您正在将所有已启用 UM 的用户移到 2013年的 Exchange 邮箱服务器，您必须使用 EAC 或**New-MoveRequest** cmdlet Exchange 2013 服务器从 Shell 中要保留的所有属性和设置，包括该用户的 PIN。

移动请求是将邮箱从一个邮箱数据库移动到另一个邮箱数据库的过程。本地移动请求是在单林内发生的邮箱移动。有关邮箱移动的详细信息，请参阅：

  - [Exchange 2013 中的邮箱移动](mailbox-moves-in-exchange-2013-exchange-2013-help.md)

  - [New-MoveRequest](https://technet.microsoft.com/zh-cn/library/dd351123\(v=exchg.150\))

  - [New-MigrationBatch](https://technet.microsoft.com/zh-cn/library/jj219166\(v=exchg.150\))

  - [移动邮箱](https://go.microsoft.com/fwlink/p/?linkid=296351)

要使用 EAC 将 Exchange 2007 邮箱移至 Exchange 2013 邮箱服务器，请执行以下步骤：

1.  在 EAC 中，单击\&quot;收件人\&quot;\>\&quot;迁移\&quot;，然后单击\&quot;添加\&quot;![编辑图标](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "编辑图标").

2.  在\&quot;新建本地邮箱移动\&quot;向导中，选择要移动的用户并单击\&quot;确定\&quot;，然后单击\&quot;下一步\&quot;。

3.  在\&quot;移动配置\&quot;页面上，为新的批处理指定名称。选择您需要存档邮箱的哪些选项以及邮箱数据位置，然后单击\&quot;新建\&quot;。

若要使用命令行管理程序将 Exchange 2007 邮箱移至 Exchange 2013 邮箱服务器，请运行以下命令。

    New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase "DB01"

## 第 12 步︰ 启用了 UM 的新用户，或为现有的已启用 UM 的用户配置设置

用户首先必须有邮箱，然后才能为他们启用统一消息。但在默认情况下，不会为已有邮箱的用户启用 UM。为用户启用了 UM 后，可以为该用户管理、修改和配置 UM 属性和语音邮件功能。可以使用 EAC 或命令行管理程序为用户启用 UM。有关详细信息，请参阅[用户的语音邮件](voice-mail-for-users-exchange-2013-help.md)。

当您为用户启用 UM 时，必须至少定义一个分机号码，以便在将语音邮件提交到用户的邮箱时供 UM 使用并允许用户使用 Outlook Voice Access。为用户启用了 UM 后，可以通过配置用户邮箱的 Exchange 统一消息 (EUM) 代理地址，或者在 EAC 中添加或删除用户的其他或辅助分机号码，从而给用户邮箱添加辅助分机号码，或者修改或删除分机号码。若要添加、修改或删除分机号码、E.164 号码或 SIP 地址，请参阅[声音已启用邮件的用户的过程](voice-mail-enabled-user-procedures-exchange-2013-help.md)。

要使用 EAC 为用户启用统一消息，请执行以下步骤：

1.  在 EAC 中，单击\&quot;收件人\&quot;。

2.  在列表视图中，选择要为其邮箱启用统一消息的用户。

3.  在\&quot;详细信息\&quot;窗格的\&quot;电话和语音功能\&quot;下，单击\&quot;启用\&quot;。

4.  在\&quot;启用 UM 邮箱\&quot;页上，单击\&quot;UM 邮箱策略\&quot;旁的\&quot;浏览\&quot;按钮，找到 UM 邮箱策略，以从列表中分配用户，然后单击\&quot;确定\&quot;。

5.  在\&quot;启用 UM 邮箱\&quot;页上，填写下列框：
    
      - **SIP 地址或 E.164 号码**  输入用户的 SIP 地址或 E.164 号码。如果您启用统一消息的用户分配给链接到 SIP URI 或 E.164 拨号计划的 UM 邮箱策略，则这些选项不可用。添加的 SIP 地址或 E.164 号码的用户不可用如果用户与电话扩展拨号计划相关联。当您将用户分配到链接到 SIP URI UM 邮箱策略或 E.164 拨号计划时，您还必须为用户输入分机号码。当用户访问使用Outlook语音访问其邮箱时使用此分机号码。在此框中配置的位数必须匹配的数字位数配置 SIP URI 或 E.164 拨号计划。
    
      - **分机号码**   为将启用 UM 的用户输入分机号码。
        
        必须为用户提供有效的分机号码，且该号码必须与在拨号计划中指定的位数匹配。您只能输入介于 1 到 20 之间的数字字符或数字。典型的分机号码长度为 3 位到 7 位。分机号码中的位数在与分配给用户的 UM 邮箱策略关联的拨号计划中设置。
    
      - 根据\&quot;PIN 设置\&quot;，完成下列操作：
        
          - **自动生成 PIN**   单击此按钮可为已启用 UM 的用户自动生成 PIN，从而可以通过 Outlook Voice Access 进行语音邮件访问。这是默认设置。在单击此按钮后，系统会根据在分配给此用户的 UM 邮箱策略上配置的 PIN 策略自动生成一个 PIN。建议使用此设置来帮助保护用户的 PIN。此 PIN 会通过一封欢迎邮件发送给用户，在启用 UM 策略后，用户就可以收到此邮件。默认情况下，他们必须在首次登录其邮箱以接收其语音邮件时更改此 PIN。
        
          - **键入 PIN**   单击此按钮可手动指定用户将用来访问语音邮件系统的 PIN。PIN 必须符合与已启用 UM 的用户关联的 UM 邮箱策略上所配置的 PIN 策略设置。例如，如果将 UM 邮箱策略配置为只接受包含七位数或更多位数的 PIN，则在此框中输入的 PIN 长度至少必须有七位数。
        
          - **要求用户在第一次登录时重置其 PIN**   选中此复选框会强制用户在首次使用 Outlook Voice Access 通过电话访问语音邮件系统时重置其语音邮件 PIN。系统将会提示用户输入他们更熟悉的 PIN。最佳的安全做法是，强制已启用 UM 的用户在首次登录时更改其 PIN，以防止其数据和收件箱受到未经授权的访问。默认情况下此复选框处于选中状态。

6.  在\&quot;启用 UM 邮箱\&quot;页上，查看设置。单击\&quot;完成\&quot;对用户启用统一消息。单击\&quot;上一步\&quot;可以更改配置。

若要在命令行管理程序中为用户启用统一消息，请运行以下命令。

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -NotifyEmail administrator@contoso.com -PINExpired $true

如果需要，可以使用 EAC 为已启用 UM 的用户进行配置：

1.  在 EAC 中，导航到\&quot;收件人\&quot;\>\&quot;邮箱\&quot;。

2.  在列表视图中，选择要更改 UM 邮箱策略的邮箱。

3.  在详细信息窗格的\&quot;电话和语音功能\&quot;\>\&quot;统一消息\&quot;下，单击\&quot;查看详细信息\&quot;。

4.  在\&quot;UM 邮箱\&quot;页上，单击\&quot;UM 邮箱设置\&quot;查看或更改启用了 UM 的现有用户的以下 UM 属性：
    
      - **PIN 状态**   此仅显示框显示用户邮箱的状态。默认情况下，如果用户已启用 UM，则 PIN 状态会列为\&quot;未锁定\&quot;。但是，如果用户已多次输入错误的 Outlook Voice Access PIN，则该状态会列为\&quot;已锁定\&quot;。
    
      - **UM 邮箱策略**   此框显示与启用 UM 的用户相关联的 UM 邮箱策略的名称。您可以单击\&quot;浏览\&quot;来定位并指定要与此 UM 邮箱关联的 UM 邮箱策略。
    
      - **个人话务员分机** 使用此框可为用户指定话务员分机号码。默认情况下不会配置分机号码。分机号码的长度可以是 1 到 20 个字符。这会使向启用了 UM 的用户发出的传入呼叫可转移到在此框中指定的分机号码。
        
        可在拨号计划和自动助理上配置其他类型的话务员分机号码。但是，这些分机号通常预定用于公司范围内的前台或话务员。当管理助理或个人助理应答特定用户的传入呼叫时，可使用个人话务员分机号设置。

5.  在\&quot;UM 邮箱\&quot;页上的\&quot;其他分机号\&quot;下，您可以添加、更改和查看用户的分机号码。
    
      - 要添加分机号码，请单击\&quot;添加\&quot;![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。在\&quot;添加其他分机号\&quot;页上，使用\&quot;浏览\&quot;选择 UM 拨号计划，然后在\&quot;分机号码\&quot;框中输入分机号码。
    
      - 要删除分机号码，请选择要删除的分机号码，然后单击\&quot;删除\&quot;![删除图标](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "删除图标")。

6.  如果您进行了任何更改，请单击\&quot;保存\&quot;。

如果需要，可以在命令行管理程序中运行以下命令，为已启用 UM 的用户进行配置。

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringAudioCodec Wma -CallAnsweringRulesEnabled $false -FaxEnabled $false -UMSMSNotificationOption VoiceMail

## 步骤 13︰ 配置您的 VoIP 网关，IP Pbx 和 SIP 启用 Pbx 发送到 Exchange 2013 客户端访问服务器的所有传入呼叫

在安装 Exchange 2013 客户端访问服务器和邮箱服务器时，会自动将它们启用，因此它们可以应答传入和传出语音呼叫，以及将语音邮件消息路由给目标收件人。在安装 Exchange 2013 客户端访问服务器和邮箱服务器以及部署统一消息时，不必将 Exchange 2013 客户端访问服务器或邮箱服务器与 UM 拨号计划关联或者将其添加到 UM 拨号计划中。Exchange 2013 客户端访问服务器和邮箱服务器应答所有传入呼叫，然后使用 UM 拨号计划查找用户。

Exchange 2013 客户端访问服务器是针对统一消息的任何入站呼叫或会话初始协议 (SIP) 请求的入口点。UM 呼叫路由器服务处理 Exchange 2013 客户端访问服务器上的 SIP 请求，它运行在组织中的每个 Exchange 2013 客户端访问服务器上。

当要升级到 Exchange 2013 UM 时，应将已安装及配置过的单个或多个 VoIP 网关连接至电话网络中的 PBX，或已安装及配置过的启用会话初始协议 (SIP) 的 PBX 或 IP PBX。

升级到 Exchange 2013 UM 过程的最后一步是将 VoIP 网关、IP PBX 或启用 SIP 的 PBX 配置为向 Exchange 2013 客户端访问服务器发送传入呼叫（包括呼叫者想给用户留下语音邮件、启用 UM 的使用者呼入 Outlook Voice Access，以及呼叫者拨号到 UM 自动助理等呼叫形式）。所有这些呼叫最初是由 VoIP 网关、IP PBX 或启用 SIP 的 PBX 收到，并转发给 Exchange 2013 组织中的 Exchange 2013 客户端访问服务器。有关详细信息，请参阅下列资源：

  -  [UM 服务](um-services-exchange-2013-help.md)

  -  [支持的 VoIP 网关、IP PBX 和 PBX 的配置说明](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  -  [Exchange 2013 电话顾问](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

## 第 14 步︰ 禁用 Exchange 2007 统一消息服务器上的呼叫应答

您可以禁用呼叫应答通过 Exchange 2007 统一消息服务器上禁用 UM 或拨号计划中删除的 UM 服务器。当禁用 UM 时，您防止应答传入呼叫统一消息服务器。您可以选择立即断开所有呼叫或等待现有呼叫之前禁用统一消息服务器进行处理。您需要禁用呼叫之前删除拨号计划的服务器，以便它将完成处理所有传入呼叫应答。

要使用 Exchange 管理控制台禁用 Exchange 2007 UM 服务器上的统一消息，请执行以下步骤：

1.  在 EMC 的控制台树中，导航到\&quot;服务器配置\&quot;\>\&quot;统一消息\&quot;。

2.  在结果窗格中，选择要禁用的统一消息服务器。

3.  在操作窗格中，单击下列选项之一：
    
    1.  选择\&quot;立即禁用\&quot;选项时，统一消息服务器将断开连接到统一消息服务器的所有呼叫。
    
    2.  选择\&quot;完成呼叫后禁用\&quot;选项时，统一消息服务器将不接受新呼叫，并且会在处理完所有呼叫后再禁用。

4.  在确认对话框中，单击\&quot;是\&quot;继续操作。

若要使用命令行管理程序禁用 Exchange 2007 UM 服务器上的统一消息，请运行以下命令：

    Disable-UMServer -Identity MyUMServer -Immediate $true

> [!tip]
> 您可以使用 Exchange 2007 UM 服务器的 <strong>Disable-UMServer</strong> cmdlet 或 Exchange 2013 邮箱服务器的 <strong>Disable-UMService</strong> cmdlet 禁用呼叫应答功能。


## 第 15 步︰ 从拨号计划中删除 Exchange 2007 统一消息服务器

要处理的调用，必须将 Exchange 2007 UM 服务器添加到至少一个 UM 拨号计划。UM 服务器可以加入多个 UM 拨号计划。Exchange 2007 UM 服务器可以删除 UM 拨号计划。当从拨号计划中删除 UM 服务器时，UM 服务器将不再接听电话或启用 UM 的用户的 UM 呼叫。

使用 Exchange 管理控制台将 Exchange 2007 UM 服务器从拨号计划中删除：

1.  在 EMC 的控制台树中，导航到\&quot;服务器配置\&quot;\>\&quot;统一消息\&quot;。

2.  在结果窗格中，选择统一消息服务器。

3.  在操作窗格中，单击\&quot;属性\&quot;。

4.  在\&quot;UM 设置\&quot;选项卡的\&quot;关联的拨号计划\&quot;部分，单击\&quot;删除\&quot;。

5.  在确认对话框中，单击\&quot;是\&quot;确认从 UM 拨号计划中删除该 Exchange 2007 统一消息服务器。

6.  单击\&quot;确定\&quot;关闭属性窗口。

若要使用命令行管理程序将 Exchange 2007 UM 服务器从拨号计划中删除，请运行以下命令。

    $dp= Get-UMDialPlan "MySIPDialPlan"
    $s=Get-UMServer -id MyUMServer
    $s.dialplans-=$dp.identity
    Set-UMServer -id MyUMServer -dialplans:$s.dialplans

在此示例中，有三个 SIP URI 拨号计划：SipDP1、SipDP2 和 SipDP3。此示例从 SipDP3 拨号计划中删除名为 `MyUMServer` 的 UM 服务器。

    Set-UMServer -id MyUMServer -DialPlans SipDP1,SipDP2

在此示例中，有两个 SIP URI 拨号计划：SipDP1 和 SipDP2。此示例从 SipDP2 拨号计划中删除名为 `MyUMServer` 的 UM 服务器。

    Set-UMServer -id MyUMServer -DialPlans SipDP1

> [!tip]
> 可以在 Exchange 2007 统一消息服务器上的 Shell 或<strong>Set-UMService</strong> cmdlet 2013 的 Exchange 邮箱服务器上使用<strong>Set-UMServer</strong> cmdlet Exchange 2007 UM 服务器删除单个或多个拨号计划。例如，若要从所有拨号计划删除 UM 服务器，运行下面的命令︰ <code>Set-UMServer -identity MyUMServer -DialPlan $null</code>


## 您如何知道操作成功？

安装统一消息之后，验证以下内容以确保其正常工作：

  - 已经启用语音邮件的用户能够登录 Outlook Web 应用程序或 Outlook 并查看统一消息的欢迎消息。

  - UM 用户可接收语音邮件。

  - UM 用户可以呼叫 Outlook 语音访问号码，以收听电子邮件、日历项和语音邮件。

  - UM 可路由来自组织外部的呼叫，并且您可发出呼叫。

