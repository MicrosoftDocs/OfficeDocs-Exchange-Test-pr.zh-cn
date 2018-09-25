---
title: '管理远程域: Exchange 2013 Help'
TOCTitle: 管理远程域
ms:assetid: 41a86907-bd9e-40d0-94d3-6deb95a0bffa
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997639(v=EXCHG.150)
ms:contentKeyID: 52061339
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.OrganizationConfiguration.NewRemoteDomainWizardForm.NewRemoteDomainWizardPage
ms.translationtype: HT
---

# 管理远程域

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-13_

远程域是 Microsoft Exchange 组织外部的 SMTP 域。可以创建远程域条目，以定义在 Exchange 组织和特定外部域之间传输的邮件的设置。远程域条目中用于特定外部域的设置会覆盖默认远程域中通常适用于所有外部收件人的设置。远程域设置是适用于 Exchange 组织的全局设置。

如果删除远程域条目，则邮件传输的设置将不再应用于发送到远程域的邮件。删除远程域条目不禁用远程域的邮件流。删除远程域条目后，默认远程域的配置设置将应用于发送到该域的新邮件。不能删除默认远程域。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤的时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“远程域”条目。

  - 只能使用命令行管理程序执行此过程。

  - 您不能为组织中配置为接受域的地址空间创建远程域。例如，如果组织接受 fabrikam.com 的邮件，则无法创建 fabrikam.com 的远程域。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 希望执行何种操作？

## 使用命令行管理程序创建远程域

若要创建新的远程域条目，请使用以下语法。

```powershell
New-RemoteDomain -Name <Descriptive Name> -DomainName <SMTP address space>
```

本示例为发送至 contoso.com 域的邮件创建远程域条目。

```powershell
New-RemoteDomain -Name Contoso -DomainName contoso.com
```

本示例为发送至 fabrikam.com 域和所有子域的邮件创建远程域条目。

  ```powershell
    New-RemoteDomain -Name Fabrikam -DomainName *.fabrikam.com
  ```

## 您如何知道操作成功？

若要验证是否已成功创建远程域，请执行以下操作：

1.  运行命令 **Get-RemoteDomain** 并验证是否已列出远程域。

2.  运行命令 `Get-RemoteDomain <Remote Domain Name> | Format-List` 来验证新远程域上的设置。将测试邮件发送到新远程域条目中指定的地址空间中的收件人，并验证邮件设置是否与新远程域条目所指定的设置相匹配。

## 使用命令行管理程序配置远程域

使用 **Set-RemoteDomain** cmdlet 配置远程域条目中的设置。有许多与自动答复、邮件格式和编码相关的不同设置以及其他邮件设置。有关详细信息，请参阅 [Set-RemoteDomain](https://technet.microsoft.com/zh-cn/library/aa997857\(v=exchg.150\))。

若要为特定方案配置远程域，请参阅以下主题：

  - [配置远程域外出答复](configure-remote-domain-out-of-office-replies-exchange-2013-help.md)

  - [配置远程域自动答复](configure-remote-domain-automatic-replies-exchange-2013-help.md)

  - [配置远程域邮件报告](configure-remote-domain-message-reporting-exchange-2013-help.md)

## 使用命令行管理程序删除远程域

若要删除远程域条目，请使用以下语法。

```powershell
Remove-RemoteDomain <RemoteDomainName>
```

此示例将删除远程域条目 Contoso

```powershell
Remove-RemoteDomain Contoso
```

## 您如何知道操作成功？

若要验证是否已成功删除远程域，请执行以下操作：

1.  运行命令 **Get-RemoteDomain** 并验证是否已列出远程域。

2.  运行命令 `Get-RemoteDomain Default | Format-List` 来验证默认远程域上的设置。将测试邮件发送到已删除的远程域中指定的地址空间中的收件人，并验证邮件设置是否与默认远程域所指定的设置相匹配。

