---
title: '管理边缘传输服务器上的收件人筛选: Exchange 2013 Help'
TOCTitle: 管理边缘传输服务器上的收件人筛选
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50491929
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理边缘传输服务器上的收件人筛选

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

收件人筛选由收件人筛选器代理提供。当收件人筛选在 Exchange 服务器上启动时，将筛选来自 Internet 但未经验证的入站邮件。这些邮件将作为外部邮件处理。

> [!NOTE]  
> 尽管收件人筛选代理在邮箱服务器上可用，但不应对其进行配置。当邮箱服务器上的收件人筛选检测到包含其他有效收件人的邮件中具有无效或受阻止接收人，邮件会被拒绝。如果在邮箱服务器上安装反垃圾邮件代理，将默认启用收件人筛选器代理。但是，未将其配置为阻止任何收件人。有关详细信息，请参阅<a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">在邮箱服务器上启用反垃圾邮件功能</a>。


## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - **Set-AcceptedDomain** cmdlet 上的参数 *AddressBookEnabled* 将启动或禁用收件人在接受域中的收件人筛选。默认情况下，启用权威域的收件人筛选，并禁用内部中继域和外部中继域的收件人筛选。要查看您组织中接受域的 *AddressBookEnabled* 参数状态，请运行下面的命令：
    
    ```powershell
Get-AcceptedDomain | Format-List Name,AddressBookEnabled
```

  - 如果您使用本主题中的步骤禁用收件人筛选，则收件人筛选功能将被禁用，但基本\&quot;收件人筛选\&quot;代理仍将为启动状态。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用收件人筛选

若要禁用收件人筛选，请运行以下命令：

```powershell
Set-RecipientFilterConfig -Enabled $false
```

若要启用收件人筛选，请运行以下命令：

```powershell
Set-RecipientFilterConfig -Enabled $true
```

> [!NOTE]  
> 禁用收件人筛选时，基本&amp;quot;收件人筛选&amp;quot;代理仍启用。若要禁用收件人筛选器代理，请运行以下命令：<code>Disable-TransportAgent &quot;Recipient Filter Agent&quot;</code>.


## 您如何知道这有效？

要验证您是否成功启用或禁用收件人筛选，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-RecipientFilterConfig | Format-List Enabled
```

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序启用或禁用收件人阻止列表

运行以下命令：

```powershell
Set-RecipientFilterConfig -BlockListEnabled <$true | $false>
```

本示例启用收件人阻止列表：

```powershell
Set-RecipientFilterConfig -BlockListEnabled $true
```

## 您如何知道这有效？

要验证您是否成功启用或禁用收件人阻止列表，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-RecipientFilterConfig | Format-List BlockListEnabled
```

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序配置收件人阻止列表

要替换现有值，请运行以下命令：

```powershell
Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>
```

本示例使用 valuesmark@contoso.com 和 kim@contoso.com 配置收件人阻止列表：

```powershell
Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com
```

要在不修改任何现有值的情况下添加或删除条目，请运行以下命令：

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

本示例将添加 chris@contoso.com 至收件人列表，并从收件人阻止列表的收件人列表中删除 michelle@contoso.com：

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## 您如何知道这有效？

要验证您是否成功配置收件人阻止列表，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-RecipientFilterConfig | Format-List BlockedRecipients
```

2.  验证显示的值是否为您配置的值。

## 使用命令行管理程序启用或禁用收件人查找

运行以下命令：

```powershell
Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>
```

若要阻止发送到组织中不存在的收件人的邮件，请运行以下命令：

```powershell
Set-RecipientFilterConfig -RecipientValidationEnabled $true
```

## 您如何知道这有效？

要验证您是否成功启用或禁用收件人查找，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-RecipientFilterConfig | Format-List RecipientValidationEnabled
```

2.  验证显示的值是否为您配置的值。

