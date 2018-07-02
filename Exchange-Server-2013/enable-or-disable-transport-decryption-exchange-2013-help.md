---
title: '启用或禁用传输解密: Exchange 2013 Help'
TOCTitle: 启用或禁用传输解密
ms:assetid: 4663f54e-dd0a-4a42-983e-8765e2adc412
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638126(v=EXCHG.150)
ms:contentKeyID: 50490406
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 启用或禁用传输解密

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

启用传输解密允许 Microsoft Exchange Server 2013上的传输规则代理邮箱服务器访问受保护的信息权限管理 (IRM) 的邮件中的内容。因此，其他传输代理可以访问消息内容，并可能对其进行更改。例如，传输规则代理可能需要检查邮件的内容和应用传输规则 （例如，应用于邮件的免责声明的规则）。要成功解密受 IRM 保护的邮件，必须将联合传递邮箱添加到[Active Directory Rights Management Services (AD RMS)](https://technet.microsoft.com/en-us/library/hh831364.aspx)服务器上配置的超级用户组中。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.important(EXCHG.150).gif" title="重要说明" alt="重要说明" />重要说明：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>当超级用户组的成员从 AD RMS 群集中请求许可证时，系统会授予他们所有者使用许可证。这样，他们便可以解密由 AD RMS 群集创建的所有受 RMS 保护的内容。</td>
</tr>
</tbody>
</table>


当启用传输解密时，可以指定下列设置：

  - **强制** 拒绝无法解密的邮件，并向发件人发送未送达报告 (NDR)。

  - **可选** 使用最佳方法进行解密。如果可能，将解密邮件，但即使解密失败仍会传递邮件。这是默认设置。

有关传输解密的详细信息，请参阅[传输解密](transport-decryption-exchange-2013-help.md)。

关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - AD RMS 服务器存在于 Active Directory 林中，并且可访问该服务器。

  - 联合传递邮箱已添加到 AD RMS 超级用户组。有关详细信息，请参阅[将联合身份验证邮箱添加到 AD RMS 超级用户组](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md)。

  - 不能使用 Exchange 管理中心 (EAC) 启用传输解密。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

<table>
<thead>
<tr class="header">
<th><img src="images/Bb124558.tip(EXCHG.150).gif" title="提示" alt="提示" />提示：</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。</td>
</tr>
</tbody>
</table>


## 您想执行什么操作？

## 使用命令行管理程序启用传输解密

此示例将为 Exchange 2013 组织启用传输解密。无法解密的邮件被拒绝，NDR 被返回到发件人。

    Set-IRMConfiguration -TransportDecryptionSetting Mandatory

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 使用命令行管理程序禁用传输解密

此示例将对 Exchange 2013 组织禁用传输解密。

    Set-IRMConfiguration -TransportDecryptionSetting Disabled

有关语法和参数的详细信息，请参阅 [Set-IRMConfiguration](https://technet.microsoft.com/zh-cn/library/dd979792\(v=exchg.150\))。

## 我如何知道这有效？

要验证是否已启用或禁用传输解密，请使用 **Get-IRMConfiguration** cmdlet，并检查 *JournalDecryptionEnabled* 属性值。

有关如何检查 IRM 配置的示例，请参阅 **Get-IRMConfiguration** 中的[Examples](https://technet.microsoft.com/zh-cn/e1821219-fe18-4642-a9c2-58eb0aadd61a\(exchg.150\)#examples)。

