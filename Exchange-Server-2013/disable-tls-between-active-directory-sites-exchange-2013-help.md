---
title: '在 Active Directory 站点之间禁用 TLS: Exchange 2013 Help'
TOCTitle: 在 Active Directory 站点之间禁用 TLS
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52061486
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 在 Active Directory 站点之间禁用 TLS

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2013-02-19_

Microsoft Exchange Server 2013 支持禁用邮箱服务器之间的 SMTP 通信的 TLS，这些服务器位于特定的拓扑中，其中使用了可压缩 SMTP 通信的 WAN 优化控制器 (WOC) 设备。

本主题提供了关于如何将受影响的邮箱服务器中的传输服务配置为禁用 TLS 的分步骤说明，以及关于如何确保将 Active Directory 路由拓扑配置为正确路由邮件的分步骤说明。有关此方案的详细信息，请参阅[方案：将 Exchange 配置为支持 WAN 优化控制器](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)。

## 在开始之前，您需要知道什么？

  - 估计完成该任务的时间：60 分钟。

  - 尽管完成本方案中的单个配置步骤不需要太多权限，但要完成整个端到端方案任务，您的帐户则需要是组织管理角色组的成员。

  - 确保仅对通过 WOC 设备的连接禁用 TLS。

  - 该步骤要求在多个 Active Directory 站点中部署 Exchange 2013，且至少有一个站点通过 WAN 链接连接到其他站点。

  - 该步骤要求将 WOC 设备部署为压缩通过 WAN 链接的 SMTP 通信。

  - 该步骤要求通过已部署 WOC 设备的 WAN 链接的 Exchange 存在逻辑邮件流路径。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 步骤 1：使用命令行管理程序配置邮箱服务器上的传输服务，以使用降级的 Exchange Server 身份验证

要配置邮箱服务器上的传输服务以使用降级的 Exchange Server 身份验证，请运行以下命令：

```powershell
  Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true
```

本示例在名为 Mailbox01 的服务器上进行了此项配置更改。

```powershell
  Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true
```

## 步骤 2：在邮箱服务器上为目标 Active Directory 站点创建专用的接收连接器

## 使用 EAC 创建接收连接器

1.  在 Exchange 管理中心 (EAC) 中，单击“邮件流”\>“接收连接器”，然后单击“添加”![添加图标](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "添加图标")。

2.  在“新建接收连接器”向导的第一页上，输入以下值
    
      - **名称**   输入一个描述性的值。
    
      - **类型**   内部
    
    完成后，单击“下一步”。

3.  在“新建接收连接器”向导的第二页上的“远程设置”部分，输入目标 Active Directory 站点的 IP 地址或 IP 地址范围。完成后，单击“完成”。

## 使用命令行管理程序创建接收连接器

要在邮箱服务器上创建接收连接器，请运行以下命令：

  ```powershell
    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal
  ```

本示例在名为 Mailbox01 的服务器上创建了名为 WAN 的接收连接器，具有如下设置：

  - *RemoteIPRanges* 参数设置为 10.0.2.0/24。此 IP 地址范围应对应于此接收连接器将从其接收未加密连接的运程 Active Directory 站点。如果远程站点中有多个 IP 子网，则可以输入这些子网，并用逗号隔开。

  - 使用类型设置为“内部”。

<!-- end list -->

```powershell
  New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal
```

## 步骤 3：使用命令行管理程序禁用专用接收连接器上的 TLS

要在接收连接器上禁用 TLS，请运行以下命令：

```powershell
  Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true
```

本示例禁用了名为 Mailbox01 的邮箱服务器上名为 WAN 的接收连接器的 TLS。

```powershell
  Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true
```

## 步骤 4：使用命令行管理程序指定 Active Directory 站点作为中心站点

要将 Active Directory 站点指定为中心站点，请运行以下命令：

```powershell
  Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true
```

需要在每个拥有参与非加密通信的邮箱服务器的 Active Directory 站点中执行一次该步骤。

本示例将名为“中心办公室站点 1”的 Active Directory 站点配置为中心站点。

```powershell
  Set-AdSite "Central Office Site 1" -HubSiteEnabled $true
```

## 步骤 5：使用命令行管理程序配置通过 WAN 连接的开销最低的路由路径

根据在 Active Directory 中配置 IP 站点链接开销的方式，该步骤可能不是必需的。您需要验证部署了 WOC 设备的网络链接是否存在于开销最低的路由路径中。要查看 Active Directory 站点链接开销，以及 Exchange 特定的站点链接开销，请运行以下命令：

```powershell
  Get-AdSiteLink
```

如果部署了 WOC 设备的网络链接不存在于开销最低的路由路径上，则需要将特定于 Exchange 的开销分配给特定的 IP 站点链接，以确保正确地路由邮件。有关此特定问题的详细信息，请参阅[方案：将 Exchange 配置为支持 WAN 优化控制器](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)中的“配置特定于 Exchange 的 Active Directory 站点链接开销”部分。

本示例在名为“分支机构 2-分支机构 1”的 IP 站点链接上将特定于 Exchange 的开销配置为 15。

```powershell
  Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15
```

