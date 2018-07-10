---
title: 'Exchange Server 混合部署: Exchange 2013 Help'
TOCTitle: '@NoTitle'
ms:assetid: 59e32000-4fcf-417f-a491-f1d8f9aeef9b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ200581(v=EXCHG.150)
ms:contentKeyID: 50492078
ms.date: 04/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 混合部署

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2018-04-16_


**摘要：**  规划 Exchange 混合部署需要了解的内容。

混合部署使组织可以将随其现有内部部署 Microsoft Exchange 组织提供的功能丰富的体验和管理控制扩展到云。混合部署可在内部部署 Exchange 组织与 Microsoft Office 365 中的 Exchange Online 之间提供单个 Exchange 组织的无缝观感。此外，混合部署还可以充当中间步骤，以完全移动到 Exchange Online 组织。

**目录**

Exchange 混合部署功能

Exchange 混合部署的注意事项

Exchange 混合部署组件

Exchange 混合部署示例

配置 Exchange 混合部署之前要考虑的事项

关键术语

Exchange 混合部署文档

## Exchange 混合部署功能

混合部署支持以下功能：

  - 内部部署组织与 Exchange Online 组织之间的安全邮件路由。

  - 使用共享域命名空间的邮件路由。例如，内部部署与 Exchange Online 组织都使用 @contoso.com SMTP 域。

  - 统一全局地址列表 (GAL)，也称为“共享地址簿”。

  - 内部部署组织与 Exchange Online 组织之间的忙/闲状态共享和日历共享。

  - 集中控制入站和出站邮件流。可以将所有入站和出站 Exchange Online 邮件配置为通过内部部署 Exchange 组织路由。

  - 用于内部部署和 Exchange Online 组织的单个 Web 上的 Outlook URL

  - 可以将现有内部部署邮箱移到 Exchange Online 组织。如果需要，还可以将 Exchange Online 邮箱移回内部部署组织。

  - 使用内部部署 Exchange 管理中心 (EAC) 集中管理邮箱。

  - 内部部署组织和 Exchange Online 组织之间的邮件跟踪、邮件提醒和多邮箱搜索。

  - 内部部署 Exchange 邮箱基于云的邮件存档。Exchange Online Archiving 可以与混合部署一起使用。有关 Exchange Online 存档的详细信息，请参阅 [Microsoft Office 365 其他服务](https://go.microsoft.com/fwlink/p/?linkid=233231)。

## Exchange 混合部署的注意事项

在实施 Exchange 混合部署前，您应考虑以下事项：

  - **混合部署要求** 配置混合部署之前的混合部署要求，您需要确保内部部署组织满足成功部署所需的所有先决条件。有关详细信息，请参阅[混合部署先决条件](hybrid-deployment-prerequisites-exchange-2013-help.md)。

  - **Exchange ActiveSync 客户端**  当您将邮箱从内部部署 Exchange 组织移到 Exchange Online 中时，需要将访问邮箱的所有客户端都更新为使用 Exchange Online；这包括 Exchange ActiveSync 设备。大多数 Exchange ActiveSync 客户端现在都会在邮箱移到 Exchange Online 中时自动重新配置，但是，某些旧的设备可能不会正确升级。有关详细信息，请参阅[Exchange ActiveSync 设备设置与 Exchange 混合部署](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **邮箱权限迁移**  将明确应用于邮箱的本地邮箱权限（如代理发送权限、完全访问权限、代表发送和文件夹权限）迁移到 Exchange Online。不会迁移继承（非明确）邮箱权限和授予给 Exchange Online 中未启用邮件的对象的权限。在迁移之前，请务必明确授予所有权限，并确保所有对象都启用邮件。因此，需要进行规划以在 Office 365 中配置这些权限（若适用于你的组织）。在代理发送权限情况下，如果尝试代理发送的用户和资源没有同时移动，则需要使用 **Add-RecipientPermission** cmdlet 在 Exchange Online 中显式添加代理发送权限。

  - **支持跨界邮箱权限** Exchange 混合部署支持在位于本地 Exchange 组织中的邮箱与位于 Office 365 中的邮箱之间使用完全访问和代表发送权限。“发送方式”权限需要其他步骤。此外，可能需要一些额外的配置来支持跨界邮箱权限，具体取决于在本地组织中安装的 Exchange 版本。有关详细信息，请参阅 [Permissions in Exchange hybrid deployments](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)和[Configure Exchange to support delegated mailbox permissions in a hybrid deployment](configure-exchange-to-support-delegated-mailbox-permissions-in-a-hybrid-deployment-exchange-2013-help.md)中的[委派邮箱权限](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md)。
    
    > [!NOTE]
    > 自 2018 年 2 月起，将推出支持完全访问权限、发送代表和跨林文件夹权限的功能，预计于 2018 年 4 月完成。


  - **场外传输**  作为日常收件人管理的一部分，您可能需要将 Exchange Online 邮箱移回本地环境。
    
    有关如何在基于 Exchange 2010 的混合部署中移动邮箱的详细信息，请参阅[将 Exchange Online 邮箱移到内部部署组织](https://technet.microsoft.com/zh-cn/library/hh882527\(v=exchg.150\))。
    
    有关如何在基于 Exchange 2013 或更新版本的混合部署中移动邮箱的详细信息，请参阅[在混合部署的本地组织和 Exchange Online 组织之间移动邮箱](move-mailboxes-between-on-premises-and-exchange-online-organizations-in-hybrid-deployments-exchange-2013-help.md)。

  - **邮箱转发设置** 可以将邮箱设置为，自动将收到的邮件转发给其他邮箱。虽然 Exchange Online 支持邮箱转发，但转发配置未随邮箱迁移一起复制到 Exchange Online 中。将邮箱迁移到 Exchange Online 前，请务必先导出各个邮箱的转发配置。转发配置存储在各个邮箱的 `DeliverToMailboxAndForward`、`ForwardingAddress` 和 `ForwardingSmtpAddress` 属性中。

## Exchange 混合部署组件

混合部署涉及多个不同的服务和组件：

  - **Exchange 服务器**  如果您想要配置混合部署，至少需要在内部部署组织中配置一个 Exchange 服务器。如果您运行 Exchange 2013 或更低版本，您需要至少安装一台运行邮箱角色和客户端访问角色的服务器。如果您运行 Exchange 2016 或更新版本，至少必须安装一台运行邮箱角色的服务器。如果需要，也可以在外围网络中安装 Exchange 边缘传输服务器，并支持与 Office 365 的安全邮件流。
    
    > [!NOTE]
    > 我们不支持在外围网络中安装运行邮箱服务器角色或客户端访问服务器角色的 Exchange 服务器。


  - **Microsoft Office 365**   Office 365 服务提供 Exchange Online 组织作为其订阅服务的一部分。配置混合部署的组织需要为迁移到 Exchange Online 组织或者在 Exchange Online 组织中创建的每个邮箱购买一个许可证。

  - **混合配置向导**Exchange 包括了混合配置向导；该向导提供了一个精简的流程，可以在内部部署 Exchange 与 Exchange Online 组织之间配置混合部署。
    
    有关详细信息，请参阅 [“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md)。

  - **Azure AD 身份验证系统**   Azure Active Directory (AD) 身份验证系统是基于云的免费服务，该服务可充当本地 Exchange 2016 组织与 Exchange Online 组织之间的信任代理。配置混合部署的本地组织必须具有与 Azure AD 身份验证系统之间的联合信任。可手动创建联合信任作为配置内部部署 Exchange 组织和其他联合 Exchange 组织之间的联合共享功能的一部分，或使用混合配置向导配置混合部署的一部分。Office 365 租户的 Azure AD 身份验证系统联合信任是在激活 Office 365 服务帐户时自动配置的。
    
    有关详细信息，请参阅 [Azure AD 身份验证系统](https://go.microsoft.com/fwlink/p/?linkid=135986)。

  - **Active Directory 同步**   Azure AD 同步使用 Azure AD Connect 将已启用邮件的对象的内部部署 Active Directory 信息复制到 Office 365 组织，以支持统一全局地址列表 (GAL) 和用户身份验证。配置混合部署的组织需要在单独的内部部署服务器上部署 Azure AD Connect 以将您的内部部署 Active Directory 与 Office 365 同步。
    
    可在以下位置了解详细信息：[Azure AD Connect - 概述](https://go.microsoft.com/fwlink/p/?linkid=203007)

关键术语

## 混合部署示例

看一下下面的情况。这是一个拓扑示例，概述了典型的 Exchange 2016 部署。Contoso, Ltd. 是一个单林单域组织，安装了两台域控制器和一台 Exchange 2016 服务器。远程 Contoso 用户使用 Web 上的 Outlook 通过 Internet 连接到 Exchange 2016 以检查其邮箱和访问其 Outlook 日历。

![在配置带有 Office 365 的混合部署之前所进行的本地 Exchange 部署](images/JJ200581.dad133ae-d18a-42ec-8f0a-dd1de391200e(EXCHG.150).png "在配置带有 Office 365 的混合部署之前所进行的本地 Exchange 部署")

假设您是 Contoso 的网络管理员，同时对配置混合部署感兴趣。您部署与配置符合要求的 Active Directory 同步服务器，同时还决定使用 Azure AD Connect 密码同步功能让用户对其内部部署网络帐户和其 Office 365 帐户使用相同的凭据。完成混合部署先决条件，以及使用混合配置向导选择了混合部署的选项之后，新的拓扑具有以下配置：

  - 用户将使用其相同的用户名和密码登录到内部部署组织和 Exchange Online 组织（“单点登录”）。

  - 位于内部部署组织和 Exchange Online 组织中的用户邮箱将使用相同的电子邮件地址域。例如，位于内部部署组织和 Exchange Online 组织中的邮箱都将在用户电子邮件地址中使用 @contoso.com。

  - 所有出站邮件都将通过内部部署组织传递到 Internet。内部部署组织控制所有邮件传输，并充当 Exchange Online 组织的中继（“集中邮件传输”）。

  - 内部部署组织用户和 Exchange Online 组织用户可以相互共享日历忙/闲信息。为这两个组织配置的组织关系还将启用跨内部部署邮件跟踪、邮件提示和邮件搜索。

  - 内部部署用户和 Exchange Online 用户使用相同的 URL 通过 Internet 连接到其邮箱。

![在配置带有 Office 365 的混合部署之后所进行的本地 Exchange 部署](images/JJ200581.e8681849-f15d-4d0e-b77e-6105b6096c4b(EXCHG.150).png "在配置带有 Office 365 的混合部署之后所进行的本地 Exchange 部署")

如果将 Contoso 的现有组织配置与混合部署配置进行比较，可以看到通过配置混合部署，添加了支持其他通信和功能的服务器和服务，这些通信和功能在内部部署组织和 Exchange Online 组织之间共享。下面概述了混合部署相对于初始内部部署 Exchange 组织所发生的变化。


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>配置</th>
<th>混合部署前</th>
<th>混合部署之后</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>邮箱位置</p></td>
<td><p>邮箱仅位于内部部署组织中。</p></td>
<td><p>内部部署邮箱与 Office 365 中的邮箱。</p></td>
</tr>
<tr class="even">
<td><p>邮件传输</p></td>
<td><p>内部部署邮箱服务器处理所有入站和出站邮件路由。</p></td>
<td><p>内部部署邮箱服务器处理内部部署组织与 Office 365 组织之间的内部邮件路由。</p></td>
</tr>
<tr class="odd">
<td><p>Web 上的 Outlook</p></td>
<td><p>内部部署邮箱服务器接收所有 Web 上的 Outlook 请求并显示邮箱信息。</p></td>
<td><p>内部部署邮箱服务器将 Web 上的 Outlook 请求重定向到内部部署 Exchange 2016 邮箱服务器或提供登录 Office 365 的链接。</p></td>
</tr>
<tr class="even">
<td><p>用于两个组织的统一 GAL</p></td>
<td><p>不适用；仅限单个组织。</p></td>
<td><p>内部部署 Active Directory 同步服务器将已启用邮件的对象的 Active Directory 信息复制到 Office 365。</p></td>
</tr>
<tr class="odd">
<td><p>用于两个组织的单一登录</p></td>
<td><p>不适用；仅限单个组织。</p></td>
<td><p>内部部署 Active Directory 和 Office 365 对位于内部部署或 Office 365 中的邮箱使用相同的用户名和密码。</p></td>
</tr>
<tr class="even">
<td><p>与 Azure AD 身份验证系统建立的组织关系和联合信任</p></td>
<td><p>可以配置与 Azure AD 身份验证系统的信任关系以及与其他联合 Exchange 组织的组织关系。</p></td>
<td><p>必须与 Azure AD 身份验证系统建立信任关系。内部部署与 Office 365 之间建立组织关系。</p></td>
</tr>
<tr class="odd">
<td><p>忙/闲共享</p></td>
<td><p>仅在内部部署用户之间共享忙/闲信息。</p></td>
<td><p>在内部部署用户之间和 Office 365 用户之间共享忙/闲信息。</p></td>
</tr>
</tbody>
</table>


## 配置混合部署之前要考虑的事项

现在，您已对什么是混合部署有了进一步的了解，该认真考虑一些重要的问题了。配置混合部署可能会影响您当前网络和 Exchange 组织中的多个方面。

## 目录同步和单一登录

内部部署组织和 Office 365 组织之间的 Active Directory 同步（由运行 Azure Active Directory Connect 的服务器每三小时执行一次）是配置混合部署的一项要求。目录同步使任一组织中的收件人可以在全局地址列表中看到彼此。它还将同步用户名和密码，使用户可以在内部部署组织和 Office 365 组织中使用相同凭据登录。

> [!NOTE]
> 如果您选择使用 AD FS 配置 Azure AD Connect，默认情况下，内部部署用户的用户名和密码将仍会同步到 Office 365。但是，用户将通过 AD FS 对内部部署 Active Directory 进行身份验证，作为其主要身份验证方法。如果出于任何原因，AD FS 无法连接到您的内部部署 Active Directory，客户端将尝试回退并对同步到 Office 365 的用户名和密码进行身份验证。


默认情况下，所有 Azure Active Directory 和 Office 365 客户的对象限制为 50,000 个（用户、已启用邮件的联系人、组）。此限制确定可以在 Office 365 组织中创建的对象数。当您验证第一个域时，此对象限制会自动增加至 300,000 个对象。如果您已验证一个域并需要同步 300,000 个以上的对象，或者您没有任何域要验证并需要同步 50,000 个以上的对象，则需要与 Azure Active Directory 支持联系以请求提高对象配额限制。

如果选择配置 AD FS，除了运行 Azure AD Connect 的服务器，您还需要部署 Web 应用程序代理服务器。此服务器应置于外围网络中，并将充当内部 Azure AD Connect 服务器和 Internet 之间的中介。Web 应用程序代理服务器需要接受 Internet 上使用 TCP 端口 443 的客户端和服务器请求进行的连接。

## 混合部署管理

通过单个统一管理控制台，您可以管理 Exchange 2016 的混合部署，允许同时管理您的内部部署和 Office 365 Exchange Online 组织。替换 Exchange 管理控制台和 Exchange 控制面板的 *Exchange 管理中心* (EAC) 允许您连接和配置两个组织的 功能。当首次运行混合配置向导时，将提示您连接 Exchange Online 组织。您需要使用作为组织管理角色组之一的 Office 365 帐户连接 EAC 到您的 Exchange Online 组织。

## 证书

安全套接字层 (SSL) 数字证书对配置混合部署非常重要。这些证书有助于保证内部部署混合服务器与 Exchange Online 组织之间的通信安全。证书是配置几个服务类型的要求。如果您的 Exchange 组织中已在使用数字证书，可能需要修改证书以包括其他域或者从受信任的证书颁发机构 (CA) 购买其他证书。如果未使用证书，则需要从受信任的 CA 购买一个或多个证书。

可在以下位置了解详细信息：[混合部署的证书要求](certificate-requirements-for-hybrid-deployments-exchange-2013-help.md)

## 带宽

与 Internet 的网络连接会直接影响内部部署组织与 Office 365 组织之间的通信性能。尤其是在将邮箱从内部部署 Exchange 2016 服务器移到 Office 365 组织时。可用的网络带宽量以及邮箱大小和同时移动的邮箱数会导致完成邮箱移动的时间有所不同。此外，其他 Office 365 服务（例如 SharePoint Server 2016 和 Skype for Business）也可能会影响可用于邮件服务的带宽。

将邮箱移动到 Office 365 之前，您应该完成以下事项：

  - 确定将移动到 Office 365 的邮箱的平均大小。

  - 确定从内部部署组织连接到 Internet 的平均连接速度和吞吐速度。

  - 计算预期的平均传输速度，然后相应地制定邮箱移动计划。

可在以下位置了解详细信息：[网络](https://go.microsoft.com/fwlink/p/?linkid=280178)

## 统一消息

内部部署组织与 Office 365 组织之间的混合部署中支持统一消息 (UM)。内部部署电话解决方案必须能与 Office 365 组织进行通信。这可能需要购买其他硬件和软件。

如果要将邮箱从内部部署组织移至 Office 365，并且为这些邮箱配置了 UM 功能，则应先在混合部署中配置 UM，然后再移动这些邮箱。如果先移动邮箱，然后再在混合部署中配置 UM，则这些邮箱将无法再访问 UM 功能。

有关详细信息，请参阅：[在混合部署中设置统一消息](https://go.microsoft.com/fwlink/p/?linkid=842271)

## 信息权限管理

通过信息权限管理 (IRM)，用户可将 Active Directory 权限管理服务 (AD RMS) 模板应用于其发送的邮件。AD RMS 模板可通过允许用户控制谁可打开受权限保护的邮件及其打开邮件后可对邮件执行什么操作，从而帮助防止信息泄漏。

混合部署中的 IRM 需要进行规划、手动配置 Office 365 组织，并要了解客户端应根据其邮箱是位于内部部署组织还是 Exchange Online 组织中而如何使用 AD RMS 服务器。

可在以下位置了解详细信息：[Exchange 混合部署中的 IRM](irm-in-exchange-hybrid-deployments-exchange-2013-help.md)

## 移动设备

混合部署中支持移动设备。如果现有服务器已经启用 Exchange ActiveSync，它们会继续将来自移动设备的请求重定向到位于内部部署邮箱服务器的邮箱。对于连接到从内部部署组织移到 Office 365 的现有邮箱的设备，将会自动更新 Exchange ActiveSync 配置文件以连接至大多电话上的 Office 365。支持 Exchange ActiveSync 的所有移动设备应与混合部署兼容。

可在以下位置了解详细信息：[移动电话](https://go.microsoft.com/fwlink/p/?linkid=206387)

## 客户端要求

建议您的客户端使用 Outlook 2016 或 Outlook 2013，以便在混合部署中实现最佳体验和性能。Outlook 2010 之前的客户端在混合部署中或者 Office 365 中不受支持。

## Office 365 的许可

若要在 Office 365 中创建邮箱或将邮箱移至 Office 365，需要注册用于企业的 Office 365 并且必须具有可用的许可证。注册 Office 365 后，您将会收到特定数量的许可证，可以将这些许可证分配给新邮箱或从内部部署组织移动的邮箱。Office 365 中的每个邮箱都必须有许可证。

## 防病毒和反垃圾邮件服务

对于移至 Office 365 的邮箱，系统会自动通过 Exchange Online Protection (EOP) 为其提供防病毒和反垃圾邮件保护，一种 Office 365 提供的服务。如果选择通过 EOP 服务路由所有传入的 Internet 邮件，则可能需要为您的内部部署用户购买其他 EOP 许可证。我们建议您仔细评估您的 Office 365 中的 EOP 保护是否也适合满足内部部署组织的防病毒和反垃圾邮件需要。如果您已经实施了内部部署组织保护，则可能需要升级或配置您的内部部署防病毒和反垃圾邮件解决方案，以期在整个组织中实现最大程度的保护。

可在以下位置了解详细信息：[反垃圾邮件和反恶意软件保护](https://technet.microsoft.com/zh-cn/library/jj200731\(v=exchg.150\))

## 公用文件夹

Office 365 支持公用文件夹，同时内部部署公共文件夹可迁移到 Office 365。此外，Office 365 中的公共文件夹可以移动到内部部署 Exchange 2016 组织。内部部署和 Office 365 用户均可以使用 Web 上的 Outlook、Outlook 2016、Outlook 2013 或 Outlook 2010 SP2或更新版本访问位于两个组织中的公用文件夹。配置混合部署时不会改变现有的内部部署公用文件夹配置和对内部部署邮箱的访问权限。

可在以下位置了解详细信息：[公用文件夹](https://technet.microsoft.com/zh-cn/library/jj150538\(v=exchg.150\))

## 辅助功能

若要了解可能适用于此清单中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](https://technet.microsoft.com/zh-cn/library/jj150484\(v=exchg.150\))。

## 关键术语

以下列表提供了与 Exchange 2013 中的混合部署关联的核心组件的定义。

  - **集中邮件传输**  
    混合配置选项，其中所有 Exchange Online 入站和出站 Internet 邮件都通过内部部署 Exchange 组织路由。此路由选项在混合配置向导中配置。有关详细信息，请参阅[Exchange 混合部署的传输选项](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)。

<!-- end list -->

  - **共存域**  
    一种接受域，添加到内部部署组织中用于 Office 365 服务的混合邮件流和自动发现请求。此域作为辅助代理域添加到具有在混合配置向导中选择的 *PrimarySmtpAddress* 域模板的任何电子邮件地址策略中。默认情况下，此域是 \<域\>.mail.onmicrosoft.com。

<!-- end list -->

  - ***HybridConfiguration* Active Directory 对象**  
    内部部署组织中的 Active Directory 对象，其中包含按混合配置向导中选择的内容定义的所需混合部署配置参数。混合配置引擎在配置内部部署和 Exchange Online 设置时使用这些参数来启用混合功能。每次运行混合配置向导时，都会重置 *HybridConfiguration* 对象的内容。

<!-- end list -->

  - **混合配置引擎**  
    混合配置引擎 (HCE) 运行配置和更新混合部署所需的核心操作。HCE 将 *HybridConfiguration* Active Directory 对象的状态与当前的内部部署 Exchange 和 Exchange Online 配置设置进行比较，然后执行任务将部署配置设置与 *HybridConfiguration* Active Directory 对象中定义的参数匹配。有关详细信息，请参阅[混合配置引擎](hybrid-configuration-wizard-exchange-2013-help.md)。

<!-- end list -->

  - **混合配置向导 (HCW)**  
    Exchange 提供的一种自适应工具，可指导管理员完成内部部署组织和 Exchange Online 组织之间的混合部署配置。该向导定义 *HybridConfiguration* 对象中的混合部署配置参数，并指示混合配置引擎运行必要的配置任务以启用定义的混合功能。有关详细信息，请参阅[“混合配置”向导](hybrid-configuration-wizard-exchange-2013-help.md)。

<!-- end list -->

  - **基于 Exchange 2010 的混合部署**  
    一种混合部署，配置时使用 Exchange Server 2010 Service Pack 3 (SP3) 内部部署服务器作为 Office 365 和 Exchange Online 服务连接终结点。一种混合部署选项，适用于内部部署 Exchange 2010、Exchange Server 2007 和 Exchange Server 2003 组织。

<!-- end list -->

  - **基于 Exchange 2013 的混合部署**  
    一种混合部署，配置时使用 2013 内部部署服务器作为 Office 365 和 Exchange Online 服务连接终结点。一种混合部署选项，适用于内部部署 Exchange 2013、Exchange 2010 和 Exchange 2007 组织。

<!-- end list -->

  - **基于 Exchange 2016 的混合部署**  
    一种混合部署，配置时使用 2016 内部部署服务器作为 Office 365 和 Exchange Online 服务连接终结点。一种混合部署选项，适用于内部部署 Exchange 2016、Exchange 2013 和 Exchange 2010 组织。

<!-- end list -->

  - **安全邮件传输**  
    一种自动配置的混合部署功能，可实现内部部署组织与 Exchange Online 组织之间的安全邮件传递。邮件使用传输层安全性 (TLS) 进行加密和身份验证，采用混合部署向导中选择的证书。Office 365 租户是源于内部部署组织的混合传输连接的终结点，是从 Exchange Online 到内部部署组织的混合传输连接的来源。

关键术语

## Exchange 混合部署文档

下表包含主题链接，这将帮助您学习和管理 Microsoft Exchange 的混合部署。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="hybrid-configuration-wizard-exchange-2013-help.md">“混合配置”向导</a></p></td>
<td><p>了解混合配置向导和混合配置引擎如何配置混合部署的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署先决条件</a></p></td>
<td><p>了解混合部署先决条件的详细信息，包括兼容 Exchange Server 组织、Office 365 要求和其他内部部署配置要求。</p></td>
</tr>
<tr class="odd">
<td><p><a href="certificate-requirements-for-hybrid-deployments-exchange-2013-help.md">混合部署的证书要求</a></p></td>
<td><p>了解有关混合部署数字证书要求的详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署的传输选项</a></p></td>
<td><p>了解有关混合部署中的入站和出站邮件传输选项的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-routing-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署中的传输路由</a></p></td>
<td><p>了解有关混合部署中的入站和出站邮件路由选项的详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-management-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署中的混合管理</a></p></td>
<td><p>了解有关使用 Exchange 管理中心和 Exchange 命令行管理程序管理混合部署的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="shared-free-busy-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署中共享的忙/闲信息</a></p></td>
<td><p>了解有关混合部署中的内部部署和 Exchange Online 组织之间的日历闲/忙共享的详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="server-roles-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署中的服务器角色</a></p></td>
<td><p>了解混合部署中的 Exchange 服务器角色如何运行的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="irm-in-exchange-hybrid-deployments-exchange-2013-help.md">Exchange 混合部署中的 IRM</a></p></td>
<td><p>了解有关混合部署中的信息权限管理如何运行的详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="permissions-in-exchange-hybrid-deployments-exchange-2013-help.md">Permissions in Exchange hybrid deployments</a></p></td>
<td><p>了解有关混合部署如何使用基于角色的访问控制 (RBAC) 控制权限的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-transport-servers-with-hybrid-deployments-exchange-2013-help.md">混合部署中的边缘传输服务器</a></p></td>
<td><p>了解 Exchange 边缘传输服务器以及如何在混合部署中部署和运营的详细信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="single-sign-on-with-hybrid-deployments-exchange-2013-help.md">混合部署中的单一登录</a></p></td>
<td><p>了解如何使用混合部署中的密码同步和 AD FS 功能进行单一登录的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployment-procedures-exchange-2013-help.md">Hybrid Deployment procedures</a></p></td>
<td><p>探索创建和修改 Exchange 内部部署和 Exchange Online 组织的混合部署的程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2010-exchange-2013-help.md">Exchange 2013 和 Exchange 2010 的混合部署</a></p></td>
<td><p>了解有关针对 Exchange 2010 组织进行基于 Exchange 2013 的混合部署的详细信息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hybrid-deployments-with-exchange-2013-and-exchange-2007-exchange-2013-help.md">Exchange 2013 和 Exchange 2007 的混合部署</a></p></td>
<td><p>了解有关针对 Exchange 2007 组织进行基于 Exchange 2013 的混合部署的详细信息。</p></td>
</tr>
</tbody>
</table>


## 刚开始接触 Office 365？


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/JJ200581.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="“领英学习”短图标" alt="“领英学习”短图标" /> <strong>刚开始接触 Office 365？</strong><br />
发现 LinkedIn Learning 向 <a href="https://support.office.com/zh-cn/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>提供的免费视频课程。</p></td>
</tr>
</tbody>
</table>

