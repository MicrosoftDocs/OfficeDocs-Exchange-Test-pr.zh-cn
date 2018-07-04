---
title: '日记报告解密: Exchange 2013 Help'
TOCTitle: 日记报告解密
ms:assetid: c063e2bd-2444-480d-8b35-73f31064a31b
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876936(v=EXCHG.150)
ms:contentKeyID: 50491451
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 日记报告解密

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2012-10-16_

在 Microsoft Exchange Server 2013，信息权限管理 (IRM) 允许 Microsoft Outlook 2010及更高版本，Microsoft OfficeOutlook Web App用户保护他们的邮件。您可以创建Outlook保护规则之前它们被从Outlook 2010客户端发送自动对邮件应用 IRM 保护。您还可以创建传输保护规则适用于与规则条件匹配的邮件在传输过程中的 IRM 保护。

有关 Outlook 保护规则的详细信息，请参阅 [Outlook 保护规则](outlook-protection-rules-exchange-2013-help.md)。

## 标准加密解决方案的限制

如果您的组织使用传统的解决方案，例如 S/MIME 加密邮件，记录管理员将无法检查或搜索加密的内容。存档包含不能访问和搜索不到内容的加密的邮件时，可能无法满足业务、 管理法规或法规遵从性要求。当面对电子查询 (eDiscovery) 请求时，不能进行解密，搜索和加密的邮件中的显示内容可以是一项挑战，并如果不这样做可能会给您的组织法律和金融风险。

此外，您组织的邮件策略可能需要日记消息，这样就可以访问到 eDiscovery 工具、 自动化的流程或记录管理者访问日志邮箱内容解密。在 Exchange 2010 的日志报告解密可以帮助您满足这些要求。

有关日记的详细信息，请参阅[日记](journaling-exchange-2013-help.md)。

## 日记报告解密

日志报告解密允许您在日志报告，原、 受 IRM 保护的邮件并保存受 IRM 保护的邮件的纯文本副本。如果 IRM 保护的邮件，包含由您的组织中Active Directory权限管理服务 (AD RMS) 群集保护任何支持的附件，这些附件也会解密。

> [!important]
> 若要使用日记帐报告解密，必须具有Exchange企业客户端访问许可证 (CAL)。日志报告解密只支持高级日志记录。


由日志报告解密代理，专注于法规遵从性的传输代理执行解密。在**OnCategorizedMessage**事件日志报告解密代理激发。受保护的邮件传输中使用传输加密代理，引发**OnRoutedMessage**事件，到达日记帐报告解密代理之前已经加密规则的保护。日志报告解密代理对这些消息进行解密。

> [!NOTE]
> 在Exchange 2013，日志报告解密代理是内置代理。内置代理不包括在返回的<strong>Get-TransportAgent</strong> cmdlet 的代理的列表。有关详细信息，请参阅<a href="transport-agents-exchange-2013-help.md">传输代理</a>。


该代理解密以下类型的受 IRM 保护的邮件：

  - 由 Outlook Web App 中的用户进行 IRM 保护的邮件。

  - 由 Outlook 2010 中的用户进行 IRM 保护的邮件。

  - 在 Outlook 2010 中使用 Outlook 保护规则自动受 IRM 保护的邮件。

  - 使用传输保护规则在传送过程中自动受 IRM 保护的邮件。

> [!important]
> 只是由您的组织中 AD RMS 服务器受 IRM 保护的邮件被解密由日志报告解密代理。代理不会解密附件，如果它不受保护邮件时 （并因此不会有相同的使用许可证），或者受 IRM 保护的文件附加到未受保护的邮件。


## 配置日志报告解密

日志报告解密是 configuredb 在Exchange命令行管理程序中使用[Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\)) cmdlet。但是，在配置日志报告解密之前，您必须分配Exchange 2013服务器解密是由 AD RMS 服务器受 IRM 保护的内容的权限。若要执行此操作，您添加到您的组织的 AD RMS 群集上配置的超级用户组联盟邮箱。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

> [!important]
> 在跨林 AD RMS 部署中（即每个林中都部署有 AD RMS 群集），必须将联合邮箱添加到每个林中 AD RMS 群集的超级用户组，以使 Exchange 2013 传输服务器可解密针对每个 AD RMS 群集进行保护的邮件。


有关如何配置日志报告解密的信息，请参阅[启用或禁用日记报告解密](enable-or-disable-journal-report-decryption-exchange-2013-help.md)。

启用日记帐报告解密后，日记邮箱可能包含敏感信息以未加密形式的日志报告。作为一种最佳做法，建议日记邮箱访问权限进行严密监视，并仅限于授权的个人。即使您没有使用 IRM 保护的电子邮件，这是一种最佳做法。

