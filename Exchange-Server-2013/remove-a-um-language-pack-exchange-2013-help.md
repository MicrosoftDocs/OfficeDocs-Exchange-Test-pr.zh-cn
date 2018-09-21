---
title: '删除 UM 语言包: Exchange 2013 Help'
TOCTitle: 删除 UM 语言包
ms:assetid: a2bc2753-2c25-4ea0-a9d5-e3d42a699c6c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb124004(v=EXCHG.150)
ms:contentKeyID: 50491244
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 删除 UM 语言包

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2013-02-14_

可以在运行 Microsoft Exchange 统一消息服务的邮箱服务器上使用 EAC 或命令行管理程序管理统一消息 (UM) 语言。但是，若要从 UM 拨号计划上的列表中删除语言，必须使用 **Setup.exe /RemoveUmLanguagePack** 命令从邮箱服务器中删除相应的 UM 语言包。从邮箱服务器中删除该 UM 语言包后，配置 UM 拨号计划或 UM 自动助理时该语言将不再可用。可通过查看邮箱服务器的属性或使用 **Get-UMService** cmdlet 来查看已安装的 UM 语言包。

有关与 UM 语言相关的其他任务，请参阅 [UM 语言、 提示和问候过程](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：不超过 5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)主题中的“邮箱服务器（UM 服务）”条目。

  - 验证安装了非 EN-US UM 语言包。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 使用 Setup.exe 删除 UM 语言包

在命令提示符下，运行以下命令。

```powershell
Setup.exe /RemoveUmLanguagePack:<UmLanguagePackName>
```

在上一个命令中，*\<UmLanguagePackName\>* 是 UM 语言包的名称，例如 fr-FR。

> [!CAUTION]  
> 安装了所有更新后，您将无法使用位于 \Bin 文件夹下的 Setup.exe 文件来删除 UM 语言包。您必须从 Exchange 2013 DVD 或下载的源文件中使用 Setup.exe 文件。否则，将看到以下错误：正在运行的应用程序和已安装的应用程序之间的版本不匹配。

