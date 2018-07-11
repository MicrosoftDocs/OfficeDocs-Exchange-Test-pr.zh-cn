---
title: '配置内容筛选以使用安全域数据: Exchange 2013 Help'
TOCTitle: 配置内容筛选以使用安全域数据
ms:assetid: 1ee2b663-b4f3-4fef-8954-986f2d820924
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn467930(v=EXCHG.150)
ms:contentKeyID: 59636391
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置内容筛选以使用安全域数据

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-12-16_

安全域数据是存储在用户白名单中的整个域（例如 @contoso.com）。默认情况下，内容筛选器代理不使用安全域数据来识别允许避开内容筛选的发件人。

这一默认设置有助于降低传递到您组织中的垃圾邮件的数量。例如，用户可以将一个大型电子邮件提供商的域添加到他们的白名单中。如果该域被频繁使用或被垃圾邮件发送者伪造，内容筛选被配置为使用安全域数据将这些邮件标记为安全，则该域中任何发件人的邮件都会传递到您组织中的收件人。

建议您在大多数情况下不要修改默认设置。然而，您可以配置要存储于 Active Directory 中并由内容过滤用于标记邮件为安全的用户安全域数据。若要执行此操作，您需要修改与 Microsoft Exchange 邮箱助理服务关联的 MSExchangeMailboxAssistants.exe.config XML 应用程序配置文件，稍后将在此主题中详细介绍。当您更改此配置时，计算安全域数据的哈希值，并将其存储在 Active Directory 中每个用户的 **msExchSafeSenderHash** 用户对象属性中，作为安全列表聚合的一部分。然后此内容筛选代理可以使用安全域数据以将来自于这些域中发件人的邮件标记为安全。有关安全列表聚合的更多信息，请参阅[安全列表聚合](safelist-aggregation-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：10 分钟

  - Exchange 权限不适用于本主题中的过程。这些过程在 Exchange Server 的操作系统中执行。

  - 在您重新启动 Microsoft Exchange 邮箱助理服务后，应用您保存到 MSExchangeMailboxAssistants.exe.config 文件中的更改。

  - 在您安装 Exchange 累积更新 (CU) 时，您在 Exchange XML 应用程序配置文件（例如，客户端访问服务器上的 web.config 文件，或邮箱服务器上的 EdgeTransport.exe.config 文件）中针对每个服务器所做的任何自定义设置都将被覆盖。请务必保存此类信息，以便在安装累积更新后，您可以轻松地重新配置服务器。安装 Exchange CU 后，您必须重新配置这些设置。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用命令提示符配置内容筛选以使用安全域数据

1.  在命令提示符窗口，通过运行以下命令，打开记事本中的 MSExchangeMailboxAssistants.exe.config 文件：
    
        Notepad %ExchangeInstallPath%Bin\MSExchangeMailboxAssistants.exe.config

2.  在文件末尾处找到 *\</appsettings\>* 项，然后将以下项粘贴到 *\</appsettings\>* 项之前：
    
        <add key="IncludeSafeDomains" value="true" />

3.  在完成后，保存并给关闭 MSExchangeMailboxAssistants.exe.config 文件。

4.  通过运行以下命令，重新启动 Microsoft Exchange 邮箱助理服务：
    
        net stop MSExchangeMailboxAssistants && net start MSExchangeMailboxAssistants

## 您如何知道操作成功？

若要验证您已成功配置内容筛选以使用安全域数据，请执行以下操作：

1.  验证将域添加到 Outlook 中的用户白名单更新了 Active Directory 中用户的 **msExchSafeSenderHash** 属性。为此，查看 ADSIEdit.exe 或 LDP.exe 中的属性，打开 Outlook 中的用户邮箱，将域添加到白名单，运行命令 `Update-Safelist <username>`，然后验证 **msExchSafeSenderHash** 的原始值是否与当前值不同。

2.  在验证安全域数据存储在 Active Directory 中之后，从该域的外部发件人将测试邮件发送到您组织的用户。通过检查邮件标头中反垃圾邮件的标头字段，验证此邮件是否标记为安全。

