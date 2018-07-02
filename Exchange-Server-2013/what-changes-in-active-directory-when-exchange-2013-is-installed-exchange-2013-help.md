---
title: '安装 Exchange 2013 后 Active Directory 中有哪些变化？: Exchange 2013 Help'
TOCTitle: 安装 Exchange 2013 后 Active Directory 中有哪些变化？
ms:assetid: 07386078-6103-49a2-8698-2d41db9cec95
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn750898(v=EXCHG.150)
ms:contentKeyID: 62371348
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安装 Exchange 2013 后 Active Directory 中有哪些变化？

 

_**适用于：**Exchange Server, Exchange Server 2013_

_**上一次修改主题：**2014-05-26_

安装 Exchange 2013 时，将会更改您的 Active Directory 林和域。Exchange 执行此操作是为了使其可以存储关于组织中 Exchange 服务器、邮箱以及与 Exchange 相关的其他对象的信息。这些更改将在 Exchange 2013 命令行设置过程中，在您运行 Exchange 2013 安装向导或运行 *PrepareSchema*、*PrepareAD* 和 *PrepareDomains* 命令时进行（在[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)中查看如何使用这些命令）。如果您想了解 Exchange 对 Active Directory 所做的更改，则本主题非常适合您。它说明了在 Active Directory 准备的每个步骤中 Exchange 执行的操作。

要针对 Exchange 准备 Active Directory，需要完成三个步骤：

  - 扩展 Active Directory 架构

  - 准备 Active Directory 容器、对象和其他项目

  - 准备 Active Directory 域

三个步骤全部完成后，您的 Active Directory 林即已为 Exchange 2013 做好准备。您可以阅读[使用安装向导安装 Exchange 2013](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)，查找有关如何安装 Exchange 2013 的详细信息。

## 扩展 Active Directory 架构

扩展 Active Directory 架构会添加和更新类、属性及其他项目。需要进行这些更改，以便 Exchange 可以创建容器和对象来存储关于 Exchange 组织的信息。Exchange 会对 Active Directory 进行大量更改，没有专用于此步骤的主题。要查看对架构所做的所有更改，请参阅 [Exchange 2013 Active Directory 架构更改](exchange-2013-active-directory-schema-changes-exchange-2013-help.md)。

当您在 Active Directory 林中的第一台 Exchange 2013 服务器上运行 Exchange 2013 安装向导时，将自动完成此步骤。当您在林中的第一台 Exchange 2013 服务器上通过 *PrepareSchema* 命令（也可以选择通过 *PrepareAD* 命令）运行 Exchange 2013 命令行安装时，也会执行此步骤。要了解有关如何扩展架构的详细信息，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)中的[Extend the Active Directory schema](prepare-active-directory-and-domains-exchange-2013-help.md)。

Exchange 扩展完架构之后，它将设置存储在 **ms-Exch-Schema-Version-Pt** 属性中的架构版本。如果您要确保 Active Directory 架构已成功扩展，您可以检查存储在该属性中的值。如果属性中的值与您安装的 Exchange 2013 版本所列的架构版本匹配，则说明架构扩展成功。要查看 Exchange 版本的列表以及如何检查该属性的值，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)中的[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)部分。

## 准备 Active Directory 容器、对象和其他项目

扩展架构后，下一步是添加 Exchange 用于在 Active Directory 中存储信息的所有容器、对象、属性和其他项目。在此步骤中所做的大部分更改将应用于整个 Active Directory 林。对安装期间运行 *PrepareAD* 命令的本地 Active Directory 域进行了少量更改。

下面是对 Active Directory 林所做的更改：

  - 在 CN=Services,CN=Configuration,DC=\<*root domain*\> 下创建 Microsoft Exchange 容器（如果尚不存在）。

  - 在 CN=\<*organization name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 下创建下列容器和对象（如果尚不存在）：
    
      - CN=Address Lists Container
    
      - CN=AddressBook Mailbox Policies
    
      - CN=Addressing
    
      - CN=Administrative Groups
    
      - CN=Approval Applications
    
      - CN=Auth Configuration
    
      - CN=Availability Configuration
    
      - CN=Client Access
    
      - CN=Connections
    
      - CN=ELC Folders Container
    
      - CN=ELC Mailbox Policies
    
      - CN=ExchangeAssistance
    
      - CN=Federation
    
      - CN=Federation Trusts
    
      - CN=Global Settings
    
      - CN=Hybrid Configuration
    
      - CN=Mobile Mailbox Policies
    
      - CN=Mobile Mailbox Settings
    
      - CN=Monitoring Settings
    
      - CN=OWA Mailbox Policies
    
      - CN=Provisioning Policy Container
    
      - CN=Push Notification Settings
    
      - CN=RBAC
    
      - CN=Recipient Policies
    
      - CN=Remote Accounts Policies Container
    
      - CN=Retention Policies Container
    
      - CN=Retention Policy Tag Container
    
      - CN=ServiceEndpoints
    
      - CN=System Policies
    
      - CN=Team Mailbox Provisioning Policies
    
      - CN=Transport Settings
    
      - CN=UM AutoAttendant Container
    
      - CN=UM DialPlan Container
    
      - CN=UM IPGateway Container
    
      - CN=UM Mailbox Policies
    
      - CN=Workload Management Settings

  - 在 CN=Transport Settings,CN=\<*Organization Name*\>,CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 下创建下列容器和对象（如果尚不存在）：
    
      - CN=Accepted Domains
    
      - CN=ControlPoint Config
    
      - CN=DNS Customization
    
      - CN=Interceptor Rules
    
      - CN=Malware Filter
    
      - CN=Message Classifications
    
      - CN=Message Hygiene
    
      - CN=Rules
    
      - CN=MicrosoftExchange329e71ec88ae4615bbc36ab6ce41109e

  - 在 Active Directory 中的整个配置分区设置权限。

  - 导入 Rights.ldf 文件。该文件将添加安装 Exchange 和配置 Active Directory 所需的权限。

  - MicrosoftExchange 安全组组织单位 (OU) 在林的根域中创建，并会向其分配权限。

  - 在 Microsoft Exchange 安全组 OU 内创建以下管理角色组（如果尚不存在）：
    
      - 遵从性管理
    
      - 委派安装
    
      - 发现管理
    
      - 技术支持
    
      - 清洁管理
    
      - 组织管理
    
      - 公用文件夹管理
    
      - 收件人管理
    
      - 记录管理
    
      - 服务器管理
    
      - UM 管理
    
      - 仅查看组织管理

  - 在 MicrosoftExchange 安全组 OU 中创建的新管理角色组（在 Active Directory 中显示为通用安全组 (USG)）将添加到存储在 CN=Microsoft Exchange,CN=Services,CN=Configuration,DC=\<*root domain*\> 容器中的 **otherWellKnownObjects** 属性。

  - 在根域的 Microsoft Exchange 系统对象容器中创建统一消息语音原始发送方联系人。

  - 运行 *PrepareAD* 命令的域已为 Exchange 2013 做好准备。有关应执行哪些操作以便为 Exchange 准备好 Active Directory 域的信息，请参阅准备 Active Directory 域。

  - Exchange 组织对象上的 **msExchProductId** 属性已设置。如果您要确保 Active Directory 架构已成功扩展，您可以检查存储在该属性中的值。如果属性中的值与您安装的 Exchange 2013 版本所列的架构版本匹配，则说明架构扩展成功。要查看 Exchange 版本的列表以及如何检查该属性的值，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)中的[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)部分。

## 准备 Active Directory 域

为 Exchange 准备 Active Directory 的最后一步是准备将安装 Exchange 服务器或启用邮箱的用户将位于的所有 Active Directory 域。最后一步将在运行 *PrepareAD* 命令的域中自动执行。

下面是对 Active Directory 域所做的更改：

  - 已在 Active Directory 中的根域分区中创建 Microsoft Exchange 系统对象容器（如果尚不存在）。

  - 已在 Exchange 服务器、组织管理和经过身份验证的用户安全组的 Microsoft Exchange 系统对象容器中设置权限。

  - Exchange 安装域服务器域全局组已在当前域中创建，并放置在 Microsoft Exchange 系统对象容器中。

  - Exchange 安装域服务器组已添加到根域中 Exchange 服务器 USG。

  - 已为 Exchange Server USG 和组织管理 USG 分配域级权限。

  - 已设置 DC=\<*root domain*\> 下 Microsoft Exchange 系统对象容器中的 **objectVersion** 属性。如果您要确保 Active Directory 架构已成功扩展，您可以检查存储在该属性中的值。如果属性中的值与您安装的 Exchange 2013 版本所列的架构版本匹配，则说明架构扩展成功。要查看 Exchange 版本的列表以及如何检查该属性的值，请参阅[准备 Active Directory 和域](prepare-active-directory-and-domains-exchange-2013-help.md)中的[How do you know this worked?](prepare-active-directory-and-domains-exchange-2013-help.md)部分。

