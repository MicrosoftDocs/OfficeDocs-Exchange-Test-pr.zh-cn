---
title: '管理发件人信誉: Exchange 2013 Help'
TOCTitle: 管理发件人信誉
ms:assetid: f2716bd9-e3ac-46d9-9264-4e3dabfa0f38
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Bb125186(v=EXCHG.150)
ms:contentKeyID: 50491927
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 管理发件人信誉

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

发件人信誉是由协议分析代理提供的。发件人信誉根据发件人的不同特征阻止邮件。发件人信誉依赖于有关发件人的保留数据来确定对入站邮件执行的操作（如果有）。

## 在开始之前，您需要知道什么？

  - 估计完成每个步骤时间：5 分钟

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅 [反垃圾邮件和反恶意软件权限](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)主题中的\&quot;反垃圾邮件功能\&quot;条目。

  - 只能使用命令行管理程序执行此过程。

  - 默认情况下，邮箱服务器上的传输服务未启用反垃圾邮件功能。一般情况下，只有当您的 Exchange 组织在接受传入的邮件前未事先进行任何反垃圾邮件筛选时，您才需要在邮箱服务器上启用反垃圾邮件功能。有关详细信息，请参阅[在邮箱服务器上启用反垃圾邮件功能](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)。

  - 协议分析代理是发件人信誉功能的基本代理。当您禁用发件人信誉时，\&quot;协议分析代理\&quot;仍处于启用状态。

  - 若要了解可能适用于此主题中过程的键盘快捷键，请参阅 [Exchange 管理中心内的键盘快捷键](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 您想执行什么操作？

## 使用命令行管理程序启用或禁用发件人信誉

此示例禁用发件人信誉。

```powershell
Set-SenderReputationConfig -Enabled $false
```

此示例启用发件人信誉。

```powershell
Set-SenderReputationConfig -Enabled $true
```

## 您如何知道这有效？

要验证您是否成功启用或禁用发件人信誉，请执行以下操作：

1.  运行下面的命令，验证\&quot;协议分析\&quot;代理已安装和启用：
    
    ```powershell
Get-TransportAgent
```

2.  运行下面的命令，验证您配置的发件人信誉值：
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

## 使用命令行管理程序为内部和外部邮件启用或禁用发件人信誉

默认情况下，将为外部邮件启用发件人信誉，并为内部邮件禁用发件人信誉。如果邮件来自 Exchange 组织以外的未经验证的连接，则邮件被视为外部邮件。如果邮件来自未验证的连接，且发件人的域在您的 Exchange 组织中被配置为权威域，则邮件被视为内部邮件。

若要为外部邮件禁用发件人信誉，请运行以下命令：

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $false
```

若要为外部邮件启用发件人信誉，请运行以下命令：

```powershell
Set-SenderReputationConfig -ExternalMailEnabled $true
```

若要为内部邮件禁用发件人信誉，请运行以下命令：

```powershell
Set-SenderReputationConfig -InternalMailEnabled $false
```

若要为内部邮件启用发件人信誉，请运行以下命令：

```powershell
Set-SenderReputationConfig -InternalMailEnabled $true
```

## 您如何知道这有效？

要验证您是否成功启用或禁用内部和外部邮件发件人信誉，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderReputationConfig | Format-List Enabled,*MailEnabled

2.  验证显示的值是否与配置的值匹配。

## 使用命令行管理程序配置发件人信誉属性

若要配置发件人信誉，请运行以下命令：

```powershell
Set-SenderReputationConfig -SrlBlockThreshold <Value> -SenderBlockingPeriod <Hours>
```

本示例将发件人信誉级别 (SRL) 阻止阈值设置为 6，并对发件人信誉进行配置以将违反此阀值的发件人添加到 IP 阻止列表中 36 小时：

```powershell
Set-SenderReputationConfig -SrlBlockThreshold 6 -SenderBlockingPeriod 36
```

## 您如何知道这有效？

要验证您是否成功配置发件人信誉属性，请执行以下操作：

1.  运行以下命令：
    
    ```powershell
Get-SenderReputationConfig
```

2.  验证显示的值是否与配置的值匹配。

## 使用命令行管理程序配置出站访问，以实现开放代理服务器的检测功能

您可能需要执行更多步骤，以允许发件人信誉遍历任何位于 Internet 和运行\&quot;协议分析\&quot;代理的 Exchange 服务器之间的防火墙。下表列出了发件人信誉所需的出站端口。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>协议</th>
<th>端口</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SOCKS4、SOCKS5</p></td>
<td><p>1081, 1080</p></td>
</tr>
<tr class="even">
<td><p>Wingate、Telnet、Cisco</p></td>
<td><p>23</p></td>
</tr>
<tr class="odd">
<td><p>HTTP CONNECT、HTTP POST</p></td>
<td><p>6588, 3128, 80</p></td>
</tr>
</tbody>
</table>


若要配置出站访问以实现开放代理服务器的检测功能，请运行以下命令：

    Set-SenderReputationConfig -ProxyServerName <String> -ProxyServerPort <Port> -ProxyServerType <String>

本示例配置发件人信誉，以使用名为 SERVER01 并在端口 80 上使用 HTTP CONNECT 协议的开放代理服务器。

    Set-SenderReputationConfig - ProxyServerName SERVER01 -ProxyServerPort 80 -ProxyServerType HttpConnect

## 您如何知道这有效？

要验证您是否成功配置出站访问以检测开放代理服务器，请执行以下操作：

1.  运行以下命令：
    
        Get-SenderReputationConfig | Format-List ProxyServer*

2.  验证显示的值是否为您配置的值。

