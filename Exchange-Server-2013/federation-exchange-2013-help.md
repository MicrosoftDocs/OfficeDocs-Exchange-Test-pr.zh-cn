---
title: '联盟: Exchange 2013 Help'
TOCTitle: 联盟
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50489819
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 联盟

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

信息工作人员经常需要与外部收件人、供应商、合作伙伴和客户协作，并共享其忙/闲（也称为日历可用性）信息。Microsoft Exchange Server 2013 中的联合身份验证可帮助进行这些协作工作。“联合身份验证”指支持“联合共享”（用户与其他外部联盟组织中的收件人共享日历信息的一种简单方法）的基本信任基础结构。若要了解有关联合共享的详细信息，请参阅[共享](sharing-exchange-2013-help.md)。

> [!IMPORTANT]  
> Exchange Server 2013 的此项功能与由世纪互联在中国运营的 Office 365 不完全兼容，可能需要遵循一些功能限制。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/?linkid=313640">了解由世纪互联运营的 Office 365</a>。


**目录**

关键术语

Azure AD 身份验证系统

联合身份验证信任

联盟组织标识符

联合身份验证示例

联合身份验证证书要求

转换到新证书

联合身份验证的防火墙注意事项

## 关键术语

下表定义 Exchange 2013 中与联合身份验证关联的核心组件。

  - **应用程序标识符 (AppID)**  
    由 Azure Active Directory 身份验证系统生成的唯一编号用于标识 Exchange 组织。在创建与 Azure Active Directory 身份验证系统的联合身份验证信任时，会自动生成 AppID。

<!-- end list -->

  - **委派令牌**  
    Azure Active Directory 身份验证系统颁发的安全声明标记语言 (SAML) 令牌，使一个联盟组织中的用户可以受到另一个联盟组织的信任。委派令牌包含用户的电子邮件地址、不可变标识符以及与颁发该令牌进行行动所针对的要约相关联的信息。

<!-- end list -->

  - **外部联盟组织**  
    与 Azure Active Directory 身份验证系统建立了联合身份验证信任的外部 Exchange 组织。

<!-- end list -->

  - **联合共享**  
    利用与 Azure Active Directory 身份验证系统的联合身份验证信任跨 Exchange 组织工作的一组 Exchange 功能，包括跨界 Exchange 部署。这些功能结合在一起用于跨多个 Exchange 组织，代表用户在服务器之间进行经身份验证的请求。

<!-- end list -->

  - **联盟域**  
    添加到 Exchange 组织的组织标识符 (OrgID) 的接受权威域。

<!-- end list -->

  - **域证明加密字符串**  
    一种密码安全字符串，Exchange 组织使用它来证明组织拥有用于 Azure Active Directory 身份验证系统的域。此字符串可在使用“启用联合身份验证信任”向导时自动生成，也可以使用 **Get-FederatedDomainProof** cmdlet 生成。

<!-- end list -->

  - **联合共享策略**  
    一种组织级别策略，可启用和控制用户建立的、日历信息的人员对人员共享。

<!-- end list -->

  - **联合**  
    两个 Exchange 组织之间为实现共同目的而达成的基于信任的协议。使用联合身份验证时，两个组织都希望来自一个组织的身份验证断言可由对方识别。

<!-- end list -->

  - **联合身份验证信任**  
    与 Azure Active Directory 身份验证系统的一种关系，为 Exchange 组织定义了以下组件：
    
      - 帐户命名空间
    
      - 应用程序标识符 (AppID)
    
      - 组织标识符 (OrgID)
    
      - 联盟域
    
    若要配置与其他联盟 Exchange 组织的联合共享，必须与 Azure Active Directory 身份验证系统建立联合身份验证信任。

<!-- end list -->

  - **非联盟组织**  
    未与 Azure Active Directory 身份验证系统建立联合身份验证信任的组织。

<!-- end list -->

  - **组织标识符 (OrgID)**  
    定义为联合身份验证启用了组织中配置的哪些权威接受域。只有具有电子邮件地址以及在 OrgID 中配置了联盟域的收件人，才会被 Azure Active Directory 身份验证系统识别，并能够使用联合共享功能。此 OrgID 是预定义字符串与在“启用联合身份验证信任”向导中为联合身份验证选择的第一个接受的域的组合。例如，如果指定联盟域 contoso.com 作为组织的主 SMTP 域，则会自动创建 FYDIBOHF25SPDLT.contoso.com 帐户命名空间作为联合身份验证信任的 OrgID。

<!-- end list -->

  - **组织关系**  
    两个联盟 Exchange 组织之间的一种一对一关系，该关系使收件人可以共享忙/闲（日历可用性）信息。组织关系需要与 Azure Active Directory 身份验证系统建立联合身份验证信任，从而无需在 Exchange 组织之间使用 Active Directory 林或域信任。

<!-- end list -->

  - **Azure Active Directory 身份验证系统**  
    在联盟 Microsoft Exchange 组织之间充当信任代理的基于云的免费标识服务。它负责在 Exchange 收件人请求从其他联盟 Exchange 组织中的收件人获取信息时，向这些收件人颁发委派令牌。若要了解详细信息，请参阅 [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)。

## Azure AD 身份验证系统

Azure Active Directory 身份验证系统是由 Microsoft 提供的一种基于云的免费服务，充当本地 Exchange 2013 组织与其他联盟 Exchange 2010 和 Exchange 2013 组织之间的信任代理。如果您要在 Exchange 组织中配置联合身份验证，则必须与 Azure Active Directory 身份验证系统建立一次性联合身份验证信任，以便该网关可以成为组织的联盟伙伴。建立了此信任之后，Azure AD 身份验证系统可为通过 Active Directory（称为“身份提供程序”）身份验证的用户颁发安全声明标记语言 (SAML) 委派标记。这些委派令牌可以让来自一个联盟 Exchange 组织的用户受到其他联盟 Exchange 组织的信任。有了 Azure AD 身份验证系统充当信任代理，组织便无需与其他组织建立多个单独的信任关系，用户可以使用单一登录 (SSO) 功能访问外部资源。有关详细信息，请参阅 [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)。

关键术语

## 联合身份验证信任

若要使用 Exchange 2013 联合共享功能，必须在 Exchange 2013 组织与 Azure AD 身份验证系统之间建立联合身份验证信任。与 Azure AD 身份验证系统建立联合身份验证信任会与 Azure AD 身份验证系统交换组织的数字安全证书，并检索 Azure AD 身份验证系统证书和联合身份验证元数据。可以在 Exchange 管理中心 (EAC) 中使用“启用联合身份验证信任”向导，或在 Exchange 命令行管理程序中使用 **New-FederationTrust** cmdlet 建立联合身份验证信任。“启用联合身份验证信任”向导会自动创建一个自签名证书，该证书用于对来自 Azure AD 身份验证系统的、使用户可以受外部联盟组织信任的委派令牌进行签名和加密。有关证书要求的详细信息，请参阅本主题后面的联合身份验证证书要求。

使用 Azure AD 身份验证系统创建联合身份验证信任时，将自动为您的 Exchange 组织生成一个“应用程序标识符”(AppID)，该标识符在 **Get-FederationTrust** cmdlet 的输出中提供。Azure AD 身份验证系统使用 AppID 来唯一标识您的 Exchange 组织。Exchange 组织也使用 AppID 来证明组织拥有用于 Azure AD 身份验证系统的域。这通过在各个联盟域的公用域名系统 (DNS) 区域中创建文本 (TXT) 记录来实现。

关键术语

## 联盟组织标识符

“联盟组织标识符”(OrgID) 定义对组织中配置的哪些权威接受域启用联合身份验证。只有具有电子邮件地址以及在 OrgID 中配置了接受域的收件人，才会被 Azure AD 身份验证系统识别，并能够使用联合共享功能。创建新联合身份验证信任时，会自动通过 Azure AD 身份验证系统创建一个 OrgID。此 OrgID 是预定义字符串与在向导中选择作为主共享域的接受的域的组合。例如，在“编辑启用共享的域”向导中，如果指定联盟域“contoso.com”作为组织中的主共享域，则会自动创建“FYDIBOHF25SPDLT.contoso.com”帐户命名空间作为 Exchange 组织的联合身份验证信任的 OrgID。

虽然通常是 Exchange 组织的主 SMTP 域，但是此子域不必是 Exchange 组织中的接受域，并且不需要域名系统 (DNS) 所有权证明 TXT 记录。唯一的要求是选择进行联盟的接受的域限制为最多 32 个字符。此子域的唯一用途是充当 Azure AD 身份验证系统的联合命名空间，以便维护与请求 SAML 委派令牌的收件人对应的唯一标识符。有关 SAML 令牌的详细信息，请参阅 [SAML 令牌和声明](https://go.microsoft.com/fwlink/?linkid=198561)

可以随时从联合身份验证信任中添加或删除接受的域。如果您要在组织中启用或禁用所有联合共享功能，则您只需为联合身份验证信任启用或禁用 OrgID。

> [!IMPORTANT]  
> 如果更改用于联合身份验证信任的 OrgID、接受的域或 AppID，则组织中的所有联合共享功能都会受到影响。这还会影响所有外部联盟 Exchange 组织，包括 Exchange Online 和混合部署配置。建议您将对这些联合身份验证信任配置设置的任何更改都通知给所有外部联盟伙伴。


关键术语

## 联合身份验证示例

两个 Exchange 组织 Contoso, Ltd. 和 Fabrikam, Inc. 都希望其用户能够互相共享日历忙/闲信息。每个组织都与 Azure AD 身份验证系统创建联合身份验证信任，并将其帐户命名空间配置为包括用于其用户电子邮件地址域的域。

Contoso 员工使用以下电子邮件地址域之一：contoso.com、contoso.co.uk 或 contoso.ca。Fabrikam 员工使用以下电子邮件地址域之一：fabrikam.com、fabrikam.org 或 fabrikam.net。两个组织都确保在用于与 Azure AD 身份验证系统之间的联合身份验证信任的帐户命名空间中包括所有接受的电子邮件域。两个组织配置相互之间的组织关系以启用日历忙/闲共享，而不需要在两个组织之间进行复杂的 Active Directory 林或域信任配置。

下图说明 Contoso, Ltd. 与 Fabrikam, Inc. 之间的联合身份验证配置。

**联合共享示例**

![联合身份验证信任和联合共享](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "联合身份验证信任和联合共享")

## 联合身份验证证书要求

若要与 Azure AD 身份验证系统建立联合身份验证信任，必须创建自签名证书或由证书颁发机构 (CA) 签名的 X.509 证书，并在用于创建信任的 Exchange 2013 服务器上进行安装。强烈建议使用自签名证书，该证书可以在 EAC 中使用“启用联合身份验证信任”向导自动创建和安装。此证书仅用于对用于联合共享的委派令牌进行签名和加密，并且联合身份验证信任只需要一个证书。Exchange 2013 会将该证书自动分发给组织中的所有其他 Exchange 2013 服务器。

如果您要使用某个由外部 CA 签名的 X.509 证书，则该证书必须满足以下要求：

  - **受信任的 CA**   如果可以，应从受 Windows Live 信任的 CA 颁发 X.509 安全套接字层 (SSL) 证书。但是，可以使用由当前未经 Microsoft 认证的 CA 颁发的证书。有关受信任的 CA 的当前列表，请参阅[联合身份验证信任的受信任根证书颁发机构](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md)。

  - **主题密钥标识符：** 该证书必须具有主题密钥标识符字段。商业 CA 颁发的大多数 X.509 证书都具有此标识符。

  - **CryptoAPI 加密服务提供程序 (CSP)：** 该证书必须使用 CryptoAPI CSP。使用加密 API 的证书：联合身份验证不支持下一代 (CNG) 提供程序。如果使用 Exchange 创建证书请求，则使用 CryptoAPI 提供程序。有关详细信息，请参阅[加密 API：下一代](https://go.microsoft.com/fwlink/?linkid=187890)。

  - **RSA 签名算法：** 该证书必须使用 RSA 作为签名算法。

  - **可导出私钥：** 用于生成该证书的私钥必须可导出。在 EAC 中使用“新建 Exchange 证书”向导或在命令行管理程序中使用 [New-ExchangeCertificate](https://technet.microsoft.com/zh-cn/library/aa998327\(v=exchg.150\)) cmdlet 创建证书请求时，可以指定私钥可导出。

  - **当前证书：** 该证书必须是当前证书。不能使用过期或已吊销的证书来创建联合身份验证信任。

  - **增强密钥用法：** 证书必须包含增强密钥用法 (EKU) 类型的“客户端身份验证 (1.3.6.1.5.5.7.3.2)”。此使用类型用于向远程计算机证明您的身份。如果使用 EAC 或命令行管理程序生成证书请求，则此使用类型为默认包含项。

> [!NOTE]  
> 由于该证书不用于身份验证，因此它不包含任何主题名称或主题备用名称要求。可以使用主题名称与主机名、域名或任何其他名称相同的证书。


关键术语

## 转换到新证书

用于创建联合身份验证信任的证书被指定为当前证书。但是，您可能需要定期为联合身份验证信任安装和使用新证书。例如，如果当前证书过期，或为了满足新业务或安全要求，您可能需要使用新证书。为确保无缝转换为新证书，必须在 Exchange 2013 服务器上安装新证书，并配置联合身份验证信任以将其指定为新证书。Exchange 2013 会自动将新证书分发到组织中的所有其他 Exchange 2013 服务器。证书的分发可能需要一段时间，具体取决于您的 Active Directory 拓扑。可以在命令行管理程序中使用 [Test-FederationTrustCertificate](https://technet.microsoft.com/zh-cn/library/dd335228\(v=exchg.150\)) cmdlet 验证证书状态。

验证证书的分发状态后，便可将信任配置为使用新证书。切换证书后，当前证书被指定为上一个证书，而新证书则被指定为当前证书。新证书会发布到 Azure AD 身份验证系统，与 Azure AD 身份验证系统交换的所有新标记也将使用新证书加密。

> [!NOTE]  
> 只有联合身份验证才使用此证书转换过程。如果将同一证书用于其他需要证书的 Exchange 2013 功能，则在计划采购、安装或转换到新证书时，必须考虑相应的功能要求。


关键术语

## 联合身份验证的防火墙注意事项

联合身份验证功能要求您所在组织中的邮箱和客户端访问服务器使用 HTTPS 出站访问 Internet。必须允许出站 HTTPS 访问（TCP 的端口是 443）该组织中的所有 Exchange 2013 邮箱和客户端访问服务器。

为了使外部组织能够访问您所在组织的忙/闲信息，必须将一个客户端访问服务器发布到 Internet 上。这需要在 Internet 上通过入站 HTTPS 访问客户端访问服务器。Active Directory 站点（该站点未将客户端访问服务器发布到 Internet 上）中的客户端访问服务器可使用能够从 Internet 访问的其他 Active Directory 站点中的客户端访问服务器。未发布到 Internet 上的客户端访问服务器必须将 Web 服务虚拟目录的外部 URL 设置为对外部组织可见的 URL。

[返回顶部](sharing-exchange-2013-help.md)

