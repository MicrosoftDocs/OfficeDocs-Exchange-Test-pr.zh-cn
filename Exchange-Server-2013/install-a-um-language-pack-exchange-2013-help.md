---
title: '安装 UM 语言包: Exchange 2013 Help'
TOCTitle: 安装 UM 语言包
ms:assetid: ed14ffa5-c9b0-4367-b5da-564024b360ff
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876951(v=EXCHG.150)
ms:contentKeyID: 50491914
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安装 UM 语言包

 

_**适用于：** Exchange Server 2013, Exchange Server 2016_

_**上一次修改主题：** 2016-12-09_

若要使某种语言显示在 UM 拨号计划或 UM 自动助理上的可用统一消息语言列表中，必须先安装相应的 UM 语言包。您可以通过语言特定的自解压可执行文件或 **setup.exe /AddUmLanguagePack** 命令，在运行 Microsoft Exchange 统一消息服务的邮箱服务器上安装该语言包。在安装 UM 语言包之前，必须先将它下载到邮箱服务器的本地文件夹中。可以从 [Exchange Server 2013 UM 语言包](http://go.microsoft.com/fwlink/p/?linkid=266542) 下载 UM 语言包。每种语言有一个单独的可执行文件。

在安装相应的 UM 语言包后，可通过查看 UM 拨号计划的“设置”页面上的下拉列表或 UM 自动助理的“常规”页面上的“自动语音界面的语言”下拉列表来查看已安装 UM 语言包的列表。此外，还可以将 UM 拨号计划和自动助理的默认语言配置为英语 (en-US) 以外的语言。

> [!CAUTION]  
> Microsoft Exchange Server 2007 或 Exchange 2007 Service Pack 1 (SP1)、SP2 或 SP3 或者 Exchange 2010 Service Pack 1 SP1、SP2 或 SP3 的 UM 语言包不能用在 Exchange 2013 邮箱服务器上。


有关与 UM 语言相关的其他任务，请参阅 [UM 语言、 提示和问候过程](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[统一消息权限](unified-messaging-permissions-exchange-2013-help.md)中的“邮箱服务器（UM 服务）”条目。

  - 验证邮箱服务器是否安装在与客户端访问服务器不同的计算机上，或者客户端访问和邮箱服务器是否位于同一硬件上。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。.


## 您想执行什么操作？

## 使用 UM 语言包安装文件 (.exe) 安装 UM 语言包

1.  在 [Microsoft 下载中心](https://go.microsoft.com/fwlink/p/?linkid=266542)中，将语言特定的 UM 语言包文件 (.exe) 下载到邮箱服务器上的本地文件夹。

2.  双击 UMLanguagePack.*\<CultureCode\>.exe* 文件。例如，对于德语的 UM 语言包，请下载名为 UMLanguagePack.de-DE.exe 的文件。

3.  
    
    在Exchange 2013安装向导的“**许可协议**”页中，阅读协议条款，选择“**我接受许可协议中的条款**”，然后单击“**下一步**”。

4.  
    
    在“统一消息语言包”页上，验证“将安装以下统一消息语言包”窗口中是否列出了正确的语言，然后单击“安装”。

5.  单击“完成”结束 UM 语言包的安装。

## 使用 setup.exe 安装 UM 语言包

以下示例将安装日语 (ja-JP) 的 UM 语言包，该语言包已下载到邮箱服务器上的 D:\\Exchange\\UMLanguagePacks 文件夹。

```powershell
setup.exe /AddUmLanguagePack:ja-JP /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms
```

以下示例将安装墨西哥西班牙语 (es-MX) 和德语 (de-DE) 的 UM 语言包，这些语言包已下载到邮箱服务器上的 D:\\Exchange\\UMLanguagePacks 文件夹。

    setup.exe /AddUmLanguagePack:es-MX,de-DE /s:d:\Exchange\UMLanguagePacks /IAcceptExchangeServerLicenseTerms

> [!WARNING]  
> 如果不使用 /IAcceptExchangeServerLicenseTerms 参数，则将看到以下错误：欢迎使用 Microsoft Exchange Server 2013 无人参与安装程序。您需要接受许可条款才能安装 Microsoft Exchange Server 2013。若要阅读许可协议，请访问 http://go.microsoft.com/fwlink/p/?LinkId=150127。若要接受许可协议，请将 /IAcceptExchangeServerLicenseTerms 参数添加到运行的命令中。有关详细信息，请运行 setup /?。


有关可用 UM 语言包和区域性代码的详细信息，请参阅[UM 语言、提示和问候语](um-languages-prompts-and-greetings-exchange-2013-help.md)。

