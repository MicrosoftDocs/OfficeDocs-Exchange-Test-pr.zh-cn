---
title: '修改 AD LDS 配置: Exchange 2013 Help'
TOCTitle: 修改 AD LDS 配置
ms:assetid: 381f582c-15ec-43bc-b674-5399fad72c97
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Aa997269(v=EXCHG.150)
ms:contentKeyID: 61183388
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 修改 AD LDS 配置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-08_

在将边缘传输服务器订阅到 Exchange 组织之前，您可以使用 **ConfigureAdam.ps1** 脚本（位于 $env:ExchangeInstallPath\\Scripts 中）修改边缘传输服务器上的默认 Active Directory 轻型目录服务 (AD LDS) 配置。

> [!IMPORTANT]  
> <strong>ConfigureAdam.ps1</strong> 脚本通过调用 <strong>dsdbutil</strong> 命令来更改 AD LDS 的注册表设置。<strong>dsdbutil</strong> 命令是一种 AD LDS 管理工具，仅面向经验丰富的管理员使用；推荐使用 <strong>ConfigureAdam.ps1</strong> 更改 AD LDS 配置。


下表中的参数适用于 **ConfigureAdam.ps1** 脚本。您可以使用这些参数中的某一个、全部或任意组合来修改 AD LDS。

### 适用于 ConfigureAdam.ps1 脚本的参数

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Ldapport</em></p></td>
<td><p>修改 LDAP 通信端口。默认情况下，边缘传输服务器使用非标准端口 50389。</p></td>
</tr>
<tr class="even">
<td><p><em>Sslport</em></p></td>
<td><p>修改安全 LDAP 通信端口。默认情况下，边缘传输服务器使用非标准端口 50636。</p></td>
</tr>
<tr class="odd">
<td><p><em>LogPath</em></p></td>
<td><p>修改日志文件的位置。默认情况下，边缘传输服务器在路径 %ExchangeInstallPath%Transport Roles\Data\adam 下创建日志文件。</p></td>
</tr>
<tr class="even">
<td><p><em>DataPath</em></p></td>
<td><p>修改目录数据库文件的位置。默认情况下，边缘传输服务器在路径 %ExchangeInstallPath%Transport Roles\Data\adam 下存储目录数据库。</p></td>
</tr>
</tbody>
</table>


## 在开始之前，您需要知道什么？

  - 估计完成时间：5 分钟。

  - 您必须先获得权限，然后才能执行此过程或多个过程。若要查看所需的权限，请参阅[邮件流权限](mail-flow-permissions-exchange-2013-help.md)主题中的“边缘传输服务器”部分。

  - 如果您需要对边缘传输服务器的 AD LDS 配置进行任何修改，请在将边缘传输服务器订阅到 Exchange 组织之前执行修改操作。如果您修改已订阅的边缘传输服务器的 AD LDS 配置，则需要重新将边缘传输服务器订阅到 Exchange 组织。

  - 请务必使用脚本来修改注册表设置。手动对 AD LDS 配置进行注册表更改可能会导致 AD LDS 实例不可用。

  - 如果您需要修改 AD LDS 使用的 LDAP 端口或 SSL 端口，请先验证所选端口当前是否未由其他应用程序使用。可以使用 **netstat** 命令查看边缘传输服务器所使用的端口。

  - 只能使用命令行管理程序执行此过程。

> [!TIP]  
> 遇到问题了吗？请在 Exchange 论坛中寻求帮助。 请访问以下论坛：<a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>、 <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a> 或 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>。


## 修改边缘传输服务器上的 AD LDS 配置

本示例将 AD LDS 使用的 LDAP 端口更改为 5000。命令语法包含 & 号。

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000

本示例对 AD LDS 配置进行以下更改。命令语法包含 & 号。请注意，每个参数与其值之间使用冒号 (:)：

  - 将 LDAP 端口更改为 5000

  - 将 SSL 端口更改为 500

  - 将日志路径更改为 D:\\Exchange Server\\Data\\ADLDS

  - 将数据路径更改为 D:\\Exchange Server\\Data\\ADLDS

<!-- end list -->

    & $env:ExchangeInstallPath\Scripts\ConfigureAdam.ps1 -LdapPort:5000 -SslPort:5001 -LogPath:"D:\Exchange Server\Data\ADLDS" -DataPath:"D:\Exchange Server\Data\ADLDS"

