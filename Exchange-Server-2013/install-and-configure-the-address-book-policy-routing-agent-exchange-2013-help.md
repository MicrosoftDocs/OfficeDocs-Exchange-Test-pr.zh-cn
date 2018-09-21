---
title: '安装并配置通讯簿策略路由代理: Exchange 2013 Help'
TOCTitle: 安装并配置通讯簿策略路由代理
ms:assetid: 20e8a43d-4508-4388-a2c9-aa3073593cc2
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/JJ907308(v=EXCHG.150)
ms:contentKeyID: 51408207
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 安装并配置通讯簿策略路由代理

 

_**适用于：** Exchange Online, Exchange Server 2013_

_**上一次修改主题：** 2014-01-09_

通讯簿策略路由代理是一个传输代理，运行在邮箱服务器上，控制组织中收件人解析的方式。在安装并配置 ABP 路由代理后，分配到不同 GAL 的用户会显示为外部收件人，因为他们无法对外部收件人的联系卡进行查看。

关于 ABP 的更多管理任务，请参阅[通讯簿策略程序](address-book-policy-procedures-exchange-2013-help.md)。

是否正在寻找此主题的 Exchange Online 版本？请参阅[打开通讯簿策略路由](https://technet.microsoft.com/zh-cn/library/jj891095\(v=exchg.150\))。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：15 分钟。

  - 安装并配置 ABP 路由代理后，代理可能需要 30 分钟的时间来对组织中的电子邮件进行评估。

  - 无法使用 EAC 执行此过程。必须使用命令行管理程序。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您该如何做？

## 步骤 1：安装 ABP 路由代理

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输代理”条目。

通过运行以下命令安装 ABP 路由代理。这是您将需要使用的确切命令和语法。

    Install-TransportAgent -Name "ABP Routing Agent" -TransportAgentFactory "Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.AddressBookPolicyRoutingAgentFactory" -AssemblyPath $env:ExchangeInstallPath\TransportRoles\agents\AddressBookPolicyRoutingAgent\Microsoft.Exchange.Transport.Agent.AddressBookPolicyRoutingAgent.dll

您将收到一条警告，指示传输服务需要重新启动以使更改生效，但请首先执行步骤 2，以便传输服务仅需重新启动一次。

有关语法和参数的详细信息，请参阅 [Install-TransportAgent](https://technet.microsoft.com/zh-cn/library/aa997998\(v=exchg.150\))。

## 步骤 2：启动传输路由代理

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输代理”条目。

安装了 ABP 路由代理之后，您需要通过运行以下命令启动它：

```powershell
Enable-TransportAgent "ABP Routing Agent"
```

有关语法和参数的详细信息，请参阅 [Enable-TransportAgent](https://technet.microsoft.com/zh-cn/library/bb124921\(v=exchg.150\))。

## 步骤 3：重新启动传输服务，并验证 ABP 路由代理是否已安装并启用

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输代理”条目。

1.  通过运行以下命令重新启动传输服务。
    
    ```powershell
Restart-Service MSExchangeTransport
```

2.  重新启动服务之后，通过运行以下 cmdlet 验证 ABP 路由代理是否已安装并启用。
    
    ```powershell
Get-TransportAgent
```
    
    如果 ABP 路由代理已经列出，说明代理已经正确安装。

有关语法和参数的详细信息，请参阅 [Get-TransportAgent](https://technet.microsoft.com/zh-cn/library/bb123536\(v=exchg.150\))。

## 步骤 4：启用 ABP 路由代理

您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“传输配置”条目。

此过程的最后一个步骤是为组织启用 ABP 路由。运行以下命令。

```powershell
Set-TransportConfig -AddressBookPolicyRoutingEnabled $true
```

有关语法和参数的详细信息，请参阅 [Set-TransportConfig](https://technet.microsoft.com/zh-cn/library/bb124151\(v=exchg.150\))。

