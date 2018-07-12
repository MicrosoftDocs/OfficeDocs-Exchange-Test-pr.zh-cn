---
title: '通过自动检查帮助识别我的问题 - Active Directory: Exchange 2013 Help'
TOCTitle: 通过自动检查帮助识别我的问题 - Active Directory
ms:assetid: af08e7a1-775a-4e56-a6fe-4ffc10460514
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn793979(v=EXCHG.150)
ms:contentKeyID: 62633058
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通过自动检查帮助识别我的问题 - Active Directory

 

_**适用于：** Exchange Server 2013_

_**上一次修改主题：** 2016-12-09_

此页上的检查将有助于确定一些最常见的配置问题。您可以使用下面的自动检查，以验证您的配置并帮助您更新环境。

如果您已经有一个 Office 365 用户帐户，请选择\&quot;登录\&quot;。无需 Azure ID 帐户。在运行检查时，可能要求您再次输入用户帐户。如果是这样，您的用户帐户的格式为 username@youroffice365login.domain 和您的密码。

## 先决条件

我们将查看您是否安装了 Azure Active Directory 登录助理 和 用于 Windows PowerShell 的 Azure Active Directory 模块。

Azure Active Directory 登录助理有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286261)和[64 位](https://go.microsoft.com/fwlink/?linkid=286262)。

用于 Windows PowerShell 的 Azure Active Directory 模块有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286258)和[64 位](https://go.microsoft.com/fwlink/?linkid=286259)。

## Active Directory 检查


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
<td><p>Exchange 版本</p></td>
<td><p>我不确定是否本地安装了 Exchange Server 或不确定安装的是哪个版本。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834879">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>凭据</p></td>
<td><p>我不确定是否将合适的凭据移到 Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834880">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>第三方工具</p></td>
<td><p>我不确定已在邮件环境中安装哪些第三方集成/应用程序。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834907">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>共享邮箱</p></td>
<td><p>我希望确定是谁在管理其他人（代理人）的邮箱。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834917">运行此检查</a></p></td>
</tr>
</tbody>
</table>

