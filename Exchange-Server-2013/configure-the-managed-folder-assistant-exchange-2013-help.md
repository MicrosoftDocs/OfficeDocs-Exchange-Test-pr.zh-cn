---
title: '配置托管文件夹助理: Exchange 2013 Help'
TOCTitle: 配置托管文件夹助理
ms:assetid: 9fcfb9b6-bd24-4218-a163-bc599cd5476a
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb123958(v=EXCHG.150)
ms:contentKeyID: 50491178
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 配置托管文件夹助理

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2014-10-01_

\&quot;托管文件夹助理\&quot;是 MicrosoftExchange 邮箱助理，它应用保留策略中配置的邮件保留设置。

有关与邮件记录管理 (IRM) 相关的其他管理任务，请参阅[邮件记录管理程序](messaging-records-management-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 完成时间：1 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [邮件策略和遵从性权限](messaging-policy-and-compliance-permissions-exchange-2013-help.md)主题中的\&quot;邮件记录管理\&quot;条目。

  - 不能使用 Exchange 管理中心 (EAC) 配置托管文件夹助理。必须使用命令行管理程序

  - 在 Exchange 2013 中，托管文件夹助理是基于限制的助理。基于限制的助理始终运行，无需进行计划。这些助理可以占用的系统资源会受到限制。可以将托管文件夹助理配置为在特定期间内（称为\&quot;工作周期\&quot;）处理邮箱服务器上的所有邮箱。默认情况下，工作周期设置为一天。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序配置托管文件夹助理

此示例将托管文件夹助理配置为在一天内处理所有邮箱。

```powershell
Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1
```

有关语法和参数的详细信息，请参阅 [Set-MailboxServer](https://technet.microsoft.com/zh-cn/library/aa998651\(v=exchg.150\))。

## 我如何知道这有效？

若要验证是否已成功配置托管文件夹助理，请使用 [Get-MailboxServer](https://technet.microsoft.com/zh-cn/library/bb123539\(v=exchg.150\)) cmdlet 检查 *ManagedFolderWorkCycle* 参数。

此命令检索组织中的所有邮箱服务器并以表格格式从每台服务器输出托管文件夹助理的工作周期属性。*Auto* 开关用于自动调整列宽。

    Get-MailboxServer | Format-Table Name,ManagedFolderWorkCycle* -Auto

## 使用命令行管理程序启动托管文件夹助理

此示例触发托管文件夹助理，以立即处理 Morris Cornejo 的邮箱。

```powershell
Start-ManagedFolderAssistant -Identity morris.cornejo@contoso.com
```

有关语法和参数的详细信息，请参阅 [Start-ManagedFolderAssistant](https://technet.microsoft.com/zh-cn/library/aa998864\(v=exchg.150\))。

