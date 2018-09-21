---
title: '管理边缘传输服务器上的附件筛选: Exchange 2013 Help'
TOCTitle: 管理边缘传输服务器上的附件筛选
ms:assetid: 2ec91cc6-6ade-48ee-88bb-66153874393d
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997139(v=EXCHG.150)
ms:contentKeyID: 60829983
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理边缘传输服务器上的附件筛选

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

附件筛选是由仅在边缘传输服务器上可用的附件筛选器代理提供。附件筛选可以帮助阻止电子邮件中的附加文件进入您的组织。您可以将一个或多个附件筛选器条目配置为按内容类型或文件名筛选附件。

## 在开始之前，您需要知道什么？

  - 完成每个过程的估计时间：10 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目和[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的\&quot;传输代理\&quot;条目。

  - 您对边缘传输服务器上的附件筛选所做的配置更改只对本地计算机有效。如果您在外围网络中有多个边缘传输服务器，则需要分别在每个边缘传输服务器上配置附件筛选。

  - 只能使用命令行管理程序执行此过程。

  - 当您禁用附件筛选并重启 Microsoft Exchange 传输服务时，所有附件筛选功能均停止运行。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用附件筛选

当您启用或禁用附件筛选代理时，所做的更改将在您重启 Microsoft Exchange 传输服务之后生效。重启边缘传输服务器上的 Microsoft Exchange 传输服务时，服务器上的邮件流会临时中断。

若要禁用附件筛选，请运行以下命令：

```powershell
Disable-TransportAgent "Attachment Filtering Agent"
```

若要启用附件筛选，请运行以下命令：

```powershell
Enable-TransportAgent "Attachment Filtering Agent"
```

在您启用或禁用附件筛选之后，请通过运行以下命令来重启 Microsoft Exchange 传输服务：

```powershell
Restart-Service MSExchangeTransport
```

## 您如何知道这有效？

若要验证您是否已成功启用或禁用附件筛选，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-TransportAgent "Attachment Filtering Agent"
```

2.  如果 **Enabled** 的值为 `True`，则表示附件筛选已启用。如果值为 `False`，则表示附件筛选已禁用。

## 使用命令行管理程序查看附件筛选条目

附件筛选条目界定了您想将其隔离在组织之外的邮件附件。若要查看附件筛选代理使用的附件筛选条目，请运行以下命令：

```powershell
Get-AttachmentFilterEntry | Format-Table
```

若要查看特定的 MIME 内容类型条目，请使用以下语法：

```powershell
Get-AttachmentFilteringEntry ContentType:<MIMEContentType>
```

例如，若要查看 JPEG 图像的内容类型条目，请运行以下命令：

```powershell
Get-AttachmentFilteringEntry ContentType:image/jpeg
```

若要查看特定的文件名或文件扩展名条目，请使用以下语法：

```powershell
Get-AttachmentFilteringEntry FileName:<FileName or FileNameExtension>
```

例如，若要查看 JPEG 附件的文件扩展名条目，请运行以下命令：

    Get-AttachmentFilteringEntry FileName:*.jpg

## 使用命令行管理程序添加附件筛选条目

若要添加按 MIME 内容类型筛选附件的附件筛选条目，请使用以下语法：

```powershell
Add-AttachmentFilterEntry -Name <MIMEContentType> -Type ContentType
```

以下示例添加筛选 JPEG 图像的 MIME 内容类型条目。

```powershell
Add-AttachmentFilterEntry -Name image/jpeg -Type ContentType
```

若要添加按文件名或文件扩展名筛选附件的附件筛选条目，请使用以下语法：

```powershell
Add-AttachmentFilterEntry -Name <FileName or FileNameExtension> -Type FileName
```

以下示例筛选具有 .jpg 文件扩展名的附件。

    Add-AttachmentFilterEntry -Name *.jpg -Type FileName

## 您如何知道这有效？

若要验证是否已成功添加附件筛选条目，请执行以下操作：

1.  运行以下命令来验证筛选条目是否存在。
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  从外部邮箱向内部收件人发送包含禁止的附件的测试邮件，并验证该邮件是否被拒绝、去除或删除。

## 使用命令行管理程序删除附件筛选条目

若要删除按 MIME 内容类型筛选附件的附件筛选条目，请使用以下语法：

```powershell
Remove-AttachmentFilterEntry ContentType:<ContentType>
```

以下示例删除 JPEG 图像的 MIME 内容类型条目。

```powershell
Remove-AttachmentFilterEntry ContentType:image/jpeg
```

若要删除按文件名或文件扩展名筛选附件的附件筛选条目，请使用以下语法：

```powershell
Remove-AttachmentFilterEntry FileName:<FileName or FileNameExtension>
```

以下示例删除 .jpg 文件扩展名的文件名条目。

    Remove-AttachmentFilterEntry FileName:*.jpg

## 您如何知道这有效？

若要验证是否已成功删除附件筛选条目，请执行以下操作：

1.  运行以下命令来验证筛选条目是否已删除。
    
    ```powershell
Get-AttachmentFilterEntry | Format-Table
```

2.  从外部邮箱向内部收件人发送包含允许的附件的测试邮件，并验证该邮件（包含附件）是否已成功发送。

## 使用命令行管理程序查看附件筛选操作

若要查看当邮件中检测到禁止的附件时执行的附件筛选操作，请运行以下命令：

```powershell
Get-AttachmentFilterListConfig
```

## 使用命令行管理程序配置附件筛选操作

若要配置当邮件中检测到禁止的附件时执行的附件筛选操作，请使用以下语法：

    Set-AttachmentFilterListConfig [-Action <Reject | Strip | SilentDelete>] [-RejectResponse "<Message text>"] [-AdminMessage "<Replacement file text>"] [-ExceptionConnectors <ConnectorGUID>]

本示例对附件筛选配置做出以下更改：

  - 拒绝（阻止）包含禁止的附件的邮件。

  - 对拒绝的邮件使用自定义响应。

<!-- end list -->

    Set-AttachmentFilterListConfig -Action Reject -RejectResponse "This message contains a prohibited attachment. Your message can't be delivered. Please resend the message without the attachment."

有关详细信息，请参阅 [Set-AttachmentFilterListConfig](https://technet.microsoft.com/zh-cn/library/bb123483\(v=exchg.150\))。

## 您如何知道这有效？

若要验证是否已成功配置附件筛选操作，请从外部邮箱向内部收件人发送包含禁止的附件的测试邮件，并验证该邮件和附件的处理方式是否符合您的预期。

