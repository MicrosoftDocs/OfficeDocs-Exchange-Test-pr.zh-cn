---
title: '通过自动检查帮助识别我的问题 - 迁移: Exchange 2013 Help'
TOCTitle: 通过自动检查帮助识别我的问题 - 迁移
ms:assetid: c1cd235d-8e8b-44a8-862d-9d36dc3a44c3
ms:mtpsurl: https://technet.microsoft.com/zh-cn/library/Dn793980(v=EXCHG.150)
ms:contentKeyID: 62633060
ms.date: 05/21/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 通过自动检查帮助识别我的问题 - 迁移

 

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
<td><p>邮箱大小</p></td>
<td><p>我想确定我的用户是否正在使用我的组织的默认邮箱大小，以便我可以更好地计划我的迁移。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834877">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>单个目录林</p></td>
<td><p>我将尝试评估我是否可以使用目录同步迁移我的用户的帐户。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834875">运行此检查</a></p></td>
</tr>
<tr class="even">
<td><p>域功能模式</p></td>
<td><p>我不确定我是否做好了集成 ADFS 2.0/单一登录的准备</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">运行此检查</a></p></td>
</tr>
<tr class="odd">
<td><p>公用文件夹</p></td>
<td><p>我不确定我是否已经将公用文件夹迁移到 Office 365。</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834896">运行此检查</a></p></td>
</tr>
</tbody>
</table>

