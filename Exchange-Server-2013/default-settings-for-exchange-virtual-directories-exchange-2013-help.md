---
title: 'Exchange 虚拟目录的默认设置: Exchange 2013 Help'
TOCTitle: Exchange 虚拟目录的默认设置
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52061556
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 虚拟目录的默认设置

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2015-04-07_

Exchange Server 2013 会在安装过程中，自动配置多个 Internet 信息服务 (IIS) 虚拟目录。本主题包含有关客户端访问和邮箱服务器的默认 IIS 身份验证设置和默认安全套接字层 (SSL) 设置的信息。

## 客户端访问服务器

下表列出了独立 Exchange 2013 客户端访问服务器上的默认设置。

### 默认客户端访问服务器 IIS 身份验证和 SSL 设置

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>虚拟目录</th>
<th>身份验证方法</th>
<th>SSL 设置</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认网站</p></td>
<td><ul>
<li><p>匿名</p></li>
</ul></td>
<td><ul>
<li><p>必需</p></li>
</ul></td>
<td><p>IIS 管理控制台</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>IIS 管理控制台</p></td>
</tr>
<tr class="odd">
<td><p>自动发现</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
<li><p>基本身份验证</p></li>
<li><p>Windows 身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>Exchange 命令行管理程序 (Shell)</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
<li><p>基本身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>Exchange 管理中心 (EAC) 或命令行管理程序</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
<li><p>Windows 身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>命令行管理程序</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>基本身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>EAC 或命令行管理程序</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Windows 身份验证</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>EAC 或命令行管理程序</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>基本身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>EAC 或命令行管理程序</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>命令行管理程序</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>基本身份验证</p></li>
<li><p>Windows 身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>命令行管理程序</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>默认情况下，禁用所有身份验证方法。</p></td>
<td><ul>
<li><p>必需</p></li>
</ul></td>
<td><p> </p></td>
</tr>
</tbody>
</table>


## 邮箱服务器

下表列出了独立 Exchange 2013 邮箱服务器上的默认设置。

### 默认邮箱服务器 IIS 身份验证和 SSL 设置

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>虚拟目录</th>
<th>身份验证方法</th>
<th>SSL 设置</th>
<th>管理方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认网站</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
</ul></td>
<td><ul>
<li><p>需要 SSL</p></li>
<li><p>要求 128 位加密</p></li>
</ul></td>
<td><p>用户不能配置此虚拟目录。</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>匿名身份验证</p></li>
</ul></td>
<td><ul>
<li><p>不需要</p></li>
</ul></td>
<td><p>命令行管理程序</p></td>
</tr>
</tbody>
</table>

