---
title: 'Azure：通过自动检查帮助确定我的问题 - DNS 记录: Exchange 2013 Help'
TOCTitle: Azure：通过自动检查帮助确定我的问题 - DNS 记录
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62629976
ms.date: 01/11/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Azure：通过自动检查帮助确定我的问题 - DNS 记录

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

不正确地配置 DNS 记录是最常见的配置安装问题之一。您可以使用下面列出的自动检查，以验证您的配置并帮助您更新环境。

如果您已经拥有 Office 365 用户帐户，请选择“登录”，而无需 Azure ID 帐户。在运行检查时，可能要求您再次输入用户帐户。如果是这样，您的用户帐户的格式为 username@youroffice365login.domain 和您的密码。

## 先决条件

我们将查看您是否安装了 Azure Active Directory 登录助理 和 用于 Windows PowerShell 的 Azure Active Directory 模块。

Azure Active Directory 登录助理 有两个版本：[32 位](https://go.microsoft.com/fwlink/?linkid=286261)和 [64 位](https://go.microsoft.com/fwlink/?linkid=286262)。

用于 Windows PowerShell 的 Azure Active Directory 模块 有两个版本：[32 位](https://go.microsoft.com/fwlink/?linkid=286258)和 [64 位](https://go.microsoft.com/fwlink/?linkid=286259)。

## DNS 记录检查


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>应用程序</p></td>
<td><p>症状</p></td>
<td><p>检查</p></td>
</tr>
<tr class="even">
<td><p>域</p></td>
<td><p>我的自定义域（例如 contoso.com）似乎不使用 Office 365 进行配置</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>域</p></td>
<td><p>我的自定义域（例如 contoso.com）似乎不使用 Office 365 进行配置（我使用了 CNAME 记录）</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>域</p></td>
<td><p>我的自定义域（例如 contoso.com）似乎不使用 Office 365 进行配置（我使用了 TXT 记录）</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>即时消息</p></td>
<td><p>我的用户在让 Lync 客户端正常工作时遇到问题</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>即时消息</p></td>
<td><p>我的用户在让 Lync 客户端与其他组织正常工作时遇到问题</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件</p></td>
<td><p>我无法使 Outlook 自动配置 Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>邮件</p></td>
<td><p>我的电子邮件似乎没有路由到 Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>邮件</p></td>
<td><p>我的组织正收到大量的垃圾邮件</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>邮件</p></td>
<td><p>我似乎无法让 Exchange 混合工作</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">运行此检查</a></p></td>
</tr>
</tbody>
</table>

