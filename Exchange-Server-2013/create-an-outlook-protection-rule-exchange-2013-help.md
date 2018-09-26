---
title: '创建 Outlook 保护规则: Exchange 2013 Help'
TOCTitle: 创建 Outlook 保护规则
ms:assetid: da64750d-faaf-44de-ad8c-888eba7fbdbf
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd638196(v=EXCHG.150)
ms:contentKeyID: 50491662
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 创建 Outlook 保护规则

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

使用 Microsoft Outlook保护规则，您可以通过发送邮件前请先应用在Outlook 2010Active Directory权限管理服务 (AD RMS) 模板保护邮件信息权限管理 (IRM)。

关于 IRM 的更多管理任务，请参阅[信息权限管理过程](information-rights-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间︰ 1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;权限保护\&quot;条目。

  - 您必须在同一个林中Active Directory运行 Microsoft Exchange Server 2013服务器中部署[AD RMS](https://technet.microsoft.com/en-us/library/hh831364.aspx)服务器。

  - 如果配置Outlook保护规则，以 IRM 保护的邮件时，请考虑启用传输解密允许传输代理，包括传输规则代理，以解密并访问该邮件。如果您使用日记，还应考虑启用日志报告解密，使日志记录代理保存该邮件的未加密的副本日志报告中。有关详细信息，请参阅[日记报告解密](journal-report-decryption-exchange-2013-help.md)。

  - 不能使用 Exchange 管理中心 (EAC) 来创建Outlook保护规则。您必须使用外壳程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 使用外壳程序创建一个 Outlook 保护规则

本示例创建项目 Contoso 的Outlook保护规则。该规则保护发送到 ContosoPMs 通讯组与 AD RMS 模板关键业务的消息。

```powershell
New-OutlookProtectionRule -Name "Project Contoso" -SentTo "DL-ContosoPMs@contoso.com" -ApplyRightsProtectionTemplate "Business Critical"
```

> [!NOTE]  
> 当您使用<code>SentTo</code>谓词的Outlook保护规则和指定通讯组，仅将邮件发送到通讯组在收件人、 抄送或密件抄送字段是受 IRM 保护。IRM 保护不被应用于邮件发送到通讯组中的单个成员。


此外可以使用`FromDepartment`和`SentToScope`谓词来从指定的部门或消息发送到指定的作用域 （`InOrganization`内部邮件， `All`的所有收件人） 中的用户发送的邮件应用 IRM 保护。

有关详细的语法和参数的信息，请参阅[New-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd298182\(v=exchg.150\))。

## 您如何知道这有效？

要验证您已成功创建了 Outlook 的保护规则，请执行以下操作︰

  - 运行[Get-OutlookProtectionRule](https://technet.microsoft.com/zh-cn/library/dd298004\(v=exchg.150\)) cmdlet 以确保已创建规则并查看规则的属性。如何检索 Outlook 保护规则的示例，请参阅**Get-OutlookProtectionRule**中的[示例](https://technet.microsoft.com/zh-cn/dd298004\(exchg.150\)#examples)。

  - 使用Outlook 2010来创建测试邮件，以满足该规则的条件，并确保该规则触发客户端上。
    
    > [!NOTE]  
    > 它可能需要一些时间才能在 Outlook 中可用的 Outlook 保护规则。

