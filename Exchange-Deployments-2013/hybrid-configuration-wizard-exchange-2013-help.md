---
title: '“混合配置”向导: Exchange 2013 Help'
TOCTitle: “混合配置”向导
ms:assetid: 2e6ed294-ee74-4038-8b71-b61786372ba4
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Hh529921(v=EXCHG.150)
ms:contentKeyID: 50492073
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# “混合配置”向导

 

_<strong>适用于：</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>上一次修改主题：</strong>2016-12-09_

本主题将概述对您可用的 Exchange 混合部署配置过程、混合部署功能和选项以及混合配置引擎，这将执行同时配置和更新混合部署所需的核心操作。

有关混合部署的详细信息，请查看[Exchange Server 混合部署](exchange-server-hybrid-deployments-exchange-2013-help.md)。

**内容**

混合配置过程

混合配置功能

混合配置选项

混合配置引擎

## 混合配置过程

这里是“混合配置”向导过程的快速概述。首先，向导将在您的内部部署 Active Directory 中创建 **HybridConfiguration** 对象。此 Active Directory 对象会存储混合部署的混合配置信息，并通过“混合配置”向导进行更新。其次，向导将收集现有内部部署 Exchange 和 Active Directory 拓扑配置数据，Office 365 租户和 Exchange Online 配置数据，定义几个组织参数，然后同时在内部部署组织和 Exchange Online 组织中执行大量配置任务。

<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用“混合配置”向导之前您需要考虑一些重要因素和满足一些前提条件。您需要满足<a href="hybrid-deployment-prerequisites-exchange-2013-help.md">混合部署先决条件</a>中概括的混合部署的要求。满足这些要求即表示您已准备好使用“混合配置”向导为混合部署配置 Exchange 组织。</td>
</tr>
</tbody>
</table>


混合部署配置过程的一般阶段是：

1.  “验证先决条件并执行拓扑检查”   管理“混合配置”向导会验证内部部署组织和 Exchange Online 组织是否可以支持混合部署。向导在内部部署与 Exchange Online 组织中验证与检查的部分项目：
    
      - 内部部署 Exchange 服务器版本
    
      - Exchange Online 版本
    
      - Active Directory 同步状态和配置
    
      - 联盟与接受域
    
      - 现有联合身份验证信任和组织的关系
    
      - Web 服务虚拟目录
    
      - Exchange 证书

2.  **测试帐户凭据**   指定的内部部署和 Office 365 混合管理帐户会访问内部部署组织和 Exchange Online 组织，以收集先决条件验证信息并更改组织参数配置来启用混合部署功能。“混合配置”向导会检查这些帐户是否具有合适凭据以及是否可以连接到内部部署和 Exchange Online 组织。内部部署和 Office 365 组织的混合部署管理帐户必须是“混合配置”向导的组织管理角色组成员，才能成功完成这些任务。

3.  **进行混合部署配置更改**   在测试混合管理帐户、执行验证和拓扑检查，以及收集在向导过程中定义的配置信息之后，“混合配置”向导会更改配置以创建和启用混合部署。对混合配置进行的所有更改会自动记录在混合配置日志中。默认情况下，混合配置日志位于内部部署邮箱服务器的以下位置：`%UserProfile%\AppData\Roaming\Microsoft\Exchange Hybrid Configuration`。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>入站邮件流由组织的 MX 记录进行控制。“混合配置”向导不会配置混合部署的入站 Internet 电子邮件。</td>
    </tr>
    </tbody>
    </table>


## 混合配置功能

“混合配置”向导每次运行时，在默认情况下会自动启用所有混合部署功能。如果想要禁用某些特定混合配置功能，需要使用Exchange 命令行管理程序和 **Set-HybridConfiguration** cmdlet。默认情况下，该向导会启用以下混合部署功能：

  - **忙/闲共享**   通过忙/闲共享功能可在内部部署与 Exchange Online 的组织用户之间共享日历信息。忙/闲共享会在针对内部部署组织和 Exchange Online 组织的联合共享和组织关系配置中启用。有关详细信息，请参阅 [共享](https://technet.microsoft.com/zh-cn/library/dd638083\(v=exchg.150\))。

  - **邮件提示**   邮件提示是用户撰写邮件时向其显示的提示性消息。通过在混合部署中启用邮件提示，内部部署和 Exchange Onlline 的发件人可以调整所撰写的邮件，以避免组织之间出现不利情况或未送达报告 (NDR)。有关详细信息，请参阅 [MailTips](https://technet.microsoft.com/zh-cn/library/jj649091\(v=exchg.150\))。

  - **联机存档**   联机存档使 Exchange Online 的组织可以为内部部署和 Exchange Online 的用户承载用户电子邮件存档。有关更多信息，请参阅[配置 Exchange 在线存档](http://go.microsoft.com/fwlink/p/?linkid=266565)。

  - **Web 上的 Outlook重定向**Web 上的 Outlook 重定向提供单个通用 URL，以同时访问内部部署和 Exchange Online 邮箱。客户端访问服务器自动将 Web 上的 Outlook 请求重定向到内部部署邮箱服务器，或向用户提供其在 Exchange Online 组织中的邮箱的链接。

  - **Exchange ActiveSync 重定向**  当您将邮箱从本地 Exchange 组织移到 Exchange Online 中时，需要将访问邮箱的所有客户端都更新为使用 Exchange Online；这包括 Exchange ActiveSync 设备。大多数 Exchange ActiveSync 客户端现在都会在邮箱移到 Exchange Online 中时自动重新配置。有关详细信息，请参阅[Exchange ActiveSync 设备设置与 Exchange 混合部署](exchange-activesync-device-settings-with-exchange-hybrid-deployments-exchange-2013-help.md)。

  - **安全邮件**    安全邮件可通过传输层安全性 (TLS) 协议在内部部署与 Exchange Online 组织之间实现安全邮件传递。内部部署组织和 Exchange Online 组织通过数字证书主题互相进行身份验证，电子邮件头和 RTF 邮件格式会在组织间保留。

## 混合配置选项

“混合配置”向导允许选择某些方面的特定选项进行混合部署。如果混合部署完成最初配置之后，想要更新特定的混合配置选项，可以使用“混合配置”向导或Exchange 命令行管理程序选择不同的配置选项。

下表概括了“混合配置”向导修改和配置的主要选项。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>配置方面</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>域</p></td>
<td><p>向导会将一个接受的域添加到内部部署组织以实现云组织的混合邮件流和自动发现请求。此域（称为“共存域”）会作为辅助代理域添加到将 <em>PrimarySmtpAddress</em> 模板用于在“混合配置”向导中选择的域的任何电子邮件地址策略。默认情况下，此域是 &lt;域&gt;.mail.onmicrosoft.com。</p>
<p>可以通过在 Exchange Online 上的Exchange 命令行管理程序中运行以下命令来查看接受的域。</p>
<pre><code>Get-AcceptedDomain | FL DomainName, IsCoexistenceDomain</code></pre></td>
</tr>
<tr class="even">
<td><p>安全邮件证书</p></td>
<td><p>向导要求选择由第三方证书颁发机构 (CA) 颁发的特定证书。该机构负责验证和确保在内部部署与 Exchange Online 组织之间发送的邮件是安全的。</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 联合共享</p></td>
<td><p>该向导会查看对于本地组织，是否存在与 Azure Active Directory 身份验证系统的现有 OAuth 身份验证关系或联合身份验证信任。如果存在，则现有 OAuth 身份验证或联合身份验证信任将用于支持混合部署。如果不存在，则向导会为本地组织创建与 Azure AD 身份验证系统之间的联合身份验证信任，具体取决于本地 Exchange 配置的类型。向导还会根据需要，将在“混合配置”向导中选择的所有域都添加到联合身份验证信任中。</p>
<p>除了 OAuth 身份验证或联合身份验证信任配置之外，向导还会为内部部署组织和 Exchange Online 组织创建和配置组织关系。这些组织关系使向导可以启用几个混合部署功能，包括忙/闲共享、Web 上的 Outlook 重定向和邮件提示。</p></td>
</tr>
<tr class="even">
<td><p>邮件流</p></td>
<td><p>向导允许您选择和配置要在本地环境与 Exchange Online 组织之间处理安全邮件传输的 Exchange 服务器。在 Exchange 2010 中为集线器传输服务器。在 Exchange 2013 中为客户端访问服务器。在 Exchange 2016 中为邮箱服务器。</p>
<p>向导会配置内部部署 Exchange 和 Exchange Online 组织，以实现混合邮件路由。通过配置内部部署组织中新的和现有的发送与接收连接器以及 Exchange Online 中的入站与出站连接器，向导使您可以选择从 Exchange Online 组织传递到 Internet 的出站邮件是直接发送到外部邮件收件人，还是通过混合部署包含的内部部署 Exchange 服务器进行路由。</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Dn151302.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>入站邮件流由组织的 MX 记录进行控制。“混合配置”向导不会配置混合部署的入站 Internet 电子邮件。</td>
</tr>
</tbody>
</table>

</td>
</tr>
</tbody>
</table>


## 混合配置引擎

混合配置引擎运行配置和更新混合部署所需的核心操作。混合配置引擎负责处理 `Update-HybridConfiguration` cmdlet 操作，它将 *HybridConfiguration*Active Directory 对象的状态与当前内部部署 Exchange 和 Exchange Online 配置设置比较，然后运行任务以将部署配置设置与 *HybridConfiguration*Active Directory 对象中定义的参数匹配。如果当前内部部署 Exchange 和 Exchange Online 部署配置状态已与 *HybridConfiguration*Active Directory 对象中定义的设置匹配，则混合配置引擎不会对内部部署或 Exchange Online 组织进行任何更改。

当更新现有混合部署时，混合配置引擎会执行以下步骤：

1.  *Update-HybridConfiguration* cmdlet 触发混合配置引擎启动。

2.  混合配置引擎读取在 `HybridConfiguration`Active Directory 对象上存储的“所需状态”。

3.  混合配置引擎从内部部署 Exchange 组织发现拓扑数据和当前配置。

4.  混合配置引擎从 Exchange Online 组织发现拓扑数据和当前配置。

5.  混合配置引擎基于所需状态、拓扑数据和当前配置，在内部部署 Exchange 和 Exchange Online 组织之间建立“差异”，然后执行配置任务以建立“所需状态”。

下图摘要显示混合配置引擎如何在混合部署过程中检索和修改内部部署 Exchange 服务器和 Exchange Online 配置设置。

![混合配置引擎流](images/Hh529921.7e01b239-b978-4377-9eac-aa5bc4561866(EXCHG.150).gif "混合配置引擎流")

