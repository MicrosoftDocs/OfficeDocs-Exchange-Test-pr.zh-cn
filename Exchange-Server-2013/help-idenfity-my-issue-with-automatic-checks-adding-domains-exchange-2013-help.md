---
title: '通过自动检查帮助确定我的问题 - 添加域: Exchange 2013 Help'
TOCTitle: 通过自动检查帮助确定我的问题 - 添加域
ms:assetid: ea90a24b-7c9c-48d5-9475-0eb7777452f3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn793981(v=EXCHG.150)
ms:contentKeyID: 62633063
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通过自动检查帮助确定我的问题 - 添加域

 

_**适用于：**Exchange Server 2013_

_**上一次修改主题：**2016-12-09_

此页上的检查将有助于确定一些最常见的配置问题。您可以使用下面的自动检查，以验证您的配置并帮助您更新环境。

如果您已经有一个 Office 365 用户帐户，请选择\&quot;登录\&quot;。无需 Azure ID 帐户。在运行检查时，可能要求您再次输入用户帐户。如果是这样，您的用户帐户的格式为 username@youroffice365login.domain 和您的密码。

## 先决条件

我们将查看您是否安装了 Azure Active Directory 登录助理 和 用于 Windows PowerShell 的 Azure Active Directory 模块。

Azure Active Directory 登录助理有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286261)和[64 位](https://go.microsoft.com/fwlink/?linkid=286262)。

用于 Windows PowerShell 的 Azure Active Directory 模块有两个版本︰ [32 位](https://go.microsoft.com/fwlink/?linkid=286258)和[64 位](https://go.microsoft.com/fwlink/?linkid=286259)。

## 添加域检查


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
<td><p>我想要确定本地中存在哪些域/我不知道我拥有哪些域。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834925">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>域</p></td>
<td><p>我不确定是否已为我的租户添加并验证了正确的域。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>域</p></td>
<td><p>我需要帮助来确保我针对 Office 365 的所有 DNS 记录均正确。</p></td>
<td><ol>
<li><p><a href="https://portal.microsoftonline.com/">登录到 Office 365</a></p></li>
<li><p>选择<a href="https://portal.microsoftonline.com/tools">工具</a></p></li>
<li><p>选择&amp;quot;使用 Office 365 最佳实践分析工具检查您的本地电脑&amp;quot;。</p></li>
</ol></td>
</tr>
</tbody>
</table>

