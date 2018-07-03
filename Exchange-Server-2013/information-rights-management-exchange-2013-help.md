---
title: '信息权限管理: Exchange 2013 Help'
TOCTitle: 信息权限管理
ms:assetid: 6ea3a695-3ddd-4d53-b3c6-90041f44ef64
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638140(v=EXCHG.150)
ms:contentKeyID: 50490799
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 信息权限管理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

信息工作人员每天都会使用电子邮件交换敏感信息，例如财务报告和数据、法律合同、机密产品信息、销售报告和规划、竞争分析、研究和专利信息，以及客户和员工信息。因为用户现在随处都可以访问他们的电子邮件，所以邮箱已成为包含大量潜在敏感信息的存储库。因此，信息泄露可能对组织构成严重威胁。为防止信息泄露，Microsoft Exchange Server 2013 包括了信息权限管理 (IRM) 功能，此功能可对电子邮件和附件提供持久联机和脱机保护。

**目录**

什么是信息泄露？

针对信息泄露的传统解决方案

Exchange 2013 中的 IRM

对邮件应用 IRM 保护

IRM 保护的方案

解密受 IRM 保护的邮件以强制执行邮件策略

预许可

IRM 代理

IRM 要求

配置和测试 IRM

使用权限管理连接器扩展权限管理

## 什么是信息泄露？

潜在敏感信息的泄露可能会使组织付出高昂的代价，并对组织及其业务、员工、客户和合作伙伴存在广泛的影响。地方和行业法规正日益加强对某些类型的信息的存储、传输和保护方式的管理。为了避免违反适用法规的情况，组织必须进行自我保护，避免出现有意、无意或意外信息泄露的情况。

以下是信息泄露导致的一些后果：

  - **经济损失：** 由于业务损失或是法院或监管机构收取的罚款和惩罚性赔偿，信息泄露可能会产生经济方面的影响，具体取决于企业规模、行业和当地法规。上市公司还可能由于媒体的负面报道而面临着损失市值的风险。

  - **对形象和信誉的损害：** 信息泄露可能会损害组织在客户面前的形象和信誉。此外，根据通信的性质，电子邮件泄露可能会成为使发件人和组织陷入尴尬境地的潜在原因。

  - **失去竞争优势：** 信息泄露造成的最严重威胁之一是失去业务上的竞争优势。泄露战略计划或泄露合并和收购信息可能会导致收入或市值受到损失。其他威胁包括丢失研究信息、分析数据和其他知识产权。

什么是信息泄露？

## 针对信息泄露的传统解决方案

虽然针对信息泄露的传统解决方案可以对数据的初次访问提供保护，但是这些解决方案通常不会提供持续的保护。下表列出了某些传统解决方案及其限制。

### 传统解决方案

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>解决方案</th>
<th>描述</th>
<th>限制</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>传输层安全性 (TLS)</p></td>
<td><p>TLS 是一个 Internet 标准协议，用于通过加密手段保护网络上的通信。在邮件环境中，TLS 用于保护服务器/服务器和客户端/服务器的通信。</p>
<p>默认情况下，Exchange 2010 将 TLS 用于所有内部邮件的传输。默认情况下，还会为与外部主机的会话启用机会型 TLS。Exchange 会首先尝试为会话使用 TLS 加密，但是如果无法在 TLS 与目标服务器之间建立连接，Exchange 将使用 SMTP。还可以配置域安全性，以便强制执行与外部组织的相互 TLS。</p></td>
<td><p>TLS 仅保护两个 SMTP 主机之间的 SMTP 会话。也就是说，TLS 可保护移动的信息，但它不会提供邮件级的保护或对静止信息的保护。除非使用另一种方法加密邮件，否则发件人和收件人邮箱中的邮件仍然不会受到保护。对于发送到组织外部的电子邮件，仅第一个跃点可以要求 TLS。组织外部的远程 SMTP 主机收到邮件之后，该主机可通过未加密会话将邮件中继到另一 SMTP 主机中。由于 TLS 是一种传输层技术，因此它无法控制收件人对邮件执行的操作。</p></td>
</tr>
<tr class="even">
<td><p>电子邮件加密</p></td>
<td><p>用户可以使用 S/MIME 等技术对邮件进行加密。</p></td>
<td><p>用户决定是否加密邮件。公钥基础结构 (PKI) 部署会产生额外成本，同时还伴有用户证书管理和保护私钥的开销。在邮件解密之后，将无法控制收件人可以对信息执行的操作。解密的信息可以复制、打印或转发。默认情况下，保存的附件不受保护。</p>
<p>组织无法访问使用 S/MIME 等技术加密的邮件。由于组织无法检查邮件内容，因此无法强制执行邮件策略、扫描邮件是否存在病毒或恶意内容，或执行其他任何需要访问内容的操作。</p></td>
</tr>
</tbody>
</table>


最后，传统解决方案通常缺少应用统一邮件策略防止信息泄露的强制执行工具。例如，用户发送了包含敏感信息的邮件，并且将其标记为“公司机密”以及“不转发”。当邮件传递给收件人之后，发件人或组织将不能再控制该信息。收件人可能会有意或无意地（使用自动转发规则等功能）向外部电子邮件帐户转发该邮件，导致组织可能面临巨大的信息泄露风险。

什么是信息泄露？

## Exchange 2013 中的 IRM

在 Exchange 2013 中，可使用 IRM 功能对邮件和附件应用持久保护。IRM 使用 Active Directory 权限管理服务 (AD RMS)，这是 Windows Server 2008 及更高版本中的一种信息保护技术。借助 Exchange 2013 中的 IRM 功能，组织和用户可以控制收件人对电子邮件的权限。IRM 还有助于允许或限制某些收件人操作，例如向其他收件人转发邮件、打印邮件或附件，或者是通过复制和粘贴提取邮件或附件内容。用户可在 Microsoft Outlook 或 Microsoft Office Outlook Web App 中应用 IRM 保护，或者可以根据组织的邮件策略并使用传输保护规则或 Outlook 保护规规则应用 IRM 保护。与其他电子邮件加密解决方案不同，IRM 还允许组织解密受保护的内容，以强制执行策略遵从性。

AD RMS 使用基于可扩展权限标记语言 (XrML) 的证书和许可证，验证计算机和用户并保护内容。使用 AD RMS 保护文档或邮件等内容时，将会附加包含授权用户对内容所拥有的权限的 XrML 许可证。若要访问受 IRM 保护的内容，启用了 AD RMS 的应用程序必须为来自 AD RMS 群集的授权用户购买使用许可证。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，预许可代理会将使用许可证附加到组织中使用 AD RMS 群集保护的邮件上。有关详细信息，请参阅本主题后面的预许可。</td>
</tr>
</tbody>
</table>


用于创建内容的应用程序必须已启用 RMS，以使用 AD RMS 对内容应用持久保护。Microsoft Office 应用程序（如 Word、Excel、PowerPoint 和 Outlook）启用了 RMS，可用于创建和使用受保护的内容。

IRM 有助于执行以下操作：

  - 防止受 IRM 保护的内容的授权收件人转发、修改、打印、传真、保存或剪切和粘贴该内容。

  - 用与邮件相同的保护级别保护所支持的附件文件格式。

  - 支持受 IRM 保护的邮件和附件的过期，使其在指定时间段之后，无法再进行查看。

  - 防止使用 Microsoft Windows 中的截图工具复制受 IRM 保护的内容。

但是，IRM 无法防止使用以下方法复制信息：

  - 第三方屏幕捕获程序

  - 使用照相机等图像处理设备对显示在屏幕上的受 IRM 保护的内容进行照相

  - 用户记住或手动抄录信息

有关 AD RMS 的详细信息，请参阅 [Active Directory 权限管理服务](https://go.microsoft.com/fwlink/p/?linkid=129823)。

## AD RMS 权限策略模板

AD RMS 使用基于 XrML 的权限策略模板，允许启用了 IRM 的兼容应用程序应用一致的保护策略。在 Windows Server 2008 及更高版本中，AD RMS 服务器提供了可用于枚举和获取模板的 Web 服务。Exchange 2013 附带有“不要转发”模板。将“不要转发”模板应用于邮件时，只有邮件的收件人可解密该邮件。收件人无法转发邮件、复制邮件内容或打印邮件。可在组织中的 AD RMS 服务器上创建其他 RMS 模板，以满足 IRM 保护要求。

通过应用 AD RMS 权限策略模板应用 IRM 保护。使用策略模板可控制收件人对邮件拥有的权限。通过对邮件应用适当的权限策略模板，可以控制答复、全部答复、转发、从邮件提取信息、保存邮件或打印邮件等操作。

有关权限策略模板的详细信息，请参阅 [AD RMS 策略模板注意事项](https://go.microsoft.com/fwlink/p/?linkid=179455)。

有关创建 AD RMS 权限策略模板的详细信息，请参阅 [AD RMS 权限策略模板部署分步指南](https://go.microsoft.com/fwlink/p/?linkid=136593)。

什么是信息泄露？

## 对邮件应用 IRM 保护

在 Exchange 2010 中，可使用以下方法对邮件应用 IRM 保护：

  - **由 Outlook 用户手动进行：** Outlook 用户可使用他们可使用的 AD RMS 权限策略模板对邮件进行 IRM 保护。此过程使用的是 Outlook 而非 Exchange 中的 IRM 功能。但是，可以使用 Exchange 访问这些邮件，并执行相关操作（如应用传输规则）强制执行组织的邮件策略。有关使用 Outlook 中 IRM 的详细信息，请参阅[用于电子邮件的 IRM 简介](https://go.microsoft.com/fwlink/p/?linkid=166897)。

  - **由 Outlook Web App 用户手动进行：** 启用 Outlook Web App 中的 IRM 后，用户可以对其发送的邮件执行 IRM 保护，并查看其接收到的受 IRM 保护的邮件。在 Exchange 2013 累计更新 1 (CU1) 中，Outlook Web App 用户还可以使用 Web-Ready 文档查看来查看受 IRM 保护的附件。有关 Outlook Web App 中的 IRM 的详细信息，请参阅[Outlook Web App 中的信息权限管理](information-rights-management-in-outlook-web-app-exchange-2013-help.md)。

  - **由 Windows Mobile 和 Exchange ActiveSync 设备用户手动进行：** 在 Exchange 2010 的正式发布 (RTM) 版本中，Windows Mobile 设备的用户可以查看和创建受 IRM 保护的邮件。这要求用户将其受支持的 Windows Mobile 设备连接到计算机并针对 IRM 激活这些设备。在 Exchange 2010 SP1 中，可以启用 Microsoft Exchange ActiveSync 中的 IRM，以允许 Exchange ActiveSync 设备（包括 Windows Mobile 设备）的用户查看、答复、转发和创建受 IRM 保护的邮件。有关 Exchange ActiveSync 中的 IRM 的详细信息，请参阅[Exchange ActiveSync 中的信息权限管理](information-rights-management-in-exchange-activesync-exchange-2013-help.md)。

  - **在 Outlook 2010 及更高版本中自动进行：** 可创建 Outlook 保护规则，以便在 Outlook 2010 及更高版本中自动对邮件进行 IRM 保护。Outlook 保护规则将自动部署到 Outlook 2010 客户端，且当用户撰写邮件时，Outlook 2010 将应用 IRM 保护。有关 Outlook 保护规则的详细信息，请参阅[Outlook 保护规则](outlook-protection-rules-exchange-2013-help.md)。

  - **在邮箱服务器上自动进行：** 可创建传输保护规则，以在 Exchange 2013 邮箱服务器上自动对邮件进行 IRM 保护。有关传输保护规则的详细信息，请参阅[传输保护规则](transport-protection-rules-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>对已经受 IRM 保护的邮件将不再应用 IRM 保护。例如，如果用户在 Outlook 或 Outlook Web App 中对邮件进行了 IRM 保护，则不会使用传输保护规则对邮件应用 IRM 保护。</td>
    </tr>
    </tbody>
    </table>


什么是信息泄露？

## IRM 保护的方案

下表说明了 IRM 保护的方案。

### IRM 保护的方案

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>发送受 IRM 保护的邮件</th>
<th>支持</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>在相同的内部部署 Exchange 2013 部署中</p></td>
<td><p>是</p></td>
<td><p>有关要求，请参阅本主题后面的 IRM 要求。</p></td>
</tr>
<tr class="even">
<td><p>一个内部部署中的不同林之间</p></td>
<td><p>是</p></td>
<td><p>有关要求，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=199009">配置 AD RMS 以便跨多个林与 Exchange Server 2010 集成</a>。</p></td>
</tr>
<tr class="odd">
<td><p>一个内部部署 Exchange 2013 部署与一个基于云的 Exchange 组织之间</p></td>
<td><p>是</p></td>
<td><ul>
<li><p>使用内部部署 AD RMS 服务器。</p></li>
<li><p>从内部部署 AD RMS 服务器导出可信发布域。</p></li>
<li><p>在基于云的组织中导入可信发布域。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>到外部收件人</p></td>
<td><p>否</p></td>
<td><p>Exchange 2010 不包含将受 IRM 保护的邮件发送给非联盟组织中的外部收件人的解决方案。AD RMS 使用信任策略提供解决方案。可以在 AD RMS 群集和 Microsoft 帐户（以前称为 Windows Live ID）之间配置信任策略。对于在两个组织之间发送的邮件，可以使用 Active Directory 联合身份验证服务 (AD FS) 在两个 Active Directory 林之间创建联合信任。要了解详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=182909">了解 AD RMS 信任策略</a>。</p></td>
</tr>
</tbody>
</table>


什么是信息泄露？

## 解密受 IRM 保护的邮件以强制执行邮件策略

为强制执行邮件策略和法规遵从性，必须拥有对加密邮件内容的访问权限。为满足诉讼、监管审核或内部调查的电子数据展示要求，还必须能够搜索加密的邮件。为了帮助执行此类任务，Exchange 2013 包括以下 IRM 功能：

  - **传输解密：** 若要应用邮件策略，传输规则代理等传输代理应拥有对邮件内容的访问权限。传输解密允许安装在 Exchange 2013 服务器上的传输代理访问邮件内容。有关详细信息，请参阅[传输解密](transport-decryption-exchange-2013-help.md)。

  - **日记报告解密：** 若要满足遵从性或业务要求，组织可使用日记功能保留邮件内容。日记代理为要记录的邮件创建日记报告，并且在报告中包括了有关邮件的元数据。原始邮件将会附加到日记报告中。如果日记报告中的邮件受 IRM 保护，则日记报告解密会将邮件的明文副本附加到日记报告中。有关详细信息，请参阅[日记报告解密](journal-report-decryption-exchange-2013-help.md)。

  - **Exchange 搜索的 IRM 解密：** 通过 Exchange 搜索的 IRM 解密，Exchange 搜索可以在受 IRM 保护的邮件中建立内容索引。当发现管理员执行就地电子数据展示搜索时，搜索结果中会返回已编制索引的受 IRM 保护的邮件。有关详细信息，请参阅[就地电子数据展示](in-place-ediscovery-exchange-2013-help.md)。
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>在 Exchange 2010 SP1 及更高版本中，发现管理角色组的成员可访问由发现搜索返回并位于发现邮箱中的受 IRM 保护的邮件。要启用此功能，请将 <em>EDiscoverySuperUserEnabled</em> 参数与 <a href="https://technet.microsoft.com/zh-cn/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a> cmdlet 配合使用。有关详细信息，请参阅<a href="configure-irm-for-exchange-search-and-in-place-ediscovery-exchange-2013-help.md">为 Exchange 搜索和就地 eDiscovery 配置 IRM</a>。</td>
    </tr>
    </tbody>
    </table>


若要启用这些解密功能，Exchange 服务器必须拥有对邮件的访问权限。将联合邮箱（由 Exchange 安装程序创建的系统邮箱）添加到 AD RMS 服务器上的超级用户组可完成此操作。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

什么是信息泄露？

## 预许可

为查看受 IRM 保护的邮件和附件，Exchange 2013 会自动将预许可证附加到受保护的邮件中。这样可以防止客户端为检索使用许可证而不得不在 AD RMS 服务器之间进行重复往返，并可对受 IRM 保护的邮件和附件启用脱机查看。通过预许可还可在 Outlook Web App 中查看受 IRM 保护的邮件。如果启用了 IRM 功能，则默认情况下会启用预许可。

什么是信息泄露？

## IRM 代理

在 Exchange 2013 中，使用邮箱服务器上的传输服务中的传输代理启用 IRM 功能。IRM 代理由 Exchange 安装程序安装在邮箱服务器上。无法使用传输代理的管理任务控制 IRM 代理。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，IRM 代理为内置代理。内置代理不包含在 <strong>Get-TransportAgent</strong> cmdlet 所返回的代理列表中。有关详细信息，请参阅<a href="transport-agents-exchange-2013-help.md">传输代理</a>。</td>
</tr>
</tbody>
</table>


下表列出了在邮箱服务器上的传输服务中实施的 IRM 代理。

### 邮箱服务器上的传输服务中的 IRM 代理

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>代理</th>
<th>事件</th>
<th>功能</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RMS 解密代理</p></td>
<td><p>OnEndOfData (SMTP) 和 OnSubmittedMessage</p></td>
<td><p>解密邮件，以允许访问传输代理。</p></td>
</tr>
<tr class="even">
<td><p>传输规则代理</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>将与传输保护规则中的规则条件匹配的邮件标记为由 RMS 加密代理进行 IRM 保护的邮件。</p></td>
</tr>
<tr class="odd">
<td><p>RMS 加密代理</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>对传输规则代理标记的邮件应用 IRM 保护并重新加密传输解密邮件。</p></td>
</tr>
<tr class="even">
<td><p>预许可代理</p></td>
<td><p>OnRoutedMessage</p></td>
<td><p>将预许可证附加到受 IRM 保护的邮件中。</p></td>
</tr>
<tr class="odd">
<td><p>日记报告解密代理</p></td>
<td><p>OnCategorizedMessage</p></td>
<td><p>解密附加到日记报告中的受 IRM 保护的邮件，并嵌入明文版本以及原始加密邮件。</p></td>
</tr>
</tbody>
</table>


有关传输代理的详细信息，请参阅[传输代理](transport-agents-exchange-2013-help.md)。

什么是信息泄露？

## IRM 要求

若要在 Exchange 2013 组织中实现 IRM，部署必须满足下表中说明的要求。

### IRM 要求

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>服务器</th>
<th>要求</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AD RMS 群集</p></td>
<td><ul>
<li><p><strong>操作系统：</strong>需要装有修补程序 <a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973247">Windows Server 2008 中的 Active Directory 权限管理服务角色</a>的 Windows Server 2012、Windows Server 2008 R2 或 Windows Server 2008 SP2。</p></li>
<li><p><strong>服务连接点</strong>Exchange 2010 和可感知 AD RMS 的应用程序使用在 Active Directory 中注册的服务连接点来发现 AD RMS 群集和 URL。通过 AD RMS，可从 AD RMS 安装程序中注册服务连接点。如果用于安装 AD RMS 的帐户不是 Enterprise Admins 安全组成员，则可在安装之后执行服务连接点注册。AD RMS 在 Active Directory 林中仅有一个服务连接点。</p></li>
<li><p><strong>权限：</strong>必须向以下对象分配对 AD RMS 服务器证书管道（AD RMS 服务器上的 <code>ServerCertification.asmx</code> 文件）的读取和执行权限：</p>
<ul>
<li><p>Exchange Servers 组或各个 Exchange 服务器</p></li>
<li><p>AD RMS 服务器上的 AD RMS 服务组</p></li>
</ul>
<p>默认情况下，ServerCertification.asmx 文件位于 AD RMS 服务器上的 <code>\inetpub\wwwroot\_wmcs\certification\</code> 文件夹中。有关详细信息，请参阅<a href="https://go.microsoft.com/fwlink/p/?linkid=186951">设置对 AD RMS 服务器证书管道的权限</a>。</p></li>
<li><p><strong>AD RMS 超级用户：</strong>若要启用传输解密、日记报告解密、Outlook Web App 中的 IRM 和 Exchange 搜索的 IRM，必须将联合邮箱（由 Exchange 2013 安装程序创建的系统邮箱）添加到 AD RMS 群集上的超级用户组。有关详细信息，请参阅<a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">将联合身份验证邮箱添加到 AD RMS 超级用户组</a>。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange</p></td>
<td><ul>
<li><p>需要 Exchange 2010 或更高版本。</p></li>
<li><p>建议将修补程序<a href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=973136">修复：基于 .NET Framework 2.0 SP2 的应用程序尝试处理对异步 ASP.NET Web 服务请求的零长度内容响应时，出现 ArgumentNullException 异常错误消息：“值不能为空”</a>用于 Microsoft .NET Framework 2.0 SP2。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook</p></td>
<td><ul>
<li><p>用户可在 Outlook 中对邮件进行 IRM 保护。从 Outlook 2003 开始，支持用于 IRM 保护邮件的 AD RMS 模板。</p></li>
<li><p>Outlook 保护规则是 Exchange 2010 和 Outlook 2010 功能。以前版本的 Outlook 不支持此功能。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync</p></td>
<td><ul>
<li><p>支持 Exchange ActiveSync 协议版本 14.1 的设备（包括 Windows Mobile 设备）可以支持 Exchange ActiveSync 中的 IRM。设备上的移动电子邮件应用程序必须支持 Exchange ActiveSync 协议版本 14.1 中定义的 <strong>RightsManagementInformation</strong> 标记。在 Exchange 2013 中，Exchange ActiveSync 中的 IRM 使具有受支持设备的用户可以查看、答复、转发和创建受 IRM 保护的邮件，而无需用户将设备连接到计算机并针对 IRM 激活设备。有关详细信息，请参阅<a href="information-rights-management-in-exchange-activesync-exchange-2013-help.md">Exchange ActiveSync 中的信息权限管理</a>。</p></li>
</ul></td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>“AD RMS 群集”是用于在组织中进行 AD RMS 部署（包括单个服务器部署）的术语。AD RMS 是一项 Web 服务。它不要求您安装 Windows Server 故障转移群集。为实现高可用性和负载平衡，可在群集中部署多个 AD RMS 服务器，并使用网络负载平衡。</td>
</tr>
</tbody>
</table>


<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在生产环境中，不支持在同一台服务器上安装 AD RMS 和 Exchange。</td>
</tr>
</tbody>
</table>


Exchange 2013 IRM 功能支持 Microsoft Office 文件格式。可通过部署自定义保护程序将 IRM 保护扩展到其他文件格式。有关自定义保护程序的详细信息，请参阅[独立软件供应商](https://go.microsoft.com/fwlink/p/?linkid=210336)中的“信息保护和控制合作伙伴”。

什么是信息泄露？

## 配置和测试 IRM

必须使用 Exchange 命令行管理程序配置 Exchange 2013 中的 IRM 功能。若要配置各项 IRM 功能，请使用 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet。可以为内部邮件、传输解密、日记报告解密、Exchange 搜索和 Outlook Web App 启用或禁用 IRM。有关配置 IRM 功能的详细信息，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

设置 Exchange 2013 服务器之后，可使用 [Test-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979798\(v=exchg.150\)) cmdlet 执行 IRM 部署的端到端测试。对初次配置 IRM 之后立即验证 IRM 功能并持续进行验证而言，这些测试十分有用。cmdlet 将执行以下测试：

  - 检查 Exchange 2013 组织的 IRM 配置。

  - 检查 AD RMS 服务器的版本和修补程序信息。

  - 验证是否可以通过检索权限帐户证书 (RAC) 和客户端许可方证书为 RMS 激活 Exchange 服务器。

  - 从 AD RMS 服务器获取 AD RMS 权限策略模板。

  - 验证指定的发件人是否可以发送受 IRM 保护的邮件。

  - 检索指定收件人的超级用户使用许可证。

  - 获取指定收件人的预许可证。

什么是信息泄露？

## 使用权限管理连接器扩展权限管理

Microsoft 权限管理连接器（RMS 连接器）是一个可选的应用程序，它可以通过使用基于云的 Microsoft 权限管理服务为 Exchange 2013 服务器增强数据保护。安装 RMS 连接器后，它将可以在信息的生命期内提供连续的数据保护，并且，由于这些服务是可自定义的，您可以根据需要定义保护级别。例如，您可以限制对特定用户电子邮件的访问或对某些邮件设置只读权限。

有关 RMS 连接器及其安装方法的详细信息，请参阅[权限管理连接器](https://technet.microsoft.com/zh-cn/library/dn375964.aspx)。

