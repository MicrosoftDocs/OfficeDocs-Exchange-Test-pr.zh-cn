---
title: '启用或禁用日记报告解密: Exchange 2013 Help'
TOCTitle: 启用或禁用日记报告解密
ms:assetid: 1dedbe73-2c1a-4b14-8799-5091aaec7965
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638092(v=EXCHG.150)
ms:contentKeyID: 50490023
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用日记报告解密

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

启用日记帐报告解密允许日志记录代理将解密受权限保护的邮件的副本附加到日志报告。启用日志报告解密之前，您必须将联合传递邮箱添加到[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)服务器上配置的超级用户组。

有关信息权限管理 (IRM) 的其他管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：1 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - 当超级用户组的成员从 AD RMS 群集中请求许可证时，系统会授予他们所有者使用许可证。这样，他们便可以解密由 AD RMS 群集创建的所有受 RMS 保护的内容。

  - 必须在 Active Directory 林中安装一个 AD RMS 群集。

  - 联合提供邮箱已添加到 AD RMS 超级用户组。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 不能使用 Exchange 管理中心 (EAC) 以启用日志报告解密。您必须使用外壳程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行启用日记报告解密

本示例启用 Exchange 组织的日记报告解密。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $true

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 使用命令行禁用日记报告解密

本示例禁用 Exchange 组织的日记报告解密。

    Set-IRMConfiguration -JournalReportDecryptionEnabled $false

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 您如何知道这有效？

要验证是否已启用或禁用日记报告解密，请运行 **Get-IRMConfiguration** cmdlet 并检查 *JournalDecryptionEnabled* 属性的值。

有关如何检查 IRM 配置的示例，请参阅 **Get-IRMConfiguration** 中的[Examples](https://technet.microsoft.com/zh-cn/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

