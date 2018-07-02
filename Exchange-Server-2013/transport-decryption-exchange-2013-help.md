﻿---
title: '传输解密: Exchange 2013 Help'
TOCTitle: 传输解密
ms:assetid: 4267c46d-f488-404d-a5cb-51f9127461c0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638122(v=EXCHG.150)
ms:contentKeyID: 50490436
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 传输解密

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2015-04-07_

在 Microsoft Exchange Server 2013、Microsoft Outlook 2010 及更高版本以及 Microsoft OfficeOutlook Web App 中，用户可以使用信息权限管理 (IRM) 功能保护邮件。可创建 Outlook 保护规则，在从 Outlook 2010 客户端中发送邮件之前自动对这些邮件应用 IRM 保护。此外，还可以创建传输保护规则，以对符合规则条件的正在传送中的邮件应用 IRM 保护。利用传输解密机制，可以访问受 IRM 保护的邮件内容，以强制执行邮件策略。

有关管理 IRM 的管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 其他加密解决方案的局限性

如果组织对于敏感信息（包括对业务影响很大 (HBI) 的信息和个人的可识别信息 (PII)）的保护至关重要，则可以考虑对电子邮件和附件进行加密。长期以来，可供使用的有 S/MIME 等电子邮件加密解决方案。不同类型的组织已经在不同程度上采用了这些加密解决方案。但是，此类解决方案存在着以下缺点：

  - **无法应用邮件策略**   组织还面临着需要检查邮件内容以确保其符合邮件策略的遵从性要求。但是，使用大多数基于客户端的加密解决方案（包括 S/MIME）加密的邮件会妨碍在服务器上进行的内容检查。如果不进行内容检查，组织将无法验证其用户发送或接收的所有邮件是否符合邮件策略。例如，为了符合法律条例，您已将传输规则配置为检测 PII（如社会保险号），并自动对邮件应用免责声明。如果该邮件经过了加密，传输服务上的传输规则代理将无法访问邮件内容，因此不会应用免责声明。这将导致违反策略。

  - **安全性降低**   防病毒软件无法扫描加密的邮件内容，这使组织更容易受到病毒和蠕虫等恶意内容的攻击。通常认为大多数用户都信任加密邮件，因此，病毒在整个组织中传播的可能性将会增大。例如，您配置了 Outlook 保护规则，以自动将 IRM 保护应用于发送到具有公司机密权限管理服务 (RMS) 模板的\&quot;All Employees\&quot;通讯组列表的所有邮件。某个用户的工作站感染了病毒，这种病毒可以通过自动使用\&quot;全部答复\&quot;回复邮件来进行传播。如果对携带这种病毒的邮件进行了加密，则防病毒扫描程序将无法扫描该邮件。

  - **影响自定义传输代理**   许多组织出于不同目的开发了自定义传输代理，如满足遵从性、安全性或自定义邮件路由的额外处理需求。组织开发的用于检查或修改邮件的自定义传输代理无法处理加密邮件。如果组织开发的自定义传输代理无法访问邮件内容，则邮件加密可能会妨碍组织实现开发自定义传输代理的目标。

## 对加密内容采用传输解密

在 Exchange 2013 中，IRM 功能解决了这些问题。如果邮件受 IRM 保护，传输解密机制允许您在传输过程中对其进行解密。受 IRM 保护的邮件由解密代理（一个注重合规性的传输代理）进行解密。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.note(EXCHG.150).gif" title="注意" alt="注意" />注意：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在 Exchange 2013 中，解密代理是内置代理。内置代理不包含在 <strong>Get-TransportAgent</strong> cmdlet 所返回的代理列表中。有关详细信息，请参阅<a href="transport-agents-exchange-2013-help.md">传输代理</a>。</td>
</tr>
</tbody>
</table>


解密代理可解密以下类型的受 IRM 保护的邮件：

  - 在 Outlook Web App 中，由用户通过 IRM 保护的邮件。

  - 在 Outlook 2010 中，由用户通过 IRM 保护的邮件。

  - 在 Exchange 2013 和 Outlook 2010 中，由 Outlook 保护规则自动通过 IRM 保护的邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>解密代理仅解密由组织中的 AD RMS 服务器通过 IRM 保护的邮件。</td>
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
<td>使用传输保护规则在传输过程中保护的邮件无须由解密代理进行解密。解密代理会触发 <strong>OnEndOfData</strong> 和 <strong>OnSubmit</strong> 传输事件。传输保护规则通过传输规则代理应用，此传输规则代理将会触发 <strong>OnRoutedMessage</strong> 事件，而 IRM 保护则通过 <strong>OnRoutedMessage</strong> 事件上的加密代理应用。有关传输代理以及可在其上注册传输代理的 SMTP 事件列表的详细信息，请参阅<a href="transport-agents-exchange-2013-help.md">传输代理</a>。</td>
</tr>
</tbody>
</table>


传输解密操作在 Active Directory 林中第一个处理邮件的 Exchange 2013 传输服务上执行。如果邮件传递至另一 Active Directory 林中的某个传输服务，会再次对邮件进行解密。解密之后，该服务器上的其他传输代理可处理未加密内容。例如，传输服务上的传输规则代理可检查邮件内容并应用传输规则。对未加密的邮件可执行规则中指定的任何操作，如应用免责声明或者以其他任何方式修改邮件。防病毒扫描程序等第三方传输代理可对邮件进行扫描，检查是否存在病毒和恶意软件。在其他传输代理检查了该邮件并对其进行了可能的修改之后，将使用与解密代理解密邮件之前所拥有的权限相同的用户权限再次加密此邮件。组织中其他邮箱服务器上的其他传输服务不会再次解密同一邮件。

解密代理解密后的邮件在未经过再次加密的情况下不会离开传输服务。如果在解密或加密邮件时返回暂时性错误，传输服务将重试操作两次。在第三次失败之后，此错误将视为永久性错误。如果发生任何永久错误（包括重试失败后将暂时性错误视为永久错误的情况），传输服务将进行如下处理：

  - 如果在解密过程中发生永久性错误，则仅当传输解密设置为 `Mandatory` 时才会发送未送达报告 (NDR)，并将加密邮件与 NDR 一起发送。有关可用于传输解密的配置选项的详细信息，请参阅本主题后面的Configuring Transport Decryption。

  - 如果在重新加密过程中发生永久性错误，则发送 NDR 时始终不发送解密邮件。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>安装在传输服务上的任何自定义或第三方代理都有权访问解密的邮件。必须考虑此类传输代理的行为。建议您在将自定义和第三方传输代理部署到生产环境中之前对所有这些代理进行全面测试。<br />
解密代理对邮件进行解密后，如果传输代理新建邮件并将原始邮件嵌入（附加到）新邮件，将只有新邮件会受到保护。作为新邮件附件的原始邮件将不再重新加密。收到此类邮件的收件人可以打开附加的邮件并执行转发或答复等操作，绕过强制执行的权限。</td>
</tr>
</tbody>
</table>


## 配置传输解密

传输解密是通过使用 Exchange 命令行管理程序中的 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet 配置的。但是，在配置传输解密之前，必须为 Exchange 2013 服务器提供可对 AD RMS 服务器保护的内容进行解密的权限。通过将联合邮箱添加到组织中的 AD RMS 群集上配置的超级用户组，可以授予需要的权限。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>在跨林 AD RMS 部署中，每个林中都部署了一个 AD RMS 群集，您必须将联合邮箱添加到每个林中 AD RMS 群集上的超级用户组，这样 Exchange 2013 邮箱服务器或 Exchange 2010 集线器传输服务器上的传输服务才能解密针对每个 AD RMS 群集受到保护的邮件。</td>
</tr>
</tbody>
</table>


有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

启用传输解密时，Exchange 2013 可以有两种不同的设置：

  - **强制**   当传输解密设置为 `Mandatory` 时，如果在解密邮件时返回永久性错误，则解密代理将拒绝该邮件，并向发件人返回 NDR。如果组织不希望在无法成功解密邮件和应用了防病毒扫描和传输规则等操作的情况下传递邮件，则必须选择此设置。

  - **可选**   当传输解密设置为\&quot;可选\&quot;时，解密代理将使用最佳方法。可解密的邮件将会被解密，但解密时发生永久性错误的邮件也会被传递。如果组织要将邮件传递设置为优先于邮件策略，则必须使用此设置。

有关配置传输解密的详细信息，请参阅[启用或禁用传输解密](enable-or-disable-transport-decryption-exchange-2013-help.md)。

